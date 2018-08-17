---
title: 'アイテム保持ポリシーの作成: Exchange Online Help'
TOCTitle: アイテム保持ポリシーの作成
ms:assetid: d8806c98-fea5-492f-906d-f514e25361b2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ150573(v=EXCHG.150)
ms:contentKeyID: 48270123
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# アイテム保持ポリシーの作成

 

_**適用先:** Exchange Online, Exchange Server 2013_

Exchange Online および Exchange Server 2013 では、メールのライフ サイクルを管理するアイテム保持ポリシーを使用できます。アイテム保持ポリシーは、保持タグを作成して、それらをアイテム保持ポリシーに適用し、そのポリシーをメールボックス ユーザーに適用することで適用されます。

アイテム保持ポリシーを作成し、Exchange Online のメールボックスに適用する方法を説明した[ビデオ](https://go.microsoft.com/fwlink/?linkid=825854) を参照してください。

アイテム保持ポリシーに関連する追加の管理タスクについては、「[メッセージング レコード管理の手順](messaging-records-management-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - このタスクの予想所要時間:30 分。

  - このトピックの手順には、特定のアクセス許可が必要です。アクセス許可情報については、各手順を参照してください。

  - アイテム保持ポリシーを適用するメールボックスは、Exchange Server 2010 以降のサーバー上にある必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

## 実行方法

## 手順 1:保持タグを作成する

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「メッセージング レコード管理」。

**EAC を使用して保持タグを作成する**

1.  <strong>コンプライアンス管理</strong>、<strong>保持タグ</strong> の順に移動して、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  以下のいずれかのオプションを選択します。
    
      - **メールボックス全体に自動的に適用する (既定)**   既定のポリシー タグ (DPT) を作成するには、このオプションを選択します。DPT を使用すると、メールボックスのすべてのアイテムに適用される既定の削除ポリシーと既定のアーカイブ ポリシーを作成できます。
        

        > [!NOTE]
        > EAC を使用して、ボイス メール アイテムを削除する DPT を作成することはできません。ボイス メール アイテムを削除する DPT を作成する方法の詳細については、以下のシェル例を参照してください。

    
      - **特定のフォルダーに自動的に適用する** <strong>受信トレイ</strong> や <strong>削除済みアイテム</strong> などの既定フォルダーに対するアイテム保持ポリシー タグ (RPT) を作成するには、このオプションを選択します。
        

        > [!NOTE]
        > <STRONG>[削除して回復を許可する]</STRONG> または <STRONG>[完全に削除]</STRONG> アクションを持つ RPT だけを作成できます。

    
      - **ユーザー別にアイテムとフォルダーに適用する (個人)**   個人タグを作成するには、このオプションを選択します。これらのタグにより、Outlook ユーザーおよび Outlook Web App ユーザーは、メールボックス全体の親フォルダーに適用された設定とは異なるアーカイブまたは削除の設定を、メッセージまたはフォルダーに適用できます。

3.  <strong>New retention tag (保持タグの新規作成)</strong> ページのタイトルおよびオプションは、選択したタグの種類によって異なります。以下のフィールドに入力します。
    
      - **名前** 保持タグの名前を入力します。このタグ名は表示目的のものであり、タグが適用されるフォルダーやアイテムに対する影響はありません。ユーザー向けに入力する個人タグは、Outlook および Outlook Web App において使用可能になると考えてください。
    
      - **次の既定フォルダーにこのタグを適用する**   このオプションを使用できるのは、<strong>特定のフォルダーに自動的に適用する</strong> を選択した場合だけです。
    
      - **保持アクション**   アイテムがその保持期間に達した後に実行する次のいずれかのアクションを選択します。
        
          - **削除して回復を許可する** アイテムは削除しますが、Outlook または Outlook Web App の <strong>削除済みアイテムの復元</strong> オプションを使用してアイテムを復元することをユーザーに対して許可するには、このアクションを選択します。アイテムは、メールボックス データベースまたはメールボックス ユーザーに対して設定された削除済みアイテムの保持期間に達するまで保持されます。
        
          - **完全に削除する** メールボックス データベースからアイテムを完全に削除するには、このオプションを選択します。
            

            > [!IMPORTANT]
            > インプレース保持または訴訟ホールドの対象であるメールボックスまたはアイテムは、インプレース電子情報開示検索に保持または返されます。詳細については、「<A href="in-place-hold-and-litigation-hold-exchange-2013-help.md">インプレース保持と訴訟ホールド</A>」を参照してください。

        
          - **アーカイブに移動する**   このアクションを使用できるのは、DPT または個人タグを作成する場合だけです。ユーザーのインプレース アーカイブにアイテムを移動するには、このアクションを選択します。
    
      - **保持期間** 次のオプションのいずれか 1 つを選択します。
        
          - **実行しない**   アイテムが削除されたり、アーカイブに移動されたりしないように指定するには、このオプションを選択します。
        
          - **アイテムの保管日数が次の期間 (単位日) に達したとき**   このオプションを選択し、アイテムが移動または削除されるまでアイテムを保持する日数を指定します。サポートされるすべてのアイテム (予定表およびタスクを除く) の保持期間は、アイテムが受信または作成された日付から計算されます。予定表およびタスクのアイテムの保持期間は終了日から計算されます。
    
      - **コメント**   管理上の注記やコメントを入力するには、このオプションを使用します。このフィールドはユーザーに表示されません。

**シェルを使用して保持タグを作成する**

保持タグを作成するには、**New-RetentionPolicyTag** コマンドレットを使用します。コマンドレットで利用できる異なるオプションを使用すると、異なる種類の保持タグを作成できます。*Type* パラメーターを使用して、DPT (`All`)、RPT (`Inbox` などの既定のフォルダーの種類を指定)、または個人タグ (`Personal`) を作成します。

この例では、7 年 (2,556 日) 経過後にメールボックスのすべてのメッセージを削除する DPT を作成します。

    New-RetentionPolicyTag -Name "DPT-Corp-Delete" -Type All -AgeLimitForRetention 2556 -RetentionAction DeleteAndAllowRecovery

この例では、2 年 (730 日) 経過後にメールボックスのすべてのメッセージをインプレース アーカイブに移動する DPT を作成します。

    New-RetentionPolicyTag -Name "DPT-Corp-Move" -Type All -AgeLimitForRetention 730 -RetentionAction MoveToArchive

この例では、20 日経過後にすべてのボイス メール メッセージを削除する DPT を作成します。

    New-RetentionPolicyTag -Name "DPT-Corp-Voicemail" -Type All -MessageClass Voicemail -AgeLimitForRetention 20 -RetentionAction DeleteAndAllowRecovery

この例では、30 日経過後に \[迷惑メール\] フォルダーのメッセージを完全に削除する RPT を作成します。

    New-RetentionPolicyTag -Name "RPT-Corp-JunkMail" -Type JunkEmail -AgeLimitForRetention 30 -RetentionAction PermanentlyDelete

この例では、メッセージを削除しない個人タグを作成します。

    New-RetentionPolicyTag -Name "Never Delete" -Type Personal -RetentionAction DeleteAndAllowRecovery -RetentionEnabled $false

## 手順 2:アイテム保持ポリシーを作成する

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「メッセージング レコード管理」。

**EAC を使用してアイテム保持ポリシーを作成する**

1.  <strong>コンプライアンス管理</strong>、<strong>アイテム保持ポリシー</strong> の順に移動して、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  <strong>アイテム保持ポリシーの新規作成</strong> で、次のフィールドを入力します。
    
      - **名前** アイテム保持ポリシーの名前を入力します。
    
      - **保持タグ** <strong>追加</strong> ![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックして、このアイテム保持ポリシーに追加するタグを選択します。
        
        アイテム保持ポリシーには、次のタグを含めることができます。
        
          - <strong>アーカイブへ移動</strong> アクションを持つ 1 つの DPT
        
          - <strong>削除して回復を許可する</strong> または <strong>完全に削除</strong> アクションを持つ 1 つの DPT
        
          - <strong>削除して回復を許可する</strong> または <strong>完全に削除</strong> アクションを持つボイス メール メッセージ用の 1 つの DPT
        
          - <strong>受信トレイ</strong> などの既定のフォルダーごとに、アイテムを削除する １ つの RPT
        
          - 個人タグの数
            

            > [!NOTE]
            > アイテム保持ポリシーには個人タグをいくつでも追加できますが、さまざまな保存期間の設定がある個人タグを数多く設定するとユーザーを混乱させることがあります。アイテム保持ポリシーにリンクする個人タグは 10 以下にすることをお勧めします。

        
        保持タグを追加せずにアイテム保持ポリシーを作成できますが、ポリシーが適用されるメールボックスのアイテムは移動または削除されません。アイテム保持ポリシーを作成した後で、アイテム保持ポリシーに保持タグを追加したり、アイテム保持ポリシーから保持タグを削除したりすることもできます。

**シェルを使用してアイテム保持ポリシーを作成する**

この例では、アイテム保持ポリシー RetentionPolicy-Corp を作成し、*RetentionPolicyTagLinks* パラメーターを使用して、ポリシーに 5 つのタグを関連付けます。

    New-RetentionPolicy "RetentionPolicy-Corp"  -RetentionPolicyTagLinks "DPT-Corp-Delete","DPT-Corp-Move","DPT-Corp-Voicemail","RPT-Corp-JunkMail","Never Delete"

構文およびパラメーターの詳細については、「[New-RetentionPolicy](https://technet.microsoft.com/ja-jp/library/dd297970\(v=exchg.150\))」を参照してください。

## 手順 3:メールボックス ユーザーにアイテム保持ポリシーを適用する

アイテム保持ポリシーを作成した後は、それをメールボックス ユーザーに適用する必要があります。異なるユーザーのセットに異なるアイテム保持ポリシーを適用することができます。詳細な説明については、「[メールボックスにアイテム保持ポリシーを適用する](apply-a-retention-policy-to-mailboxes-exchange-2013-help.md)」を参照してください。

## このタスクの検証方法

保持タグを作成した後は、それらをアイテム保持ポリシーに適用して、そのポリシーをメールボックス ユーザーに適用します。次回、MRM メールボックス アシスタントがメールボックスを処理するときに、保持タグで構成した設定に基づいてメッセージを移動または削除します。

アイテム保持ポリシーが適用されたことを確認するには、次の手順を実行します。

1.  次のシェル コマンドを実行して、単一のメールボックスに対して MRM アシスタントを手動で実行します。
    
        Start-ManagedFolderAssistant -Identity <mailbox identity>

2.  Outlook または Outlook Web App を使用してメールボックスにログインし、ポリシーの構成に従ってメッセージが削除またはアーカイブに移動されていることを確認します。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。


