---
title: 'Windows Rights Management をサポートしていない電子メール クライアントに表示するテキストを指定する'
TOCTitle: Windows Rights Management をサポートしていない電子メール クライアントに表示するテキストを指定する
ms:assetid: a9b2238a-b534-469c-a0c3-2768bc3d005b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee423552(v=EXCHG.150)
ms:contentKeyID: 52057486
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Windows Rights Management をサポートしていない電子メール クライアントに表示するテキストを指定する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

保護されている音声メッセージを受信する際にユーザーに送信されるテキストを指定することは可能ですが、電子メール クライアントは Information Rights Management (IRM) も Windows Rights Management もサポートしていません。

保護されているボイス メールにアクセスできるのは、Windows Rights Management をサポートしている電子メール クライアントか、または UM が有効なユーザーが Outlook Voice Access を使用する場合のみです。

保護されたボイス メールは暗号化されています。音声メッセージが保護されている場合

  - メッセージは、Microsoft Outlook および Outlook Web App で親展とマークされます。

  - 音声メッセージを開くことができるのは、音声メッセージの宛先である受信者のみです。

  - 受信者は音声メッセージに返信できますが、元の音声メッセージに含まれていないユーザーに転送することはできません。

電子メール クライアントが Windows Rights Management をサポートしておらず、Outlook Voice Access を使用してメッセージにアクセスしていないユーザーに保護されている音声メッセージが送信されると、指定したテキストを含む電子メール メッセージがそのユーザーに送信されます。このテキストには、保護された音声メッセージを呼び出し先が受信するための手順を含める必要があります。

保護されたボイス メールの手順に関連するその他の管理タスクについては、「[保護されているボイス メールの手順](protected-voice-mail-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス ポリシー」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して Windows Rights Management をサポートしていない電子メール クライアントに表示するテキストを指定する

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページの **\[UM メールボックス ポリシー\]** で管理する UM メールボックス ポリシーを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[UM メールボックス ポリシー\]** ページの **\[保護されているボイス メール\]** にある **\[Windows Rights Management をサポートしていないユーザーに送信するメッセージ\]** のテキスト ボックスにメッセージ テキストを入力します。

4.  **\[保存\]** をクリックします。

## シェルを使用して Windows Rights Management をサポートしていない電子メール クライアントに表示するテキストを指定する

この例では、Windows Rights Management をサポートしていない電子メール クライアントを持つ、`MyUMMailboxPolicy` という名前の UM メールボックス ポリシーに関連付けられているユーザーに表示するテキストを指定します。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -ProtectedVoiceMailText "Your email client software does not support Protected Voice Mail. Please contact the Help Desk."

