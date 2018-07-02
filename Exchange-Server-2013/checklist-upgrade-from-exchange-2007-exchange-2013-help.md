---
title: 'チェックリスト: Exchange 2007 からのアップグレード: Exchange 2013 Help'
TOCTitle: 'チェックリスト: Exchange 2007 からのアップグレード'
ms:assetid: 53aaa370-4562-43e4-9b75-7a705400c5a5
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff805032(v=EXCHG.150)
ms:contentKeyID: 51407529
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# チェックリスト: Exchange 2007 からのアップグレード

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

このチェックリストを使用して、Microsoft Exchange Server 2007 から Exchange Server 2013 にアップグレードします。このチェックリストで作業を開始する前に、以下のトピックで説明する概念を理解していることを確認してください。

  - [計画と展開](planning-and-deployment-for-exchange-2013-installation-instructions.md)

  - [Exchange 2013 の新機能](what-s-new-in-exchange-2013-exchange-2013-help.md)

このチェックリストは、標準的なアップグレード シナリオ全般について解説したガイドです。


> [!NOTE]
> Exchange Server 展開アシスタントは、Exchange Server の展開方法に関する、カスタマイズされた詳細なガイダンスを提供します。展開アシスタントでは、Exchange Server 2013 の新規インストールの展開、Exchange 2013 への以前のバージョンからのアップグレード、または Exchange 2013 と Exchange Online のハイブリッド展開の構成を支援することができます。詳細については、次を参照してください。<A href="exchange-server-deployment-assistant-exchange-2013-help.md">Exchange Server 展開アシスタント</A>.



## Exchange 2007 から Exchange 2013 へのアップグレードのチェックリスト


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
<td><p>1 リリース ノートを読む。</p></td>
<td><p><a href="release-notes-for-exchange-2013-exchange-2013-help.md">Exchange 2013 のリリース ノート</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>2. システム要件を確認する</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 のシステム要件</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>3. 前提条件の手順が完了したことを確認する</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 の前提条件</a></p>
<p><a href="deployment-security-checklist-exchange-2013-help.md">展開のセキュリティ チェックリスト</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>4. 名前空間の不整合を構成する</p>

> [!NOTE]
> この手順は省略可能です。組織で不整合の名前空間が実行されている場合にのみ必須です。


</td>
<td><p><a href="configure-the-dns-suffix-search-list-for-a-disjoint-namespace-exchange-2013-help.md">名前空間の不整合の DNS サフィックス検索一覧を構成する</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>5. すべての Exchange 2007 メールボックス データベース用のオフライン アドレス帳を選択する</p></td>
<td><p>「<a href="https://go.microsoft.com/fwlink/?linkid=320546">オフライン アドレス帳ダウンロードの受信者の準備</a>」</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>6. 従来の Exchange ホスト名の作成</p></td>
<td><p><a href="https://technet.microsoft.com/ja-jp/library/dn130105(v=exchg.150)">従来の Exchange ホスト名の作成</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>7. Exchange 2013 をインストールする</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">セットアップ ウィザードを使用した Exchange 2013 のインストール</a></p>
<p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">セットアップ ウィザードを使用して Exchange 2013 エッジ トランスポートの役割をインストールする</a></p>
<p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Exchange 2013 のインストールの確認</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>8. Exchange 2013 のメールボックスを作成する</p></td>
<td><p><a href="create-user-mailboxes-exchange-2013-help.md">ユーザー メールボックスを作成する</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>9. Exchange 関連の仮想ディレクトリを構成する</p>

> [!NOTE]
> この手順は、Exchange Web サービス、Outlook Anywhere、またはオフライン アドレス帳を使用する場合に必須です。また、Exchange コントロール パネル、Microsoft OfficeOutlook Web App、または Exchange ActiveSync の既定の設定のいずれかを変更する場合も必須です。<BR>


<p></p></td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Exchange 2013 クライアント アクセス サーバーの構成</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>10. Exchange 2013 証明書を構成する</p></td>
<td><p><a href="digital-certificates-and-ssl-exchange-2013-help.md">デジタル証明書と SSL</a></p>
<p></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>11. Exchange 2007 証明書を構成する</p></td>
<td><p>「<a href="https://go.microsoft.com/fwlink/?linkid=320553">クライアント アクセス サーバーの SSL の管理</a>」</p></td>
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
<td> </td>
<td><p>13. ユニファイド メッセージングを構成する</p>

> [!NOTE]
> この手順は省略可能です。組織でユニファイド メッセージングを使用する場合にのみ必須です。


</td>
<td><p><a href="planning-for-unified-messaging-exchange-2013-help.md">ユニファイド メッセージングの計画</a></p>
<p><a href="deploy-exchange-2013-um-exchange-2013-help.md">Exchange 2013 UM の展開</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>14. Outlook Anywhere を有効化して構成する</p></td>
<td><p><a href="outlook-anywhere-exchange-2013-help.md">Outlook Anywhere</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>15. サービス接続ポイントを構成する</p></td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Exchange 2013 クライアント アクセス サーバーの構成</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>16. Exchange 2007 URL を構成する</p></td>
<td><p><a href="https://technet.microsoft.com/ja-jp/library/dn282262(v=exchg.150)">Exchange 2007 外部 URL の構成</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>17. DNS レコードを構成する</p></td>
<td><p><a href="https://technet.microsoft.com/ja-jp/library/dn283988(v=exchg.150)">Exchange 2007 の複数サーバー インストール用に DNS レコードを構成する</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>18.  メールボックスをExchange 2007 から Exchange 2013に移動する</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Exchange 2013 でのメールボックスの移動</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>19. パブリック フォルダーのデータを Exchange 2013 から Exchange 2013に移動する</p>

> [!NOTE]
> この手順は省略可能です。組織がパブリック フォルダーを使用している場合にのみ必要です。


</td>
<td><p><a href="public-folders-exchange-2013-help.md">パブリック フォルダー</a></p>
<p><a href="https://technet.microsoft.com/ja-jp/library/jj150486(v=exchg.150)">シリアル移行を使用して以前のバージョンから Exchange 2013 にパブリック フォルダーを移行する</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>20. インストール後の作業</p></td>
<td><p><a href="exchange-2013-post-installation-tasks-exchange-2013-help.md">Exchange 2013 のインストール後のタスク</a></p></td>
</tr>
</tbody>
</table>

