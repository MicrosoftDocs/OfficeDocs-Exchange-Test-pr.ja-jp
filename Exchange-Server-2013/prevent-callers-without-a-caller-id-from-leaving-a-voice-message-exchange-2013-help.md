---
title: '呼び出し ID のない呼び出し元が音声メッセージを残すことを禁止する: Exchange Online Help'
TOCTitle: 呼び出し ID のない呼び出し元が音声メッセージを残すことを禁止する
ms:assetid: dd5dad32-2f69-4bf4-8ff0-545c413d395a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ673571(v=EXCHG.150)
ms:contentKeyID: 49896516
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 呼び出し ID のない呼び出し元が音声メッセージを残すことを禁止する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

UM が有効なユーザーに対して、匿名発信者からのボイス メッセージの受信を許可または禁止することができます。既定では、ユニファイド メッセージング (UM) およびボイス メールが有効になると、ユーザーは呼び出し ID 情報を含まない匿名呼び出しを受信できます。

ほとんどの場合、Exchange サーバーによって受信された呼び出しには呼び出し ID が含まれているため、着信呼び出しの送信元を特定できます。ただし、以下のような理由から、着信呼び出しに呼び出し ID 情報が含まれない場合があります。

  - 組織のテレフォニー機器が呼び出し ID 情報を含めないように構成されている。

  - 着信呼び出しが携帯電話または外線からのものである。

  - 発信者の電話で呼び出し ID が無効になっている。

*AnonymousCallersCanLeaveMessages* パラメーターが既定で有効になっているので、UM が有効なユーザーは呼び出し ID 情報が含まれていない場合にも音声メッセージを受信できます。*AnonymousCallersCanLeaveMessages* オプションが無効になっている場合に UM が有効なユーザーが呼び出し ID を含まない呼び出しを受信すると、その呼び出しは匿名と識別されてボイス メッセージの受信は行われません。

ボイス メールが有効なユーザーに関連する追加の管理タスクについては、「[ボイス メールが有効なユーザーの手順](voice-mail-enabled-user-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス」。

  - この手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、ユーザーのメールボックスの UM が有効になっていることを確認してください。詳細な手順については、「[ボイス メール用にユーザーを有効にする](enable-a-user-for-voice-mail-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## シェルを使用して匿名発信者からのボイス メールの受信を禁止する

この例では、UM が有効なユーザー tonysmith@contoso.com が、発信者番号情報を含まない呼び出しからのボイス メールを受信することを禁止します。

    Set-UMMailbox -Identity tonysmith@contoso.com -AnonymousCallersCanLeaveMessages $false

