---
title: 'パートナー FAX サーバーの URI を設定して FAX 送受信を許可する: Exchange Online Help'
TOCTitle: パートナー FAX サーバーの URI を設定して FAX 送受信を許可する
ms:assetid: 77a9013b-d76b-4af2-8b2c-cef435cf67af
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ650873(v=EXCHG.150)
ms:contentKeyID: 52057444
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# パートナー FAX サーバーの URI を設定して FAX 送受信を許可する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) メールボックス ポリシーに関連付けられているユーザーに対して、着信 FAX を有効または無効にできます。既定では、ユーザーの UM を有効にしても、UM メールボックス ポリシーで着信 FAX を有効にして、パートナー FAX サーバーの URI を指定するまで、ユーザーは FAX メッセージを受信できません。UM メールボックス ポリシーで URI が構成されていても、UM ダイヤル プランまたは個々のユーザーで着信 FAX を許可するオプションが無効になっていると、UM メールボックス ポリシーにリンクされている UM が有効なユーザーは FAX を受信できません。

FAX パートナーの詳細は、「[Microsoft PinPoint の FAX パートナー](https://go.microsoft.com/fwlink/?linkid=190238)」を参照してください。

FAX に関するその他の管理タスクについては、「[FAX 送受信の手順](faxing-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間:1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス ポリシー」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して FAX パートナーの URI を設定する

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで変更したい UM ダイアル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン").

2.  **\[UM ダイヤル プラン\]** ページの **\[UM メールボックス ポリシー\]** で、変更するポリシーを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[UM メールボックス ポリシー\]** ページの **\[全般\]** にある **\[パートナー FAX サーバーの URI\]** ボックスに、TCP または TLS の URI を入力します。たとえば、*sip:faxserver1.contoso.com:5060;transport=tcp* または*sip:faxserver2.contoso.com:5061;transport=tls*
    

    > [!NOTE]
    > このボックスには 2 つ以上の FAX サーバーの URI を含めることができますが、使用されるのは 1 つのみです。2 つの URI を入力すると、最初の URI のみが使用されます。



4.  **\[保存\]** をクリックして変更を保存します。

## シェルを使用して FAX パートナーの URI を設定する

この例では、UM メールボックス ポリシー `UMDialPlan Default Policy` にリンクされたユーザーがパートナー FAX サーバー `faxserver1` に対して TCP ポート 5060 を使用できるようにします。

    Set-UMMailboxPolicy "UMDialPlan Default Policy" -FaxServerURI sip:faxserver1.contoso.com:5060;transport=tcp

この例では、UM メールボックス ポリシー `UMDialPlan Default Policy` にリンクされたユーザーがパートナー FAX サーバー `faxserver2` に対して TLS ポート 5061 を使用できるようにします。

    Set-UMMailboxPolicy "UMDialPlan Default Policy" -FaxServerURI sip:faxserver2.contoso.com:5061;transport=tls

