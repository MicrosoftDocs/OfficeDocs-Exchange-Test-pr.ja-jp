---
title: 'ボイス メールと不在着信通知のジャーナリングを有効または無効にする: Exchange 2013 Help'
TOCTitle: ボイス メールと不在着信通知のジャーナリングを有効または無効にする
ms:assetid: 5164a92e-69e6-4339-b80c-0cfbf0dc0198
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb201690(v=EXCHG.150)
ms:contentKeyID: 49896246
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ボイス メールと不在着信通知のジャーナリングを有効または無効にする

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-04-08_

Microsoft Exchange Server 2013 では、Exchange 組織内の受信者または送信者との間で送受信される電子メール メッセージをジャーナリングするためのジャーナル ルールを作成するとき、ユニファイド メッセージング サービスによって生成されるボイス メールおよび不在着信通知が含まれます。このトピックの手順を使用して、この機能を組織全体に対してオンまたはオフにします。

ジャーナリングに関連する他の管理タスクについては、「[ジャーナリングの管理](manage-journaling-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」トピックの「Journaling (ジャーナル)」エントリ。

  - この手順を実行するには、シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用してボイス メールおよび不在着信通知のジャーナリングを無効または有効にする

この例では、*VoicemailJournalingEnabled* パラメーターを `$false` に設定することによって、ボイス メールおよび不在着信通知のジャーナリングを無効にします。

    Set-TransportConfig -VoicemailJournalingEnabled $false

この例では、同じパラメーターを `$true` に設定することによって、ボイス メールおよび不在着信通知のジャーナリングを有効にします。

    Set-TransportConfig -VoicemailJournalingEnabled $true

構文とパラメーターの詳細については、「[Set-TransportConfig](https://technet.microsoft.com/ja-jp/library/bb124151\(v=exchg.150\))」を参照してください。

## 詳細情報

[ジャーナル](journaling-exchange-2013-help.md)

[ジャーナリングの管理](manage-journaling-exchange-2013-help.md)

