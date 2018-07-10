---
title: 'UM が有効になっていないユーザーからの呼び出しを有効にする: Exchange Online Help'
TOCTitle: UM が有効になっていないユーザーからの呼び出しを有効にする
ms:assetid: 3c39c6df-6d7a-469f-b92b-85b3f14bad31
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb267006(v=EXCHG.150)
ms:contentKeyID: 49896210
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM が有効になっていないユーザーからの呼び出しを有効にする

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) が有効になっていないユーザーからの呼び出しを有効または無効にすることができます。 既定では、認証されていない発信者からの着信呼び出しを、自動応答を通じて UM が有効なユーザーに転送することは許可されます。 このオプションが有効になっていると、組織外のユーザーは、UM が有効なユーザーに対する呼び出しを転送できるようになります。

UM が有効なユーザーに関するこの設定が無効になっている場合でも、ディレクトリ検索を使用して、そのユーザーのメールボックスを特定することができます。 ただし、そのユーザーに対して外部発信者が呼び出しの転送を試みると、"誠に申し訳ありませんが、おかけになった番号を直接呼び出すことができません。オペレーターに接続します。" という案内が流れます。 自動応答でオペレーターが構成されている場合は、発信者はオペレーターに接続されます。 自動応答でオペレーターが構成されておらず、ダイヤル プランのオペレーターが構成されている場合、ダイヤル プランのオペレーターに呼び出しが転送されます。 音声認識が有効な自動応答、デュアル トーン多重周波数 (DTMF) フォールバック自動応答、またはダイヤル プランのいずれにもオペレーターの内線番号が構成されていない場合は、"誠に申し訳ありませんが、 オペレーターとタッチトーン サービスが両方ともご利用になれません。" という案内が流れます。

ボイス メールが有効なユーザーに関連するその他の管理タスクについては、「[ユーザーのボイス メール設定の管理](manage-voice-mail-settings-for-a-user-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス」。

  - この手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[New-UMMailboxPolicy](https://technet.microsoft.com/ja-jp/library/aa998300\(v=exchg.150\))」を参照してください。

  - この手順を実行する前に、ユーザーのメールボックスの UM が有効になっていることを確認してください。詳細な手順については、「[ボイス メール用にユーザーを有効にする](enable-a-user-for-voice-mail-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## シェルを使用して UM が有効になっていないユーザーからの呼び出しを有効にする

この例では、UM が有効になっていない発信者からの音声通話を Tony Smith が受信できるように設定にします。

    Set UMMailbox -Identity tony@contoso.com -AllowUMCallsFromNonUsers SearchEnabled

