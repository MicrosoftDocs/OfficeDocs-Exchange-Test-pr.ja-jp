---
title: 'POP3 の予定表オプションを構成する: Exchange 2013 Help'
TOCTitle: POP3 の予定表オプションを構成する
ms:assetid: ac3d60a0-8697-4c06-9e93-f8d2c4b157b6
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124133(v=EXCHG.150)
ms:contentKeyID: 50555850
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# POP3 の予定表オプションを構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-11-27_

シェルを使用して、POP3 接続を使用してメールボックスに接続するユーザーの予定表アクセス設定を構成できます。指定する設定により、POP3 ユーザーによる予定表のアクセスや、他のユーザーとの予定表情報のやり取り (たとえば、会議出席依頼の送信や応答など) を行う方法が決まります。

POP3 に関連する詳細情報については、「[Exchange Server 2013 での POP3 と IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「POP3 の設定」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## シェルを使用して POP3 の予定表オプションを設定する

この例では、POP3 ユーザーが iCalendar 標準 (予定表情報をやり取りするための標準) を使用できるようにします。

```powershell
Set-PopSettings -Identity CAS01 -CalendarItemRetrievalOption iCalendar
```

この例では、POP3 ユーザーが内部のサーバーから予定表情報にアクセスできるようにします。

  ```powershell
  Set-PopSettings -Identity CAS01 -CalendarItemRetrievalOption IntranetUrl 
  ```

この例では、POP3 ユーザーが外部のサーバー上のインターネットから予定表の情報にアクセスできるようにします。

```powershell
Set-PopSettings -CalendarItemRetrievalOption InternetUrl
```

この例では、直接の Outlook Web App URL を使用して、POP3 ユーザーが予定表情報にアクセスできるようにします。`Custom` を使用する場合は、*OWAServerUrl* パラメーターを使用して Outlook Web App URL を指定する必要があります。

```powershell
Set-PopSettings -CalendarItemRetrievalOption Custom -OwaServerUrl "https://OwaServer01"
```

POP3 に予定表オプションを指定した後、POP3 サービスを再起動する必要があります。POP3 サービスを再起動する方法の詳細については、「[POP3 サービスの開始および停止](start-and-stop-the-pop3-services-exchange-2013-help.md)」を参照してください。

構文およびパラメーターの詳細については、「[Set-PopSettings](https://technet.microsoft.com/ja-jp/library/aa997154\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

予定表オプションが正常に設定されたことを確認するには、次の手順を実行します。

シェルで、次のコマンドを実行します。

```powershell
Get-PopSettings | format-list
```

予定表の設定が正しいことを確認します。

## 詳細情報

POP3 の予定表オプションを設定した後で、次の操作も実行できます。

[POP3 および IMAP4 のメッセージ取得形式オプションを構成する](configure-pop3-and-imap4-message-retrieval-format-options-exchange-2013-help.md)

[POP3 の接続タイムアウト制限を設定する](set-connection-time-out-limits-for-pop3-exchange-2013-help.md)

