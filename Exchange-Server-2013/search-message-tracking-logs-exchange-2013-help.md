---
title: 'メッセージ追跡ログの検索: Exchange 2013 Help'
TOCTitle: メッセージ追跡ログの検索
ms:assetid: e1678327-bcd5-42d4-a363-67f33067fe9a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124926(v=EXCHG.150)
ms:contentKeyID: 51407594
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メッセージ追跡ログの検索

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2013-02-25_

Microsoft Exchange Server 2013 のメッセージ追跡ログは、メッセージがメールボックス サーバーのトランスポート サービス、メールボックス サーバーのメールボックス、およびエッジ トランスポート サーバーとの間で転送される際のすべてのアクティビティを詳細に記録したものです。

Exchange 管理シェルで **Get-MessageTrackingLog** コマンドレットを使用することで、メッセージ追跡ログのエントリを特定の検索条件で検索できます。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 30 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「Message tracking (メッセージ追跡)」。

  - メッセージ追跡ログの検索を行うには、Microsoft Exchange Transport Log Search サービスを実行している必要があります。このサービスを無効にするか停止すると、メッセージ追跡ログの検索や配信レポートの実行ができません。ただし、このサービスを停止しても Exchange のその他の機能には影響しません。

  - **Get-MessageTrackingLog** コマンドレットからの結果に表示されるフィールド名は、メッセージ追跡ログで使われる実際のフィールド名とほぼ同じです。主な違いは次のとおりです。
    
      - ダッシュは、フィールド名から削除されます。たとえば、**internal-message-id** は、`InternalMessageId` と表示されます。
    
      - **date-time** フィールドは、`Timestamp`として表示されます。
    
      - **recipient-address** フィールドは、`Recipients` として表示されます。
    
      - **sender-address** フィールドは、`Sender` として表示されます。

  - メッセージ追跡ログの **date-time** フィールドは世界協定時刻 (UTC) で情報を格納します。ただし、*Start* パラメーターまたは *End* パラメーターの日時検索条件は、検索の実行に使用しているコンピューターの地域の日時形式で入力する必要があります。

  - 別の Exchange サーバーからメッセージ追跡ログ ファイルをコピーし、それを **Get-MessageTrackingLog** コマンドレットで検索することはできません。また、既存のメッセージ追跡ログを手動で保存した場合、ファイルのタイム スタンプが変更され、メッセージ追跡ログを検索するための Exchange のクエリ ロジックが正常に動作しなくなります。

  - Exchange 2013 の **Get-MessageTrackingLog** コマンドレットは、同じ Active Directory サイト内の Exchange 2007 サーバーおよび Exchange 2010 サーバーのメッセージ追跡ログを検索できます。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用してメッセージ追跡ログを検索する

特定のイベントについてメッセージ追跡ログのエントリを検索するには、次の構文を使用します。

    Get-MessageTrackingLog [-Server <ServerIdentity.] [-ResultSize <Integer> | Unlimited] [-Start <DateTime>] [-End <DateTime>] [-EventId <EventId>] [-InternalMessageId <InternalMessageId>] [-MessageId <MessageId>] [-MessageSubject <Subject>] [-Recipients <RecipientAddress1,RecipientAddress2...>] [-Reference <Reference>] [-Sender <SenderAddress>]

サーバー上のメッセージ追跡ログから最新の 1,000 件のエントリを表示するには、次のコマンドを実行します。

    Get-MessageTrackingLog

この例では、ローカルサーバー上のメッセージ追跡ログで、2013 年 3 月 28 日午前 8 時から 2013 年 3 月 28 日午後 5 時の間に発生した **FAIL** イベントのうち、メッセージ送信者が pat@contoso.com であるエントリをすべて検索します。

    Get-MessageTrackingLog -ResultSize Unlimited -Start "3/28/2013 8:00AM" -End "3/28/2013 5:00PM" -EventId "Fail" -Sender "pat@contoso.com"

## シェルを使用してメッセージ追跡ログの検索結果を制御する

以下の構文を使用します。

    Get-MessageTrackingLog <SearchFilters> | <Format-Table | Format-List> [<FieldNames>] [<OutputFileOptions>]

この例では、以下の検索条件でメッセージ追跡ログを検索します。

  - **Send** イベントの最初の 1,000 件について結果を返します。

  - 結果をリスト形式で表示します。

  - フィールド名が `Send` または `Recipient` で始まるものだけを表示します。

  - `D:\Send Search.txt` という名前の新しいファイルに結果を書き込みます。

<!-- end list -->

    Get-MessageTrackingLog -EventId Send | Format-List Send*,Recipient* > "D:\Send Search.txt"

## シェルを使用して複数のサーバー上のメッセージ追跡ログからメッセージ エントリを検索する

通常、**MessageID:**  ヘッダー フィールドの値は、メッセージが Exchange 組織内を移動する間変わりません。このプロパティの名前は、キュー表示ユーティリティでは **InternetMessageId**、メッセージ追跡ログ表示ユーティリティでは **MessageId** です。目的のメッセージの `MessageID:` が特定できたら、Exchange 組織内のすべてのメールボックス サーバー上のメッセージ追跡ログからそのメッセージに関する情報を検索できます。

すべてのメールボックス サーバーで特定のメッセージに関するメッセージ追跡ログ エントリを検索するには、次の構文を使用します。

    Get-ExchangeServer | where {$_.isHubTransportServer -eq $true -or $_.isMailboxServer -eq $true} | Get-MessageTrackingLog -MessageId <MessageID> | Select-Object <CommaSeparatedFieldNames> | Sort-Object -Property <FieldName>

この例では以下の検索条件で、すべての Exchange 2013 メールボックス サーバー上のメッセージ追跡ログを検索します。

  - **MessageID:**  の値が`<ba18339e-8151-4ff3-aeea-87ccf5fc9796@mailbox01.contoso.com>` であるメッセージに関連するエントリをすべて検索します。山かっこ (`<>`) は省略できます。省略しない場合は、**MessageID:**  の値全体を二重引用符で囲む必要があります。

  - エントリごとに、**date-time**、**server-hostname**、**client-hostname**、**source**、**event-id**、および **recipient-address** の各フィールドを表示します。

  - **date-time** フィールドに基づいて結果を並べ替えます。

<!-- end list -->

    Get-ExchangeServer | where {$_.isHubTransportServer -eq $true -or $_.isMailboxServer -eq $true} | Get-MessageTrackingLog -MessageId ba18339e-8151-4ff3-aeea-87ccf5fc9796@mailbox01.contoso.com | Select-Object Timestamp,ServerHostname,ClientHostname,Source,EventId,Recipients | Sort-Object -Property Timestamp

## EAC を使用してメッセージ追跡ログを検索する

Exchange 管理センター (EAC) にある管理者向けの配信レポート機能を使用することで、組織内の特定のメールボックスで送受信されたメッセージの情報をメッセージ追跡ログから検索できます。詳細については、「[配信レポートによるメッセージの追跡](track-messages-with-delivery-reports-exchange-2013-help.md)」を参照してください。

