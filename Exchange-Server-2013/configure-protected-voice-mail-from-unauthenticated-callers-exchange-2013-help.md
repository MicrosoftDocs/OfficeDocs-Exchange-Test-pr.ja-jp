---
title: '認証されていない発信者からの保護されたボイス メールを構成する: Exchange Online Help'
TOCTitle: 認証されていない発信者からの保護されたボイス メールを構成する
ms:assetid: 106bfa0a-a0fa-4a1b-bd59-4b6df1d0d61d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd335098(v=EXCHG.150)
ms:contentKeyID: 52057382
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 認証されていない発信者からの保護されたボイス メールを構成する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

着信呼び出しに応答してから、暗号化を使用してボイス メール メッセージを保護するかどうかを決めるように、ユニファイド メッセージングを構成できます。ボイス メール メッセージが保護されている場合

  - メッセージは、Microsoft Outlook および Outlook Web App で親展とマークされます。

  - 音声メッセージを開くことができるのは、音声メッセージの宛先である受信者のみです。

  - 受信者は音声メッセージに返信できますが、元の音声メッセージに含まれていないユーザーに転送することはできません。

この設定は、UM が有効なユーザーが電話に応答しない場合に送信される音声メッセージに適用されます。この設定は、発信者が UM 自動応答を使用している場合に、UM が有効であるユーザーに直接送信される音声メッセージにも適用されます。

保護されたボイス メールの手順に関連するその他の管理タスクについては、「[保護されているボイス メールの手順](protected-voice-mail-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間:1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス ポリシー」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して、認証されていない発信者からの保護されたボイス メールを構成する

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで変更したい UM ダイアル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン").

2.  **\[UM ダイヤル プラン\]** ページの **\[UM メールボックス ポリシー\]** で管理する UM メールボックス ポリシーを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[UM メールボックス ポリシー\]** ページの **\[保護されているボイス メール\]** にある **\[認証されていない発信者からの音声メッセージを保護する\]** で、次のオプションのいずれかを選択します。
    
      - **\[なし\]**   UM が有効なユーザーに送信される音声メッセージに保護が適用されないようにするには、この設定を使用します。
    
      - **\[親展\]**   この設定は、ユニファイド メッセージングが発信者によって親展としてマークされている音声メッセージにのみ保護を適用する場合に使用します。
    
      - **\[すべて\]**   この設定は、ユニファイド メッセージングが親展としてマークされていない音声メッセージを含むすべての音声メッセージに保護を適用する場合に使用します。

4.  **\[保存\]** をクリックします。

## シェルを使用して、認証されていない呼び出し元からの保護されたボイス メールを構成する

この例では、UM メールボックス ポリシー `MyUMMailboxPolicy` ですべての認証されていない呼び出し元からのすべての音声メッセージを保護します。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -ProtectUnauthenticatedVoiceMail -All

