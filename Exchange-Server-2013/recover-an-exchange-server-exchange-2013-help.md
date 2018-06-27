---
title: 'Exchange Server を回復する: Exchange 2013 Help'
TOCTitle: Exchange Server を回復する
ms:assetid: 46e9a1cf-b64c-43c3-a898-6171176da761
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd876880(v=EXCHG.150)
ms:contentKeyID: 48269440
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange Server を回復する

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2016-12-09_

Microsoft Exchange Server 2013 で **Setup /m:RecoverServer** スイッチを使用することにより、失われたサーバーを回復できます。Exchange 2013 を実行しているコンピューターの設定の大部分は、Active Directory に格納されます。*/m:RecoverServer* スイッチを使用すると、Exchange に格納された設定およびその他の情報によって、Active Directory サーバーが同じ名前で再構築されます。

失われた Exchange サーバーの回復は、多くの場合、新しいハードウェアを使用して実施されます。ただし、既存のサーバーを使用することもできます。

ここでは、データベース可用性グループ (DAG) に属していない失われた Exchange 2013 サーバーを回復する方法を示します。DAG に属していたサーバーを回復する方法の詳細手順については、「[データベース可用性グループのメンバー サーバーを回復させる](recover-a-database-availability-group-member-server-exchange-2013-help.md)」を参照してください。


> [!NOTE]
> Exchange が既定以外の場所にインストールされる場合、<EM>/TargetDir</EM> スイッチを使用して、Exchange のバイナリ ファイルの場所を指定する必要があります。<EM>/TargetDir</EM> スイッチを使用しない場合、Exchange のファイルは既定の場所 (%programfiles%\Microsoft\Exchange Server\V15) にインストールされます。<BR>インストールの場所を決めるには、次の手順に従います。 
> <OL>
> <LI>
> <P>ADSIEDIT.MSC または LDP.EXE を開きます。</P>
> <LI>
> <P>次の場所に移動します。<STRONG>CN=ExServerName,CN=Servers,CN=First Administrative Group,CN=Administrative Groups,CN=ExOrg Name,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=DomainName,CN=Com</STRONG></P>
> <LI>
> <P>Exchange サーバー オブジェクトを右クリックし、<STRONG>[プロパティ]</STRONG> をクリックします。</P>
> <LI>
> <P><STRONG>msExchInstallPath</STRONG> 属性を探します。この属性には、現在のインストール パスが格納されます。</P></LI></OL>



データのバックアップと復元に関する他の管理タスクについては、「[バックアップ、復元、および障害回復](backup-restore-and-disaster-recovery-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 20 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。 「[Exchange およびシェル インフラストラクチャのアクセス許可](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)」の「Exchange インフラストラクチャ アクセス許可」。

  - 回復が行われているサーバーは、失われたサーバーと同じオペレーティング システムを実行している必要があります。たとえば、Exchange 2013 および Windows Server 2008 R2 を実行していたサーバーを Windows Server 2012 を実行しているサーバー上に回復することはできません。また、その逆もできません。同様に、Exchange 2013 と Windows Server 2012 を実行していたサーバーを Windows Server 2012 R2 を実行しているサーバー上に回復することはできません。また、その逆もできません。

  - データベースがマウントされていた障害が発生したサーバーと同じディスク ドライブ文字が、回復を実行しているサーバーになければなりません。

  - 回復が行われているサーバーは、パフォーマンス特性およびハードウェア構成が失われたサーバーと同じでなくてはなりません。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 失われた Exchange サーバーを回復する

1.  失われたサーバーのコンピューター アカウントをリセットします。詳細な手順については、「[コンピューター アカウントをリセットする](https://go.microsoft.com/fwlink/p/?linkid=165388)」を参照してください。

2.  適切なオペレーティング システムをインストールして、新規サーバーに失われたサーバーと同じ名前をつけます。回復が行われているサーバーが失われたサーバーと名前が同じでない場合は、回復が成功しません。

3.  サーバーを失われたサーバーと同じドメインに追加します。

4.  必要な前提条件とオペレーティング システム コンポーネントをインストールします。詳細については、「[Exchange 2013 のシステム要件](exchange-2013-system-requirements-exchange-2013-help.md)」および「[Exchange 2013 の前提条件](exchange-2013-prerequisites-exchange-2013-help.md)」を参照してください。

5.  回復されたサーバーにログオンして、コマンド プロンプトを開きます。

6.  Exchange 2013 インストール ファイルの場所に移動し、次のコマンドを実行します。
    
        Setup /m:RecoverServer /IAcceptExchangeServerLicenseTerms

7.  Setup コマンドの完了後、回復されたサーバーを運用に移す前に、サーバーに以前存在したカスタム設定を再構成して、その後でサーバーを再起動します。

## 正常な動作を確認する方法

Setup コマンドの正常終了は、回復が成功したことを示す主要な指標になります。失われたサーバーが正常に回復されたことを確認するには、次の手順を実行します。

  - Windows サービス ツール (services.msc) を開いて、Microsoft Exchange サービスがインストールされており実行中であることを確認します。

