---
title: 'UM 自動応答を作成する: Exchange Online Help'
TOCTitle: UM 自動応答を作成する
ms:assetid: 773f53fb-d80f-4a79-8bd3-bd753942489f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998875(v=EXCHG.150)
ms:contentKeyID: 49896324
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.UnifiedMessaging.CreateAutoAttendantWizardForm.CreateAutoAttendantWizardPage
ms.translationtype: HT
---

# UM 自動応答を作成する

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) 自動応答を作成すると、通常は人間のオペレーターが応答する外線番号への着信呼び出しに、自動応答が応答するようになります。UM ダイヤル プランや UM IP ゲートウェイなど、他のユニファイド メッセージング コンポーネントとは異なり、UM 自動応答の作成は必須ではありません。ただし、自動応答は、組織の内部や外部から電話を掛けてきた人が、組織内に存在するユーザーや部署を見つけて目的の相手や部署に呼び出しを転送できるようにします。

UM 自動応答に関連する追加の管理タスクについては、「[UM 自動応答手順](um-auto-attendant-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 3 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM 自動応答」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用した UM 自動応答の作成

1.  
    
    EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** の順に選択し、自動応答を追加する UM ダイヤル プランを選択して **\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページの **\[UM 自動応答\]** の下にある **\[新規\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

3.  **\[UM 自動応答の新規作成\]** ページで、以下の情報を入力します。
    
      - **\[名前\]**   このボックスを使用して、UM 自動応答の表示名を作成します。一意な UM 自動応答名を必ず指定する必要があります。ただし、EAC およびシェルでは表示専用として使用されます。
        
        自動応答を作成した後にその表示名を変更する必要がある場合は、最初に既存の UM 自動応答を削除してから、適切な名前を持つ別の自動応答を作成する必要があります。組織で複数の UM 自動応答を使用している場合は、UM 自動応答にわかりやすい名前を使用することをお勧めします。UM 自動応答名は最大で 64 文字で、空白を含めることができます。
        
        新しい UM 自動応答には空白を含んだ名前を付けることができますが、ユニファイド メッセージングを Office Communications Server 2007 R2 または Microsoft Lync Server と統合する場合は、自動応答の名前に空白を含めることはできません。したがって、表示名に空白を含めて自動応答を作成し、その後 Office Communications Server 2007 R2 または Lync Server と統合する場合は、まずその自動応答を削除してから、表示名に空白を含まない別の自動応答を作成する必要があります。
    
      - **\[この自動応答を作成して有効にする\]**   このチェック ボックスを選択すると、UM 自動応答の新規作成ウィザードを終了したときに、自動応答が着信呼び出しに応答するようになります。既定では、新しい自動応答は無効な状態で作成されます。
        
        UM 自動応答を無効な状態で作成した場合は、ウィザードの完了後に EAC またはシェルを使用して、自動応答を有効にすることができます。
    
      - **\[音声コマンドに応答する自動応答を設定する\]**   このチェック ボックスをオンにすると、UM 自動応答の音声認識が有効になります。自動応答の音声認識が有効な場合、電話をかけてきた人は、音声入力またはタッチトーン入力を使用して、UM 自動応答のシステムまたはカスタム プロンプトに応答できます。既定では、作成直後の自動応答は音声認識に対応しません。
        
        発信者に対して音声認識が有効な自動応答を使用するためには、自動音声認識 (ASR) のサポートを含む適切な UM 言語パックをインストールし、自動応答でこの言語を使用するようにプロパティを構成する必要があります。
    
      - **\[アクセス番号\]**   このボックスを使用して、電話をかけてきた人が自動応答を呼び出すために使用する内線番号または電話番号を入力します。このボックスに内線番号または電話番号を入力し、**\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックしてその番号を一覧に追加します。入力した内線番号または電話番号の桁数と、関連付けられている UM ダイヤル プランで構成されている内線番号の桁数とが一致する必要はありません。これは、UM 自動応答では直通電話が許可されるためです。
        
        入力できる内線番号または電話番号の数に制限はありません。ただし、内線番号を持たない新しい自動応答を作成してもかまいません。内線番号または電話番号は必須ではありません。
        
        既存の内線番号または電話番号を編集または削除できます。既存の内線番号または電話番号を編集するには、**\[編集\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。既存の内線番号または電話番号を一覧から削除するには、**\[削除\]**![\[削除\] アイコン](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[削除] アイコン") をクリックします。

4.  **\[保存\]** をクリックします。

## シェルを使用した UM 自動応答の作成

この例では、音声認識が有効ではない着信呼び出しを受け付けることができる `MyUMAutoAttendant` という名前の UM 自動応答を作成します。

    New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 55000 -Enabled $false

この例では、`MyUMAutoAttendant` という名前の、音声認識が有効な UM 自動応答を作成します。

    New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 56000,56100 -SpeechEnabled $true

