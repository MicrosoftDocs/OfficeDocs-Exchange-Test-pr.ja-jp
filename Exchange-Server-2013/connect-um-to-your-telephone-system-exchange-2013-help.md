---
title: 'UM を電話システムに接続する: Exchange 2013 Help'
TOCTitle: UM を電話システムに接続する
ms:assetid: 92c3e029-f732-4d6d-b147-2b3006d5f088
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ673544(v=EXCHG.150)
ms:contentKeyID: 50555818
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM を電話システムに接続する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2012-11-30_

ユニファイド メッセージング (UM) は、音声メッセージングと電子メール メッセージングをさまざまなデバイスからアクセスできる 1 つのメールボックスに結合します。ユーザーは、それらのボイス メール メッセージを電子メールの受信トレイで確認することも、Outlook Voice Access を使用して電話で確認することもできます。

Microsoft Exchange 組織に UM を展開する場合は、単一または複数の Voice over IP (VoIP) ゲートウェイを設置、展開、および構成してテレフォニー ネットワークの構内交換機 (PBX) に接続するか、またはセッション開始プロトコル (SIP) 対応 PBX または IP PBX を設置、展開、および構成する必要があります。現在のボイス メール システムをアップグレードする場合は、テレフォニー ネットワークに接続するデバイスを展開し、Exchange クライアント アクセス サーバーおよびメールボックス サーバーを設置し、必要な UM コンポーネントを作成する必要があります。これらのコンポーネントにより、テレフォニー ネットワークをデータ ネットワークに接続できます。これにより、テレフォニー ネットワークからの着信呼び出しは VoIP ゲートウェイ、IP PBX、または SIP 対応 PBX に接続でき、これらのデバイスは Exchange 組織に接続できます。

Microsoft Office Communications Server 2007 R2 または Microsoft Lync Server のいずれかをインストール、展開、および構成する場合は、Exchange ユニファイド メッセージングに直接接続するために VoIP ゲートウェイ、IP PBX、または SIP 対応 PBX を使用しません。代わりに Lync 仲介サーバーと VoIP ゲートウェイ、または仲介サーバーと VoIP ゲートウェイの機能を備えた高度な VoIP ゲートウェイを使用することにより、Exchange UM に接続できます。エンタープライズ VoIP が有効な UM ユーザーは、音声メッセージの取得、再生、応答や、発信呼び出しを行えます。これらのユーザーは、Office Communicator または Lync クライアントを使用することにより、プレゼンスやインスタント メッセージング (IM) などの他の Lync 関連機能にもアクセスできます。

次の情報は、UM を設定および展開し、組織内のユーザーのボイス メール機能を有効にする場合に役立ちます。

  - [VoIP ゲートウェイ、IP PBX、またはセッション ボーダー コント ローラーを UM に接続する](connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md)   VoIP ゲートウェイまたは IP PBX を UM に接続する方法について説明します。

  - [Exchange 2013 のテレフォニー アドバイザー](telephony-advisor-for-exchange-2013-exchange-2013-help.md)   サポートされる VoIP ゲートウェイ、IP PBX、および PBX について説明します。

  - [サポートされる VoIP ゲートウェイ、IP Pbx、および PBX の構成に関する注意事項](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)   VoIP ゲートウェイ、IP PBX、および PBX を設定する方法について説明します。

