---
title: '高可用性とサイト復元の展開: Exchange 2013 Help'
TOCTitle: 高可用性とサイト復元の展開
ms:assetid: 4c4e00a4-1f57-4fdb-b9b2-2779abf381a9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd638129(v=EXCHG.150)
ms:contentKeyID: 48269469
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 高可用性とサイト復元の展開

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-03-09_

Microsoft Exchange Server 2013 では、高可用性とサイト復元に*増分展開*と呼ばれる概念を用います。2 台以上の Exchange 2013 メールボックス サーバーをスタンドアロン サーバーとして設置し、必要に応じてそれらのメールボックス サーバーとメールボックス データベースの高可用性とサイト復元を増分的に構成します。

## 展開処理の概要

各組織が用いる実際のステップは若干異なることがありますが、高可用性またはサイト復元構成で Exchange 2013 を展開するための全体的な処理は一般的に違いはありません。データベース可用性グループ (DAG) の構築と展開、およびメールボックス データベースのコピーの作成に必要となる計画と設計のタスクの実行後、以下の作業を実行します。

1.  DAG を作成します。詳細な手順については、「[データベース可用性グループを作成する](create-a-database-availability-group-exchange-2013-help.md)」を参照してください。

2.  必要に応じて、クラスタ名オブジェクト (CNO) を事前に設定します。CNO の事前設定が必要になるのは、メールボックス サーバーで Windows Server 2012 を実行する DAG を展開する場合です。Windows Server 2012 R2 を実行するメールボックス サーバーを使用して、管理アクセス ポイントのない DAG を展開する場合は、CNO の事前設定は不要です。コンピューター アカウント作成が制限されるか、コンピューター アカウントが既定のコンピューター コンテナー以外のコンテナーで作成される環境でも、事前設定が必要です。詳細な手順については、「[データベース可用性グループのクラスター名オブジェクトを事前設定する](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md)」を参照してください。

3.  DAG に複数のメールボックス サーバーを追加します。詳細な手順については、「[データベース可用性グループのメンバーシップを管理する](manage-database-availability-group-membership-exchange-2013-help.md)」を参照してください。

4.  必要に応じて、DAG プロパティを構成します。
    
    1.  オプションで、DAG の暗号化と圧縮、レプリケーション ポート、DAG IP アドレス、およびその他の DAG プロパティを構成します。詳細な手順については、「[データベース可用性グループのプロパティを構成する](configure-database-availability-group-properties-exchange-2013-help.md)」を参照してください。
    
    2.  DAG に対してデータセンター アクティブ化調整 (DAC) モードを有効にします。これにより、データ センター切り替えが実行され、組み込みの DAG 回復コマンドレットの使用が有効になった後、プライマリ データセンターへのスイッチバック中に、データベースレベルのスプリットブレイン状態から DAG を保護できます。詳細については、「[データセンター ライセンス認証調整モード](datacenter-activation-coordination-mode-exchange-2013-help.md)」を参照してください。

5.  DAG 内のメールボックス サーバー全体にメールボックス データベースのコピーを追加します。詳細な手順については、「[メールボックス データベース コピーを追加する](add-a-mailbox-database-copy-exchange-2013-help.md)」を参照してください。

## 展開の例:2 つのデータセンターでの 4 メンバー DAG

この例では、組織 Contoso, Ltd. が 2 つの物理的な場所にまたがる 4 メンバー DAG を構成して展開する方法の詳細を示します。Redmond (Washington 州) および Portland (Oregon 州)。

## 基本のインフラストラクチャ

各場所には、Exchange 2013 をベースとしたメッセージング インフラストラクチャを運用するのに必要となる、以下のインフラストラクチャ要素が含まれます。

  - ディレクトリ サービス (Active Directory または Active Directory ドメイン サービス (AD DS) のいずれか)

  - ドメイン ネーム システム (DNS) の名前解決

  - 複数の Exchange 2013 クライアント アクセス サーバー

  - 複数の Exchange 2013 メールボックス サーバー

次の図は、Contoso の構成を示しています。

**2 サイトにまたがるデータベース可用性グループ**

![2 サイトにまたがるデータベース可用性グループ](images/Dd638129.1c326fd4-3c7b-4416-a63d-fbfdd0cc6b18(EXCHG.150).gif "2 サイトにまたがるデータベース可用性グループ")

## ネットワークの構成

前の図にあるように、ソリューションでは複数サブネットと複数ネットワークが使用されます。DAG 内の各メールボックス サーバーは、個別のサブネットに 2 つのネットワーク アダプターを備えます。各メールボックス サーバーでは、1 つのネットワーク アダプターが MAPI ネットワーク (192.168.*x*.*x*) に、もう 1 つのネットワーク アダプターがレプリケーション ネットワーク (10.0.*x*.*x*) に使用されます。MAPI ネットワークのみが Active Directory、DNS サービス、その他の Exchange サーバーとクライアントへの接続を提供します。各メンバー内のレプリケーション ネットワーク用アダプターは、DAG 内のその他のメンバーのレプリケーション ネットワーク アダプターへの接続のみを提供します。

各ノードの各ネットワーク アダプターの設定を以下の表にまとめます。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>名前</th>
<th>IPv4 アドレス</th>
<th>サブネット マスク</th>
<th>デフォルト ゲートウェイ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MBX1 (MAPI)</p></td>
<td><p>192.168.1.4</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>MBX2 (MAPI)</p></td>
<td><p>192.168.1.5</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="odd">
<td><p>MBX3 (MAPI)</p></td>
<td><p>192.168.2.4</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.2.1</p></td>
</tr>
<tr class="even">
<td><p>MBX4 (MAPI)</p></td>
<td><p>192.168.2.5</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.2.1</p></td>
</tr>
<tr class="odd">
<td><p>MBX1 (レプリケーション)</p></td>
<td><p>10.0.1.4</p></td>
<td><p>255.255.0.0</p></td>
<td><p>なし</p></td>
</tr>
<tr class="even">
<td><p>MBX2 (レプリケーション)</p></td>
<td><p>10.0.1.5</p></td>
<td><p>255.255.0.0</p></td>
<td><p>なし</p></td>
</tr>
<tr class="odd">
<td><p>MBX3 (レプリケーション)</p></td>
<td><p>10.0.2.4</p></td>
<td><p>255.255.0.0</p></td>
<td><p>なし</p></td>
</tr>
<tr class="even">
<td><p>MBX4 (レプリケーション)</p></td>
<td><p>10.0.2.5</p></td>
<td><p>255.255.0.0</p></td>
<td><p>なし</p></td>
</tr>
</tbody>
</table>


前の表にあるように、レプリケーション ネットワークに使用されるアダプターはデフォルト ゲートウェイを使用しません。各レプリケーション ネットワーク アダプター間にネットワーク接続を提供するために、Contoso は Netsh.exe ツールを使用して構成する固定の静的ルートを使用します。

MBX1 および MBX2 のレプリケーション ネットワーク アダプターのルーティングを構成するため、各サーバー上で以下のコマンドを実行します。

    netsh interface ipv4 add route 10.0.2.0/24 <NetworkName> 10.0.1.254

MBX3 および MBX4 のレプリケーション ネットワーク アダプターのルーティングを構成するため、各サーバー上で以下のコマンドを実行します。

    netsh interface ipv4 add route 10.0.1.0/24 <NetworkName> 10.0.2.254

次の追加のネットワーク設定も構成されています。

  - **\[この接続のアドレスを DNS に登録する\]** チェック ボックスは、各 DAG メンバーの MAPI ネットワーク アダプターに対してはオンにし、各レプリケーション ネットワーク アダプターに対してはオフになっています。

  - 少なくとも 1 つの DNS サーバー アドレスは各 DAG メンバーの MAPI ネットワーク アダプターに対して構成され、レプリケーション ネットワーク アダプターに対しては何も構成されていません。冗長性のため、Contoso は MAPI ネットワーク アダプターに複数の DNS サーバー アドレスを使用します。

  - Contoso は Windows ファイアウォールを使用せず、サーバー上で無効になっています。

ネットワーク アダプターを構成すると、Contoso は DAG を作成して、DAG にメールボックス サーバーを追加する準備が整います。

## データベース可用性グループを作成して構成する

管理者は、いくつかのタスクを実行する Windows PowerShell コマンドライン インターフェイス スクリプトを作成することにしました。

  - スクリプトは [New-DatabaseAvailabilityGroup](https://technet.microsoft.com/ja-jp/library/dd351107\(v=exchg.150\)) コマンドレットを使用して DAG を作成します。REDMOND がプライマリ データセンターと見なされることから、Contoso は同一データセンター内に CAS1 という監視サーバーを使用することにしました。

  - スクリプトは [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/ja-jp/library/dd297934\(v=exchg.150\)) コマンドレットを使用して、データセンターの切り替えが必要となる場合に備え、代替監視サーバーと代替監視ディレクトリを事前構成します。

  - スクリプトは [Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/ja-jp/library/dd298049\(v=exchg.150\)) コマンドレットを使用して、DAG に 4 つのメールボックス サーバーをそれぞれ追加します。

  - スクリプトは [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/ja-jp/library/dd297934\(v=exchg.150\)) コマンドレットを使用して、DAC モードの DAG を構成します。DAC モードの詳細については、「[データセンター ライセンス認証調整モード](datacenter-activation-coordination-mode-exchange-2013-help.md)」を参照してください。

スクリプトで使用するコマンドを次に示します。

    New-DatabaseAvailabilityGroup -Name DAG1 -WitnessServer CAS1 -WitnessDirectory C:\DAGWitness\DAG1.contoso.com -DatabaseAvailabilityGroupIPAddresses 192.168.1.8,192.168.2.8

上記のコマンドは DAG DAG1 を作成し、ミラーリング監視サーバーとして機能するように CAS1 を構成し、特定のミラーリング監視ディレクトリ (C:\\DAGWitness\\DAG1.contoso.com) を構成し、DAG 用の 2 つの IP アドレス (MAPI ネットワークの各サブネット用) に構成します。

    Set-DatabaseAvailabilityGroup -Identity DAG1 -AlternateWitnessDirectory C:\DAGWitness\DAG1.contoso.com -AlternateWitnessServer CAS4

上記のコマンドは、CAS4 という代替ミラーリング監視サーバーと、CAS1 で構成されたのと同じパスを使用する CAS4 上の代替ミラーリング監視ディレクトリを使用するように、DAG1 を構成します。


> [!NOTE]
> 同じパスを使用することは必須ではありません。Contoso は同じパスを使用することで構成を標準化することを選択しました。



    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX3
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX2
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX4

このコマンドは、各メールボックス サーバーを 1 回に付き 1 つずつ DAG に追加します。上記のコマンドはまた、各メールボックス サーバーに Windows フェールオーバー クラスタリング コンポーネントをインストールし (未インストールの場合)、フェールオーバー クラスターを作成し、新しく作成したクラスターに各メールボックス サーバーを参加させます。

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatacenterActivationMode DagOnly

上記のコマンドは、DAG の DAC モードを有効にします。

## メールボックス データベースとメールボックス データベースのコピー

DAG を作成して DAG にメールボックス サーバーを追加した後、Contoso はメールボックス データベースとメールボックス データベースのコピーを作成する準備を行います。障害耐性の基準に合わせるため、Contoso は各メールボックス データベースを 3 つの時間差のないデータベース コピーと 1 つの時間差データベース コピーと構成することにします。時間差コピーには、3 日間のログ再生時間差が構成されます。

この構成により、各データベースに対して合計で 4 つのコピーが提供されます (1 つのアクティブ、2 つの時間差なしパッシブ、および時間差ありパッシブ)。Contoso は 1 サーバーあたり 4 つのアクティブ データベースを所有する予定です。1 つのサーバーあたり 4 つのアクティブなデータベースと、各データベースに 3 つのパッシブ コピーがあるため、Contoso ソリューションには、合計で 16 のデータベース コピーが含まれます。

以下の図にあるように、Contoso はデータベース レイアウトに均等なアプローチを取ります。

**Contoso, Ltd のデータベース コピー レイアウト**

![Contoso, Ltd のデータベース コピー レイアウト](images/Dd638129.41d0c78e-ccaf-4b67-8bab-6fb344668ead(EXCHG.150).gif "Contoso, Ltd のデータベース コピー レイアウト")

各メールボックス サーバーは、1 つのアクティブ メールボックス コピー、2 つの時間差なしパッシブ データベース コピー、および 1 つの時間差ありパッシブ データベース コピーをホストします。各アクティブ メールボックス データベースの時間差コピーは、もう一方のサイトのメールボックス サーバーにホストされます。

この構成を作成するのに、管理者はいくつかのコマンドを実行します。

MBX1 では、次のコマンドを実行します。

    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX2
    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX4
    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX3 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB1\MBX3 -SuspendComment "Seed from MBX4" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB1\MBX3 -SourceServer MBX4
    Suspend-MailboxDatabaseCopy -Identity DB1\MBX3 -ActivationOnly

MBX2 では、次のコマンドを実行します。

    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX1
    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX3
    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX4 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB2\MBX4 -SuspendComment "Seed from MBX3" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB2\MBX4 -SourceServer MBX3
    Suspend-MailboxDatabaseCopy -Identity DB2\MBX4 -ActivationOnly

MBX3 では、次のコマンドを実行します。

    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX4
    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX2
    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX1 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB3\MBX1 -SuspendComment "Seed from MBX2" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB3\MBX1 -SourceServer MBX2
    Suspend-MailboxDatabaseCopy -Identity DB3\MBX1 -ActivationOnly

MBX4 では、次のコマンドを実行します。

    Add-MailboxDatabaseCopy -Identity DB4 -MailboxServer MBX3
    Add-MailboxDatabaseCopy -Identity DB4 -MailboxServer MBX1
    Add-MailboxDatabaseCopy -Identity DB4 -MailboxServer MBX2 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB4\MBX2 -SuspendComment "Seed from MBX1" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB4\MBX2 -SourceServer MBX1
    Suspend-MailboxDatabaseCopy -Identity DB4\MBX2 -ActivationOnly

**Add-MailboxDatabaseCopy** コマンドレットの上記の例では、*ActivationPreference* パラメーターは指定されていませんでした。タスクは、追加される各コピーと共にアクティベーション優先番号を自動的に増大させます。元データベースは、常に優先番号 1 を持ちます。**Add-MailboxDatabaseCopy** コマンドレットによって最初に追加されたコピーには、自動的に優先番号 2 が割り当てられます。コピーが削除されなければ、次に追加されるコピーには優先番号 3 が割り当てられるというように続きます。このため、上記の例では、アクティブ コピーと同じデータセンターのパッシブ コピーはアクティベーション優先番号 2 を、リモート データセンターの時間差なしパッシブ コピーはアクティベーション優先番号 3 を、リモート データセンターの時間差パッシブ コピーはアクティベーション優先番号 4 を持ちます。

各アクティブ データベースには、WAN をまたがってもう一方の場所に 2 つのコピーが存在するものの、WAN 経由でのシードは 1 回しか実行されていません。これは、Contoso が Exchange 2013 の機能を利用することで、シードのシード元としてデータベースのパッシブ コピーを使用するためです。[Add-MailboxDatabaseCopy](https://technet.microsoft.com/ja-jp/library/dd298105\(v=exchg.150\)) コマンドレットに *SeedingPostponed* パラメーターを付けて使用することで、タスクは作成される新しいデータベース コピーの自動的なシードを行わなくなります。次に、管理者はシードされていないコピーを中断し、[Update-MailboxDatabaseCopy](https://technet.microsoft.com/ja-jp/library/dd335201\(v=exchg.150\)) コマンドレットに *SourceServer* パラメーターを付けて使用することで、管理者はシード操作のシード元としてデータベースのローカル コピーを指定できます。これにより、各場所に追加された第 2 のデータベース コピーのシードは、WAN 経由ではなく、ローカルで実行されます。


> [!NOTE]
> 上記の例では、時間差なしデータベース コピーは WAN 経由でシードされ、その後、そのコピーを使用して時間差なしコピーと同じデータセンターにあるデータベースの時間差コピーをシードします。



Contoso は、各メールボックス データベースのパッシブ コピーの 1 つを時間差データベース コピーとして構成することで、まれに発生する壊滅的なデータベースの論理的破損に対する保護を確立します。このため、管理者は [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/ja-jp/library/dd351074\(v=exchg.150\)) コマンドレットに *ActivationOnly* パラメーターを付けて使用することで、時間差コピーがアクティベーションに対してブロックされるように構成します。これにより、データベースやサーバーのフェールオーバーが発生しない限り、時間差データベース コピーがアクティブにならないようにします。

## ソリューションを検証する

ソリューションの展開および構成後、管理者は、運用メールボックスを DAG 内のデータベースに移動する前に、ソリューションの準備が整っていることを検証するいくつかのタスクを実行します。ソリューションは、障害シミュレーションを含むいくつかの方法を使用してテストして検査する必要があります。ソリューションを検証するため、管理者はいくつかのタスクを実行します。

DAG の総合的な正常性を確認するため、管理者は [Test-ReplicationHealth](https://technet.microsoft.com/ja-jp/library/bb691314\(v=exchg.150\)) コマンドレットを実行します。このコマンドレットは、レプリケーションと再生の状態のいくつかの側面を確認することで、DAG 内の各メールボックス サーバーとデータベース コピーに関する情報を提供します。

レプリケーションと再生の動作を確認するため、管理者は [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/ja-jp/library/dd298044\(v=exchg.150\)) コマンドレットを実行します。このコマンドレットは、特定のメールボックス データベース コピー、または特定サーバー上のすべてのメールボックス データベース コピーに関するリアルタイム状態情報を提供できます。DAG 内のレプリケーションされたデータベースの正常性と状態の監視の詳細については、「[データベース可用性グループの監視](monitoring-database-availability-groups-exchange-2013-help.md)」を参照してください。

切り替えが期待通りに機能することを確認するため、管理者は [Move-ActiveMailboxDatabase](https://technet.microsoft.com/ja-jp/library/dd298068\(v=exchg.150\)) コマンドレットを使用して、一連のデータベース切り替えとサーバー切り替えを実行します。これらのタスクが正常に完了したら、管理者は同じコマンドレットを使用して、アクティブ データベース コピーを元の場所に戻します。

さまざまな障害シナリオでの期待される動作を確認するため、管理者は障害をシミュレートした李、実際に障害を発生させるいくつかのタスクを実行します。たとえば、管理者は以下の操作を実行する場合があります。

  - MBX1 の電源コードを抜き取り、サーバー フェールオーバーをトリガーします。その後、管理者はもう 1 つのサーバーで DB1 がアクティブになることを確認します (アクティベーションの優先の値から、MBX2 が望ましい)。

  - MBX2 の MAPI ネットワーク アダプターのネットワーク ケーブルを引き抜き、サーバー フェールオーバーをトリガーします。その後、管理者はもう 1 つのサーバーで DB2 がアクティブになることを確認します (アクティベーションの優先の値から、MBX1 が望ましい)。

  - DB3 のアクティブ コピーに使用されるディスクをオフラインで取り外し、データベース フェールオーバーをトリガーします。その後、管理者はもう 1 つのサーバーで DB3 がアクティブになることを確認します (アクティベーションの優先の値から、MBX4 が望ましい)。

ビジネス ニーズに応じて、組織がテストする障害シナリオは他にも挙げられます。単一障害 (電源プラグの引き抜きなど) をシミュレートし、ソリューションの回復動作を確認したら、管理者はソリューションを本来の構成へと戻すことができます。場合によっては、複数同時障害についてソリューションをテストする場合があります。ソリューション テスト計画では、最終的には各障害シミュレーションの完了後、ソリューションを本来の構成へと戻す必要があります。

さらに、管理者は 2 つのデータセンター間のネットワーク接続を切断して、サイト障害をシミュレートする場合があります。データセンター切り替えの実行はさらに複雑で調整が必要な処理です。ただし、展開されるソリューションがメッセージング サービスとデータのサイト復元を提供することを目的としている場合、データセンター切り替えは推奨される処理となります。

## 運用に移行する

ソリューションの展開後、増分展開を使用してソリューションをさらに拡張することができます。このとき、ソリューションの管理も運用処理へと移行します。このとき、以下のタスクが実行されます。

  - DAG とメールボックス データベース コピーの正常性と状態を監視します。詳細については、「[データベース可用性グループの監視](monitoring-database-availability-groups-exchange-2013-help.md)」を参照してください。

  - 必要に応じて、データベースの切り替えを実行します。データベース切り替えを実行する方法の詳細手順については、「[メールボックス データベース コピーをアクティブにする](activate-a-mailbox-database-copy-exchange-2013-help.md)」を参照してください。

ソリューションの管理の詳細については、「[高可用性とサイト復元の管理](managing-high-availability-and-site-resilience-exchange-2013-help.md)」を参照してください。

