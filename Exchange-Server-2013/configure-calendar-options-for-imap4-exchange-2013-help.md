---
title: 'IMAP4 の予定表オプションを構成する: Exchange 2013 Help'
TOCTitle: IMAP4 の予定表オプションを構成する
ms:assetid: 6679c8b2-3f0f-449a-a17c-a7b30001538c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998606(v=EXCHG.150)
ms:contentKeyID: 50555794
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# IMAP4 の予定表オプションを構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-11-27_

シェルを使用して、IMAP4 接続を使用して自分のメールボックスに接続するユーザーの予定表アクセス設定を構成できます。指定した設定によって、IMAP4 ユーザーが予定表にアクセスする方法と予定表情報を他のユーザーと交換する方法 (会議出席依頼の送信方法または応答方法) が決まります。

IMAP4 に関連する詳細情報については、「[Exchange Server 2013 での POP3 と IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間: 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「IMAP4 の設定」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## シェルを使用して IMAP4 の予定表オプションを設定する

この例では、IMAP4 ユーザーが予定表情報を交換する標準である iCalendar 標準を使用できるようにします。

```powershell
Set-ImapSettings -Identity CAS01 -CalendarItemRetrievalOption iCalendar
```

この例では、IMAP4 ユーザーが内部サーバーから予定表情報にアクセスできるようにします。

```powershell
    Set-ImapSettings -Identity CAS01 -CalendarItemRetrievalOption IntranetUrl 
```

この例では、IMAP4 ユーザーが外部サーバー上のインターネットから予定表情報にアクセスできるようにします。

```powershell
Set-ImapSettings -CalendarItemRetrievalOption InternetUrl
```

この例では、IMAP4 ユーザーが直接 Outlook Web App の URL を使用して予定表情報にアクセスできるようにします。`Custom` を使用している場合、*OWAServerUrl* パラメーターを使用して Outlook Web App URL を指定する必要があります。

```powershell
Set-Imap4Settings -CalendarItemRetrievalOption Custom -OwaServerUrl "https://OwaServer01"
```

IMAP4 の予定表オプションを指定した後に、IMAP4 サービスを再起動する必要があります。IMAP4 サービスを再起動する方法の詳細については、「[IMAP4 サービスの開始および停止](start-and-stop-the-imap4-services-exchange-2013-help.md)」を参照してください。

構文およびパラメーターの詳細については、「[Set-ImapSettings](https://technet.microsoft.com/ja-jp/library/aa998252\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

予定表オプションが正常に設定されたことを確認するには、次の手順を実行します。

シェルで、次のコマンドを実行します。

```powershell
Get-ImapSettings | format-list
```

予定表の設定が正しいことを確認します。

## 詳細情報

IMAP4 の予定表オプションを設定した後、必要に応じて次の操作も実行してください。

[POP3 および IMAP4 のメッセージ取得形式オプションを構成する](configure-pop3-and-imap4-message-retrieval-format-options-exchange-2013-help.md)

[IMAP4 の接続タイムアウト制限を設定する](set-connection-time-out-limits-for-imap4-exchange-2013-help.md)

