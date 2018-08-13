---
title: 'データベース可用性グループのメンバー サーバーを回復させる: Exchange 2013 Help'
TOCTitle: データベース可用性グループのメンバー サーバーを回復させる
ms:assetid: eccd8f61-9706-4bb7-a62a-ec7c166f8019
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd638206(v=EXCHG.150)
ms:contentKeyID: 48270217
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# データベース可用性グループのメンバー サーバーを回復させる

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

データベース可用性グループ (DAG) のメンバーであるメールボックス サーバーが失われたか、または障害が発生し、回復不能で交換が必要な場合は、サーバー回復操作を実行することができます。Microsoft Exchange Server 2013 セットアップには、サーバー回復操作を実行するために使用するスイッチ */m:RecoverServer* が含まれています。セットアップを */m:RecoverServer* スイッチで実行すると、セットアップは、セットアップの実行に使用されたサーバーと同じ名前を持つサーバーの構成情報を Active Directory から読み取ります。Active Directory からサーバーの構成情報を収集した後、元の Exchange ファイルとサービスはサーバーにインストールされ、Active Directory に保存されていた役割と設定がサーバーに適用されます。

DAG に関連する他の管理タスクについては、「[データベース可用性グループの管理](managing-database-availability-groups-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 30 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[高可用性とサイト復元のアクセス許可](high-availability-and-site-resilience-permissions-exchange-2013-help.md)」の「メールボックス データベースのコピー」。

  - Exchange が既定以外の場所にインストールされる場合、*/TargetDir* セットアップ スイッチを使用して、Exchange のプログラム ファイルの場所を指定する必要があります。*/TargetDir* スイッチを使用しない場合、Exchange のプログラム ファイルは既定の場所 (%programfiles%\\Microsoft\\Exchange Server\\V15) にインストールされます。
    
    インストールの場所を決めるには、次の手順に従います。
    
    1.  ADSIEDIT.MSC または LDP.EXE を開きます。
    
    2.  次の場所に移動します。**CN=ExServerName,CN=Servers,CN=First Administrative Group,CN=Administrative Groups,CN=ExOrg Name,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=DomainName,CN=Com**
    
    3.  Exchange サーバー オブジェクトを右クリックし、**\[プロパティ\]** をクリックします。
    
    4.  **msExchInstallPath** 属性を探します。この属性には、現在のインストール パスが格納されます。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## サーバーを回復するためのセットアップ /m:RecoverServer の使用

1.  次の [Get-MailboxDatabase](https://technet.microsoft.com/ja-jp/library/bb124924\(v=exchg.150\)) コマンドレットを使用して、回復対象のサーバーに存在するいずれかのメールボックス データベース コピーのすべての再生ラグ設定または切り詰めラグ設定を取得します。
    
        Get-MailboxDatabase DB1 | Format-List *lag*

2.  次の [Remove-MailboxDatabaseCopy](https://technet.microsoft.com/ja-jp/library/dd335119\(v=exchg.150\)) コマンドレットを使用して、回復対象のサーバーに存在するいずれかのメールボックス データベース コピーを削除します。
    
        Remove-MailboxDatabaseCopy DB1\MBX1

3.  次の [Remove-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/ja-jp/library/dd297956\(v=exchg.150\)) コマンドレットを使用して、失敗したサーバーの構成を DAG から削除します。
    
        Remove-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1
    

    > [!NOTE]
    > 削除される DAG メンバーがオフラインになっており、オンラインにすることができない場合は、<EM>ConfigurationOnly</EM> パラメーターを前のコマンドに追加する必要があります。<EM>ConfigurationOnly</EM> スイッチを使用する場合、ノードをクラスターから手動で削除する必要もあります。



4.  Active Directory 内のサーバー コンピューター アカウントをリセットします。詳細な手順については、「[コンピューター アカウントをリセットする](http://go.microsoft.com/fwlink/p/?linkid=167188)」を参照してください。

5.  コマンド プロンプト ウィンドウを開きます。元のセットアップ メディアを使用して、次のコマンドを実行します。
    
        Setup /m:RecoverServer

6.  セットアップ回復処理が完了したら、次の [Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/ja-jp/library/dd298049\(v=exchg.150\)) コマンドレットを使用して、回復したサーバーを DAG に追加します。
    
        Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1

7.  サーバーを DAG に再び追加したら、[Add-MailboxDatabaseCopy](https://technet.microsoft.com/ja-jp/library/dd298105\(v=exchg.150\)) コマンドレットを使用して、メールボックス データベース コピーを再構成できます。追加対象のデータベース コピーのいずれかの再生ラグ タイムまたは切り詰めラグ タイムが以前に、0 よりも大きい値に設定されていた場合は、次の [Add-MailboxDatabaseCopy](https://technet.microsoft.com/ja-jp/library/dd298105\(v=exchg.150\)) コマンドレットの *ReplayLagTime* パラメーターと *TruncationLagTime* パラメーターを使用して、これらの設定を再構成することができます。
    
        Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX1
        Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX1 -ReplayLagTime 3.00:00:00
        Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX1 -ReplayLagTime 3.00:00:00 -TruncationLagTime 3.00:00:00

## 正常な動作を確認する方法

DAG メンバーが正常に復元されたことを確認するには、次の手順を実行します。

  - シェルで次のコマンドを実行して、復元された DAG メンバーの正常性と状態を確認します。
       ```
        Test-ReplicationHealth <ServerName>
       ```
       ```
        Get-MailboxDatabaseCopyStatus -Server <ServerName>
       ```
    すべてのレプリケーションの正常性テストに正常に合格し、データベースとそのコンテンツ インデックスの状態が正常でなければなりません。

