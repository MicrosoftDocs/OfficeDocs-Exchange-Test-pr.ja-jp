---
title: 'ポリシー ヒントの管理: Exchange Online Help'
TOCTitle: ポリシー ヒントの管理
ms:assetid: cec50a35-1d00-47b3-b72f-ac1bb0fd630e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ619307(v=EXCHG.150)
ms:contentKeyID: 49129777
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ポリシー ヒントの管理

 

_**適用先:** Exchange Online, Exchange Server 2013_

ポリシー ヒントは、メッセージの作成中に電子メール送信者に表示される情報通知です。ポリシー ヒントの目的は、既に確立したデータ損失防止 (DLP) ポリシーによって実施しているビジネス プラクティスまたはビジネス ポリシーに違反している可能性があることをユーザーが理解できるようにすることです。次の手順により、ポリシー ヒントの使用を開始する助けが得られます。詳細については、ビデオをご覧ください。

> [!VIDEO https://www.microsoft.com/ja-jp/videoplayer/embed/dd629bb7-063d-49f3-b7e1-8f2e0aa4de13]

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:30 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「データ損失防止 (DLP)」。

  - ポリシー ヒントは、次の条件が満たされている場合のみ電子メール送信者に対して表示されます。
    
    1.  送信者のメッセージ クライアント プログラムが Microsoft Outlook 2013 である。組織が Exchange 2013 SP1 を展開しているか、Exchange Online を使用している場合は、Outlook Web App と OWA for Devices でもポリシー ヒントが表示されます。
    
    2.  ポリシー ヒント通知を実行するトランスポート ルールが存在している。このようなトランスポート ルールは、<strong>ポリシー ヒントを使用して送信者に通知する</strong> アクションを含む DLP ポリシーを設定することにより作成できます。
    
    3.  トランスポート エージェントによってスキャンされるメッセージ ヘッダー、メッセージ本文、またはメッセージ添付ファイルの内容が、ポリシー ヒント通知ルールも含まれている DLP ポリシーまたは DLP ルール内で確立された条件を満たす必要があります。つまり、関連付けられたルールによりアクションが実行される原因となることをユーザーが行った場合にのみ、ポリシー ヒントがエンド ユーザーに対して表示されます。

  - ポリシー ヒント設定機能を使用してポリシー ヒント テキストをカスタマイズしない場合は、システムに組み込まれた既定のポリシー ヒント通知テキストが表示されます。既定のテキストの詳細については、「[ポリシー ヒント](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/data-loss-prevention/policy-tips)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## 通知のみのポリシー ヒントを作成または変更する

この手順の結果、特定のルールが満たされた場合に、電子メール送信者に情報ポリシー ヒントが表示されます。Microsoft Outlook では、ポリシー ヒントのオプション ダイアログ ボックスを使用して、送信者はこのヒントが表示されないようにできます。カスタムのポリシー ヒントのテキストを構成するには、「カスタムのポリシー ヒント通知テキストを作成する」を参照してください。

## EAC を使用して通知のみのポリシー ヒントを構成する

1.  EAC 内で、<strong>コンプライアンス管理</strong> \> <strong>データ損失防止</strong> に移動します。

2.  ポリシーの一覧に表示されているいずれかのポリシーをダブルクリックするか、1 つのアイテムを強調表示して <strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") を選択します。

3.  <strong>DLP ポリシーの編集</strong> ページで、<strong>ルール</strong> を選択します。

4.  既存のルールにポリシー ヒントを追加するには、ルールを強調表示して <strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") を選択します。
    
    新しい空のルールを追加して完全にカスタマイズできるようにするには、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") を選択してから <strong>新しいルールを作成する</strong> を選択します。

5.  <strong>このルールを適用する条件</strong> で、<strong>メッセージに機密情報が含まれる</strong> を選択します。この条件は必須です。

6.  ![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") を選択し、機密情報の種類を選択してから、<strong>追加</strong>、<strong>OK</strong>、そして <strong>OK</strong> の順に選択します。

7.  <strong>実行する処理</strong> ボックスで <strong>ポリシー ヒントを使用して送信者に通知する</strong> を選択し、<strong>メッセージをブロックするか、送信できるかを選択します</strong> ドロップダウン リストからオプションを 1 つ選択した後、<strong>OK</strong> を選択します。

8.  さらに条件またはアクションを追加する場合は、ウィンドウの下部にある <strong>その他のオプション</strong> を選択します。
    

    > [!NOTE]
    > 使用できるのは次の条件のみです。 
    > <UL>
    > <LI>
    > <P><STRONG>SentTo (受信者が次の場合)</STRONG></P>
    > <LI>
    > <P><STRONG>SentToScope (受信者の場所が次の場合)</STRONG></P>
    > <LI>
    > <P><STRONG>From (送信者が次の場合)</STRONG></P>
    > <LI>
    > <P><STRONG>FromMemberOf (送信者が次のメンバーの場合)</STRONG></P>
    > <LI>
    > <P><STRONG>FromScope (送信者の場所が次の場合)</STRONG></P></LI></UL>次のアクションは使用できません。 
    > <UL>
    > <LI>
    > <P><STRONG>RejectMessageReasonText (メッセージを拒否して説明を含める)</STRONG></P>
    > <LI>
    > <P><STRONG>RejectMessageEnhancedStatusCode (次の拡張状態コードのメッセージを拒否する)</STRONG></P>
    > <LI>
    > <P><STRONG>DeletedMessage (だれにも通知せずにメッセージを削除する)</STRONG></P></LI></UL>



9.  <strong>このルールのモードの選択</strong> リストで、ルールを適用するかどうかを選択します。まずルールをテストすることをお勧めします。

10. <strong>保存</strong> を選択して、ルールの変更を終了し、変更内容を保存します。

## 正常な動作を確認する方法

送信者に対して通知のみを行うポリシー ヒントが正常に作成されたことを確認するには、次の手順を実行します。

1.  EAC 内で、<strong>コンプライアンス管理</strong> \> <strong>データ損失防止</strong> に移動します。

2.  通知メッセージを含むと思われるポリシーを選択します。

3.  <strong>編集</strong> ![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") を選択し、<strong>ルール</strong> を選択します。

4.  通知メッセージを含むと思われる特定のルールを選択します。

5.  <strong>送信者に通知する</strong> アクションがルール概要の下部に表示されていることを確認します。

## メッセージ ブロックのポリシー ヒントを作成または変更する

この手順の結果、メッセージは拒否されており、問題のある条件がなくなるまではメッセージが配信されないことを示すポリシー ヒントが電子メール送信者に表示されます。送信者は、電子メール メッセージに問題のある条件が含まれていないことを示すオプションを選ぶことができます。これは誤検知の上書きとも呼ばれています。送信者がこれを示した場合は、送信トレイからのメッセージの送信が可能になり、ユーザーのレポートが監査される場合があります。ただし、Exchange によりメッセージの送信はブロックされます。カスタムのポリシー ヒントのテキストを構成するには、「カスタムのポリシー ヒント通知テキストを作成する」を参照してください。

## EAC を使用してメッセージ ブロックのポリシー ヒントを構成するには

1.  EAC 内で、<strong>コンプライアンス管理</strong> \> <strong>データ損失防止</strong> に移動します。

2.  ポリシーの一覧に表示されているいずれかのポリシーをダブルクリックするか、1 つのアイテムを強調表示して <strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") を選択します。

3.  <strong>DLP ポリシーの編集</strong> ページで、<strong>ルール</strong> を選択します。

4.  既存のルールにポリシー ヒントを追加するには、ルールを強調表示して <strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") を選択します。

5.  完全にカスタマイズできる新しい空のルールを追加するには、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") を選択します。

6.  ポリシー ヒントを表示するアクションを追加するには、<strong>その他のオプション...</strong> を選択し、<strong>処理の追加</strong> ボタンを選択します。

7.  ドロップダウン リストから <strong>ポリシー ヒントを使用して送信者に通知する</strong> を選択し、<strong>メッセージをブロックする</strong> を選択します。

8.  <strong>OK</strong> を選択してから <strong>保存</strong> を選択して、ルールの変更を終了し、変更内容を保存します。

## 正常な動作を確認する方法

メッセージ拒否のポリシー ヒントが正常に作成されたことを確認するには、次の手順を実行します。

1.  EAC 内で、<strong>コンプライアンス管理</strong> \> <strong>データ損失防止</strong> に移動します。

2.  通知メッセージを含むと思われるポリシーを強調表示するには、1 回選択します。

3.  <strong>編集</strong> ![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") を選択し、<strong>ルール</strong> を選択します。

4.  通知メッセージを含むと思われる特定のルールを強調表示するには、1 回選択します。

5.  <strong>送信者にメッセージを送信できないことを通知する</strong> アクションがルール概要の下部に表示されていることを確認します。

## ブロックしない場合は上書きのポリシー ヒントを作成または変更する

メッセージを拒否できる、またはメッセージが送信者の送信トレイから送信されないようにできるポリシー ヒントのオプションは 4 つあります。これらのオプションの詳細については、「[ポリシー ヒント](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/data-loss-prevention/policy-tips)」を参照してください。

## EAC を使用して、ブロックしない場合は上書きのポリシー ヒントを構成する

1.  EAC 内で、<strong>コンプライアンス管理</strong> \> <strong>データ損失防止</strong> に移動します。

2.  ポリシーの一覧に表示されているいずれかのポリシーをダブルクリックするか、1 つのアイテムを強調表示して <strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") を選択します。

3.  <strong>DLP ポリシーの編集</strong> ページで、<strong>ルール</strong> を選択します。

4.  既存のルールにポリシー ヒントを追加するには、ルールを強調表示して <strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") を選択します。
    
    新しい空のルールを追加して完全にカスタマイズできるようにするには、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") を選択してから <strong>その他のオプション...</strong> を選択します。

5.  ポリシー ヒントを表示するアクションを追加するには、<strong>処理の追加</strong> ボタンを選択します。

6.  ドロップダウン リストから <strong>ポリシー ヒントを使用して送信者に通知する</strong> を選択し、<strong>メッセージをブロックするが、送信者に上書きと送信を許可する</strong> を選択します。

7.  <strong>OK</strong> を選択してから <strong>保存</strong> を選択して、ルールの変更を終了し、変更内容を保存します。

## 正常な動作を確認する方法

拒否しない場合は上書きのポリシー ヒントが正常に作成されたことを確認するには、次の手順を実行します。

1.  EAC 内で、<strong>コンプライアンス管理</strong> \> <strong>データ損失防止</strong> に移動します。

2.  通知メッセージを含むと思われるポリシーを強調表示するには、1 回選択します。

3.  <strong>編集</strong> ![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") を選択し、<strong>ルール</strong> を選択します。

4.  通知メッセージを含むと思われる特定のルールを強調表示するには、1 回選択します。

5.  <strong>メッセージをブロックするが、送信者に上書きと送信を許可する</strong> アクションがルール概要の下部に表示されていることを確認します。

## カスタムのポリシー ヒント通知テキストを作成する

この手順は省略可能ですが、電子メール送信者の電子メール プログラムに表示されるポリシー ヒント通知テキストのカスタマイズに役立ちます。これを行った場合は、通知を表示させるアクションを使用した DLP ポリシー ルールもまた構成しない限り、カスタムのポリシー ヒント通知テキストは表示されません。ポリシー ヒント通知テキストをカスタマイズしない場合は、既定のシステム ポリシー ヒント通知を表示できることに注意してください。既定のテキストの詳細については、「[ポリシー ヒント](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/data-loss-prevention/policy-tips)」を参照してください。

## EAC を使用してカスタムのポリシー ヒント通知テキストを作成および管理する

1.  EAC 内で、<strong>コンプライアンス管理</strong> \> <strong>データ損失防止</strong> に移動します。

2.  <strong>ポリシー ヒントの設定</strong> ![ポリシー ヒントの設定](images/JJ619307.54d1813d-3289-4765-a9a3-a7303a5ab3c7(EXCHG.150).gif "ポリシー ヒントの設定") を選択します。

3.  独自のカスタマイズしたメッセージを使用して新しいポリシー ヒントを追加するには、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") を選択します。使用可能なアクション選択肢の詳細については、「[ポリシー ヒント](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/data-loss-prevention/policy-tips)」を参照してください。
    
    既存のポリシー ヒントを変更するには、ヒントを強調表示して <strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") を選択します。
    
    既存のポリシー ヒントを削除するには、ヒントを強調表示して <strong>削除</strong>![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") を選択し、操作を確認します。

4.  <strong>保存</strong> を選択して、ポリシー ヒントの変更作業を終了し、変更内容を保存します。

5.  <strong>閉じる</strong> を選択して、ポリシー ヒントの管理を終了し、変更内容を保存します。

## シェルを使用してカスタムのポリシー ヒント通知テキストを作成する

次の例では、メッセージの送信をブロックする英語のポリシー ヒントを新しく作成します。このカスタム ポリシー ヒントのテキストは、次の値に変更されます。「This message appears to contain restricted content and will not be delivered.」

    New-PolicyTipConfig -Name en\Reject -Value "This message appears to contain restricted content and will not be delivered."

DLP コマンドレットの詳細については、「[ポリシーとコンプライアンスのコマンドレット](https://technet.microsoft.com/ja-jp/library/dd298082\(v=exchg.150\))」を参照してください。

## シェルを使用してカスタムのポリシー ヒント通知テキストを変更する

次の例では、既存の英語の通知のみのポリシー ヒントを変更します。このカスタムのポリシー ヒントのテキストは、「Sending bank account numbers in email is not recommended.」に変更されます。

    Set-PolicyTipConfig en\NotifyOnly "Sending bank account numbers in email is not recommended."

DLP コマンドレットの詳細については、「[ポリシーとコンプライアンスのコマンドレット](https://technet.microsoft.com/ja-jp/library/dd298082\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

カスタムのポリシー ヒント テキストが正常に作成されたことを確認するには、次の手順を実行します。

1.  EAC 内で、<strong>コンプライアンス管理</strong> \> <strong>データ損失防止</strong> に移動します。

2.  <strong>ポリシー ヒントの設定</strong> ![ポリシー ヒントの設定](images/JJ619307.54d1813d-3289-4765-a9a3-a7303a5ab3c7(EXCHG.150).gif "ポリシー ヒントの設定") を選択します。

3.  <strong>最新の情報に更新</strong> ![\[最新の情報に更新\] アイコン](images/Dn624163.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "[最新の情報に更新] アイコン") を選択します。

4.  アクション、ロケール、およびそのロケールのテキストが一覧に表示されていることを確認します。

## 詳細情報

[データ損失防止](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)

[ポリシー ヒント](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/data-loss-prevention/policy-tips)

[メール フローやトランスポート ルール](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)Exchange 2013

[Exchange Online のメール フロー ルール (トランスポート ルール)](https://technet.microsoft.com/ja-jp/library/jj919238\(v=exchg.150\))Exchange Online

[Exchange 2010 メール ヒント](https://go.microsoft.com/fwlink/?linkid=265179)

