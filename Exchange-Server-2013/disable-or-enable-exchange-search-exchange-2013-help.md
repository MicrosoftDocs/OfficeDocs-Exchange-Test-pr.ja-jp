---
title: 'Exchange Search を無効または有効にする: Exchange 2013 Help'
TOCTitle: Exchange Search を無効または有効にする
ms:assetid: 195b25be-53fb-4215-90a5-04340d640bcc
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa996416(v=EXCHG.150)
ms:contentKeyID: 52057799
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Search を無効または有効にする

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-05-07_

既定で、Exchange Search はすべての新規メールボックス データベースで有効になっており、追加の構成は必要ありません。ただし、Exchange Search によるメールボックスの内容のインデックス処理を停止する場合は、個々のメールボックス データベースまたはメールボックス サーバー全体に対して無効にできます。


> [!NOTE]
> Exchange Search を無効にすると、Outlook のオンライン モードの使用時、あるいは Windows モバイル デバイス上において、ユーザーが実行するフルテキスト検索の機能やパフォーマンスが影響を受けます。<BR><A href="in-place-ediscovery-exchange-2013-help.md">インプレース電子情報開示 (eDiscovery)</A> も Exchange Search に依存しています。メールボックス データベースまたはメールボックス サーバーの Exchange Search を無効にすると、インプレース電子情報開示の検索が実行されてもデータベースまたはサーバーからメッセージが返らなくなります。



Exchange Search に関連するその他の管理タスクについては、「[Exchange Search の手順](exchange-search-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:1 分

  - このトピックの手順には、特定のアクセス許可が必要です。アクセス許可情報については、各手順を参照してください。

  - Exchange Search は、サーバーまたはメールボックス データベースに対して有効または無効にすることができますが、個々のメールボックス ユーザーに対して有効または無効にすることはできません。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## 必要な作業

## メールボックス データベースの Exchange Search を無効または有効にする

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「Exchange Search」。


> [!NOTE]
> EAC を使用して、メールボックス データベースの Exchange Search を無効にしたり有効にしたりすることはできません。



このコマンドは、EXCH01 という名前のメールボックス データベースの Exchange Search を無効にします。

    Set-MailboxDatabase "Mailbox Database (EXCH01)" -IndexEnabled $false

このコマンドは、EXCH01 という名前のメールボックス データベースの Exchange Search を有効にします。

    Set-MailboxDatabase "Mailbox Database (EXCH01)" -IndexEnabled $true

構文およびパラメーターの詳細については、「[Set-MailboxDatabase](https://technet.microsoft.com/ja-jp/library/bb123971\(v=exchg.150\))」を参照してください。

## メールボックス サーバーの Exchange Search を無効または有効にする

メールボックス サーバーの Exchange Search を無効にするには、Microsoft Exchange Search サービスを無効にして停止する必要があります。同様に、メールボックス サーバーの Exchange Search を有効にするには、Microsoft Exchange Search サービスを有効にして開始する必要があります。これは、サービス コンソールまたはシェルを使用して行うことができます。

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「メールボックス サーバーの Exchange Search サービスを管理する」。

**サービス コンソールを使用する**

1.  **\[スタート\]** \> **\[管理ツール\]** \> **\[サービス\]** に移動します。

2.  **\[サービス\]** 詳細ウィンドウで、**\[Microsoft Exchange Search\]** サービスを右クリックし、**\[プロパティ\]** を選択します。

3.  **\[全般\]** タブの **\[スタートアップの種類\]** ボックスで、**\[無効\]** を選択してサービスを無効にするか、または **\[自動\]** を選択してサービスが自動で開始するようにします。
    

    > [!NOTE]
    > スタートアップの種類は次回のサービス開始に影響を与え、サーバーの再起動後にサービスが自動で開始するか、または手動でサービスを開始するかを決定します。次の手順では、サービスを手動で開始または停止します。



4.  **\[停止\]** をクリックしてサービスを停止するか、**\[開始\]** をクリックしてサービスを開始します。

5.  **\[OK\]** をクリックして変更を保存します。

**シェルを使用する**

次のコマンドを実行して、Microsoft Exchange Search サービスを停止して無効にします。
```
Stop-Service MSExchangeFastSearch
```
```
Set-Service MSExchangeFastSearch -StartupType Disabled
```

次のコマンドを実行して、Exchange Search サービスを自動的に起動するように構成してから、サービスを開始します。
```
Set-Service MSExchangeFastSearch -StartupType Automatic
```
```
Start-Service MSExchangeFastSearch
```
