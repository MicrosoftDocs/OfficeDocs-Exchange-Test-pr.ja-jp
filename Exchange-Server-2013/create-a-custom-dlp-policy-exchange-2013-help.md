---
title: 'カスタム DLP ポリシーの作成: Exchange Online Help'
TOCTitle: カスタム DLP ポリシーの作成
ms:assetid: b3299a39-9663-41e4-b76e-9d2f7879d486
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ150550(v=EXCHG.150)
ms:contentKeyID: 48269084
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# カスタム DLP ポリシーの作成

 

_**適用先:** Exchange Online, Exchange Server 2013_

カスタム データ損失防止 (DLP) ポリシーを使用すると、既存の DLP テンプレートでは対応できない組織の特定のニーズを満たす条件、ルール、および操作を確立できます。

1 つのポリシーで使用可能なルール条件には、[Exchange での機密情報の種類の検索基準：](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md) によって提供される機密情報の種類に加えて、従来のすべてのトランスポート ルールが含まれます。トランスポート ルールについて詳しくは、「[メール フローやトランスポート ルール](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)」(Exchange 2013) または「[Exchange Online のメール フロー ルール (トランスポート ルール)](https://technet.microsoft.com/ja-jp/library/jj919238\(v=exchg.150\))」(Exchange Online) をご覧ください。


> [!NOTE]
> DLP ポリシーを運用環境で適用する前に、テスト モードで DLP ポリシーを有効にします。テスト中は、サンプルのユーザー メールボックスを構成し、テスト ポリシーを呼び出すテスト メッセージを送信することによって、結果を確認することをお勧めします。テストについて詳しくは、「<A href="test-a-mail-flow-rule-exchange-2013-help.md">メール フロー ルールのテスト</A>」をご覧ください。



カスタム DLP ポリシー作成に関連する追加の管理タスクについては、「[DLP の手順](dlp-procedures-exchange-2013-help.md)」(Exchange 2013) または「[DLP に関する手順](https://technet.microsoft.com/ja-jp/library/jj938003\(v=exchg.150\))」(Exchange Online) をご覧ください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 60 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「データ損失防止 (DLP)」。

  - 新しいカスタム DLP ポリシーを作成するには、Exchange 2013 のインストール手順に従う必要があります。展開の詳細については、「[計画と展開](planning-and-deployment-for-exchange-2013-installation-instructions.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!NOTE]
> お客様の環境とはさまざまな相違があるため、Microsoft カスタマー サポート サービス (CSS) は、カスタムの正規表現スクリプト (“RegEx スクリプト”) の開発またはテストには参加できません。カスタムの RegEX スクリプトの開発、テストとデバッグについては、Office 365 のお客様ご自身の組織内の IT リソースをご利用いただく必要があります。あるいは、Office 365 のお客様は、Microsoft Consulting Services (MCS) などの外部コンサルティング リソースの利用をお選びいただけます。スクリプトの開発リソースを問わず、CSS EXO および EOP のサポート エンジニアは、お客様からのカスタムの RegEx スクリプトについてのお問い合わせには対応していません。




> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## EAC を使用して既存ルールのないカスタム DLP ポリシーを作成する

1.  EAC 内で、**コンプライアンス管理** \> **データ損失防止** に移動します。構成した既存のポリシーが一覧に表示されます。

2.  **\[追加\]** ![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") アイコンの横にある矢印をクリックし、**\[カスタム ポリシーの新規作成\]** を選択します。
    

    > [!IMPORTANT]
    > 矢印でなく <STRONG>[追加]</STRONG><IMG title="[追加] アイコン" alt="[追加] アイコン" src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif"> アイコンをクリックすると、テンプレートに基づいて新しいポリシーを作成することになります。テンプレートの使用の詳細については、「<A href="how-to-new-dlp-data-loss-prevention-policy-template.md">テンプレートからの DLP ポリシーの作成</A>」を参照してください。



3.  **\[カスタム ポリシーの新規作成\]** ページで、以下のフィールドに入力します。
    
    1.  **\[名前\]**   このポリシーを他と区別する名前を追加します。
    
    2.  **\[説明\]**   このポリシーの概要説明を追加します。
    
    3.  **\[状態を選択\]**   このポリシーのモードまたは状態を選択します。新しいポリシーを完全に有効にするには、そのように指定する必要があります。ポリシーの既定のモードは、通知なしのテストです。

4.  **\[保存\]** をクリックして、新しいポリシーの参照情報の作成を完了します。ポリシーが構成済みのすべてのポリシーの一覧に追加されますが、この新しいカスタム ポリシーに関連付けられているルールまたは操作はまだありません。

5.  作成したポリシーをダブルクリックするか、選択して **\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

6.  **\[DLP ポリシーの編集\]** ページで、**\[ルール\]** をクリックします。
    
    **\[追加\]** ![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックして新しい空のルールを追加します。機密情報の種類に加えて従来のすべてのトランスポート ルールを使用して、条件を確立できます。
    
    混乱を避けるため、ポリシーまたはルールの部分ごとに、固有の文字列を使用できる場合は一意の名前を付けます。使用できるいくつかの追加オプションがあります。
    
    1.  **\[追加\]** ![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") アイコンの横にある矢印をクリックし、送信者通知に関するルールまたは優先を許可するルールを追加します。
    
    2.  ルールを削除するには、ルールを強調表示して、**\[削除\]**![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") をクリックします。
    
    3.  **\[その他のオプション\]** ![\[その他のオプション\] アイコン](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "[その他のオプション] アイコン") をクリックして、強制実行の時間制限またはこのポリシー内の他のルールへの影響を含む、このルールのその他の条件と操作を追加します。

7.  **\[保存\]** をクリックして、ポリシーの変更を終了し、変更を保存します。

DLP ポリシー テンプレートは、メッセージング環境用の堅牢なポリシーと法令遵守システムを設計および適用できる、Microsoft Exchange の機能の 1 つです。法令遵守機能の詳細については、「[メッセージングのポリシーと準拠](messaging-policy-and-compliance-exchange-2013-help.md)」(Exchange 2013) または「[Exchange Online のセキュリティとコンプライアンス](https://technet.microsoft.com/ja-jp/library/jj200706\(v=exchg.150\))」をご覧ください。

## 詳細情報

[データ損失防止](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[メール フローやトランスポート ルール](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)Exchange 2013

[Exchange Online のメール フロー ルール (トランスポート ルール)](https://technet.microsoft.com/ja-jp/library/jj919238\(v=exchg.150\))Exchange Online

[機密情報ルールとトランスポート ルールの統合](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

