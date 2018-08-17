---
title: 'ドメイン コントローラーへの Exchange のインストールは推奨されない: Exchange 2013 Help'
TOCTitle: ドメイン コントローラーへの Exchange のインストールは推奨されない
ms:assetid: 48922de2-a68c-4092-96a5-d38c8e5f49f5
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.warninginstallexchangerolesondomaincontroller(v=EXCHG.150)
ms:contentKeyID: 48269442
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ドメイン コントローラーへの Exchange のインストールは推奨されない

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2013-03-22_

Microsoft Exchange Server 2013 セットアップ プログラムが、Exchange 2013 のインストールが試みられているコンピューターが、Active Directory ドメイン コントローラーであることを検出しました。ドメイン コントローラーへの Exchange 2013 のインストールは推奨されていません。

ドメイン コントローラーに Exchange 2013 をインストールする場合は、次の問題に注意してください。

  - Active Directory 分割アクセス許可に対する Exchange 2013 の構成はサポートされていません。

  - ドメイン コントローラーに Exchange がインストールされるとき、Exchange Trusted Subsystem ユニバーサル セキュリティ グループ (USG) が Domain Admins グループに追加されます。このグループが追加されると、ドメイン内のすべての Exchange サーバーがそのドメインでドメイン管理者の権利を付与されます。

  - Exchange Server と Active Directory はどちらもリソースを集中的に使用するアプリケーションです。両方のアプリケーションを同じコンピューターで実行する場合は、パフォーマンス面の影響を考慮する必要があります。

  - Exchange 2013 がインストールされているドメイン コントローラーがグローバル カタログ サーバーであることを確認する必要があります。

  - Exchange サービスは、ドメイン コントローラーがグローバル カタログ サーバーでもある場合に、正しく起動しないことがあります。

  - サーバーをシャットダウンまたは再起動する前に Exchange サービスが停止されていないと、システムのシャットダウンにかかる時間が大幅に長くなります。

  - ドメイン コントローラーのメンバー サーバーへの降格はサポートされていません。

  - Active Directory ドメイン コントローラーでもある、クラスター化されたノードでの Exchange 2013 の実行はサポートされていません。

Exchange 2013 は、メンバー サーバーにインストールすることをお勧めします。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

探しているものは見つかりましたか？検索したい情報に関する[フィードバックを送信](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback)してください。

