---
title: 'Outlook Voice Access ユーザーが検索する主な方法を構成する: Exchange Online Help'
TOCTitle: Outlook Voice Access ユーザーが検索する主な方法を構成する
ms:assetid: 3d93a037-5820-41d3-9206-69f534414daf
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997563(v=EXCHG.150)
ms:contentKeyID: 49896220
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Voice Access ユーザーが検索する主な方法を構成する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) ダイヤル プランを作成すると、発信者が Outlook Voice Access 番号またはダイヤル プランに関連付けられた UM 自動応答を呼び出すときにユーザーを名前で検索するための第 1 の方法と第 2 の方法を構成できます。発信者は、タッチトーン入力を使用して UM が有効なユーザーを検索できます。


> [!NOTE]
> <STRONG>[なし]</STRONG> は、発信者が名前を検索するために使用する第 1 の方法では、使用できません。発信者が名前を検索するために使用する第 2 の方法に対して <STRONG>[なし]</STRONG> を選択すると、発信者は第 1 の方法しか使用できません。発信者が名前を検索するために使用する第 1 の方法と第 2 の方法の両方を構成すると、発信者に両方の方法についてプロンプト メッセージが表示されます。



UM ダイヤル プランに関連するその他の管理タスクについては、「[UM ダイヤル プラン手順](um-dial-plan-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ダイヤル プラン」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して第 1 の名前によるダイヤル方法を変更する

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。

2.  リスト ビューで、変更する UM ダイヤル プランを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>UM ダイヤル プラン</strong> ページで、<strong>構成</strong> をクリックします。

4.  <strong>設定</strong> の <strong>名前を検索するときに最初に使用する方法</strong> の下にあるドロップダウン リストから必要なオプションを選択します。
    
      - <strong>姓 名</strong> (既定)
    
      - <strong>名 姓</strong>
    
      - **SMTP アドレス**

5.  <strong>保存</strong> をクリックします。

## シェルを使用して第 1 の名前によるダイヤル方法を変更する

この例では、名前によるダイヤルの第 1 の方法を `FirstLast` に設定します。これにより、Outlook Voice Access 番号またはダイヤル プランに関連付けられた UM 自動応答を呼び出す発信者が、UM が有効になっているユーザーを名、次に姓で検索できるようになります。

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNamePrimary FirstLast

この例では、名前によるダイヤルの第 1 の方法を `LastFirst` に設定します。これにより、Outlook Voice Access 番号またはダイヤル プランに関連付けられた UM 自動応答を呼び出す発信者が、UM が有効になっているユーザーを姓、次に名で検索できるようになります。

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNamePrimary LastFirst 

この例では、名前によるダイヤルの第 1 の方法を `SMTP address` に設定します。これにより、Outlook Voice Access 番号またはダイヤル プランに関連付けられた UM 自動応答を呼び出す発信者が、UM が有効になっているユーザーをその SMTP アドレスで検索できるようになります。

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNamePrimary SMTPAddress

