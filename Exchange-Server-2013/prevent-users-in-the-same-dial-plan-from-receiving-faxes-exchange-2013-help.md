---
title: '同じダイヤル プランのユーザーが FAX を受信できないようにする: Exchange Online Help'
TOCTitle: 同じダイヤル プランのユーザーが FAX を受信できないようにする
ms:assetid: 4fc66414-c950-4bca-ac20-4e489f288d06
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb201688(v=EXCHG.150)
ms:contentKeyID: 52057421
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 同じダイヤル プランのユーザーが FAX を受信できないようにする

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) ダイヤル プランとリンクされている UM が有効なユーザーが FAX メッセージを受信しないようにすることができます。既定では、ユニファイド メッセージングが有効で、UM ダイヤル プランとリンクされているユーザーは、FAX メッセージを受信することができます。ただし、特定の UM ダイヤル プランに関連付けられているユーザーが FAX を受信できないようにする必要がある場合もあります。

UM ダイヤル プラン、UM メールボックス ポリシー、または UM が有効なユーザーのメールボックスを構成することによって、UM が有効なユーザーが FAX を受信できないようにすることができます。UM ダイヤル プランで着信 FAX メッセージの配信を無効にすると、そのダイヤル プランに関連付けられているすべてのユーザーが FAX メッセージを受信できなくなります。UM ダイヤル プランでの FAX 送受信の有効化または無効化は、個々の UM が有効なユーザーに対する設定より優先されます。


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



## シェルを使用してダイヤル プランにリンクされているユーザーが FAX を受信できないようにする

この例では、`MyUMDialPlan` という名前の UM ダイヤル プランに関連付けられた UM が有効なユーザーが FAX を受信できないようにします。

    Set-UMDialPlan -Identity MyUMDialPlan -FaxEnabled $false

