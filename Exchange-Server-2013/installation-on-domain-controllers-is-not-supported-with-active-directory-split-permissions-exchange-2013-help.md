---
title: 'Active Directory 分割アクセス許可を使用する場合、ドメイン コントローラーへのインストールはサポートされていない'
TOCTitle: Active Directory 分割アクセス許可を使用する場合、ドメイン コントローラーへのインストールはサポートされていない
ms:assetid: 977e3758-5e09-40a2-80c1-fe344b1d8a2a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.installondcinadsplitpermissionmode(v=EXCHG.150)
ms:contentKeyID: 48269836
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Active Directory 分割アクセス許可を使用する場合、ドメイン コントローラーへのインストールはサポートされていない

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2012-11-12_

Microsoft Exchange Server 2013 セットアップ プログラムが、Active Directory ドメイン コントローラー上でセットアップ プログラムの実行が試みられていることと、次のいずれかが該当することを検出しました。

  - Exchange 組織が、既に Active Directory 分割アクセス許可に対応するように構成されている。

  - Exchange 2013 セットアップ プログラムで、Active Directory 分割アクセス許可オプションが選択されている。

Exchange 組織がActive Directory 分割アクセス許可に対応するように構成されている場合、ドメイン コントローラーへの Exchange 2013 のインストールはサポートされません。

Exchange 2013 をドメイン コントローラーにインストールする場合は、役割ベースのアクセス制御 (RBAC) 分割アクセス許可または共有アクセス許可に対応するように Exchange 組織を構成する必要があります。


> [!IMPORTANT]
> Active Directory ドメイン コントローラーへの Exchange 2013 のインストールはお勧めしません。詳細については、「<A href="installing-exchange-on-a-domain-controller-is-not-recommended-exchange-2013-help.md">ドメイン コントローラーへの Exchange のインストールは推奨されない</A>」を参照してください。



Active Directory 分割アクセス許可を引き続き使用する場合、Exchange 2013 は、必ず、メンバー サーバーにインストールしてください。

Exchange 2013 での分割アクセス許可および共有アクセス許可の詳細については、以下のトピックを参照してください。

[分割型アクセス許可について](understanding-split-permissions-exchange-2013-help.md)

[Exchange 2013 の分割型アクセス許可を構成する](configure-exchange-2013-for-split-permissions-exchange-2013-help.md)

[Exchange 2013 の共有アクセス許可を構成する](configure-exchange-2013-for-shared-permissions-exchange-2013-help.md)

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

探しているものは見つかりましたか？検索したい情報に関する[フィードバックを送信](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback)してください。

