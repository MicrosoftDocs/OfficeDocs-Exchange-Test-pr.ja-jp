---
title: 'UM メールボックス ポリシーの作成: Exchange Online Help'
TOCTitle: UM メールボックス ポリシーの作成
ms:assetid: 7f20874b-c46c-4505-9a78-f63eacb578ff
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb123510(v=EXCHG.150)
ms:contentKeyID: 50555805
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMMailboxPolicyWizardForm.CreateUMMailboxPolicyWizardPage
ms.translationtype: HT
---

# UM メールボックス ポリシーの作成

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) メールボックス ポリシーを作成すると、PIN のポリシー設定やダイヤル制限などの共通の UM ポリシー設定を、UM が有効なメールボックスの集合に適用することができます。UM メールボックス ポリシーでは、UM が有効なユーザーを UM ダイヤル プランにリンクして、UM が有効なメールボックスの集合に、ポリシーやセキュリティ設定の共通セットを適用します。UM が有効なユーザーに対して UM 構成設定を適用および標準化する場合に便利です。

既定では、UM ダイヤル プランを作成すると、UM メールボックス ポリシーも作成されます。ユニファイド メッセージングを組織内に展開した後で、追加の UM メールボックス ポリシーの作成、または既存の UM メールボックス ポリシーの変更が必要になる場合があります。

UM メールボックス ポリシーに関連する追加の管理タスクについては、「[UM メールボックス ポリシー手順](um-mailbox-policy-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 3 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス ポリシー」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して UM メールボックス ポリシーを作成する

1.  
    
    EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。リスト ビューで変更したい UM ダイアル プランを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  <strong>UM ダイヤル プラン</strong> ページの <strong>UM メールボックス ポリシー</strong> で <strong>新規</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

3.  <strong>UM メールボックス ポリシーの新規作成</strong> ページで、<strong>名前</strong> テキスト ボックスに新しい UM メールボックス ポリシーの名前を入力します。
    
    このボックスを使用して、UM メールボックス ポリシーに一意の名前を指定します。これは、EAC に表示される表示名です。UM メールボックス ポリシーを作成した後にその表示名を変更する必要が生じた場合は、まず既存の UM メールボックス ポリシーを削除し、その後で適切な名前を持つ別の UM メールボックス ポリシーを作成する必要があります。UM が有効なユーザーが UM メールボックス ポリシーに関連付けられている場合は、UM メールボックス ポリシーを削除できません。
    
    UM メールボックス ポリシー名は必須ですが、この名前が使用されるのは表示のためだけです。組織で複数の UM メールボックス ポリシーを使用する場合もあるため、わかりやすい名前を使用することをお勧めします。UM メールボックス ポリシー名の長さの上限は 64 文字で、スペースも使用できます。ただし、次の文字を含めることはできません。" / \\ \[ \] : ; | = , + \* ? \< \>.

4.  <strong>保存</strong>をクリックして、新しい UM メールボックス ポリシーを保存します。UM メールボックス ポリシーを保存すると、PIN ポリシー、ボイス メール機能、および保護ボイス メールの設定を含むすべての既定の設定が有効になります。既定の設定をカスタマイズまたは変更する場合は、**Set-UMMailbox** コマンドレットを使用して、作成したばかりの UM メールボックス ポリシーの設定を変更します。

## シェルを使用した UM メールボックス ポリシーの作成

この例では、`MyUMDialPlan` という名前の UM ダイヤル プランに関連付けられた、`MyUMMailboxPolicy` という名前の新しい UM メールボックス ポリシーを作成します。

    New-UMMailboxPolicy -Name MyUMMailboxPolicy -UMDialPlan MyUMDialPlan

