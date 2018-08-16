---
title: 'キューを管理する: Exchange 2013 Help'
TOCTitle: キューを管理する
ms:assetid: 37f11378-a884-4aff-ab55-689f40a46321
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997263(v=EXCHG.150)
ms:contentKeyID: 51407518
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# キューを管理する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-01-31_

Microsoft Exchange Server 2013 では、Exchange ツールボックスのキュー ビューアーまたは Exchange 管理シェルを使用してキューを管理できます。Exchange 管理シェルでのキュー管理コマンドレットの使用の詳細については、「[Exchange 管理シェルを使用してキューを管理する](use-the-exchange-management-shell-to-manage-queues-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「キュー」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## \[キューの表示\]

## Exchange ツールボックスのキュー ビューアーを使用してキューを表示する

1.  <strong>スタート</strong> \> <strong>すべてのプログラム</strong> \> <strong>Microsoft Exchange 2013</strong> \> <strong>Exchange ツールボックス</strong> の順にクリックします。

2.  <strong>メール フロー ツール</strong> セクションで、<strong>キュー ビューアー</strong> をダブルクリックして、新しいウィンドウにツールを開きます。

3.  キュー ビューアーで、<strong>キュー</strong> タブをクリックします。接続先のサーバー上にあるすべてのキューの一覧が表示されます。

4.  操作ウィンドウで <strong>エクスポート一覧</strong> リンクを使用して、キューの一覧をエクスポートできます。詳細については、「[キュー ビューアーからのリストのエクスポート](export-lists-from-queue-viewer-exchange-2013-help.md)」を参照してください。

## シェル を使用してキューを表示する

キューを表示するには、次の構文を使用します。

    Get-Queue [-Filter <Filter> -Server <ServerIdentity> -Include <Internal | External | Empty | DeliveryType> -Exclude <Internal | External | Empty | DeliveryType>]

この例では、Mailbox01 という名前の Exchange 2013 メールボックス サーバーにある空ではないすべてのキューについて、基本情報を表示します。

    Get-Queue -Server Mailbox01 -Exclude Empty

この例では、コマンドが実行されているメールボックス サーバー上の 100 を超えるメッセージを含むすべてのキューに関する詳細を表示します。

    Get-Queue -Filter {MessageCount -gt 100} | Format-List

## シェルを使用して複数の Exchange サーバー上のキューの概要情報を表示する

**Get-QueueDigest** コマンドレットは、DAG、Active Directory サイト、サーバー一覧、Active Directory フォレスト全体などの特定のスコープ内のすべてのサーバー上のキューの状態に関する高レベルの集計ビューを提供します。境界ネットワーク内のサブスクライブされているエッジ トランスポート サーバー上のキューが結果に含まれていないことに注意してください。また、**Get-QueueDigest** はエッジ トランスポート サーバー上で使用できますが、エッジ トランスポート サーバー上のキューの結果のみが返されます。


> [!NOTE]
> 既定では、<STRONG>Get-QueueDigest</STRONG> コマンドレットは、10 以上のメッセージを含む配信キューを表示します。この結果は 1 ～ 2 分間前のものです。これらの既定値の変更方法の説明については、「<A href="configure-get-queuedigest-exchange-2013-help.md">Configure Get-QueueDigest</A>」を参照してください。



複数の Exchange サーバー上のキューについて概要情報を表示するには、次のコマンドを実行します。

    Get-QueueDigest <-Server <ServerIdentity1,ServerIdentity2,..> | -Dag <DagIdentity1,DagIdentity2...> | -Site <ADSiteIdentity1,ADSiteIdentity2...> | -Forest> [-Filter <Filter>]

この例では、FirstSite という名前の Active Directory サイト内にあるすべての Exchange 2013 メールボックス サーバー上の、メッセージ数が 100 を超えているキューについて概要情報を表示します。

    Get-QueueDigest -Site FirstSite -Filter {MessageCount -gt 100}

この例では、DAG01 という名前のデータベース可用性グループ (DAG) 内にあるすべての Exchange 2013 メールボックス サーバー上の、キューの状態が **Retry** 値のキューについて概要情報を表示します。

    Get-QueueDigest -Dag DAG01 -Filter {Status -eq "Retry"}

## キューを再開する

キューを再開して、状態が "中断" であるキューの送信処理を再開します。この操作を有効にするには、キューの状態が "中断" である必要があります。キューを再開しても、キューにあるメッセージの状態は変わりません。状態が "中断" であるメッセージは引き続き中断されたままとなり、キューから送信されません。

## Exchange ツールボックスのキュー ビューアーを使用してキューを再開する

1.  <strong>スタート</strong> \> <strong>すべてのプログラム</strong> \> <strong>Microsoft Exchange 2013</strong> \> <strong>Exchange ツールボックス</strong> の順にクリックします。

2.  <strong>メール フロー ツール</strong> セクションで、<strong>キュー ビューアー</strong> をダブルクリックして、新しいウィンドウにツールを開きます。

3.  キュー ビューアーで、<strong>キュー</strong> タブをクリックします。接続先のサーバー上にあるすべてのキューの一覧が表示されます。

4.  <strong>フィルターの作成</strong> をクリックし、次のようにフィルター式を入力します。
    
    1.  キューのプロパティのボックスの一覧から <strong>状態</strong> を選択します。
    
    2.  比較演算子のボックスの一覧から <strong>次の値と等しい</strong> を選択します。
    
    3.  値のボックスの一覧から <strong>中断</strong> を選択します。

5.  <strong>フィルターの適用</strong> をクリックします。現在中断されているサーバー上のすべてのキューが表示されます。

6.  一覧から 1 つ以上のキューを選択し、右クリックして、<strong>再開</strong> をクリックします。

## シェルを使用してキューを再開する

キューを再開するには、次の構文を使用します。

    Resume-Queue <-Identity QueueIdentity | -Filter {QueueFilter} [-Server ServerIdentity]>

この例では、状態が "中断" になっているローカル サーバー上のすべてのキューを再開します。

    Resume-Queue -Filter {Status -eq "Suspended"}

この例では、Mailbox01 という名前のサーバー上で、contoso.com という名前の中断されている配信キューを再開します。

    Resume-Queue -Identity Mailbox01\contoso.com

## 正常な動作を確認する方法

キューが正常に再開されたことを確認するには、次の手順を実行します。

1.  キュー ビューアーまたは **Get-Queue** コマンドレットを使用して、再開を試みるキューを検索します。

2.  キューの **Status** プロパティが、`Suspended` 値ではないことを確認します。

## キューを再試行する

トランスポート サーバーが次のホップに接続できないと、配信キューの状態は "再試行" となります。キュー ビューアーまたはシェルを使用して配信キューを再試行する場合は、次に予定されている再試行を待たずに直ちに接続を試行することができます。接続に失敗すると、再試行の間隔がリセットされます。この操作を有効にするには、配信キューの状態が "再試行" である必要があります。

## Exchange ツールボックスのキュー ビューアーを使用してキューを再試行する

1.  <strong>スタート</strong> \> <strong>すべてのプログラム</strong> \> <strong>Microsoft Exchange 2013</strong> \> <strong>Exchange ツールボックス</strong> の順にクリックします。

2.  <strong>メール フロー ツール</strong> セクションで、<strong>キュー ビューアー</strong> をダブルクリックして、新しいウィンドウにツールを開きます。

3.  キュー ビューアーで、<strong>キュー</strong> タブをクリックします。接続先のサーバー上にあるすべてのキューの一覧が表示されます。

4.  <strong>フィルターの作成</strong> をクリックし、次のようにフィルター式を入力します。
    
    1.  キューのプロパティのボックスの一覧から <strong>状態</strong> を選択します。
    
    2.  比較演算子のボックスの一覧から <strong>次の値と等しい</strong> を選択します。
    
    3.  値のボックスの一覧から <strong>再試行</strong> を選択します。

5.  <strong>フィルターの適用</strong> をクリックします。現在 <strong>再試行</strong> 状態のキューがすべて表示されます。

6.  1 つ以上のキューをリストから選択します。そのキューを右クリックし、<strong>キューの再試行</strong> を選択します。接続試行に成功すると、キューの状態は <strong>アクティブ</strong> に変わります。接続が確立しないと、キューの状態は <strong>再試行</strong> のままで、次の再試行の時間が更新されます。

## シェルを使用してキューを再試行する

キューを再試行するには、次の構文を使用します。

    Retry-Queue <-Identity QueueIdentity | -Filter QueueFilter [-Server ServerIdentity]>

この例では、ローカル サーバー上で状態が "再試行" のキューをすべて再試行します。

    Retry-Queue -Filter {status -eq "retry"}

この例では、Mailbox01 という名前のサーバー上で `Retry` 状態になっている contoso.com という名前のキューを再試行します。

    Retry-Queue -Identity Mailbox01\contoso.com

## 正常な動作を確認する方法

キューが正常に再試行されたことを確認するには、次の手順を実行します。

1.  キュー ビューアーまたは **Get-Queue** コマンドレットを使用して、再試行を試みるキューを検索します。

2.  キューの **LastRetryTime** プロパティがキューを再試行しようとした時間と一致することを確認します。

## キュー内のメッセージを再送信する

キューの再送信はキューの再試行と似ていますが、メッセージが再処理するカテゴライザー用の発信キューに送信される点が異なります。以下の状態のメッセージを再送信できます。

  - 状態が "再試行" の配信キュー。キュー内のメッセージは "中断" 状態であってはいけません。

  - 状態が "中断" ではない、到達不能キュー内のメッセージ。

  - 有害メッセージ キューのメッセージ。

## シェルを使用してメッセージを再送信する

メッセージを再送信するには、次の構文を使用します。

    Retry-Queue <-Identity QueueIdentity | -Filter {Status -eq "Retry"} -Server ServerIdentity> -Resubmit $true

この例では、Mailbox01 という名前のサーバー上の配信キューに置かれている、状態が "再試行" であるメッセージをすべて再送信します。

    Retry-Queue -Filter {Status -eq "Retry"} -Server Mailbox01 -Resubmit $true

この例では、サーバー Mailbox01 上の到達不能キューに置かれているメッセージをすべて再送信します。

    Retry-Queue -Identity Mailbox01\Unreachable -Resubmit $true

## 有害メッセージ キュー内にあるメッセージを再送信する

メッセージを再送信することで、有害なメッセージ キュー内のメッセージを再送信します。キュー ビューアーまたはシェルを使用して、有害なメッセージ キューからメッセージを再送信します。有害なメッセージ キューは、その中にメッセージが存在する場合にのみ、キュー ビューアーに表示されますので注意してください。


> [!NOTE]
> 有害メッセージ キューには、サーバー エラー後に Exchange システムにとって有害であると見なされたメッセージが含まれています。これらのメッセージは、その内容や形式の点で本当に有害な場合もあります。または、有害なメッセージだと推測されるメッセージの処理中に Exchange サーバーをクラッシュさせた、適切に記述されていないエージェントの被害を受けたメッセージである可能性もあります。有害メッセージ キューに置かれたメッセージの安全性を確信できない場合は、検査できるようにメッセージをファイルにエクスポートする必要があります。詳細については、「<A href="export-messages-from-queues-exchange-2013-help.md">キューからメッセージをエクスポートする</A>」を参照してください。



## Exchange ツールボックスのキュー ビューアーを使用して有害メッセージ キュー内にあるメッセージを再送信する

1.  <strong>スタート</strong> \> <strong>すべてのプログラム</strong> \> <strong>Microsoft Exchange 2013</strong> \> <strong>Exchange ツールボックス</strong> の順にクリックします。

2.  <strong>メール フロー ツール</strong> セクションで、<strong>キュー ビューアー</strong> をダブルクリックして、新しいウィンドウにツールを開きます。

3.  キュー ビューアーで、<strong>キュー</strong> タブをクリックします。接続先のサーバー上にあるすべてのキューの一覧が表示されます。

4.  有害なメッセージ キューをクリックします。操作ウィンドウで、<strong>メッセージの表示</strong> を選択します。

5.  一覧から 1 つ以上のメッセージを選択し、右クリックして、<strong>再開</strong> をクリックします。

## シェルを使用して有害メッセージ キュー内にあるメッセージを再送信する

有害なメッセージ キューからメッセージを再送信するには、以下の手順を実行します。

1.  次のコマンドを実行してメッセージの ID を検索します。
    
        Get-Message -Queue Poison | Format-Table Identity

2.  次のコマンドに前の手順で取得したメッセージの ID を使用します。
    
        Resume-Message <PoisonMessageIdentity>
    
    この例では、メッセージ ID の値が 222 であるメッセージを有害なメッセージ キューから再開します。
    
        Resume-Message 222

## 正常な動作を確認する方法

有害なメッセージ キューからメッセージを正常に再送信したことを確認するには、以下を実行します。

1.  キュー ビューアーまたは **Get-Queue** コマンドレットを使用して、メッセージを再送信しようとした有害なメッセージ キューを表示します。

2.  有害なメッセージ キューにメッセージがないことを確認します。有害なメッセージ キューが空の場合は、キュー ビューアーまたは **Get-Queue** コマンドレットには表示されませんので注意してください。そのため、再送信したメッセージが有害なメッセージ キュー内の唯一のメッセージであった場合、その有害なメッセージ キューは表示されなくなり、それがメッセージの再送信に成功したことの印となります。

## キューを中断する

キューを中断すると、メッセージはキューから送信されなくなりますが、キュー内のメッセージの状態は変更されません。SMTP を介して配信されているメッセージが操作を終了します。キューを中断してメール フローを停止した後、キュー内の 1 つ以上のメッセージを中断できます。キューを再開しても、中断されていたメッセージはキューに残ります。

状態が "アクティブ" または "再試行" であるキューを中断できます。また、到達不能キューや送信キューも中断できます。

到達不能キューを中断した場合は、トランスポート サーバーが構成の更新を受信しても、そのキューが再開されるまでアイテムはカテゴライザーに再送信されません。送信キューを中断した場合は、そのキューが再開されるまで、メッセージはカテゴライザーによって取得されません。

## Exchange ツールボックスのキュー ビューアーを使用してキューを中断する

1.  <strong>スタート</strong> \> <strong>すべてのプログラム</strong> \> <strong>Microsoft Exchange 2013</strong> \> <strong>Exchange ツールボックス</strong> の順にクリックします。

2.  <strong>メール フロー ツール</strong> セクションで、<strong>キュー ビューアー</strong> をダブルクリックして、新しいウィンドウにツールを開きます。

3.  キュー ビューアーで、<strong>キュー</strong> タブをクリックします。接続先のサーバー上にあるすべてのキューの一覧が表示されます。特定の条件に一致するキューのみを表示するためのフィルターを作成することができます。

4.  1 つ以上のキューを選択し、右クリックし、<strong>中断</strong> をクリックします。

## シェルを使用してキューを中断する

キューを中断するには、次の構文を使用します。

    Suspend-Queue <-Identity QueueIdentity | -Filter {QueueFilter} [-Server ServerIdentity]>

この例では、メッセージ数が 1,000 以上で状態が "再試行" であるローカル サーバー上のキューをすべて中断します。

    Suspend-Queue -Filter {MessageCount -ge 1000 -and Status -eq "Retry"}

次の例では、Mailbox01 という名前のサーバー上にある contoso.com という名前のキューを中断します。

    Suspend-Queue -Identity Mailbox01\contoso.com

## 正常な動作を確認する方法

キューが正常に中断されたことを確認するには、次の手順を実行します。

1.  キュー ビューアーまたは **Get-Queue** コマンドレットを使用して、中断を試みるキューを検索します。

2.  キューの **Status** プロパティが、`Suspended` 値であることを確認します。

