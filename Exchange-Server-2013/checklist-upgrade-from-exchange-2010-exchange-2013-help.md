---
title: 'チェックリスト: Exchange 2010 からのアップグレード: Exchange 2013 Help'
TOCTitle: 'チェックリスト: Exchange 2010 からのアップグレード'
ms:assetid: 06c1045a-5fcf-4e24-a901-1a979302fb8d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee332309(v=EXCHG.150)
ms:contentKeyID: 51407496
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# チェックリスト: Exchange 2010 からのアップグレード

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-07_

このチェックリストを使用して、Microsoft Exchange 2010 から Exchange 2013 にアップグレードします。このチェックリストで作業を開始する前に、次の概念を十分理解していることを確認してください。

  - [計画と展開](planning-and-deployment-for-exchange-2013-installation-instructions.md)

  - [Exchange 2013 の新機能](what-s-new-in-exchange-2013-exchange-2013-help.md)

このチェックリストは、標準的なアップグレード シナリオ全般について解説したガイドです。


> [!NOTE]
> Exchange Server 展開アシスタントは、Exchange Server の展開方法に関する、カスタマイズされた詳細なガイダンスを提供します。展開アシスタントでは、Exchange Server 2013 の新規インストールの展開、Exchange 2013 への以前のバージョンからのアップグレード、または Exchange 2013 と Exchange Online のハイブリッド展開の構成を支援することができます。詳細については、次を参照してください。<A href="exchange-server-deployment-assistant-exchange-2013-help.md">Exchange Server 展開アシスタント</A>.



## Exchange 2010 から Exchange 2013 へのアップグレードのチェックリスト


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>完了</p></td>
<td><p>タスク</p></td>
<td><p>トピック</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>1. リリース ノートを参照する</p></td>
<td><p><a href="release-notes-for-exchange-2013-exchange-2013-help.md">Exchange 2013 のリリース ノート</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>2. システム要件を確認する</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 のシステム要件</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>3. 前提条件の手順が完了したことを確認する</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 の前提条件</a></p>
<p><a href="deployment-security-checklist-exchange-2013-help.md">展開のセキュリティ チェックリスト</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>4. 名前空間の不整合を構成する</p>

> [!NOTE]
> この手順は省略可能です。組織で不整合の名前空間が実行されている場合にのみ必須です。


</td>
<td><p><a href="configure-the-dns-suffix-search-list-for-a-disjoint-namespace-exchange-2013-help.md">名前空間の不整合の DNS サフィックス検索一覧を構成する</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>5. すべての Exchange 2010 メールボックス データベース用のオフライン アドレス帳を選択する</p></td>
<td><p><a href="manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md">Set mailbox database properties</a> の<a href="manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md">Exchange 2013 のメールボックス データベースの管理</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>6. Exchange 2013 をインストールする</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">セットアップ ウィザードを使用した Exchange 2013 のインストール</a></p>
<p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">セットアップ ウィザードを使用して Exchange 2013 エッジ トランスポートの役割をインストールする</a></p>
<p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Exchange 2013 のインストールの確認</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>7. Exchange 2013 のメールボックスを作成する</p></td>
<td><p><a href="create-user-mailboxes-exchange-2013-help.md">ユーザー メールボックスを作成する</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>8. Exchange 関連の仮想ディレクトリを構成する</p>

> [!NOTE]
> この手順は、Exchange Web サービス、Outlook Anywhere、またはオフライン アドレス帳を使用する場合に必須です。また、Exchange コントロール パネル、Microsoft OfficeOutlook Web App、または Exchange ActiveSync の既定の設定のいずれかを変更する場合も必須です。<BR>


</td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Exchange 2013 クライアント アクセス サーバーの構成</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>9. クライアント アクセス サーバー上でデジタル証明書を追加する</p></td>
<td><p><a href="digital-certificates-and-ssl-exchange-2013-help.md">デジタル証明書と SSL</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>10. 調停メールボックスを移動する</p></td>
<td><p><a href="move-the-exchange-2010-system-mailbox-to-exchange-2013-exchange-2013-help.md">Exchange 2010 システム メールボックスの Exchange 2013 への移動</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>11. ユニファイド メッセージングを構成する</p>

> [!NOTE]
> この手順は省略可能です。組織でユニファイド メッセージングを使用する場合にのみ必須です。


</td>
<td><p><a href="upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md">Exchange 2010 UM から Exchange 2013 UM へのアップグレード</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>12. エッジ トランスポート サーバーの構成</p>

> [!NOTE]
> この手順は省略可能です。組織がエッジ トランスポート サーバーを使用している場合にのみ必要です。


</td>
<td><p><a href="configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md">購読済みのエッジ トランスポート サーバーを介してインターネット メール フローを構成する</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>13. Outlook Anywhere を有効化して構成する</p></td>
<td><p><a href="outlook-anywhere-exchange-2013-help.md">Outlook Anywhere</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>14. サービス接続ポイントを構成する</p></td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Exchange 2013 クライアント アクセス サーバーの構成</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>15. DNS レコードを構成する</p></td>
<td><p><a href="https://technet.microsoft.com/ja-jp/library/dn307232(v=exchg.150)">Exchange 2010 複数サーバー インストール用に DNS レコードを構成する</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>16. メールボックスをExchange 2010 から Exchange 2013に移動する</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Exchange 2013 でのメールボックスの移動</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>17. パブリック フォルダーのデータを Exchange 2013 から Exchange 2013に移動する</p></td>
<td><p><a href="public-folders-exchange-2013-help.md">パブリック フォルダー</a></p>
<p><a href="https://technet.microsoft.com/ja-jp/library/jj150486(v=exchg.150)">シリアル移行を使用して以前のバージョンから Exchange 2013 にパブリック フォルダーを移行する</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>18. インストール後の作業</p></td>
<td><p><a href="exchange-2013-post-installation-tasks-exchange-2013-help.md">Exchange 2013 のインストール後のタスク</a></p></td>
</tr>
</tbody>
</table>

