---
title: 'メール フロー ルールを管理します: Exchange Online Help'
TOCTitle: メール フロー ルールを管理します
ms:assetid: e7a81372-b6d7-4d1f-bc9e-a845a7facac2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657505(v=EXCHG.150)
ms:contentKeyID: 49896533
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メール フロー ルールを管理します

 

_**適用先:** Exchange Online, Exchange Online Protection, Exchange Server 2013_

メール フロー ルール (トランスポート ルールとも呼ばれます) を使用して、組織を通過するメッセージの特定条件を確認してこれらを処理することができます。ここでは、ルールの作成、コピー、順序の調整、有効化または無効化、削除、インポートまたはエクスポートの方法と、ルールの使用状況を監視する方法について説明します。


> [!TIP]
> ルールの働きが期待どおりになるようにするには、各ルールとルール間の相互動作を十分にテストしてください。



この手順を使用しているシナリオに興味はありますか?次のトピックを参照してください。

  - [組織全体の免責事項、署名、フッター、またはヘッダー](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md)

  - [トランスポート ルールを使用してメッセージの添付を検査する](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)

  - [添付ファイル ブロックの一般的なシナリオ](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/common-attachment-blocking-scenarios)

  - [単語、語句、パターンの一覧に基づいてメールをルーティングするメール フロー ルールの使用](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/use-rules-to-route-email)

  - [一般的なメッセージの承認シナリオ](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/common-message-approval-scenarios)

  - [メッセージが低優先メール機能を迂回できるメール フロー ルールを使用する](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/use-rules-to-bypass-clutter)

  - [メール フローのルールを構成するためのベスト プラクティス](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/configuration-best-practices)

  - [Office 365 で、メール フロー ルールを使用してメッセージの添付ファイルを検査する](https://technet.microsoft.com/ja-jp/library/jj919236\(v=exchg.150\))

  - [トランスポート ルールを使用して、一括メールのフィルタ リングを構成するのには](https://technet.microsoft.com/ja-jp/library/dn720438\(v=exchg.150\))

  - [電子メール メッセージの暗号化または暗号化解除ルールの定義](https://go.microsoft.com/fwlink/p/?linkid=402846)

  - [Office 365 で組織全体の信頼できる差出人またはブロックする差出人の一覧を作成する](https://technet.microsoft.com/ja-jp/library/dn198251\(v=exchg.150\))

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」(Exchange Server) または「[Exchange Online の機能アクセス許可](https://technet.microsoft.com/ja-jp/library/jj200673\(v=exchg.150\))」の「トランスポート ルール」。

  - ルールが <strong>バージョン 14</strong> として一覧表示されている場合には、ルールが Exchange Server 2010 メール フロー ルール形式に基づいていることを意味します。この種のルールの場合は、すべてのオプションを使用できます。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## メール フロー ルールの作成

メール フロー ルールを作成するには、データ損失防止 (DLP) ポリシーをセットアップするか、新しいルールを作成するか、ルールをコピーします。Exchange 管理センター (EAC) または Exchange 管理シェル を使用できます。


> [!NOTE]
> メール フロー ルールを作成または変更した後に、新規または更新されたルールがメールに適用されるまで、最大で 30 分かかります。



## DLP ポリシーを使用してメール フロー ルールを作成する

各 DLP ポリシーは、メール フロー ルールの集合です。DLP ポリシーを作成した後は、次の手順を使用して、メール フロー ルールを調整できます。

1.  DLP ポリシーを作成します。手順については、以下を参照してください。
    
      - [Exchange Server 2013 の DLP の手順](dlp-procedures-exchange-2013-help.md)
    
      - [Exchange Online の DLP の手順](dlp-procedures-exchange-2013-help.md)

2.  DLP ポリシーによって作成されたメール フロー ルールを変更します。「トランスポート ルールを表示または変更する」をご覧ください。

## EAC を使用してメール フロー ルールを作成する

EAC を使用すると、テンプレートを使用するか、既存のルールをコピーするか、ゼロからメール フロー ルールを作成できます。

1.  <strong>メール フロー</strong> \> <strong>ルール</strong> に移動します。

2.  次のオプションのいずれかを使用してルールを作成します。
    
      - テンプレートからルールを作成するには、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックしてテンプレートを選択します。
    
      - ルールをコピーするには、ルールを選択してから <strong>コピー</strong>![\[コピー\] アイコン](images/JJ657480.ed7f7abf-39d8-4f43-a918-ccb3bff87ef5(EXCHG.150).gif "[コピー] アイコン") を選択します。
    
      - 最初から新しいルールを作成するには、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") を選択してから <strong>新しいルールを作成する</strong> を選択します。

3.  <strong>新しいルール</strong> ダイアログ ボックスで、ルールの名前を指定してから、このルールの条件とアクションを選択します。
    
    1.  <strong>このルールを適用する条件</strong> で、利用可能な条件の一覧から使用条件を選択します。
        
          - 値を指定する必要がある条件もあります。たとえば、<strong>送信者が...</strong> の条件を選択した場合は、送信者のアドレスを指定する必要があります。単語または語句を追加する場合、末尾のスペースが許可されていないことに注意します。
        
          - 必要な条件が一覧にない場合や、例外を追加する必要がある場合は、<strong>その他のオプション</strong> を選択します。追加の条件と例外が一覧に表示されます。
        
          - この条件を指定しないで、このルールを組織のすべてのメッセージに適用する場合は、<strong>すべてのメッセージに適用</strong> の条件を選択します。
    
    2.  <strong>実行する処理...</strong> で、使用可能な処理の一覧から、条件と一致するメッセージに対してルールが実行する処理を選択します。
        
          - 一部の処理では、値を指定する必要があります。たとえば、<strong>承認を受けるためにメッセージを転送する...</strong> の条件を選択した場合は、組織内の受信者を選択する必要があります。
        
          - 必要な条件が一覧にない場合は、<strong>その他のオプション</strong> を選択します。追加の他の条件が一覧に表示されます。
    
    3.  [データ損失防止 (DLP) レポート](https://go.microsoft.com/fwlink/p/?linkid=402768) と [トランスポート ルール レポート](https://go.microsoft.com/fwlink/p/?linkid=402769) に、このルールと一致するデータが表示される方法を指定します。
        
          - <strong>このルールを次の重大度レベルで監査する</strong> の下でレベルを選んで、このルールの重要度レベルを指定します。メール フロー ルールに関する Office 365 のアクティビティ レポートは、ルールと一致したデータを重大度レベルによってグループ化します。重大度レベルは、レポートを使いやすくための単なるフィルターです。重要度レベルは、ルールが処理される優先度には影響しません。
            

            > [!NOTE]
            > <STRONG>[このルールを次の重大度レベルで監査する]</STRONG> チェック ボックスをオフにすると、ルールと一致するデータはルールのレポートに表示されなくなります。

    
    4.  ルールのモードを設定します。メール フローに影響を与えずにルールをテストするには、2 つのテスト モードのいずれかを使用できます。どちらのテスト モードも、条件が満たされると、メッセージ トレースにエントリが追加されます。
        
          - <strong>強制</strong> これを使用するとルールがオンになり、ルールによるメッセージの処理が即座に開始されます。ルールのすべてのアクションが実行されます。
        
          - <strong>ポリシー ヒントありのテスト</strong>  ルールがオンになり、ポリシー ヒント アクション (<strong>ポリシー ヒントを使用して送信者に通知する</strong>) が送信されますが、メッセージ配信に関連したアクションは実行されません。このモードを使うには、データ損失防止 (DLP) が必要です。詳細については、「[ポリシー ヒント](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/data-loss-prevention/policy-tips)」を参照してください。
        
          - <strong>ポリシー ヒントなしのテスト</strong> インシデント レポートの作成アクションだけが適用されます。メッセージの配信に関連するアクションは実行されません。

4.  ルールに問題がない場合は手順 5 に進み、さらに条件やアクションを追加する場合、例外を指定する場合、追加のプロパティを設定する場合は <strong>その他のオプション</strong> をクリックします。<strong>その他のオプション</strong> をクリックしたら、次のフィールドを入力してルールを作成します。
    
    1.  条件をさらに追加するには、<strong>条件の追加</strong> をクリックします。1 つ以上の条件がある場合は、条件の横にある <strong>削除\] X** をクリックして、いずれかの条件を削除できます。<strong>その他のオプション</strong> をクリックすると、さらに多くのさまざまな条件があります。
    
    2.  処理をさらに追加するには、<strong>処理の追加</strong> をクリックします。1 つ以上の処理がある場合は、処理の横にある <strong>削除\] X** をクリックして、いずれかの処理を削除できます。<strong>その他のオプション</strong> をクリックすると、さらに多くのさまざまな処理があります。
    
    3.  例外を指定するには、<strong>例外の追加</strong> をクリックし、<strong>ただし次の場合を除く...</strong> ドロップダウンを使用して例外を選択します。例外の横にある <strong>削除\] X** をクリックして、ルールから例外を削除できます。
    
    4.  このルールを特定の日付以降に有効にする場合は、<strong>このルールを次の日付に有効にする:</strong> をクリックし、日付を指定します。この場合でも、ルールは日付の前に有効になりますが、ルールは処理されないことに注意してください。
        
        同様に、特定の日付でルールの処理を停止できます。これを行うには、<strong>このルールを次の日付に無効にする:</strong> をクリックし、日付を指定します。ルールは有効なままになりますが、処理されないことに注意してください。
    
    5.  このルールがメッセージを処理した後には、追加のルールが適用されないように選択できます。これを行うには、<strong>他のルールは処理しない</strong> をクリックします。これを選択した場合は、このルールによってメッセージが処理され、そのメッセージに対して以降のルールは処理されません。
    
    6.  ルールの処理が完了できない場合は、メッセージの処理方法を指定できます。既定では、ルールは無視され、メッセージは通常通りに処理されますが、処理するためにメッセージを再送信することもできます。再送信するには、<strong>ルール処理が完了しない場合メッセージを優先する</strong> チェックボックスをオンにします。
    
    7.  ルールにより送信者のアドレスを分析する場合、既定ではメッセージ ヘッダーのみが調べられます。ただし、SMTP メッセージ エンベロープも調べるようにルールを構成できます。調査対象を指定するには、<strong>メッセージ内の送信者のアドレスを照合する</strong> で次のいずれかの値をクリックします。
        
          - **ヘッダー**   メッセージ ヘッダーのみを調べます。
        
          - **エンベロープ**   SMTP メッセージ エンベロープのみを調べます。
        
          - **ヘッダーまたはエンベロープ**   メッセージ ヘッダーと SMTP メッセージ エンベロープの両方を調べます。
    
    8.  <strong>コメント</strong> ボックスで、このルールに対するコメントを追加できます。

5.  <strong>保存</strong> をクリックして、ルールの作成を完了します。

## Exchange 管理シェル を使用してメール フロー ルールを作成する

この例では、[New-TransportRule](https://technet.microsoft.com/ja-jp/library/bb125138\(v=exchg.150\)) コマンドレットを使って、組織外部から Sales Department 配布グループに対して送信されるメッセージの前に "`External message to Sales DG:`" を追加するという新規メール フロー ルールを作成します。

    New-TransportRule -Name "Mark messages from the Internet to Sales DG" -FromScope NotInOrganization -SentTo "Sales Department" -PrependSubject "External message to Sales DG:"

上記の手順で使用されるルールのパラメーターと操作は、図のみで表示されています。すべてのメール フロー ルールの条件とアクションを確認し、どれが必要な条件を満たしているかをご判断ください。

## 正常な動作を確認する方法

新しいメール フロー ルールが正常に作成されたことを確認するには、次の手順を実行します。

  - EAC から、作成した新しいメール フロー ルールが <strong>ルール</strong> の一覧に表示されていることを確認します。

  - Exchange 管理シェル から次のコマンドを実行して、新しいメール フロー ルールが正常に作成されたことを確認します (下記の例では、上記の Exchange 管理シェル 例で作成したルールを確認します)。
    
        Get-TransportRule "Mark messages from the Internet to Sales DG"

## メール フロー ルールを表示または変更する


> [!NOTE]
> メール フロー ルールを作成または変更した後に、新規または更新されたルールがメールに適用されるまで、最大で 30 分かかります。



## EAC を使用してメール フロー ルールを表示または変更する

1.  EAC から、<strong>メール フロー</strong> \> <strong>ルール</strong> に移動します。

2.  一覧のルールを選択すると、そのルールの条件、処理、例外、および選択されたプロパティが詳細ウィンドウに表示されます。特定のルールのすべてのプロパティを表示するには、ルールをダブルクリックします。これによりルール エディター ウィンドウが開き、このウィンドウを使用してルールを変更できます。ルールのプロパティの詳細については、このトピックで前述した「EAC を使用してメール フロー ルールを作成する」セクションを参照してください。

## Exchange 管理シェル を使用してメール フロー ルールを表示または変更する

次の例では、組織において構成されたすべてのルールの一覧を表示します。

    Get-TransportRule

特定のメール フロー ルールのプロパティを表示するには、そのルールの名前または GUID を入力します。通常、プロパティをフォーマットするには、出力を **Format-List** コマンドレットに送信すると役立ちます。次の例では、**Sender is a member of Marketing** という名前のメール フロー ルールのすべてのプロパティが返されます。

    Get-TransportRule "Sender is a member of marketing" | Format-List

既存のルールのプロパティを変更するには、[Set-TransportRule](https://technet.microsoft.com/ja-jp/library/bb123534\(v=exchg.150\)) コマンドレットを使います。このコマンドレットを使用すると、ルールに関連付けられたすべてのプロパティ、条件、処理、または例外を変更できます。次の例では、Kelly Rollin によって送信されたメッセージにはルールが適用されないように、ルール "Sender is a member of marketing" に例外を追加します。

    Set-TransportRule "Sender is a member of marketing" -ExceptIfFrom "Kelly Rollin"

## 正常な動作を確認する方法

メール フロー ルールが正常に変更されたことを確認するには、次の手順を実行します。

  - EAC から、<strong>ルール</strong> の一覧で変更したルールを選択し、詳細ウィンドウを表示します。

  - Exchange 管理シェル から、次のコマンドを実行して変更したプロパティとルールの名前を一覧表示し、メール フロー ルールが正常に変更されたことを確認します (下記の例では、上記の Exchange 管理シェル 例で変更したルールを確認します)。
    
        Get-TransportRule "Sender is a member of marketing" | Format-List Name,ExceptIfFrom

## メール フロー ルールのプロパティ

組織の既存のトランスポート ルールを変更するには、Set-TransportRule コマンドレットも使用できます。以下はリストのプロパティです 変更できる EAC では使用できません。Set-TransportRule コマンドレットを使用してこれらの変更を行う方法の詳細については、「[Set-TransportRule](https://technet.microsoft.com/ja-jp/library/bb123534\(v=exchg.150\))」をご参照ください。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC における条件名</th>
<th>Exchange 管理シェル における条件名</th>
<th>プロパティ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ルールの処理を中止する</strong></p></td>
<td><p><code>StopRuleProcessing </code></p></td>
<td><p><code> Not applicable</code></p></td>
<td><p>これを使用することにより、追加ルールの処理を停止できます</p></td>
</tr>
<tr class="even">
<td><p><strong>ヘッダー/エンベロープの照合</strong></p></td>
<td><p><code>SenderAddressLocation </code></p></td>
<td><p>該当しない</p></td>
<td><p>これを使用することにより、SMTP メッセージ エンベロープを調べて、ヘッダーとエンベロープが一致しているかどうかを確認できます</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><strong>監査重大度</strong></p></td>
<td><p><code>SetAuditSeverity </code></p></td>
<td><p><code>Not applicable</code></p></td>
<td><p>監査重大度レベルを選択できます</p></td>
</tr>
<tr class="even">
<td><p><strong>ルールのモード</strong></p></td>
<td><p><code>Mode</code></p></td>
<td><p><code>Not applicable</code></p></td>
<td><p>ルールのモードの設定を可能にする</p></td>
</tr>
</tbody>
</table>


## メール フロー ルールの優先度を設定する

一覧の最上位のルールが最初に処理されます。このルールの <strong>優先度</strong> は 0 です。

## EAC を使用してルールの優先度を設定する

1.  EAC から、<strong>メール フロー</strong> \> <strong>ルール</strong> に移動します。ルールが処理される順序で表示されます。

2.  ルールを選択し、矢印を使用して、一覧でルールを上または下に移動します。

## Exchange 管理シェル を使用してルールの優先度を設定する

次の例では、"Sender is a member of marketing" の優先度を 2 に設定します。

    Set-TransportRule "Sender is a member of marketing" priority "2"

## 正常な動作を確認する方法

メール フロー ルールが正常に変更されたことを確認するには、次の手順を実行します。

  - EAC のルールの一覧から、ルールの順序を参照します。

  - Exchange 管理シェル から、ルールの優先度を確認します (下記の例では、上記の Exchange 管理シェル 例で変更したルールを確認します)。
    
        Get-TransportRule * | Format-List Name,Priority

## メール フロー ルールを有効または無効にする

ルールは、作成時には有効になっています。メール フロー ルールを無効にすることができます。

## EAC を使用してメール フロー ルールを有効または無効にする

1.  EAC から、<strong>メール フロー</strong> \> <strong>ルール</strong> に移動します。

2.  ルールを無効にするには、その名前の横にあるチェック ボックスをオフにします。

3.  無効になっているルールを有効にするには、その名前の横にあるチェック ボックスをオンにします。

## Exchange 管理シェル を使用してメール フロー ルールを有効または無効にする

次の例では、メール フロー ルール "Sender is a member of marketing" を無効にします。

    Disable-TransportRule "Sender is a member of marketing"

次の例では、メール フロー ルール "Sender is a member of marketing" を有効にします。

    Enable-TransportRule "Sender is a member of marketing"

## 正常な動作を確認する方法

メール フロー ルールが正常に有効化または無効化されたことを確認するには、次の手順を実行します。

  - EAC から、<strong>ルール</strong> の一覧でルールの一覧を表示し、<strong>オン</strong> 列のチェック ボックスの状態を確認します。

  - Exchange 管理シェル から、ルールの状態と共に組織内のすべてのルールの一覧を返す次のコマンドを実行します。
    
        Get-TransportRule | Format-Table Name,State

## メール フロー ルールの削除

## EAC を使用してメール フロー ルールを削除する

1.  EAC から、<strong>メール フロー</strong> \> <strong>ルール</strong> に移動します。

2.  削除するルールを選択し、<strong>削除</strong>![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") をクリックします。

## Exchange 管理シェル を使用してメール フロー ルールを削除する

次の例では、メール フロー ルール "Sender is a member of marketing" を削除します。

    Remove-TransportRule "Sender is a member of marketing"

## 正常な動作を確認する方法

メール フロー ルールが正常に削除されたことを確認するには、次の手順を実行します。

  - EAC から、<strong>ルール</strong> の一覧でルールを表示し、削除したルールが表示されていないことを確認します。

  - Exchange 管理シェル から次のコマンドを実行して、削除したルールが一覧に表示されていないことを確認します。
    
        Get-TransportRule

## ルールの使用状況を監視する

Exchange Online か Exchange Online Protection を使用している場合は、ルール レポートを使って、各ルールが一致した回数を確認できます。ルールをレポートに組み込むには、<strong>このルールを次の重大度レベルで監査する</strong> チェック ボックスを選択する必要があります。オンラインでレポートを参照するか、Excel バージョンのすべてのメール保護レポートをダウンロードできます。


> [!NOTE]
> レポート内のほとんどのデータは 24 時間以内のものですが、表示されるまでに 5 日かかるデータもあります。



## Office 365 管理センターを使用してルール レポートを生成する

1.  Office 365 管理センターで、<strong>レポート</strong> を選択します。

2.  <strong>ルール</strong> セクションで、<strong>メールの上位ルール一致</strong> か <strong>メールのルール一致</strong> を選択します。

詳細については、「[メール保護レポートの表示](https://go.microsoft.com/fwlink/p/?linkid=402958)」を参照してください。

## Excel バージョンのレポートをダウンロードする

1.  Office 365 の管理センターの \[レポート\] ページで、<strong>メール保護レポート (Excel)</strong> を選択します。

2.  初めて Excel メール保護レポートを使う際には、ダウンロード ページへのタブが開きます。
    
    1.  <strong>ダウンロード</strong> を選択して、Microsoft Office 365 Excel Plugin 用 Exchange Online Reporting をダウンロードします。
    
    2.  ダウンロードしたものを開きます。
    
    3.  <strong>Office 365 のメール保護レポートのセットアップ</strong> ダイアログ ボックスで、<strong>次へ</strong> を選択し、使用許諾契約書を確認したうえで同意してから、<strong>次へ</strong> を選択します。
    
    4.  使おうとしているサービスを選択し、<strong>次へ</strong> を選択します。
    
    5.  前提条件を確認し、<strong>次へ</strong> を選択します。
    
    6.  <strong>インストール</strong> を選択します。レポートへのショートカットがデスクトップ上に作成されます。

3.  デスクトップで、<strong>Office 365 のメール保護レポート</strong> を選択します。

4.  レポートで、<strong>ルール</strong> タブを選択します。

## メール フロー ルール コレクションをインポートまたはエクスポートする

メール フロー ルール コレクションをインポートまたはエクスポートするには、Exchange 管理シェル を使用する必要があります。メール フロー ルール コレクションを XML ファイルからインポートする方法の詳細については、「[Import-TransportRuleCollection](https://technet.microsoft.com/ja-jp/library/bb123582\(v=exchg.150\))」をご覧ください。メール フロー ルール コレクションを XML ファイルにエクスポートする方法については、「[Export-TransportRuleCollection](https://technet.microsoft.com/ja-jp/library/bb124410\(v=exchg.150\))」をご覧ください。

## サポートが必要な場合

Exchange Online のリソース:

[Exchange Online のメール フロー ルール (トランスポート ルール)](https://technet.microsoft.com/ja-jp/library/jj919238\(v=exchg.150\))

[Exchange Online でのメール フロー ルールの条件と例外 (述語)](https://technet.microsoft.com/ja-jp/library/jj919235\(v=exchg.150\))

[Exchange Online でのメール フロー ルールの処理](https://technet.microsoft.com/ja-jp/library/jj919237\(v=exchg.150\))

[トランスポートおよび受信トレイのルールの制限](https://go.microsoft.com/fwlink/p/?linkid=324584)

Exchange Online Protection のリソース:

[Exchange Online Protection のメール フロー ルール (トランスポート ルール)](https://technet.microsoft.com/ja-jp/library/dn271424\(v=exchg.150\))

[Exchange Online Protection でのメール フロー ルールの条件と例外 (述語)](https://technet.microsoft.com/ja-jp/library/jj919234\(v=exchg.150\))

[メール フロー ルールの処理 (Exchange Online Protection 向け)](https://technet.microsoft.com/ja-jp/library/jj920117\(v=exchg.150\))

[トランスポートおよび受信トレイのルールの制限](https://go.microsoft.com/fwlink/p/?linkid=324584)

Exchange Server 2013 のリソース：

[メール フローやトランスポート ルール](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[トランスポート ルールの条件 (述語)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[トランスポート ルールのアクション](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

