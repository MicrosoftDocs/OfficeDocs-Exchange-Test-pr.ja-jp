---
title: 'Exchange 2013 での Exchange 2010 または 2007 エッジ トランスポート サーバーの使用'
TOCTitle: Exchange 2013 での Exchange 2010 または 2007 エッジ トランスポート サーバーの使用
ms:assetid: ce99b4bd-868c-4767-9009-e22c17ac0ac7
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ150569(v=EXCHG.150)
ms:contentKeyID: 48270060
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 での Exchange 2010 または 2007 エッジ トランスポート サーバーの使用

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

エッジ トランスポート サーバーは Microsoft Exchange Server 2013 Service Pack 1 (SP1) で使用できます。ただし、境界ネットワークに配備された既存の Exchange Server 2007 または Exchange Server 2010 エッジ トランスポート サーバーは引き続き使用できます。さらに、新規またはアップグレードされた Exchange 2013 組織の境界ネットワークに、新しい Exchange 2007 または Exchange 2010 エッジ トランスポート サーバーをインストールすることができます。

以下の事項を理解しておく必要があります。

  - Exchange 2007 または Exchange 2010 エッジ トランスポート サーバーは、ハブ トランスポート サーバーとの接続を使用することを前提としています。Exchange 2013 では、トランスポート サービスは、メールボックス サーバー上に存在します。そのため、メールボックス サーバー上のトランスポート サービスとエッジ トランスポート サーバーの間でインターネット メール フローが発生し、Exchange 2013 クライアント アクセス サーバーを効率的にバイパスします。

  - Exchange 2013 サーバーだけで構成されている Active Directory サイトに対して、Exchange 2007 または Exchange 2010 エッジ トランスポート サーバーをサブスクライブできます。スタンドアロンの Exchange 2013 メールボックス サーバー、またはメールボックス サーバーとクライアント アクセス サーバーが同一のコンピューターにインストールされているサーバーに、エッジ サブスクリプション ファイルをインポートし、EdgeSync を実行することができます。エッジ サブスクリプション ファイルのインポートや EdgeSync の実行は、スタンドアロンの Exchange 2013 クライアント アクセス サーバーで実行することはできません。

  - 新しい Exchange 2007 または Exchange 2010 エッジ トランスポート サーバーを Exchange 2013 組織に配備する手順は、基本的には、前バージョンの Exchange の場合と同じです。ただし、ハブ トランスポートで実行される手順はすべて、Exchange 2013 内のメールボックス サーバー上で実行されます。手順は次のとおりです。
    
      - [購読済みのエッジ トランスポート サーバーを介してインターネット メール フローを構成する](https://go.microsoft.com/fwlink/p/?linkid=275859)
    
      - [EdgeSync を使用しないエッジ トランスポート サーバーとハブ トランスポート サーバー間のメール フローを構成する](https://go.microsoft.com/fwlink/p/?linkid=276661)

