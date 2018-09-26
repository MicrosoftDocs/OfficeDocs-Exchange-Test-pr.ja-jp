---
title: '管理者監査ログの管理: Exchange 2013 Help'
TOCTitle: 管理者監査ログの管理
ms:assetid: 15c284c0-b8e6-42ca-9913-7c59fdb6885d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd335109(v=EXCHG.150)
ms:contentKeyID: 50555733
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理者監査ログの管理

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2013-05-17_

Microsoft Exchange Server 2013 の管理者監査ログにより、指定されたコマンドレットを実行するたびにログ エントリを作成できます。ログ エントリには、実行されたコマンドレット、使用されたパラメーター、コマンドレットを実行したユーザー、および影響を受けたオブジェクトに関する情報が記録されます。管理者監査ログの詳細については、「[管理者監査ログ](administrator-audit-logging-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分未満

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[Exchange およびシェル インフラストラクチャのアクセス許可](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)」の「管理者監査ログ」。

  - 管理者の監査ログは、Active Directory レプリケーションに依存して、組織内のドメイン コントローラーに指定する構成設定をレプリケートします。レプリケーション設定によっては、加えた変更が組織内のすべての Exchange 2013 サーバーに直ちに適用されない場合もあります。

  - 監査ログ構成への変更は、構成変更の実行時にシェルを開いたコンピューター上で 60 分ごとに更新されます。変更を直ちに適用するには、各コンピューター上でシェルを閉じてから再度開きます。

  - コマンドは、実行してから監査ログの検索結果に表示されるまで、最大 15 分かかることがあります。そのため、監査ログのエントリをインデックス処理してから検索してください。管理者監査ログにコマンドが表示されない場合は、数分待機してから検索を再実行してください。

  - これらの手順を実行するには、シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## 監査の対象となるコマンドレットを指定する

既定では、監査ログによって実行されるすべてのコマンドレットのログ エントリが作成されます。初めて監査ログを有効にしてこの動作を望む場合、コマンドレットの監査リストを変更する必要はありません。以前は監査するコマンドレットを指定していて、今回はすべてのコマンドレットを監査する場合、次のコマンドで示すように、**Set-AdminAuditLogConfig** コマンドレットの *AdminAuditLogCmdlets* パラメーターでアスタリスク (\*) ワイルドカード文字を指定すると、すべてのコマンドレットを監査できます。

```powershell
    Set-AdminAuditLogConfig -AdminAuditLogCmdlets *
```

監査するコマンドレットを指定するには、*AdminAuditLogCmdlets* パラメーターを使用してコマンドレットの一覧を提供する必要があります。監査するコマンドレットの一覧を提供する場合、単一のコマンドレット、アスタリスク (\*) ワイルドカード文字を指定したコマンドレット、またはその両方が混在したものを提供できます。一覧の各エントリはコンマで区切られています。次の値はすべて有効です。

  - `New-Mailbox`

  - `*TransportRule`

  - `*Management*`

  - `Set-Transport*`

この例では、上記の一覧で指定されたコマンドレットを監査します。

```powershell
    Set-AdminAuditLogConfig -AdminAuditLogCmdlets New-Mailbox, *TransportRule, *Management*, Set-Transport*
```

構文およびパラメーターの詳細については、「[Set-AdminAuditLogConfig](https://technet.microsoft.com/ja-jp/library/dd298169\(v=exchg.150\))」を参照してください。

## 監査の対象となるパラメーターを指定する

既定では、監査ログによって、指定されたパラメーターに無関係に実行されるすべてのコマンドレットのログ エントリが作成されます。初めて監査ログを有効にしてこの動作を望む場合、パラメーターの監査リストを変更する必要はありません。以前は監査するパラメーターを指定していて、今回はすべてのパラメーターを監査する場合、次のコマンドで示すように、**Set-AdminAuditLogConfig** コマンドレットの *AdminAuditLogParameters* パラメーターでアスタリスク (\*) ワイルドカード文字を指定すると、すべてのパラメーターを監査できます。

```powershell
    Set-AdminAuditLogConfig -AdminAuditLogParameters *
```

*AdminAuditLogParameters* パラメーターを使用すると、監査するパラメーターを指定できます。監査するパラメーターの一覧を提供する場合、単一のパラメーター、アスタリスク (\*) ワイルドカード文字を指定したパラメーター、またはその両方が混在したものを提供できます。一覧の各エントリはコンマで区切られています。次の値はすべて有効です。

  - `Database`

  - `*Address*`

  - `Custom*`

  - `*Region`


> [!NOTE]
> コマンドの実行時に監査ログ エントリを作成するには、コマンドに、<EM>AdminAuditLogCmdlets</EM> パラメーターで指定した少なくとも 1 つ以上のコマンドレットに存在している少なくとも 1 つ以上のパラメーターを指定する必要があります。



この例では、上記の一覧で指定されたパラメーターを監査します。

```powershell
    Set-AdminAuditLogConfig -AdminAuditLogParameters Database, *Address*, Custom*, *Region
```

構文およびパラメーターの詳細については、「[Set-AdminAuditLogConfig](https://technet.microsoft.com/ja-jp/library/dd298169\(v=exchg.150\))」を参照してください。

## 監査ログの有効期限を指定する

監査ログ有効期限は、監査ログ エントリを保持する期間を指定します。有効期限を過ぎると、ログ エントリは削除されます。既定値は 90 日です。

監査ログ エントリを保存しておく日数、時間数、分数、秒数を指定できます。値を指定するには、dd.hh.mm:ss (各項の意味は以下を参照) の形式を使用します。

  - **dd**   監査ログ エントリを保持する日数

  - **hh**   監査ログ エントリを保持する時間数

  - **mm**   監査ログ エントリを保持する分数

  - **ss**   監査ログ エントリを保持する秒数


> [!NOTE]
> 監査ログの有効期限は、現在の有効期限よりも小さく指定できます。この場合、新たに指定した有効期限を超えている監査ログ エントリは削除されます。<BR>有効期限を 0 に設定すると、Exchange により監査ログのエントリがすべて削除されます。<BR>監査ログの有効期限を構成するためのアクセス許可は、十分に信頼できるユーザーのみに付与することをお勧めします。



この例では、有効期限を 2 年 6 か月に指定します。

```powershell
Set-AdminAuditLogConfig -AdminAuditLogAgeLimit 913.00:00:00
```

構文およびパラメーターの詳細については、「[Set-AdminAuditLogConfig](https://technet.microsoft.com/ja-jp/library/dd298169\(v=exchg.150\))」を参照してください。

## Test コマンドレットのログ記録を有効または無効にする

動詞 **Test** で始まるコマンドレットは、既定ではログ記録されません。これは、**Test** コマンドレットが短時間で膨大なデータを生成できるためです。**Test** コマンドレットのログ記録を有効にする場合は短時間のみにとどめてください。

このコマンドは、**Test** コマンドレットを有効にします。

```powershell
Set-AdminAuditLogConfig -TestCmdletLoggingEnabled $True
```

このコマンドは、**Test** コマンドレットを無効にします。

```powershell
Set-AdminAuditLogConfig -TestCmdletLoggingEnabled $False
```

構文およびパラメーターの詳細については、「[Set-AdminAuditLogConfig](https://technet.microsoft.com/ja-jp/library/dd298169\(v=exchg.150\))」を参照してください。

## 管理者監査ログを無効にする

管理者監査ログを無効にするには、次のコマンドを使用します。

```powershell
Set-AdminAuditLogConfig -AdminAuditLogEnabled $False
```

## 管理者監査ログを有効にする

管理者の監査ログを有効にするには、次のコマンドを使用します。

```powershell
Set-AdminAuditLogConfig -AdminAuditLogEnabled $True
```

## 管理者監査ログの設定を表示する

組織に対して既に設定した、管理者の監査ログ構成の設定を表示するには、次のコマンドを使用します。

```powershell
Get-AdminAuditLogConfig
```

