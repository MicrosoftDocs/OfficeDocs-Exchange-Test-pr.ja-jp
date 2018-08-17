---
title: '保護された音声メッセージのマルチメディア再生を有効または無効にする: Exchange Online Help'
TOCTitle: 保護された音声メッセージのマルチメディア再生を有効または無効にする
ms:assetid: 3c33370c-4262-42b1-8d83-d61fc7c426cd
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee423543(v=EXCHG.150)
ms:contentKeyID: 52057406
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 保護された音声メッセージのマルチメディア再生を有効または無効にする

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

保護されたボイス メール メッセージを受信したユーザーに、電話での再生機能を使用してメッセージを聞かせることができます。または、クライアント ソフトウェアが Rights Management をサポートしない場合、ユーザーは Outlook Voice Access を使用してメッセージを聞く必要があります。

ユニファイド メッセージング (UM) が有効なユーザーが音声メッセージを聞く場合は、電話での再生機能を使用するか、コンピューターまたはモバイル デバイスのマルチメディア ソフトウェアを使用できます。マルチメディア再生では、UM が有効なユーザーは、メディア プレーヤーとコンピューターのスピーカーを使用するか、モバイル デバイスのメディア プレーヤーを使用して、音声メッセージを聞くことができます。


> [!NOTE]
> 保護されたボイス メールは、Rights Management をサポートしている Outlook バージョンを使用しているクライアントでのみ使用できます。クライアント ソフトウェアが Rights Management をサポートしない場合、ユーザーは Outlook Voice Access を使用して通話を聞く必要があります。



既定では、UM メールボックス ポリシーの **RequireProtectedPlayOnPhone** プロパティの値は、false に設定されています。つまり、UM が有効なユーザーが UM メールボックス ポリシーと関連付けられている場合は、保護された音声メッセージを以下の方法で聞くことができます。

  - Outlook Voice Access を使用する。

  - 組み込みのメディア プレーヤー、または Outlook 2010 以降のバージョンの \[電話での再生\] ボタンを使用する。

  - 組み込みのメディア プレーヤー、または Outlook Web App の \[電話での再生\] ボタンを使用する。

この値が true に設定されている場合、保護されているボイス メールのマルチメディア再生は許可されません。この値が true に設定された UM メールボックス ポリシーと関連付けられている UM が有効なユーザーは、保護されたボイス メール メッセージを以下の方法でのみ聞くことができます。

  - Outlook Voice Access を使用する。

  - Outlook 2010 以降のバージョンの \[電話での再生\] ボタンを使用する。

  - Outlook Web App の \[電話での再生\] ボタンを使用する。

この設定は、UM が有効であるユーザーが公共のコンピューター、公共の場所でのラップトップ、またはモバイル デバイスのメディア プレーヤーを使用して、非公開の情報が含まれる保護されたボイス メールを再生する場合に特に便利です。

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

## EAC を使用して保護された音声メッセージのマルチメディア再生を有効または無効にする

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  <strong>UM メールボックス ポリシー</strong>で、管理する UM メールボックス ポリシーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>UM メールボックス ポリシー</strong> ページの <strong>保護されたボイス メール</strong> で、<strong>保護された音声メッセージの電話での再生を要求する</strong> の横にあるチェック ボックスをオンにして、この設定を有効にします。この設定を無効にするには、チェック ボックスをオフにします。

4.  <strong>保存</strong> をクリックします。

## シェルを使用して、保護されている音声メッセージのマルチメディア再生を有効または無効にする

この例では、`MyUMMailboxPolicy` という名前の UM メールボックス ポリシーと関連付けられたユーザーが、メディア プレーヤーを使用して保護された音声メッセージを再生できるようにします。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -RequireProtectedPlayOnPhone $false

この例では、`MyUMMailboxPolicy` という名前の UM メールボックス ポリシーと関連付けられたユーザーが、メディア プレーヤーを使用して保護された音声メッセージを再生できないようにします。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -RequireProtectedPlayOnPhone $true

