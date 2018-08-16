---
title: '方法: 新しい DLP (データ損失防止) ポリシー テンプレート'
TOCTitle: テンプレートからの DLP ポリシーの作成
ms:assetid: 4432ef8b-6108-48d3-b2af-43ef5b40d2bc
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ150515(v=EXCHG.150)
ms:contentKeyID: 48269016
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# テンプレートからの DLP ポリシーの作成

 

_**適用先:** Exchange Online, Exchange Server 2013_

Microsoft Exchange Server 2013 では、組織のメッセージング ポリシーおよびコンプライアンス ニーズに対応するため、データ損失防止 (DLP) ポリシー テンプレートを使用することができます。これらのテンプレートは作成済みのルールのセットが含まれているため、いくつかの一般的な法的/規制要件に関連するメッセージ データの管理に役立てることができます。Microsoft が提供するすべてのテンプレートの一覧を確認するには、「[Exchange で提供される DLP ポリシー テンプレート](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md)」を参照してください。提供されている DLP テンプレートの例は、以下を管理するのに有用です。

  - グラム リーチ ブライリー法 (GLBA) データ

  - クレジット カード業界データ セキュリティ基準 (PCI DSS)

  - 米国の個人識別情報 (U.S. PII)

これらの DLP テンプレートは、カスタマイズすることも、そのまま使用することもできます。DLP ポリシー テンプレートは、新しい条件または述語、およびアクションを含めたトランスポート ルールの上に構築されます。DLP ポリシーは従来のトランスポート ルールの全範囲をサポートしています。DLP ポリシーを作成した後に、追加のルールを追加することができます。ポリシー テンプレートの詳細については、「[DLP ポリシー テンプレート](dlp-policy-templates-exchange-2013-help.md)」を参照してください。トランスポート ルール機能の詳細については、「[メール フローやトランスポート ルール](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013)」または「[Exchange Online のメール フロー ルール (トランスポート ルール)](https://technet.microsoft.com/ja-jp/library/jj919238\(v=exchg.150\)) (Exchange Online)」を参照してください。ポリシーの適用の開始後は、次のトピックを参照して結果を確認する方法を調べることができます。

Exchange 2013: [DLP ポリシー検出のレポートの表示](view-dlp-policy-detection-reports-exchange-2013-help.md)

Exchange Online: [DLP ポリシー検出のレポート](https://technet.microsoft.com/ja-jp/library/dn904484\(v=exchg.150\))


> [!NOTE]
> 運用環境で DLP ポリシーを実行する前に、テスト モードでこれらのポリシーを有効にする必要があります。テスト中は、サンプルのユーザー メールボックスを構成し、テスト ポリシーを呼び出すテスト メッセージを送信することによって、結果を確認することをお勧めします。



テンプレートからの DLP ポリシーの作成に関連する追加の管理タスクについては、「[DLP の手順](dlp-procedures-exchange-2013-help.md)Exchange Server 2013」または「[DLP に関する手順](https://technet.microsoft.com/ja-jp/library/jj938003\(v=exchg.150\))Exchange Online」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 30 分

  - 「[計画と展開](planning-and-deployment-for-exchange-2013-installation-instructions.md)」の説明に従って Exchange 2013 がセットアップされていることを確認します。

  - 組織内の管理者アカウントとユーザー アカウントの両方を構成し、基本的なメール フローを検証します。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「データ損失防止 (DLP)」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## EAC を使用してテンプレートから DLP ポリシーを構成する

1.  EAC で、<strong>コンプライアンス管理</strong> \> <strong>データ損失防止</strong> に移動して、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。
    

    > [!NOTE]
    > <STRONG>[追加]</STRONG><IMG title="[追加] アイコン" alt="[追加] アイコン" src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif"> アイコンの横にある矢印をクリックし、ドロップダウン メニューから <STRONG>[テンプレートから DLP ポリシーを新規作成する]</STRONG> を選択しても、このアクションを選択できます。



2.  <strong>テンプレートから新しい DLP ポリシーを作成する</strong> ページで、以下のフィールドに入力します。
    
    1.  <strong>名前</strong>   このポリシーを他と区別する名前を追加します。
    
    2.  <strong>説明</strong>   このポリシーの概要説明を追加します。
    
    3.  <strong>テンプレートの選択</strong>   新しいポリシーの作成を開始するために適切なテンプレートを選択します。
    
    4.  <strong>その他のオプション</strong>   モードまたは状態を選択します。新しいポリシーを完全に有効にするには、そのように指定する必要があります。ポリシーの既定のモードは、通知なしのテストです。
    
    5.  <strong>保存</strong> をクリックしてポリシーの作成を完了します。


> [!NOTE]
> 特定のテンプレート内のルールに加えて、組織固有の予想される事態や企業ポリシーがあり、メッセージング環境内の規制対象データに適用する場合があります。Exchange 2013 では、基本テンプレートを変更し、Exchange メッセージング環境がユーザー固有の要件に適合するようにアクションを簡単に追加できます。



ポリシーが Exchange 2013 環境内に保存されたら、ポリシー内のルールを編集して、ポリシーを変更することができます。ルールの変更としては、特定の人をポリシーの適用対象から除外したり、あるいはメッセージに機密コンテンツが含まれていることが検知されたら、通知を送信してメッセージ配信をブロックしたりすることなどが挙げられます。ポリシーおよびルールの編集の詳細については、「[DLP ポリシーの管理](manage-dlp-policies-exchange-2013-help.md)」を参照してください。

Exchange 2013 で既に作成しておいた DLP ポリシーを変更する場合は、<strong>DLP ポリシーの編集</strong> ページで特定のポリシーのルール セットに移動して、そのページで使用可能なツールを使用する必要があります。

一部のポリシーでは、メッセージ用の RMS を呼び出すルールを追加できます。これらの種類のルールを利用するには、Exchange Server 上で RMS を構成してから、アクションを追加する必要があります。

どの DLP ポリシーについても、ルール、アクション、適用除外、適用期間や、ポリシー内の他のルールを適用するかどうかを変更できます。また、DLP ポリシーごとにユーザー固有のカスタム条件を追加することもできます。

## 詳細情報

[データ損失防止](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[DLP ポリシー テンプレート](dlp-policy-templates-exchange-2013-help.md)

