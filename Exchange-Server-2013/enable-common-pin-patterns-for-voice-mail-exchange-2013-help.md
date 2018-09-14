---
title: 'ボイス メールの共通 PIN パターンを有効にする: Exchange Online Help'
TOCTitle: ボイス メールの共通 PIN パターンを有効にする
ms:assetid: 9940a8c2-f576-4089-ab96-8b318ad3da0f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ673546(v=EXCHG.150)
ms:contentKeyID: 50555833
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ボイス メールの共通 PIN パターンを有効にする

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

Outlook Voice Access ユーザーの共通のユニファイド メッセージング (UM) PIN パターンを有効または無効にできます。UM メールボックス ポリシーで共通の PIN パターン設定を有効または無効にする場合、その設定は UM メールボックス ポリシーに関連付けられているUM が有効なユーザーすべてに適用されます。既定では、UM が有効なユーザーは PIN 作成時に共通パターンを使用できません。

UM メールボックス ポリシーには、いくつかの PIN に関連する設定を構成できます。<strong>PIN の共通のパターンを許可する</strong> の設定を使用して、ユーザーが PIN を作成する際に共通の数字パターンの使用を許可または禁止することができます。既定ではこの設定は無効になっており、ユーザーは次の数字のパターンの使用が禁止されます。

  - **連続した数字**   連続した数字だけで構成されている PIN の値です。連続した数字の PIN の例としては、1234 や 65432 があります。

  - **同じ数字の繰り返し**   同じ数字の繰り返しだけで構成されている PIN の値です。同じ数字の繰り返しの例としては、11111 や 22222 があります。

  - **メールボックスの内線番号のサフィックス**   ユーザーのメールボックスの内線番号のサフィックスを含んだ PIN の値です。たとえば、ユーザーのメールボックスの内線番号が 36697 の場合、ユーザーの PIN を 3669712 にすることはできません。


> [!NOTE]
> <STRONG>[PIN の共通のパターンを許可する]</STRONG> の設定が有効になっている場合は、メールボックスの内線番号のサフィックスだけが拒否されます。



Outlook Voice Access の PIN セキュリティに関連するその他のタスクについては、「[PIN セキュリティ手順](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/set-outlook-voice-access-pin-security/pin-security-procedures)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス ポリシー」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/set-up-voice-mail/create-um-mailbox-policy)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して共通の PIN パターンを有効にする

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。リスト ビューで、修正する UM ダイヤル プランを選択し、ツール バーで、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  <strong>UM ダイヤル プラン</strong> ページの <strong>UM メールボックス ポリシー</strong> で、管理する UM メールボックス ポリシーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>UM メールボックス ポリシー</strong> ページの <strong>PIN ポリシー</strong> で、<strong>PIN の共通のパターンを許可する</strong> の隣のチェック ボックスをオンにします。

4.  <strong>保存</strong> をクリックします。

## シェルを使用して共通の PIN パターンを有効にする

この例では、`MyUMMailboxPolicy` という名前の UM メールボックス ポリシーに関連付けられているユーザーが、共通パターンを含む PIN を使用できるようにします。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -AllowCommonPatterns $true

