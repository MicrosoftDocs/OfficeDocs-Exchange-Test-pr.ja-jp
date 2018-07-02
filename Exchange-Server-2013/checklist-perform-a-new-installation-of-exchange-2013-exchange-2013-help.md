---
title: 'チェックリスト: Exchange 2013 の新規インストールを実行する: Exchange 2013 Help'
TOCTitle: 'チェックリスト: Exchange 2013 の新規インストールを実行する'
ms:assetid: f70d9dd3-7370-472e-b05e-1ea1671272b2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff805042(v=EXCHG.150)
ms:contentKeyID: 49129888
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# チェックリスト: Exchange 2013 の新規インストールを実行する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

このチェックリストを使用して Microsoft Exchange Server 2013 を展開します。このチェックリストで作業を開始する前に、次の概念を十分理解していることを確認してください。

  - [計画と展開](planning-and-deployment-for-exchange-2013-installation-instructions.md)

  - [展開のセキュリティ チェックリスト](deployment-security-checklist-exchange-2013-help.md)

このチェックリストは、一般的なシナリオについて説明しているため汎用的です。


> [!NOTE]
> Exchange Server 展開アシスタントは、Exchange Server の展開方法に関する、カスタマイズされた詳細なガイダンスを提供します。展開アシスタントでは、Exchange Server 2013 の新規インストールの展開、Exchange 2013 への以前のバージョンからのアップグレード、または Exchange 2013 と Exchange Online のハイブリッド展開の構成を支援することができます。詳細については、次を参照してください。<A href="exchange-server-deployment-assistant-exchange-2013-help.md">Exchange Server 展開アシスタント</A>.



## Exchange 2013 の新規インストール用チェックリスト


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>完了?</p></td>
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
<td><p>2. システム要件を確認する。</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 のシステム要件</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>3. 前提条件の手順が完了したことを確認する。</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 の前提条件</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>4. 名前空間の不整合を構成する。</p>

> [!NOTE]
> この手順は省略可能です。組織が名前空間の不整合を実行している場合のみ、この手順が必要になります。


</td>
<td><p><a href="disjoint-namespace-scenarios-exchange-2013-help.md">名前空間の不整合のシナリオ</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>5. メールボックス サーバーの役割をインストールする。</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">セットアップ ウィザードを使用した Exchange 2013 のインストール</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>6. クライアント アクセス サーバーの役割をインストールする。</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">セットアップ ウィザードを使用した Exchange 2013 のインストール</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>7. エッジ トランスポート サーバーの役割をインストールする。</p>

> [!NOTE]
> この手順は省略可能です。これはエッジ トランスポート サーバーをインストールする場合にのみ必要です。詳細については、「<A href="edge-transport-servers-exchange-2013-help.md">エッジ トランスポート サーバー</A>」を参照してください。


</td>
<td><p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">セットアップ ウィザードを使用して Exchange 2013 エッジ トランスポートの役割をインストールする</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>8. EdgeSync サブスクリプションを作成する。</p>
<p>この手順は省略可能です。これは、エッジ トランスポート サーバーがインストール済みで、エッジ トランスポート サーバーとハブ トランスポート サーバーとの間に EdgeSync サブスクリプションを構成する場合にのみ必要です。詳細については、「<a href="edge-subscriptions-exchange-2013-help.md">エッジ サブスクリプション</a>」を参照してください。</p></td>
<td><p><a href="configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md">購読済みのエッジ トランスポート サーバーを介してインターネット メール フローを構成する</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>9. トランスポートを構成する。</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 1: Create a Send connector</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>10. 承認済みドメインを追加する。</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 2: Add additional accepted domains</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>11. 電子メール アドレス ポリシーを構成する。</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 3: Configure the default email address policy</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>12. オフライン アドレス帳、Exchange Web サービス、Exchange 管理センター (EAC)、Outlook Web App、Exchange ActiveSync 仮想ディレクトリなど、仮想ディレクトリの設定を行う。</p>

> [!NOTE]
> Exchange Web サービス、Outlook Anywhere、またはオフライン アドレス帳を使用する場合のみ、この手順が必要になります。また、EAC、Outlook Web App、または Exchange ActiveSync の既定の設定を変更する必要がある場合、この手順が必要になる場合があります。


</td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 4: Configure external URLs</a></p>
<p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 5: Configure internal URLs</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>13. クライアント アクセス サーバー上でデジタル証明書を追加する。</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 6: Configure an SSL certificate</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>14. ユニファイド メッセージングを構成する。</p>

> [!NOTE]
> この手順は省略可能です。組織でユニファイド メッセージングを使用する場合のみ、この手順が必要になります。


</td>
<td><p><a href="deploying-voice-mail-and-um-exchange-2013-help.md">ボイス メールと UM の展開</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>15. 追加のユニファイド メッセージングおよび Lync Server の設定を構成する。</p>

> [!NOTE]
> この手順は省略可能です。組織にユニファイドメッセージングが構成されており、それを Lync Server と統合する場合にのみ必要です。


</td>
<td><p><a href="deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md">Exchange 2013 UM および Lync Server の展開の概要</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>16. インストール後の作業。</p></td>
<td><p><a href="exchange-2013-post-installation-tasks-exchange-2013-help.md">Exchange 2013 のインストール後のタスク</a></p></td>
</tr>
</tbody>
</table>

