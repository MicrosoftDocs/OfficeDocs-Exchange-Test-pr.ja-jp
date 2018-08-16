---
title: 'メールボックス監査ログの検索を作成する: Exchange 2013 Help'
TOCTitle: メールボックス監査ログの検索を作成する
ms:assetid: 48ba22cf-b1f2-4dbc-98fc-fed22d97db14
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff461929(v=EXCHG.150)
ms:contentKeyID: 49896231
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックス監査ログの検索を作成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-11_

メールボックス監査ログ検索を作成して 1 つ以上のメールボックスを非同期に検索し、検索結果を XML ファイルとして指定したアドレスに電子メールで送信できます。

1 つのメールボックスのメールボックス監査ログを検索し、結果をシェル ウィンドウに表示させるには、「[メールボックスのメールボックス監査ログを検索する](search-the-mailbox-audit-log-for-a-mailbox-exchange-2013-help.md)」を参照してください。

メールボックス監査ログに関連する追加の管理タスクについては、「[メールボックス監査ログの手順](mailbox-audit-logging-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」トピックの「メールボックス監査ログ」エントリ。

  - 既定では、すべてのメールボックスに対してメールボックス監査ログは無効になっています。 監査するメールボックスそれぞれについて監査ログを有効にし、監査を行うメールボックスの所有者、代理人、または管理者の操作を指定する必要があります。 詳細については、「[メールボックスのメールボックス監査ログを有効または無効にする](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md)」を参照してください。

  - EAC を使用してメールボックス監査ログを検索して所有者のアクセスを見つけることはできません。 EAC の監査セクションには、所有者以外のメールボックス アクセスに関するレポートが表示されており、これを使用して、所有者以外のアクセス イベントを検索し、エクスポートすることもできます。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EAC を使用して、メールボックス監査ログ検索を作成する

1.  <strong>コンプライアンス管理</strong> \> <strong>監査</strong> に移動します。

2.  リスト ビューで、<strong>メールボックス監査ログのエクスポート</strong> を選択します。

3.  <strong>メールボックス監査ログのエクスポート</strong> で、次のフィールドに入力してから <strong>エクスポート</strong> をクリックします。
    
      - <strong>開始日</strong>
    
      - <strong>終了日</strong>
    
      - **これらのメールボックスを検索するか、このフィールドを空欄のままにして所有者以外のユーザーによってアクセスされたすべてのメールボックスを検索します。**
        

        > [!NOTE]
        > 組織内のメールボックス数と各メールボックス内のメールボックス監査ログ データ数によっては、すべてのメールボックスの検索に時間がかかる場合があります。

    
      - <strong>次のユーザーによるアクセスを検索する</strong>
        
        検索するアクセス イベントの種類を以下から選択します:
        
          - <strong>所有者以外すべて</strong>
        
          - <strong>外部ユーザー</strong>
        
          - <strong>管理者と委任されたユーザー</strong>
        
          - <strong>管理者</strong>
    
      - <strong>監査レポートの送信先</strong>

## シェルを使用して、メールボックス監査ログ検索を作成する

シェルを使用してメールボックス監査ログ検索を作成する方法の例は、「**New-MailboxAuditLogSearch**」の「[Example 1](https://technet.microsoft.com/ja-jp/95365cab-bbb2-4a64-8e8f-1c89fa9e0352\(exchg.150\)#example1)」を参照してください。

