---
title: 'DAG ミラーリング監視サーバーとしての Microsoft Azure VM の使用: Exchange 2013 Help'
TOCTitle: DAG ミラーリング監視サーバーとしての Microsoft Azure VM の使用
ms:assetid: 03d1e215-518b-4b48-bfcd-8d187ff8f5ef
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn903504(v=EXCHG.150)
ms:contentKeyID: 63892231
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# DAG ミラーリング監視サーバーとしての Microsoft Azure VM の使用

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

Exchange Server 2013 では、データセンターの自動フェールオーバーのためのデータベース可用性グループ (DAG) にあるメールボックス データベースの構成が可能です。この構成では、次の 3 つの物理的な場所 (メールボックス サーバー用の 2 つのデータセンターと、DAG のミラーリング監視サーバーを配置する第 3 の場所) が別個に必要です。現在 2 つの物理的な場所のみがある組織は、DAG のミラーリング監視サーバーの役割をする Microsoft Azure ファイル サーバーの仮想マシンを使用して、データセンターの自動フェールオーバーを活用することもできます。

この記事では、Microsoft Azure における DAG のミラーリング監視の配置を中心に説明します。この記事は、読者がサイト復元の概念に精通しており、2 つのデータセンターにまたがる完全機能の DAG インフラストラクチャが既にあることを前提としています。DAG のインフラストラクチャをまだ構成していない場合は、先に次の記事を確認することをお勧めします。

[高可用性とサイトの復元](high-availability-and-site-resilience-exchange-2013-help.md)

[データベース可用性グループ (DAG)](database-availability-groups-dags-exchange-2013-help.md)

[高可用性とサイトの復元計画](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)

## Microsoft Azure への変更

この構成では、複数サイト VPN が必要です。サイト間の VPN 接続を使用して、組織のネットワークを Microsoft Azure に接続することは常に可能です。ただし、以前、Azure は 1 つのサイト間 VPN のみをサポートしていました。3 つのデータセンター全体に DAG とそのミラーリング監視を構成するには複数のサイト間 VPN が必要であったため、Azure 仮想マシンでの DAG ミラーリング監視の配置は最初は不可能でした。

2014 年 6 月、組織が複数のデータセンターを 1 つの Azure 仮想ネットワークに接続できるようにする、複数サイト VPN のサポートが Microsoft Azure に導入されました。また、この変更により、2 つのデータセンターを持つ組織が 3 つ目の場所として Microsoft Azure を活用し、DAG ミラーリング監視サーバーを配置できるようになりました。Azure での複数サイト VPN 機能の詳細については、「[複数サイト VPN の構成](http://go.microsoft.com/fwlink/?linkid=522621)」を参照してください。


> [!NOTE]
> この構成では、ミラーリング監視サーバーを展開するために Azure 仮想マシンと複数サイト VPN を活用し、Azure クラウド ミラーリング監視は使用しません。



## Microsoft Azure ファイル サーバーのミラーリング監視

次の図は、DAG のミラーリング監視としての Microsoft Azure ファイル サーバーの使用の概要です。Azure 仮想ネットワーク、データセンターを Azure 仮想ネットワークに接続する複数サイト VPN、および Azure 仮想マシンに展開されたドメイン コントローラーとファイル サーバーが必要です。


> [!NOTE]
> 1 つの Azure 仮想マシンを DAG のミラーリング監視の目的に使用し、ファイルのミラーリング監視共有をドメイン コントローラーに配置することは、技術的に可能です。ただし、結果として不要な特権の昇格が発生します。そのため、これは推奨される構成ではありません。



**Microsoft Azure での DAG ミラーリング監視サーバー**

![Azure における Exchange DAG の監視の概要](images/Dn903504.7cbda882-bbae-4be7-b0ea-60947b8aa4ef(EXCHG.150).png "Azure における Exchange DAG の監視の概要")

Microsoft Azure 仮想マシンを DAG のミラーリング監視に使用するために最初に必要なことは、サブスクリプションの取得です。Azure サブスクリプションを取得する最善の方法については、「[Azure の購入方法](http://go.microsoft.com/fwlink/?linkid=398989)」を参照してください。

Azure サブスクリプションを取得したら、以下を順番に実行する必要があります。

1.  Microsoft Azure 仮想ネットワークを準備する

2.  複数サイト VPN を構成する

3.  仮想マシンを構成する

4.  DAG のミラーリング監視を構成する


> [!NOTE]
> この記事におけるガイダンスの大部分は Microsoft Azure の構成に関することです。したがって、該当する箇所には Azure ドキュメントへのリンクが使用されます。



## 前提条件

  - Exchange の高可用性とサイト復元の展開をサポートできる 2 つのデータセンター。詳細については「[高可用性とサイトの復元計画](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)」を参照してください。

  - (NAT の背後にない) 各サイトの VPN ゲートウェイのパブリック IP アドレス

  - Microsoft Azure と互換性がある各サイト内の VPN デバイス。互換性のあるデバイスの詳細については、「[仮想ネットワークに使用する VPN デバイスについて](http://go.microsoft.com/fwlink/?linkid=522619)」を参照してください。

  - DAG の概念と管理に精通していること

  - Windows PowerShell に精通していること

## フェーズ 1: Microsoft Azure 仮想ネットワークを準備する

Microsoft Azure ネットワークの構成は、展開プロセスの最も重要な部分です。このフェーズの終わりには、複数サイト VPN 経由で 2 つのデータセンターに接続された、完全機能の Azure 仮想ネットワークができます。

## DNS サーバーを登録する

この構成では、オンプレミスのサーバーと Azure 仮想マシンの間での名前解決が必要となるため、独自の DNS サーバーを使用するように Azure を構成する必要があります。トピック「[名前解決 (DNS)](http://msdn.microsoft.com/ja-jp/library/azure/jj156088.aspx)」では、Azure での名前解決の概要について説明しています。

DNS サーバーを登録するには、次のようにします。

1.  Azure ポータルで、<strong>ネットワーク</strong> に移動してから、<strong>新規</strong> をクリックします。

2.  <strong>ネットワーク サービス</strong> \> <strong>仮想ネットワーク</strong> \> <strong>DNS サーバーの登録</strong> の順にクリックします。

3.  DNS サーバーの名前と IP アドレスを入力します。ここに指定された名前は、管理ポータルで使用される論理名であり、DNS サーバーの実際の名前と一致する必要はありません。

4.  他に追加する DNS サーバーがある場合は、手順 1 ～ 3 を繰り返します。
    

    > [!NOTE]
    > 登録する DNS サーバーは、ラウンド ロビン方式では使用されません。Azure 仮想マシンは、一覧表示されている最初の DNS サーバーを使用し、最初の DNS サーバーが使用できない場合にのみ追加のサーバーを使用します。



5.  Microsoft Azure に展開するドメイン コントローラーに使用する IP アドレスを追加するには、手順 1 ～ 3 を繰り返します。

## Azure にローカル (オンプレミス) ネットワーク オブジェクトを作成する

次に、以下を実行して Microsoft Azure でのデータセンターを表す論理ネットワーク オブジェクトを作成します。

1.  Azure ポータルで、<strong>ネットワーク</strong> に移動してから、<strong>新規</strong> をクリックします。

2.  <strong>ネットワーク サービス</strong> \> <strong>仮想ネットワーク</strong> \> <strong>ローカル ネットワークの追加</strong> の順にクリックします。

3.  最初のデータセンターのサイト名と、そのサイトの VPN デバイスの IP アドレスを入力します。この IP アドレスは、NAT の背後にない静的パブリック IP アドレスである必要があります。

4.  次の画面で、最初のサイトの IP サブネットを指定します。

5.  2 番目のサイトについて、手順 1 ～ 4 を繰り返します。

## Azure 仮想ネットワークを作成する

ここで、仮想マシンが使用する Azure 仮想ネットワークを作成するために、次のようにします。

1.  Azure ポータルで、<strong>ネットワーク</strong> に移動してから、<strong>新規</strong> をクリックします。

2.  <strong>ネットワーク サービス</strong> \> <strong>仮想ネットワーク</strong> \> <strong>カスタム作成</strong> の順にクリックします。

3.  <strong>仮想ネットワークの詳細</strong> ページで、仮想ネットワークの名前を指定してから、ネットワークの地理的な場所を選択します。

4.  <strong>DNS サーバーと VPN 接続</strong> ページで、既に登録した DNS サーバーが DNS サーバーとして一覧表示されることを確認します。

5.  <strong>サイト間接続</strong> の下で、<strong>サイト間 VPN の構成</strong> チェック ボックスを選択します。
    

    > [!IMPORTANT]
    > <STRONG>[ExpressRoute を使用する]</STRONG> は選択しないでください。選択すると、複数サイト VPN のセットアップに必要な構成変更ができなくなるためです。



6.  <strong>ローカル ネットワーク</strong> で、構成した 2 つのオンプレミス ネットワークのいずれかを選択します。

7.  <strong>仮想ネットワークのアドレス スペース</strong> ページで、Azure 仮想ネットワークに使用する IP アドレスの範囲を指定します。

## チェックポイント: ネットワーク構成の確認

この時点で、<strong>ネットワーク</strong> に移動すると、<strong>仮想ネットワーク</strong> で構成した仮想ネットワーク、<strong>ローカル ネットワーク</strong> で構成したローカル サイト、および <strong>DNS サーバー</strong> で登録した DNS サーバーが表示されています。

## フェーズ 2: 複数サイト VPN を構成する

次の手順では、オンプレミスのサイトに VPN ゲートウェイを確立します。そのためには、次のようにする必要があります。

1.  Azure ポータルを使用して、いずれかのサイトに VPN ゲートウェイを確立する。

2.  仮想ネットワークの構成設定をエクスポートする。

3.  複数サイト VPN 用に構成ファイルを変更する。

4.  更新された Azure のネットワーク構成をインポートする。

5.  Azure のゲートウェイの IP アドレスと事前共有キーを記録する。

6.  オンプレミスの VPN デバイスを構成する。

複数サイト VPN の構成の詳細については、「[複数サイト VPN の構成](http://go.microsoft.com/fwlink/?linkid=522621)」を参照してください。

## 最初のサイトに VPN ゲートウェイを確立する

仮想ゲートウェイを作成する際は、仮想ゲートウェイが最初のオンプレミスのサイトに接続されるように指定済みであることに注意してください。仮想ネットワークのダッシュボードに移動すると、ゲートウェイが作成されていないことがわかります。

Azure 側で VPN ゲートウェイを確立するには、「[管理ポータルでの仮想ネットワーク ゲートウェイの構成](http://msdn.microsoft.com/ja-jp/library/azure/jj156210.aspx)」の「[仮想ネットワーク ゲートウェイを開始する](http://msdn.microsoft.com/ja-jp/library/azure/jj156210.aspx#bkmk+_startgateway)」セクションの指示に従います。


> [!IMPORTANT]
> この記事の「仮想ネットワーク ゲートウェイを開始する」セクションの手順のみを実行し、それ以降のセクションは実行しないでください。



## 仮想ネットワーク構成の設定をエクスポートする

現在、Azure 管理ポータルでは、複数サイト VPN の構成はできなくなっています。この構成では、仮想ネットワークの構成設定を XML ファイルにエクスポートしてから、そのファイルを変更する必要があります。設定をエクスポートするには、「[ネットワーク構成ファイルへの仮想ネットワーク設定のエクスポート](http://msdn.microsoft.com/ja-jp/library/azure/dn133804.aspx)」の指示に従います。

## 複数サイト VPN 用にネットワークの構成設定を変更する

任意の XML エディターでエクスポートしたファイルを開きます。オンプレミスのサイトへのゲートウェイ接続が、「ConnectionsToLocalNetwork」セクションに一覧表示されます。XML ファイルでその用語を検索すると、セクションが見つかります。この構成ファイルのセクションは次のようになります (ローカル サイトに作成されたサイト名が "Site A" であると仮定した場合)。

    <ConnectionsToLocalNetwork>
    
        <LocalNetworkSiteRef name="Site A">
    
            <Connection type="IPsec" />
    
    </LocalNetworkSiteRef>

2 番目のサイトを構成するには、「ConnectionsToLocalNetwork」セクションの下に別の「LocalNetworkSiteRef」セクションを追加します。更新した構成ファイルのセクションは次のようになります (2 番目のローカル サイトのサイト名が "Site B" であると仮定した場合)。

    <ConnectionsToLocalNetwork>
    
        <LocalNetworkSiteRef name="Site A">
    
            <Connection type="IPsec" />
    
        <LocalNetworkSiteRef name="Site B">
    
            <Connection type="IPsec" />
    
    </LocalNetworkSiteRef>

更新された構成設定ファイルを保存します。

## 仮想ネットワークの構成設定をインポートする

構成ファイルに追加した 2 番目のサイト参照は、Microsoft Azure が新しいトンネルを作成するトリガーとなります。「[ネットワーク構成ファイルのインポート](http://msdn.microsoft.com/ja-jp/library/azure/jj156213.aspx)」の指示に従って、更新されたファイルをインポートします。インポートの完了後、仮想ネットワークのダッシュ ボードは、両方のローカル サイトにゲートウェイ接続を表示します。

## Azure ゲートウェイの IP アドレスと事前共有キーを記録する

新しいネットワーク構成設定がインポートされると、仮想ネットワークのダッシュボードは Azure のゲートウェイの IP アドレスを表示します。これは、両方のサイトにある VPN デバイスの接続先となる IP アドレスです。参照用にこの IP アドレスを記録します。

また、作成された各トンネルの事前共有の IPsec/IKE キーを取得する必要があります。これらのキーを Azure のゲートウェイの IP アドレスと併用すると、オンプレミスの VPN デバイスを構成できます。

事前共有キーを取得するには、PowerShell を使用する必要があります。PowerShell を使用して Azure を管理することに慣れていない場合は、「[Azure PowerShell](http://msdn.microsoft.com/ja-jp/library/azure/jj156055.aspx)」を参照してください。

事前共有キーを抽出するには、「[Get-AzureVNetGatewayKey](http://msdn.microsoft.com/ja-jp/library/azure/dn495198.aspx)」コマンドレットを使用します。このコマンドレットは、トンネルごとに 1 回ずつ実行します。次の例は、仮想ネットワーク「Azure Site」とサイト "Site A" および "Site B" の間にあるトンネル用のキーを抽出するために実行する必要があるコマンドを示しています。この例では、出力は個別のファイルに保存されます。または、これらのキーを他の PowerShell コマンドレットにパイプライン処理したり、これらのキーをスクリプトで使用できます。

    Get-AzureVNETGatewayKey -VNetName "Azure Site" -LocalNetworkSiteName "Site A" > C:\Keys\KeysForTunnelToSiteA.txt 
    
    Get-AzureVNETGatewayKey -VNetName "Azure Site" -LocalNetworkSiteName "Site B" > C:\Keys\KeysForTunnelToSiteB.txt

## オンプレミスの VPN デバイスを構成する

Microsoft Azure は、サポートされる VPN デバイスに VPN デバイス構成スクリプトを提供します。ご使用の VPN デバイスに適したスクリプトを使用するには、仮想ネットワークのダッシュボードにある <strong>VPN デバイス スクリプトのダウンロード</strong> のリンクをクリックします。

ダウンロードするスクリプトには、仮想ネットワークのセット アップ時に構成した最初のサイトの構成設定があり、そのサイトの VPN デバイスを構成するためにそのまま使用することができます。たとえば、仮想ネットワークの作成時に Site A として**ローカル ネットワーク**を指定した場合、Site A 用に VPN デバイスのスクリプトを使用できます。ただし、これを変更して Site B 用に VPN デバイスを構成する必要があります。具体的には、事前共有キーを 2 番目のサイトのキーと一致するように更新する必要があります。

たとえば、サイトにルーティングとリモート アクセス サービス (RRAS) の VPN デバイスを使用している場合は、次のようにする必要があります。

1.  任意のテキスト エディターで、構成スクリプトを開きます。

2.  「`#Add S2S VPN interface`」セクションを検索します。

3.  このセクションで、**Add-VpnS2SInterface** コマンドを検索します。*SharedSecret* パラメーターの値が VPN デバイスを構成しているサイトの事前共有キーと一致していることを確認します。

その他のデバイスには追加の確認が必要になることがあります。たとえば、Cisco デバイスの構成スクリプトでは、ローカル IP アドレスの範囲を使用して ACL ルールを設定します。構成スクリプトを使用する前に、構成スクリプトにあるローカル サイトに対するすべての参照を確認する必要があります。詳細については、以下のトピックを参照してください。

[ルーティングとリモート アクセス サービス (RRAS) 用テンプレート](http://msdn.microsoft.com/ja-jp/library/azure/dn133801.aspx)

[Cisco ASR 用テンプレート](http://msdn.microsoft.com/ja-jp/library/azure/dn133802.aspx)

[Cisco ISR 用テンプレート](http://msdn.microsoft.com/ja-jp/library/azure/dn133800.aspx)

[Juniper SRX 用テンプレート](http://msdn.microsoft.com/ja-jp/library/azure/dn133794.aspx)

[Juniper J シリーズ用テンプレート](http://msdn.microsoft.com/ja-jp/library/azure/dn133799.aspx)

[Juniper ISG 用テンプレート](http://msdn.microsoft.com/ja-jp/library/azure/dn133797.aspx)

[Juniper SSG 用テンプレート](http://msdn.microsoft.com/ja-jp/library/azure/dn133796.aspx)

## チェックポイント: VPN の状態を確認する

この時点で、両方のサイトが VPN ゲートウェイを介して Azure 仮想ネットワークに接続されています。PowerShell で次のコマンドを実行すると、複数サイト VPN の状態を検証できます。

    Get-AzureVnetConnection -VNetName "Azure Site" | Format-Table LocalNetworkSiteName, ConnectivityState

両方のトンネルが稼働している場合、このコマンドの出力は次のようになります。

    LocalNetworkSiteName    ConnectivityState
    
    --------------------    -----------------
    
    Site A                  Connected
    
    Site B                  Connected

また、Azure 管理ポータルで仮想ネットワークのダッシュボードを表示すると、接続を確認できます。両方のサイトの <strong>ステータス</strong> 列に <strong>接続済み</strong> と表示されます。


> [!NOTE]
> 接続が正常に確立されてから Azure 管理ポータルに状態の変化が表示されるまで数分かかることがあります。



## フェーズ 3: 仮想マシンを構成する

この展開では、Microsoft Azure に少なくとも 2 つの仮想マシン、ドメイン コント ローラーおよび DAG のミラーリング監視の役割をするファイル サーバーを作成する必要があります。

1.  「[Windows を実行する仮想マシンの作成](http://azure.microsoft.com/ja-jp/documentation/articles/virtual-machines-windows-tutorial/)」の指示に従って、ドメイン コントローラーとファイル サーバー用の仮想マシンを作成します。仮想マシンの設定を指定する際は、<strong>地域/アフィニティ グループ/仮想ネットワーク</strong> について、作成した仮想ネットワークを必ず選択してください。

2.  Azure PowerShell を使用して、ドメイン コントローラーとファイル サーバーの両方に優先 IP アドレスを指定します。仮想マシンに優先 IP アドレスを指定する場合は更新する必要があります。これには仮想マシンの再起動が必要になります。次の例では、Azure-DC と Azure-FSW の IP アドレスがそれぞれ 10.0.0.10 と 10.0.0.11 に設定されています。
    
        Get-AzureVM Azure-DC | Set-AzureStaticVNetIP -IPAddress 10.0.0.10 | Update-AzureVM
        
        Get-AzureVM Azure-FSW | Set-AzureStaticVNetIP -IPAddress 10.0.0.11 | Update-AzureVM
    

    > [!NOTE]
    > 優先 IP アドレスがある仮想マシンは、このアドレスの使用を試みます。ただし、このアドレスが別の仮想マシンに割り当てられている場合、優先 IP アドレスの構成がある仮想マシンは起動しません。このような状況を回避するには、使用する IP アドレスが別の仮想マシンに割り当てられていないことを確認します。詳細については、「<A href="http://msdn.microsoft.com/ja-jp/library/azure/dn630228.aspx">VM 用の静的内部 IP アドレスを構成する</A>」を参照してください。



3.  組織で使用している基準を使用して、Azure のドメイン コントローラー仮想マシンをプロビジョニングします。

4.  Exchange DAG のミラーリング監視の前提条件を持つファイル サーバーを準備します。
    
    1.  \[役割の追加と機能\] ウィザードを使用してファイル サーバーの役割を追加するか、[Add-WindowsFeature](http://technet.microsoft.com/ja-jp/library/ee662309.aspx) コマンドレットを追加します。
    
    2.  ローカル管理者グループに、Exchange Trusted Subsystem ユニバーサル セキュリティ グループを追加します。

## チェックポイント: 仮想マシンの状態を確認する

この時点で、仮想マシンが稼働し、両方のオンプレミスのデータセンターにあるサーバーと通信できるはずです。

  - Azure のドメイン コントローラーがオンプレミスのドメイン コントローラーにレプリケートしていることを確認します。

  - 名前ごとに Azure のファイル サーバーにアクセスし、Exchange サーバーから SMB 接続を確立できることを確認します。

  - Azure のファイル サーバーから、名前によって Exchange サーバーにアクセスできることを確認します。

## フェーズ 4: DAG のミラーリング監視を構成する

最後に、新しいミラーリング監視サーバーを使用するように DAG を構成する必要があります。既定では、Exchange は、ミラーリング監視サーバー上のファイル共有監視パスとして C:\\DAGFileShareWitnesses を使用します。ユーザー設定のファイル パスを使用している場合、特定の共有向けにミラーリング監視ディレクトリを更新する必要もあります。

1.  Exchange 管理シェル に接続します。

2.  DAG 用にミラーリング監視サーバーを構成するには、次のコマンドを実行します。
    
        Set-DatabaseAvailabilityGroup -Identity DAG1 -WitnessServer Azure-FSW

詳細については、以下のトピックを参照してください。

[データベース可用性グループのプロパティを構成する](configure-database-availability-group-properties-exchange-2013-help.md)

[Set-DatabaseAvailabilityGroup](http://technet.microsoft.com/ja-jp/library/dd297934\(v=exchg.150\).aspx)

## チェックポイント: DAG のファイル共有監視を検証する

この時点で、DAG のミラーリング監視として Azure のファイル サーバーを使用するように DAG が構成されています。構成を検証するには次のようにします。

1.  次のコマンドを実行して、DAG の構成を検証します。
    
        Get-DatabaseAvailabilityGroup -Identity DAG1 -Status | Format-List Name, WitnessServer, WitnessDirectory, WitnessShareInUse
    
    *WitnessServer* パラメーターが Azure のファイル サーバーに設定されていること、*WitnessDirectory* パラメーターが適切なパスに設定されていること、*WitnessShareInUse* パラメーターが **Primary** と表示されていることを確認します。

2.  DAG のノードの数が偶数の場合、ファイル共有監視が構成されます。次のコマンドを実行して、クラスターのプロパティにあるファイル共有監視の設定を検証します。*SharePath* パラメーターの値はファイル サーバーを指し示し、正しいパスを表示するはずです。
    
        Get-ClusterResource -Cluster MBX1 | Get-ClusterParameter | Format-List

3.  次に、次のコマンドを実行して、「ファイル共有監視」クラスター リソースの状態を確認します。クラスター リソースの *State* が "**Online**" と表示されるはずです。
    
        Get-ClusterResource -Cluster MBX1

4.  最後に、ファイル エクスプローラーでフォルダーを確認し、サーバー マネージャーで共有を確認して、ファイル サーバーで共有が正常に作成されていることを確認します。

## 関連項目


[高可用性とサイトの復元計画](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)  
[切り替えとフェールオーバー](switchovers-and-failovers-exchange-2013-help.md)  
[データベース可用性グループの管理](managing-database-availability-groups-exchange-2013-help.md)

