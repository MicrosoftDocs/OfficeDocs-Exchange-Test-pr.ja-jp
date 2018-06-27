---
title: '同じダイヤル プランのユーザーが FAX を受信できるようにする: Exchange Online Help'
TOCTitle: 同じダイヤル プランのユーザーが FAX を受信できるようにする
ms:assetid: cb245028-0b86-4171-879e-934dd35fa626
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124557(v=EXCHG.150)
ms:contentKeyID: 52057520
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 同じダイヤル プランのユーザーが FAX を受信できるようにする

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) ダイヤル プランとリンクされているすべてのユーザーに対して、メールボックスで FAX メッセージを受信することを許可できます。既定では、ユニファイド メッセージングが有効で、UM ダイヤル プランとリンクされているユーザーは、FAX メッセージを受信することができます。UM が有効なユーザーがメールボックスで FAX を受信できるようにするには、着信 FAX を受け付けるようにダイヤル プランを構成する必要があります。また、UM メールボックス ポリシーとユーザーの FAX 送受信を有効にする必要があります。既定では、ダイヤル プラン、UM メールボックス ポリシー、およびユーザーの FAX 送受信は有効です。ただし、これらの既定の設定が変更されていると、UM が有効なユーザーが FAX メッセージを受信できない場合があります。

ダイヤル プランで FAX メッセージが受信されないようにした場合は、個々のユーザーのプロパティを FAX メッセージを受信できるように構成しても、そのダイヤル プランと関連付けられているユーザーはすべて FAX メッセージを受信できなくなります。UM ダイヤル プランに対する FAX 送受信の有効/無効化は、UM メールボックス ポリシーや個々の UM が有効なユーザーに対する FAX 送受信の設定よりも優先されます。


> [!NOTE]
> UM メールボックス ポリシーの FAX の設定は、EAC を使用して構成できます。ただし、ダイヤル プランまたは個々のユーザーについては、シェルを使用して FAX 設定を構成する必要があります。



FAX パートナーの詳細は、「[Microsoft PinPoint の FAX パートナー](https://go.microsoft.com/fwlink/?linkid=190238)」を参照してください。

FAX に関するその他の管理タスクについては、「[FAX 送受信の手順](faxing-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ダイヤル プラン」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## シェルを使用して、ダイヤル プランにリンクされているユーザーの FAX 受信を許可する

この例では、`MyUMDialPlan` という UM ダイヤル プランとリンクされている UM が有効なユーザーが、着信 FAX を受信できるようにします。

    Set-UMDialPlan -Identity MyUMDialPlan -FaxEnabled $true

