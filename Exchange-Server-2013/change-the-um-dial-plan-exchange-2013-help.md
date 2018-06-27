---
title: 'UM ダイヤル プランの変更: Exchange Online Help'
TOCTitle: UM ダイヤル プランの変更
ms:assetid: 4a6b6b6f-c61c-44e8-91dd-c5d28835f441
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee633465(v=EXCHG.150)
ms:contentKeyID: 49896235
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM ダイヤル プランの変更

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) が有効なユーザーを別の UM ダイヤル プランに移動したり、またはユーザーに関連付けられたダイヤル プランを変更したりすることが必要になる場合があります。 たとえば、UM が有効なユーザーを電話の内線番号ダイヤル プランから SIP URI ダイヤル プランに移動する必要がある場合があります。

UM ダイヤル プランを変更するには、ユーザーのユニファイド メッセージングを無効にして、新しい UM ダイヤル プランでユーザーのユニファイド メッセージングを有効にする必要があります。 これは、各種ダイヤル プランがさまざまな内線番号の長さ、さまざまな URI タイプなど異なる設定および要件を持っていることが理由です。 たとえば、SIP URI ダイヤル プランには SIP リソース識別子を UM が有効な各メールボックスに割り当てる必要がありますが、電話の内線番号ダイヤル プランには必要ありません。また、各 UM メールボックスには、UM ダイヤル プランと UM メールボックス ポリシーの両方への参照が含まれます。 さらに、UM メールボックス ポリシーには UM ダイヤル プランへの参照が含まれます。 UM が有効なユーザーのプライマリ プロキシ アドレスを別のダイヤル プランを指すように変更すると、UM メールボックスが不整合な状態になります。

ボイス メールが有効なユーザーに関連するその他の管理タスクについては、「[ユーザーのボイス メール設定の管理](manage-voice-mail-settings-for-a-user-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 10 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス」。

  - これらの手順を実行する前に、既存の Exchange 受信者のユニファイド メッセージングが有効になっていることを確認してください。詳細な手順については、「[ボイス メール用にユーザーを有効にする](enable-a-user-for-voice-mail-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[New-UMMailboxPolicy](https://technet.microsoft.com/ja-jp/library/aa998300\(v=exchg.150\))」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 実行方法

## 手順 1:新しい UM ダイヤル プランを作成する


> [!IMPORTANT]
> UM が有効なユーザーを Microsoft Office Communications Server 2007 R2 または Microsoft Lync Server に移行する場合、最初に SIP URI ダイヤル プランを作成する必要があります。



詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

## 手順 2:ユーザーのユニファイド メッセージングを無効にする

詳細な手順については、「[ユーザーのボイス メールを無効にする](disable-voice-mail-for-a-user-exchange-2013-help.md)」を参照してください。

## 手順 3: ユーザーのユニファイド メッセージングを新しい UM ダイヤル プランで有効にする


> [!IMPORTANT]
> Office Communications Server 2007 R2 または Lync Server の環境にユーザーを移行している場合、ユーザーの UM を有効にするときに SIP リソース識別子も対象にする必要があります。 SIP ダイヤル プランに関連付けられた UM メールボックス ポリシーも選択する必要があります。



詳細な手順については、「[ボイス メール用にユーザーを有効にする](enable-a-user-for-voice-mail-exchange-2013-help.md)」を参照してください。

