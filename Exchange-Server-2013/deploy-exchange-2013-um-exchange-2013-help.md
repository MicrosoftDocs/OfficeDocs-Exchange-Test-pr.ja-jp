﻿---
title: 'Exchange 2013 UM の展開: Exchange 2013 Help'
TOCTitle: Exchange 2013 UM の展開
ms:assetid: d147d4b1-32d7-476b-b76f-ee3c0b35ba49
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ673564(v=EXCHG.150)
ms:contentKeyID: 49896491
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 UM の展開

 

_**適用先:**Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:**2016-12-09_

ユニファイド メッセージング (UM) では、Exchange Server 展開を組織の既存のテレフォニー システムに統合する必要があります。展開を成功させるには、既存のテレフォニー インフラストラクチャを慎重に分析し、ユニファイド メッセージングのボイス メールを展開し、管理するための正しい計画手順を実行する必要があります。

**目次**

展開する前に

ユニファイド メッセージングを展開する

ユニファイド メッセージングの展開後の作業

## 展開する前に

ユニファイド メッセージングを展開する前に、以下のトピックの概念を理解しておくことを推奨します。

  - [UM ダイヤル プラン](um-dial-plans-exchange-2013-help.md)

  - [UM IP ゲートウェイ](um-ip-gateways-exchange-2013-help.md)

  - [UM サービス](um-services-exchange-2013-help.md)

  - [UM ハント グループ](um-hunt-groups-exchange-2013-help.md)

  - [着信呼び出しへの自動応答とルーティング](automatically-answer-and-route-incoming-calls-exchange-2013-help.md)

  - [UM メールボックス ポリシー](um-mailbox-policies-exchange-2013-help.md)

  - [ユーザーのボイス メール](voice-mail-for-users-exchange-2013-help.md)

## ユニファイド メッセージングを展開する

IP 構内交換機 (PBX)、VoIP ゲートウェイ、または Microsoft Lync Server を使用して UM を展開する場合のいずれにおいても、ユニファイド メッセージングのすべての展開オプションには、共通する複数の手順が含まれます。これらの手順は、多数のユニファイド メッセージング ユーザーをサポートする、拡張性と可用性が高いシステムを作成するのに必要となります。これらの手順は次のとおりです。

1.  ユニファイド メッセージングのテレフォニー コンポーネントを展開して構成します。

2.  Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスを実行するクライアント アクセス サーバー、および Microsoft Exchange ユニファイド メッセージング サービスを実行するメールボックス サーバーが正しくインストールされていることを確認します。

3.  必要となるユニファイド メッセージング コンポーネントを作成して構成します。

4.  ユニファイド メッセージングのすべての展開後タスクを実行します。

## テレフォニー コンポーネントを展開して構成する

Exchange 組織にユニファイド メッセージングを正しく展開するため、Exchange 管理者はデータ ネットワーキングの概念とテレフォニー用語と概念に精通し、UM で必要となるテレフォニー コンポーネントを正しく構成できる必要があります。新しい展開、または従来のボイス メール システムのアップグレードを行うには、テレフォニー ネットワークとユニファイド メッセージングについての多くの知識が必要です。

一般的に、UM に必要なテレフォニー コンポーネントを正しく構成するために実行すべきタスクには、次の 3 つがあります。

1.  **PBX 回線のプロビジョニング**   拡張性の高い UM ソリューションを展開するための最初の手順は、PBX 回線のプロビジョニングです。

2.  **チャネルの編成**   PBX ベースの音声チャネルをプロビジョニングした後、チャネルをハント グループとして編成できます。

3.  **VoIP ゲートウェイの展開**   音声チャネルをハント グループとして編成した後は、これらのチャネルを VoIP ゲートウェイで終端します。VoIP ゲートウェイと従来の PBX を使用して、テレフォニー ネットワークで使用されている回線交換プロトコルを、IP ベースのパケット交換プロトコルに変換します。

ユニファイド メッセージングを展開するときに、組織のテレフォニー ネットワークとデータ ネットワークを統合する場合は、テレフォニー ネットワーク コンポーネントとデータ ネットワーク コンポーネントを正しく構成する必要があります。ユニファイド メッセージングを正しく展開するには、以下のコンポーネントやインターフェイスも構成する必要があります。

  - **組織内の PBX から VoIP ゲートウェイへの接続を構成します。**   詳細については、「[VoIP ゲートウェイを PBX と通信するために接続する](connect-a-voip-gateway-to-communicate-with-a-pbx-exchange-2013-help.md)」を参照してください。

  - **VoIP ゲートウェイ インターフェイスから PBX への接続を構成します。**   サポートされている VoIP ゲートウェイと PBX インターフェィスを接続する方法については、お使いの PBX の製品ドキュメンテーション、または「[VoIP ゲートウェイを PBX と通信するために接続する](connect-a-voip-gateway-to-communicate-with-a-pbx-exchange-2013-help.md)」を参照してください。

  - **VoIP ゲートウェイ インターフェイスからクライアント アクセス サーバーおよびメールボックス サーバーへの接続を構成します。**   詳細については、「[VoIP ゲートウェイ、IP PBX、またはセッション ボーダー コント ローラーを UM に接続する](connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md)」を参照してください。

  - **クライアント アクセス サーバーおよびメールボックス サーバーから VoIP ゲートウェイ インターフェイスへの接続を構成します。**   詳細については、「[UM をサポートされる VoIP ゲートウェイに接続する](connect-um-to-a-supported-voip-gateway-exchange-2013-help.md)」を参照してください。

展開する前に

## メールボックス サーバーおよびクライアント アクセス サーバーをインストールする

Exchange ユニファイド メッセージングを展開する予定の組織は、さまざまな展開のパスを利用できます。どの方法でも同じ結果 (ユニファイド メッセージングの正常な展開) を達成できますが、顧客ごとにニーズや作業開始時の状態が異なるため、方法もそれぞれやや異なります。ただし、一般的には、サポートされているすべての展開シナリオ (新規インストールとアップグレード) で作業開始時の状態や展開方法は共通しています。次の手順に従って、クライアント アクセス サーバーおよびメールボックス サーバーを展開します。

1.  既存のインフラストラクチャが特定の前提条件を満たしていることを確認します。詳細については、「[Exchange 2013 の前提条件](exchange-2013-prerequisites-exchange-2013-help.md)」を参照してください。

2.  新しい Exchange 2013 組織を展開します。詳細については、「[セットアップ ウィザードを使用した Exchange 2013 のインストール](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)」を参照してください。
    

    > [!WARNING]
    > UM SIP と RTP トラフィックを Exchange 2013 クライアント アクセス サーバーに送信するように VoIP ゲートウェイまたは IP PBX を構成するには、その前に、組織内に 1 台以上の Exchange 2013 メールボックス サーバーを展開しておく必要があります。



3.  クライアント アクセス サーバーおよびメールボックス サーバーが正常にインストールされていることを確認します。サーバーをインストールした後で、インストールを確認し、サーバーのセットアップ ログを確認することをお勧めします。詳細については、「[Exchange 2013 のインストールの確認](verify-an-exchange-2013-installation-exchange-2013-help.md)」を参照してください。

## 必要な UM 言語パックを追加します

UM 言語パックを使用すると、発信者と Outlook Voice Access ユーザーは複数の言語でボイス メール システムを操作できます。また、追加の言語パックをメールボックス サーバーにインストールすると、発信者と Outlook Voice Access ユーザーはその言語で電子メール メッセージを聞いたり、ボイス メール システムを操作したりすることができます。

Exchange を初めてインストールした時点では、英語 (米国) が既定の言語であり、ダイヤル プランで使用できる唯一の言語オプションです。UM 言語パックをメールボックス サーバーにインストールすると、ダイヤル プランの既定の言語を構成するときに、言語パックに関連付けられた言語が使用可能なオプションとして一覧表示されます。既定では、UM 自動応答は UM ダイヤル プランに関連付けられるため、UM 自動応答を作成すると、UM 自動応答は関連付けられた UM ダイヤル プランの既定の言語設定を使用します。ただし、この設定は UM 自動応答が作成された後で変更できます。

UM 言語パックを「[Exchange Server 2013 UM Language Packs - 日本語](https://go.microsoft.com/fwlink/p/?linkid=266542)」からダウンロードした後で、Setup.exe コマンドを使用するか、*\<UMLanguagePack\>*.exe インストール プログラムを実行して、UM 言語パックを追加することができます。ただし、UM 言語パックを削除するには、Setup.exe コマンドを使用する必要があります。Exchange 管理シェル コマンドレットを実行して、メールボックス サーバーに言語パックを追加したり、削除したりすることはできません。UM 言語パックをインストールする方法の詳細については、「[UM 言語パックをインストールする](install-a-um-language-pack-exchange-2013-help.md)」を参照してください。


> [!NOTE]
> 既定では、メールボックス サーバーをインストールすると、U.S. 英語の言語 (en-US) がインストールされます。メールボックス サーバーをコンピューターから削除しないと、削除できません。



展開する前に

## UM コンポーネントを作成して構成する

ユニファイド メッセージングの展開と運用のためには、いくつかの UM コンポーネントが必要です。ユニファイド メッセージング コンポーネントにより、テレフォニー インフラストラクチャとユニファイド メッセージング環境が接続されます。クライアント アクセス サーバーおよびメールボックス サーバーを正常にインストールしたら、次の手順に従います。

## 手順 1:UM ダイヤル プランを作成して構成する

UM ダイヤル プランは、ユニファイド メッセージングの動作にとって重要であり、ユニファイド メッセージングをネットワークに正常に展開するために必要なものです。クライアント アクセス サーバーおよびメールボックス サーバーを正常にインストールした後、UM ダイヤル プランが最初に作成するコンポーネントになります。

既定では、UM ダイヤル プランと、そのダイヤル プランに関連付けられたクライアント アクセス サーバーおよびメールボックス サーバーは、暗号化を使用せずにデータを送受信します。セキュリティで保護されていないモードでは、VoIP および SIP トラフィックは暗号化されません。ダイヤル プランを作成するとき、または作成した後、相互トランスポート層セキュリティ (相互 TLS) を使用して、VoIP および SIP トラフィックを暗号化するようにダイヤル プランを構成できます。相互 TLS を使用するには、ダイヤル プランをセキュリティで保護された SIP モードまたはセキュリティで保護されたモードに設定します。また、UM 開始モードを TLS またはデュアルに設定し、Exchange サーバーおよび VoIP ゲートウェイ、IP PBX またはセッション ボーダー コントローラー (SBC) の信頼されている証明書を作成して配布します。VoIP セキュリティ設定を構成した後、クライアント アクセス サーバーおよびメールボックス サーバーの起動モードを構成する必要があります。詳細については、「[メールボックス サーバーのスタートアップ モードを構成する](configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md)」または「[クライアント アクセス サーバーのスタートアップ モードを構成する](configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md)」を参照してください。

以下の手順を実行して、新しい UM ダイヤル プランを作成します。

## UM ダイヤル プランを作成する

1.  Exchange 管理センター (EAC) で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** の順に移動し、**\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  **\[UM ダイヤル プランの新規作成\]** ページで、次のボックスに入力します。
    
      - **\[名前\]**   ダイヤル プランの名前を入力します。一意な UM ダイヤル プラン名を必ず指定する必要があります。入力した名前は EMC とシェルでの表示目的のみに使用されます。UM ダイヤル プラン名の長さは 64 文字以下で、スペースを含めることができます。ただし、次の文字を含めることはできません。" / \\ \[ \] : ; | = , + \* ? \< \>.
        

        > [!IMPORTANT]
        > ダイヤル プラン名のボックスには 64 文字まで入力できますが、49 文字を超えるダイヤル プラン名は設定できません。これは、ダイヤル プランを作成するときに、"<EM>&lt;ダイヤル プラン名&gt;</EM> の既定のポリシー" という名前で既定の UM メールボックス ポリシーも作成されるからです。UM ダイヤル プランと UM メールボックス ポリシー両方の <EM>name</EM> パラメーターは、いずれも最大 64 文字に設定できます。

    
      - **\[内線番号の長さ (桁数)\]**   ダイヤル プランにおける内線番号の桁数を入力します。内線番号の桁数は、PBX で作成されるテレフォニー ダイヤル プランに基づいています。たとえば、テレフォニー ダイヤル プランに関連付けられているユーザーが、同じテレフォニー ダイヤル プランを使用している別のユーザーに電話をかけるときに 4 桁の内線番号をダイヤルしている場合は、内線番号の桁数として 4 を選択します。
        
        これは 1 ～ 20 の値を持つ必須ボックスです。一般的な内線番号の長さは、3 ～ 7 個の数字です。既存のテレフォニー環境で内線番号が使用されている場合は、それらの内線番号と同じ桁数を指定する必要があります。
        
        内線電話番号ダイヤル プランにユーザーがリンクされている場合は、内線電話番号ダイヤル プランを作成する際に、ユーザーの内線番号を入力する必要があります。UM が有効なユーザーが SIP URI ダイヤル プランまたは E.164 ダイヤル プランにリンクされている場合は、セッション開始プロトコル (SIP) ダイヤル プランまたは E.164 ダイヤル プランにおいても内線番号が必要になります。この内線番号は、Outlook Voice Access ユーザーが Exchange メールボックスにアクセスするときに使用します。
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(UI\_URI 型)
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(UI\_VoIP セキュリティ)
    
      - **\[国/地域コード\]**   発信呼び出しに使用される国/地域コードを入力するには、このボックスを使用します。この番号は、ダイヤルされた電話番号に自動的に付加されます。このボックスには、1 ～ 4 桁の数値を入力できます。たとえば、米国内の国/地域コードは 1、英国内の国/地域コードは 44 です。

3.  **\[保存\]** をクリックします。
    

    > [!IMPORTANT]
    > Exchange の以前のバージョンでは、ユニファイド メッセージング サーバーを UM ダイヤル プランに追加する必要がありました。Exchange 2013 では、クライアント アクセス サーバーおよびメールボックス サーバーを内線電話番号ダイヤル プランまたは E.164 ダイヤル プランに関連付けることができません。クライアント アクセス サーバーおよびメールボックス サーバーは、すべての種類のダイヤル プランにおけるすべての着信呼び出しに応答します。ただし、UM を Microsoft Lync Server に統合する場合は、Lync Server との正しい動作のために、すべてのクライアント アクセス サーバーおよびメールボックス サーバーをすべての SIP URI ダイヤル プランに追加して、呼び出しのルーティングを有効にする必要があります。



展開する前に

## 手順 2:UM IP ゲートウェイを作成および構成する

UM IP ゲートウェイとは、VoIP ゲートウェイ ハードウェア デバイスまたは IP PBX のことを指します。UM IP ゲートウェイと UM ハント グループの組み合わせにより、VoIP ゲートウェイまたは IP PBX と UM ダイヤル プランの間のリンクが確立されます。

ダイヤル プランで VoIP セキュリティを作成するか有効にすると、以下の手順のいずれかで作成する UM IP ゲートウェイは、VoIP セキュリティを使用する UM ダイヤル プランと関連付けられます。この場合、UM IP ゲートウェイを作成するのに、IP アドレスではなく完全修飾ドメイン名を使用する必要があります。TCP ポート 5061 をリッスンするように UM IP ゲートウェイを構成する必要もあります。TCP ポート 5061 をリッスンするように UM IP ゲートウェイを構成するには、以下のコマンド `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`。VoIP ゲートウェイまたは IP PBX もポート 5061 で 相互 TLS の要求待ちをするように構成されていることを確認します。

以下の手順を実行して、新しい UM IP ゲートウェイを作成します。

## UM IP ゲートウェイを作成する

1.  
    
    EAC で、**\[ユニファイド メッセージング\]** \> **\[UM IP ゲートウェイ\]** の順に選択し、**\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  **\[UM IP ゲートウェイの新規作成\]** ページで、以下の情報を入力します。
    
      - **\[名前\]**   このボックスを使用して、UM IP ゲートウェイの一意の名前を指定します。これは、EAC に表示される表示名です。UM IP ゲートウェイの作成後に表示名を変更する必要がある場合、最初に既存の UM IP ゲートウェイを削除し、次に適切な名前を持つ別の UM IP ゲートウェイを作成します。UM IP ゲートウェイ名は必須ですが、表示にのみ使用されます。組織では複数の UM IP ゲートウェイを使用することがあるため、UM IP ゲートウェイにはわかりやすい名前を使用することをお勧めします。UM IP ゲートウェイ名は最大 64 文字です。スペースも使用できます。ただし、次の文字を含めることはできません。" / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **\[アドレス\]**   IP アドレスまたは完全修飾ドメイン名 (FQDN) を使用して UM IP ゲートウェイを構成できます。このボックスを使用すると、VoIP ゲートウェイ、SIP 有効 PBX、IP PBX、SBC、または FQDN に対して構成された IP アドレスを指定できます。このボックスには、有効で正しい形式の FQDN のみ指定できます。
        
        このボックスにはアルファベットと数字を入力できます。IPv4 アドレス、IPv6 アドレス、および FQDN がサポートされています。UM IP ゲートウェイと、セキュリティで保護された SIP モードまたはセキュリティ保護されたモードで運用されているダイヤル プランの間で相互 TLS を使用するには、FQDN を使用して UM IP ゲートウェイを構成する必要があります。また、ポート 5061 で接続要求を待つように構成し、VoIP ゲートウェイまたは IP PBX もすべてポート 5061 で相互 TLS の接続要求を待つように構成されていることを確認する必要があります。UM IP ゲートウェイを構成するには、次のコマンドを実行します。`Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.
        
        FQDN を使用する場合、IP アドレスについてホスト名を正しく解決できるように、VoIP ゲートウェイに対して DNS ホスト レコードを正しく構成したことも確認する必要があります。また、IP アドレスの代わりに FQDN を使用していて、かつ UM IP ゲートウェイの DNS 構成が変更される場合、UM IP ゲートウェイをいったん無効化してから有効化し、UM IP ゲートウェイの構成情報が正しく更新されていることを確認する必要があります。
    
      - **\[UM ダイヤル プラン\]**   **\[参照\]** をクリックして、UM IP ゲートウェイに関連付ける UM ダイヤル プランを選択します。UM IP ゲートウェイに関連付ける UM ダイヤル プランを選択すると、既定の UM ハント グループも作成され、選択した UM ダイヤル プランに関連付けられます。UM ダイヤル プランを選択しない場合、UM ハント グループを手動で作成し、作成した UM IP ゲートウェイとその UM ハント グループを関連付ける必要があります。

3.  
    
    **\[保存\]** をクリックします。

## 手順 3:UM ハント グループを作成して構成する (オプション)

*ハント グループ*は、ユーザーによって共有される PBX や IP PBX リソースのグループ、または内線番号のグループを表すために使用される用語です。ハント グループは、特定のビジネス単位で発着信される呼び出しを効率的に配信するために使用されます。

UM IP ゲートウェイを作成して、その UM IP ゲートウェイを UM ダイヤル プランと関連付けると、既定の UM ハント グループが作成されます。これまでに作成した UM IP ゲートウェイの個数に応じて、別の UM ハント グループを同じ、または別の UM IP ゲートウェイに関連付けることができます。

UM ハント グループを作成すると、UM ダイヤル プラン内で指定されているすべてのメールボックス サーバーが、VoIP ゲートウェイと通信できるようになります。詳細については、「[UM ハント グループ](um-hunt-groups-exchange-2013-help.md)」を参照してください。

## UM ハント グループを作成する

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページの **\[UM ハント グループ\]** にある **\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

3.  **\[UM ハント グループの新規作成\]** ページで、次のボックスを入力します。
    
      - **\[関連付けられた UM IP ゲートウェイ\]**   この表示専用ボックスには、UM ハント グループに関連付けられる UM IP ゲートウェイの名前が表示されます。
    
      - **\[名前\]**   UM ハント グループの表示名を作成するには、このボックスを使用します。UM ハント グループ名は必須で、一意である必要があります。ただし、この名前は、EAC とシェルでの表示のためにのみ使用されます。ハント グループを作成した後にその表示名を変更する必要が生じた場合は、まず既存のハント グループを削除し、その後で適切な名前を持つ別のハント グループを作成する必要があります。
        
        組織で複数のハント グループを使用する場合は、ハント グループに対してわかりやすい名前を使用することをお勧めします。UM ハント グループ名の長さの上限は 64 文字で、スペースも使用できます。ただし、次の文字を含めることはできません。" / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **\[ダイヤル プラン\]**   UM ハント グループに関連付けるダイヤル プランを選択するには、**\[参照\]** をクリックします。ハント グループとダイヤル プランの関連付けは必須です。UM ハント グループは、1 つの UM IP ゲートウェイと 1 つの UM ダイヤル プランにのみ関連付けることができます。
    
      - **\[パイロット ID\]**   PBX または IP/PBX で構成されているパイロット識別子 (またはパイロット ID) を一意に識別する文字列を指定するには、このボックスを使用します。
        
        このボックスでは、内線番号または SIP (セッション開始プロトコル) URI (Uniform Resource Identifier) を使用できます。このボックスは英数字の入力に対応しています。従来の PBX では数字のパイロット ID が使用されますが、IP PBX では SIP URI が使用される場合もあります。

4.  **\[保存\]** をクリックします。

展開する前に

## 手順 4:UM メールボックス ポリシーを作成して構成する

UM メールボックス ポリシーは、ユーザーに対してユニファイド メッセージングを有効にするときに必要です。UM が有効な各ユーザーのメールボックスは、単一の UM メールボックス ポリシーにリンクされている必要があります。UM メールボックス ポリシーを作成した後で、UM が有効な 1 つ以上のメールボックスをその UM メールボックス ポリシーにリンクします。これにより、その UM メールボックス ポリシーに関連付けられた UM が有効なユーザーに対して、PIN の最低桁数やサインインの最大試行回数などの PIN セキュリティ設定を制御できます。

UM ダイヤル プランを作成するたびに、UM メールボックス ポリシーも作成されます。UM メールボックス ポリシーには、"\<*ダイヤル プラン名*\> の既定のポリシー" という名前が付けられます。ただし、新しい UM メールボックス ポリシーを作成する必要がある場合、以下の手順を実行します。

## UM メールボックス ポリシーの作成

1.  
    
    EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで変更したい UM ダイアル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン").

2.  **\[UM ダイヤル プラン\]** ページの **\[UM メールボックス ポリシー\]** にある **\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

3.  **\[UM メールボックス ポリシーの新規作成\]** ページで、**\[名前\]** テキスト ボックスに新しい UM メールボックス ポリシーの名前を入力します。
    
    このボックスを使用して、UM メールボックス ポリシーに一意の名前を指定します。これは、EAC に表示される表示名です。UM メールボックス ポリシーを作成した後にその表示名を変更する必要が生じた場合は、まず既存の UM メールボックス ポリシーを削除し、その後で適切な名前を持つ別の UM メールボックス ポリシーを作成する必要があります。UM が有効なユーザーが UM メールボックス ポリシーに関連付けられている場合は、UM メールボックス ポリシーを削除できません。
    
    UM メールボックス ポリシー名は必須ですが、この名前が使用されるのは表示のためだけです。組織で複数の UM メールボックス ポリシーを使用する場合もあるため、わかりやすい名前を使用することをお勧めします。UM メールボックス ポリシー名の長さの上限は 64 文字で、スペースも使用できます。ただし、次の文字を含めることはできません。" / \\ \[ \] : ; | = , + \* ? \< \>.

4.  **\[保存\]**をクリックして、新しい UM メールボックス ポリシーを保存します。UM メールボックス ポリシーを保存すると、PIN ポリシー、ボイス メール機能、および保護ボイス メールの設定を含むすべての既定の設定が有効になります。既定の設定をカスタマイズまたは変更する場合は、**Set-UMMailbox** コマンドレットを使用して、作成したばかりの UM メールボックス ポリシーの設定を変更します。

## 手順 5:UM 自動応答を作成して構成する (オプション)

ユニファイド メッセージングを使用すると、組織のニーズに応じて、1 つ以上の UM 自動応答を作成することができます。UM 自動応答を作成するとき、組織の音声メニュー システムを作成します。組織の内外から電話をかけてきた発信者は、メニュー システムを使用することで組織内のユーザーや部署を見つけて、通話したり呼び出しを転送できます。

発信者は、デュアル トーン多重周波数 (DTMF) 入力 (タッチトーン入力) または音声入力を使用して、メニュー システム内を移動できます。自動音声認識 (ASR) を使用して、ユーザーが音声入力できるようにするには、UM 自動応答を音声対応にする必要があります。

ユニファイド メッセージングでの自動応答の作成と使用はオプションです。ただし、新しい UM 自動応答を作成する必要がある場合、以下の手順を実行します。

## UM 自動応答を作成する

1.  
    
    EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** の順に選択し、自動応答を追加する UM ダイヤル プランを選択して **\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページの **\[UM 自動応答\]** の下にある **\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

3.  **\[UM 自動応答の新規作成\]** ページで、以下のボックスに入力します。
    
      - **\[名前\]**   このボックスを使用して、UM 自動応答の表示名を作成します。一意な UM 自動応答名を必ず指定する必要があります。ただし、EAC およびシェルでは表示専用として使用されます。
        
        自動応答を作成した後にその表示名を変更する必要がある場合は、最初に既存の UM 自動応答を削除してから、適切な名前を持つ別の自動応答を作成する必要があります。組織で複数の UM 自動応答を使用している場合は、UM 自動応答にわかりやすい名前を使用することをお勧めします。UM 自動応答名は最大で 64 文字で、空白を含めることができます。
        
        新しい UM 自動応答には空白を含んだ名前を付けることができますが、ユニファイド メッセージングを Office Communications Server 2007 R2 または Microsoft Lync Server と統合する場合は、自動応答の名前に空白を含めることはできません。したがって、表示名に空白を含む自動応答を作成し、その後 Office Communications Server 2007 R2 または Lync Server と統合する場合は、まずその自動応答を削除してから、表示名に空白を含まない別の自動応答を作成する必要があります。
    
      - **\[この自動応答を作成して有効にする\]**   このチェック ボックスをオンにすると、UM 自動応答の作成を完了した時点で、自動応答が着信呼び出しに応答するようになります。既定では、新しい自動応答は無効な状態で作成されます。
        
        UM 自動応答を無効な状態で作成する場合は、自動応答の作成を完了した後に EAC またはシェルを使用して、自動応答を有効にすることができます。
    
      - **\[音声コマンドに応答する自動応答を設定する\]**   このチェック ボックスをオンにすると、UM 自動応答の音声認識が有効になります。自動応答の音声認識が有効な場合、電話をかけてきた人は、音声入力またはタッチトーン入力を使用して、UM 自動応答のシステムまたはカスタム プロンプトに応答できます。既定では、作成直後の自動応答は音声認識に対応しません。
        
        発信者に対して、U.S. 英語 (en-US) 以外の言語での音声認識が有効な自動応答を使用するためには、適切な UM 言語パックをインストールし、自動応答でこの言語を使用するようにプロパティを構成する必要があります。メールボックス サーバーをインストールすると、en-US UM 言語パックは既定でインストールされます。
    
      - **\[アクセス番号\]**   このボックスを使用して、発信者が自動応答を呼び出すために使用する内線番号または電話番号を入力します。このボックスに内線番号または電話番号を入力し、**\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックしてその番号を一覧に追加します。入力した内線番号または電話番号の桁数と、関連付けられている UM ダイヤル プランで構成されている内線番号の桁数とが一致する必要はありません。これは、UM 自動応答では直通電話が許可されるためです。
        
        入力できる内線番号またはパイロット ID の数に制限はありません。ただし、内線番号または電話番号を指定せずに新しい自動応答を作成することもできます。内線番号または電話番号は必須ではありません。
        
        既存の内線番号またはパイロット ID を編集または削除できます。既存の内線番号または電話番号を編集するには、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。既存の内線番号または電話番号を一覧から削除するには、**\[削除\]**![\[削除\] アイコン](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[削除] アイコン") をクリックします。

4.  **\[保存\]** をクリックします。

展開する前に

## ユニファイド メッセージングの展開後の作業

クライアント アクセス サーバーおよびメールボックス サーバーの新しいインストールを終え、ユニファイド メッセージングを正しく展開した後には、展開後タスクを完了する必要があります。展開後タスクを実行することで、ユニファイド メッセージングのユーザーを有効にし、UM 展開をセキュリティ保護し、UM が有効なユーザーの受信 FAX を展開できます。

## ユーザーのボイス メールを有効にする

VoIP ゲートウェイまたは IP PBX を展開し、クライアント アクセス サーバーおよびメールボックス サーバーをインストールし、ユニファイド メッセージングに必要なコンポーネントを作成した後、ユーザーがユニファイド メッセージングを利用できるようにする必要があります。詳細については、「[ボイス メール用にユーザーを有効にする](enable-a-user-for-voice-mail-exchange-2013-help.md)」を参照してください。

## ボイス メールを保護する

ユニファイド メッセージングは、Active Directory Rights Management サービス (AD RMS) を使用して組織の音声メッセージを保護するよう構成できます。この機能は保護されたボイス メールとして知られています。音声メッセージが保護されていると、受信者がそのメッセージを転送できないだけでなく、メッセージの内容にアクセスできるのは UM でメッセージの宛先になっている 1 人または複数の受信者のみになります。保護された音声メッセージにアクセスするには、Microsoft Outlook 2010 またはそれ以降のバージョンや、Outlook Web App、Outlook Voice Access を使用します。詳細については、「[ボイス メールを保護する](protect-voice-mail-exchange-2013-help.md)」を参照してください。

## UM の相互 TLS

相互 TLS を使用して、クライアント アクセス サーバーおよびメールボックス サーバーが送受信する SIP およびリアルタイム トランスポート プロトコル (RTP) トラフィックを暗号化するには、以下のタスクを実行します。

  - Exchange 証明書ウィザードを実行します。詳細については、「[UM の証明書の展開](deploying-certificates-for-um-exchange-2013-help.md)」を参照してください。

  - 証明書をクライアント アクセス サーバーおよびメールボックス サーバーにインポートします。

  - 組織内の VoIP ゲートウェイ、IP PBX、およびクライアント アクセス サーバー/メールボックス サーバーに、必要な証明書をインポートします。

  - UM ダイヤル プランで VoIP セキュリティを構成します。詳細については、「[VoIP セキュリティ設定の構成](configure-the-voip-security-setting-exchange-2013-help.md)」を参照してください。

  - クライアント アクセス サーバーおよびメールボックス サーバー上での起動モードを構成します。詳細については、「[メールボックス サーバーのスタートアップ モードを構成する](configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md)」および「[クライアント アクセス サーバーのスタートアップ モードを構成する](configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md)」を参照してください。

  - ポート 5061 をリッスンするように UM IP ゲートウェイを構成します。詳細については、「[リスニング ポートの構成](configure-the-listening-port-exchange-2013-help.md)」を参照してください。

## UM が有効なユーザーの PIN ポリシー

ユニファイド メッセージングでは、PIN ポリシーは UM メールボックス ポリシーで定義および構成されます。ユーザーのユニファイド メッセージングを有効にするときに、そのユーザーを既存の UM メールボックス ポリシーに関連付けます。UM メールボックス ポリシーで構成されている UM PIN ポリシーは、組織のセキュリティ要件に基づくものにする必要があります。UM が有効なユーザーの PIN 設定を構成する方法の詳細については、「[Outlook Voice Access PIN セキュリティの設定](set-outlook-voice-access-pin-security-exchange-2013-help.md)」を参照してください。

## クライアント ボイス メール機能をセットアップする

サーバーおよび必要な UM コンポーネントを展開した後、オプションでいくつかのボイス メール関連機能を構成できます。詳細については、以下のトピックを参照してください。

  - [Outlook Voice Access の設定](setting-up-outlook-voice-access-exchange-2013-help.md)

  - [ボイス メール ユーザーの呼び出し転送を許可する](allow-voice-mail-users-to-forward-calls-exchange-2013-help.md)

  - [ユーザーがボイス メールのトランスクリプトを表示できるようにする](allow-users-to-see-a-voice-mail-transcript-exchange-2013-help.md)

  - [ボイス メール ユーザーが FAX を受信できるようにする](enable-voice-mail-users-to-receive-faxes-exchange-2013-help.md)


> [!IMPORTANT]
> ユニファイド メッセージング環境を Microsoft Lync Server と統合する場合は、他にも計画の際に考慮するべきことがあります。詳細については、「<A href="deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md">Exchange 2013 UM および Lync Server の展開の概要</A>」を参照してください。



展開する前に
