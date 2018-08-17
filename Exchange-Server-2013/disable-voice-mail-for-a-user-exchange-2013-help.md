---
title: 'ユーザーのボイス メールを無効にする: Exchange Online Help'
TOCTitle: ユーザーのボイス メールを無効にする
ms:assetid: cecc9c0d-377d-489e-9db4-d487e9c0b552
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124691(v=EXCHG.150)
ms:contentKeyID: 49896483
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ユーザーのボイス メールを無効にする

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

UM が有効なユーザーのユニファイド メッセージング (UM) を無効にすることができます。 これを行うと、ユーザーは Exchange 2013 のボイス メール機能を使用できなくなります。 必要な場合は、ユーザーの UM を無効にする際に、そのユーザーの UM 設定を維持できます。

ボイス メールが有効なユーザーに関連するその他の管理タスクについては、「[ユーザーのボイス メール設定の管理](manage-voice-mail-settings-for-a-user-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス」。

  - これらの手順を実行する前に、既存のユーザーに Exchange メールボックスがあることを確認してください。

  - これらの手順を実行する前に、既存のユーザーがユニファイド メッセージングで現在有効になっていることを確認してください。詳細な手順については、「[ボイス メール用にユーザーを有効にする](enable-a-user-for-voice-mail-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[New-UMMailboxPolicy](https://technet.microsoft.com/ja-jp/library/aa998300\(v=exchg.150\))」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してユーザーのユニファイド メッセージングおよびボイス メールを無効にする

1.  EAC で、<strong>受信者</strong> をクリックします。

2.  リスト ビューで、ユニファイド メッセージングを無効にするメールボックスを持つユーザーを選択します。

3.  \[詳細\] ウィンドウの <strong>電話と音声の機能</strong> および <strong>ユニファイド メッセージング</strong> で、<strong>無効にする</strong> をクリックします。

4.  <strong>警告</strong> ボックスで <strong>はい</strong> をクリックして、ユーザーに対してユニファイド メッセージングを無効にすることを確認します。

## シェルを使用してユーザーのユニファイド メッセージングおよびボイス メールを無効にする

この例では、ユーザー tonysmith@contoso.com のユニファイド メッセージングおよびボイス メッセージを無効にするが、UM メールボックスの設定は維持します。

    Disable-UMMailbox -Identity tonysmith@contoso.com -KeepProperties $True

