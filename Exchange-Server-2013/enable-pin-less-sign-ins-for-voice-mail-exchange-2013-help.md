---
title: 'ボイス メールの PIN なしサインインを有効にする: Exchange 2013 Help'
TOCTitle: ボイス メールの PIN なしサインインを有効にする
ms:assetid: 54133753-317c-42ef-9b0d-ca9f2d2d6bd7
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg602127(v=EXCHG.150)
ms:contentKeyID: 54652965
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ボイス メールの PIN なしサインインを有効にする

 

_**適用先:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2015-04-08_

ユーザーが PIN を使用せずにボイス メールにサインインできるように、ユニファイド メッセージング (UM) をセット アップすることができます。既定では、Outlook Voice Access ユーザーは、メールボックスにサインインするときと、ボイス メール、電子メール、予定表、個人用連絡先、ディレクトリ、および個人用オプションにアクセスするときに PIN の入力が要求されます。


> [!WARNING]
> ボイス メールが有効な単一ユーザーまたはユーザーのグループに対して PIN なしサインインを有効にすると、ボイス メールのセキュリティ レベルが下がり、組織がセキュリティ リスクに晒されます。



PIN なしサインインを有効にするには、UM メールボックス ポリシーのパラメーター *AllowPinlessVoiceMailAccess* を `$true` に設定すると共に、UM メールボックスのパラメーター *PinlessAccessToVoiceMailEnabled* を `$true` に設定する必要があります。既定では、両方のパラメーターが `$false` に設定され、Outlook Voice Access ユーザーはボイス メールにアクセスするときに、PIN の入力を要求されます。

両方のパラメーターが `$true` に設定されている場合は、UM メールボックスに関連付けられている大きなユーザー グループのボイス メールへの PIN なしサインインを有効にしたり、単一の UM メールボックスまたは UM メールボックスのサブセットへの PIN なしサインインを有効にしたりできます。UM 対応ユーザーのグループまたは単一の UM 対応ユーザーのボイス メールへの PIN なしサインインを有効にした場合でも、電子メール、予定表、個人用連絡先、ディレクトリ、または個人用オプションにアクセスする際には、PIN の入力が要求されます。

ユーザーのボイス メールへの PIN なしサインインを有効にするには、次の条件を満たす必要があります。

  - UM メールボックス ポリシーに対して、次のコマンドレットを実行しておくこと。`Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowPinlessVoiceMailAccess $true`

  - UM 対応ユーザーのメールボックスに対して、次のコマンドレットを実行しておくこと。`Set-UMMailbox -id tonys@contoso.com -PinlessAccessToVoiceMailEnabled $true`

  - UM 対応ユーザーが、PIN なしサインインを有効にした UM メールボックス ポリシーと同じ UM メールボックス ポリシーに関連付けられていること。

  - UM 対応ユーザーが、割り当て済みの電話番号から Outlook Voice Access にダイヤル インできること。

  - この手順を実行するには、シェルを使用する必要があります。オンプレミスの Exchange 組織で Exchange 管理シェル を開く方法については、「[シェルを開く](https://technet.microsoft.com/ja-jp/library/dd638134\(v=exchg.150\))」を参照してください。 Windows PowerShell を使って Exchange Online に接続する方法については、「[Exchange Online PowerShell への接続](https://go.microsoft.com/fwlink/p/?linkid=396554)」を参照してください。

UM メールボックス ポリシーに関連する追加のタスクについては、「[UM メールボックス ポリシー手順](um-mailbox-policy-procedures-exchange-2013-help.md)」を参照してください。

UM メールボックスに関連するその他のタスクについては、「[ボイス メールが有効なユーザーの手順](voice-mail-enabled-user-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 3 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス ポリシー」。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、ユーザーの UM とボイス メールが有効になっていることを確認します。詳細な手順については、「[ボイス メール用にユーザーを有効にする](enable-a-user-for-voice-mail-exchange-2013-help.md)」を参照してください。

## 必要な作業

## シェルを使用して、UM メールボックス ポリシーで UM が有効なユーザーの PIN 入力不要のボイス メール アクセスを有効にする

この例では、Outlook Voice Access にダイヤル インする、メールボックス ポリシーに関連付けられたユーザーの `MyUMMailboxPolicy` という名前の UM メールボックス ポリシーに対する PIN なしボイル メール アクセスを有効にします。

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowPinlessVoiceMailAccess $true

## シェルを使用して、UM が有効なユーザーのメールボックスで PIN 入力不要のボイス メール アクセスを有効にする

この例では、Outlook Voice Access にダイヤル インして `tonys@contoso.com` という名前のメールボックスにアクセスするユーザーの PIN なしボイス メール アクセスを有効にします。

    Set-UMMailbox -id tonys@contoso.com -PinlessAccessToVoiceMailEnabled $true

