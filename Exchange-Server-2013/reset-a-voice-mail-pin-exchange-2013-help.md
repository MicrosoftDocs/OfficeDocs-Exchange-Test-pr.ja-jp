---
title: 'ボイス メール PIN のリセット: Exchange Online Help'
TOCTitle: ボイス メール PIN のリセット
ms:assetid: bf07e6e7-01d2-4933-bff5-c615cc21a480
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124404(v=EXCHG.150)
ms:contentKeyID: 50555864
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.ResetUnifiedMessagingPinPropertyControl
ms.translationtype: HT
---

# ボイス メール PIN のリセット

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) が有効なボイス メール ユーザーが Outlook Voice Access 使用時に、正しくない PIN を使用して何回かサインインしようとしたためにメールボックスからロックアウトされた場合や、PIN を忘れてしまった場合、以下のいずれかの手順を実行してユーザーの PIN をリセットできます。ユーザーの Outlook Voice Access PIN をリセットした場合、PIN を自動的に生成するように UM を構成することも、PIN を手動で指定することもできます。新しい PIN は電子メールでユーザーに送信されます。PIN に関する追加のオプションを設定して、ユーザーが初めてサインインしたときに PIN を再設定するよう求めることもできます。また、ユーザーは自分の UM PIN を Outlook や Outlook Web App で再設定できます。


> [!NOTE]
> UM が有効なメールボックスにアクセスするには、Outlook Voice Access ユーザーは、デュアル トーン多重周波数 (DTMF) とも呼ばれるタッチトーン入力を使用する必要があります。PIN 入力では、音声認識を使用することはできません。



Outlook Voice Access の PIN セキュリティに関連するその他のタスクについては、「[PIN セキュリティ手順](pin-security-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して、ユニファイド メッセージングの PIN をリセットする

1.  EAC で、**\[受信者\]** に移動します。リスト ビューで、表示するユーザー メールボックスを選択します。

2.  詳細ウィンドウの **\[電話と音声の機能\]** の下にある **\[ユニファイド メッセージング\]** で、**\[詳細の表示\]** をクリックします。

3.  **\[UM メールボックス\]** ページの **\[UM メールボックスの設定\]** で、**\[PIN のリセット\]** をクリックします。

4.  **\[UM メールボックス PIN のリセット\]** ページで、次のオプションを使用して UM が有効なユーザーの PIN をリセットします。
    
      - **\[PIN を自動的に生成する\]**   Outlook Voice Access を使用してメールボックスにアクセスするためにユーザーが使用する PIN を自動的に生成する場合は、このオプションを使用します。既定では、この設定は有効になっています。
        
        自動的に生成された PIN は、電子メール メッセージでユーザーのメールボックスに送信されます。ユーザーが PIN を受け取って自分のメールボックスにサインインすると、その PIN をもっとわかりやすい PIN に変更するように求めるメッセージが表示されます。
        
        Outlook Web App および Microsoft Outlook では、ユーザーが PIN をリセットすることもできます。PIN は、ユーザーのメールボックスに関連付けられた UM メールボックス ポリシーで構成されている PIN ポリシーに基づいて自動的に生成されます。Outlook Voice Access ユーザーの PIN は自動的に生成することをお勧めします。
    
      - **\[PIN を入力する\]**   Outlook Voice Access ユーザーの PIN を手動で指定するには、このオプションを使用します。既定では、この設定は無効になっています。
        
        ユーザーの PIN を指定すると、その PIN が電子メール メッセージでユーザーのメールボックスに送信されます。ユーザーは、PIN を受け取って自分のメールボックスにサインインした後、Outlook Voice Access の個人オプションを構成してその PIN を変更することができます。ただし、Outlook Web App および Microsoft Outlook には、PIN を手動で指定するオプションはありません。
    
      - **\[初回サインイン時にユーザーに PIN のリセットを要求する\]**   ユーザーが Outlook Voice Access に初めてサインインするときに PIN をリセットするように要求するには、このオプションを使用します。既定では、このオプションは有効になっています。
        
        ユーザーの PIN を自動的に生成するオプションを選択する場合は、このオプションを有効にして、ユーザーが Outlook Voice Access に初めてサインインするときに PIN を変更するように要求することができます。これにより、ユーザーの PIN を保護することができます。

5.  **\[保存\]** をクリックします。

## シェルを使用して、ユニファイド メッセージングの PIN をリセットする

この例では、Tony Smith のボイス メール PIN を 1985848 にリセットします。ただし、この PIN は、ユーザーが初めて Outlook Voice Access にサインインするときに変更する必要があります。

    Set-UMMailboxPIN -Identity tonysmith@contoso.com -PIN 1985848 -PinExpired $true

