---
title: 'Lync 会話と会議コンテンツを Exchange にアーカイブする: Exchange Online Help'
TOCTitle: Lync 会話と会議コンテンツを Exchange にアーカイブする
ms:assetid: 3cff970e-e5ed-4a54-88e6-3665d84b5ed7
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn508399(v=EXCHG.150)
ms:contentKeyID: 59678845
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Lync 会話と会議コンテンツを Exchange にアーカイブする

 

_**適用先:** Exchange Online, Exchange Server 2013_

IM 会話などの Lync Online コンテンツを、Exchange Online 内のユーザーのメールボックスにアーカイブできます。オンプレミスの展開では、Lync 2013 のコンテンツを Exchange 2013 のメールボックスにアーカイブできます。オンライン環境とオンプレミス環境の両方で、訴訟ホールドまたはインプレース ホールドをユーザーのメールボックスに配置することが必要です。ホールド状態のメールボックスを持つユーザーが Lync コンテンツを完全に削除する際、アーカイブされた Lync コンテンツは、ユーザーのメールボックス内の \[回復可能なアイテム\] フォルダーに保持されます。それはユーザーからは見えませんが、電子証拠開示検索に組み込まれます。

メールボックスを訴訟ホールドの対象にすると、Lync の項目を含む、すべてのコンテンツ タイプは保持されます。既定では、インプレース ホールドを作成するときにも、このことは当てはまります。ただし、Lync アイテムのみを保持するためにインプレース ホールドを使用する場合は、以下のスクリーンショットのように、**\[インプレース電子情報開示 & 保留リスト\]** ウィザードから **\[メッセージの種類の選択\]** オプションを使用し、**\[Lync アイテム\]** を選択します。

![Lync アイテムの保持](images/Dn508399.691d2324-9fac-4689-8527-c78d387e0e3e(EXCHG.150).jpg "Lync アイテムの保持")


> [!NOTE]
> Lync アイテムを除外するようにインプレース ホールドを構成することもできます。たとえば、多くの組織では、他の種類のコンテンツよりも、インスタント メッセージやボイス メール アイテムを短い期間保持することが好まれるでしょう。この種の保持ポリシーを実装するには、長期間 (たとえば、7 年間) コンテンツを保持し、Lync アイテムをこの保持から除外するようなインプレース ホールドを作成できます。そして、Lync アイテムのみを保持する、もっと保持期間が短い別のインプレース ホールドを作成できます。コンテンツを保持する期間も指定できます。特定の期間の保持を作成する方法の詳細については、<A href="in-place-hold-and-litigation-hold-exchange-2013-help.md">インプレース保持と訴訟ホールド</A> を参照してください。



ユーザーを保持に含めるための詳細な手順については、次のトピックを参照してください。

  - [インプレース保持を作成または削除する](create-or-remove-an-in-place-hold-exchange-2013-help.md)

  - [メールボックスを訴訟ホールドの対象にする](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)

アーカイブに関するその他の管理タスクについては、以下を参照してください。

  - [Exchange Online のアーカイブ メールボックスを有効または無効にする](https://technet.microsoft.com/ja-jp/library/jj984357\(v=exchg.150\))

  - [Exchange 2013 でインプレース アーカイブを管理する](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)

## 詳細情報

  - ユーザーが [Lync IM 会話を会話の履歴フォルダーに保存](https://go.microsoft.com/fwlink/p/?linkid=400589)するよう Lync クライアントを構成しているかどうかにかかわらず、サーバー上で Lync コンテンツがアーカイブされます。

  - Lync コンテンツのアーカイブは、ユーザーを訴訟ホールドまたはインプレース保持の対象にした後に始まります。ユーザーの Lync 通信がアカウントの作成時からアーカイブされるようにするには、アカウントを作成した直後にそのアカウントを保持の対象にします。

さらに、オンプレミスの Exchange 2013 および Lync 2013 展開では、以下の事項が該当します。

  - Lync 2013 と Exchange 2013 間に OAuth 認証を構成する必要があります。詳細については、「[SharePoint および Lync との統合](integration-with-sharepoint-and-lync-exchange-2013-help.md)」を参照してください。

  - ユーザーを保持の対象にするかどうかにかかわらず、Lync 2013 コンテンツを Exchange 2013 にアーカイブすることもできます。そのためには、ユーザーの Exchange アーカイブ ポリシーを構成します。Lync 2013 サーバーで `Set-CsUser` コマンドレットを使用して、Lync ユーザーの *ExchangeArchivingPolicy* プロパティを `ArchivingToExchange` に設定します。

  - オンプレミスの展開での Lync コンテンツのアーカイブの詳細については、Lync 2013 ドキュメントの「[Lync Server 2013 のアーカイブの計画](https://go.microsoft.com/fwlink/p/?linkid=400590)」を参照してください。

