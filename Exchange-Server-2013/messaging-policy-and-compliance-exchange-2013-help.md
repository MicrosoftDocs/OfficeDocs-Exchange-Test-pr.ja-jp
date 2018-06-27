---
title: 'メッセージングのポリシーと準拠: Exchange 2013 Help'
TOCTitle: メッセージングのポリシーと準拠
ms:assetid: 65f20a20-27a4-4f6e-9b27-f8705d65b8d9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998599(v=EXCHG.150)
ms:contentKeyID: 48269590
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メッセージングのポリシーと準拠

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-03-09_

電子メールは、あらゆる規模の組織のインフォメーション ワーカーにとって、信頼性が高く、どこにいても利用できる通信媒体となりました。メッセージング ストアやメールボックスは、重要なデータのリポジトリとなりました。メッセージング システムの公正な使用を指示するメッセージング ポリシーを策定すること、ポリシーに基づいて行動するためのユーザー ガイドラインを提供すること、そして必要であれば、禁止される通信の種類について詳細を提示することは、組織にとって重要です。

組織は、電子メールのライフサイクルを管理するポリシー、メッセージをビジネス要件、法的要件、規制要件に基づいて一定期間保持するポリシー、訴訟や捜査目的に備えて電子メール レコードを保存するポリシー、電子情報開示要求を満たすため必要な電子メール レコードを検索、提供できるようにしておくためのポリシーも作成する必要があります。

知的財産、企業秘密、ビジネス プラン、組織が収集し処理する個人情報 (PII) などの機密情報の漏洩も防止する必要があります。

## Exchange 2013 のメッセージング ポリシーとコンプライアンス

次の表は、Microsoft Exchange Server 2013 のメッセージング ポリシーとコンプライアンス機能の概要と、それらの機能を理解し管理するのに役立つトピックへのリンクを示します。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>説明</th>
<th>Resources</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>メッセージング レコード管理 (MRM)</p></td>
<td><p>適用される規制に従うため、または法的要件やビジネス要件を満たすため、組織はメッセージング ポリシーの一環として電子メールのライフサイクル ポリシーを含めます。これらのポリシーで対処すべき共通の課題には、次の内容が含まれます。</p>
<ul>
<li><p>メッセージの保持期間</p></li>
<li><p>メッセージの保持場所</p></li>
<li><p>すべてのメッセージを同じ期間保持するべきか</p></li>
</ul>
<p>Exchange 2013 には、組織の電子メール ライフサイクル ポリシーを実装することができる MRM 機能が含まれています。MRM を使用してすべてのメッセージに一律の保持設定を適用したり、カスタム保持ポリシーを使用して基準となる保持設定をメールボックスに適用したり、オプションとしてユーザーがメッセージを分類し、特定の期間保存できるようにしたりすることが可能です。</p></td>
<td><p><a href="messaging-records-management-exchange-2013-help.md">メッセージング レコード管理</a></p></td>
</tr>
<tr class="even">
<td><p>インプレース アーカイブ</p></td>
<td><p><em>インプレース アーカイブ</em>を使用すると、個人用ストア ファイル (.pst) を使用する必要がなくなり、ユーザーは Outlook 2010 以降および Outlook Web App でアクセスできる<em>アーカイブ メールボックス</em>にメッセージを保存することができるようになるため、組織のメッセージング データを管理しやすくなります。</p></td>
<td><p><a href="in-place-archiving-in-exchange-2013-exchange-2013-help.md">Exchange 2013 のインプレース アーカイブ</a></p></td>
</tr>
<tr class="odd">
<td><p>インプレース保持</p></td>
<td><p>訴訟となる可能性がある程度見込まれる場合、組織では、訴訟に関連する電子メールを含めた電子的に格納された情報 (ESI) を保持する必要があります。インプレース保持を使用すると、クエリ パラメーターに一致するメッセージを検索して保存できます。メッセージは、削除、変更、または改ざんされないように保護され、無期限または指定した期間、保存されます。</p></td>
<td><p><a href="in-place-hold-and-litigation-hold-exchange-2013-help.md">インプレース保持と訴訟ホールド</a></p></td>
</tr>
<tr class="even">
<td><p>インプレース電子情報開示 (eDiscovery)</p></td>
<td><p>インプレース電子情報開示を使用すると、Exchange の組織全体のメールボックスのデータ検索、検索結果のプレビュー、検索結果の探索メールボックスへのコピーができます。</p></td>
<td><p><a href="in-place-ediscovery-exchange-2013-help.md">インプレース電子情報開示 (eDiscovery)</a></p></td>
</tr>
<tr class="odd">
<td><p>ジャーナル</p></td>
<td><p>ジャーナリングは、受信および送信電子メールを記録することで、組織が法律、規則、および組織の準拠要件に応答するのに役立ちます。メッセージング保持およびコンプライアンスを計画する際、ジャーナリングについて、どのように組織のコンプライアンス ポリシーに適合するか、またどのように Exchange 2013 がジャーナリングされたメッセージのセキュリティ保護に役立つかを理解することは重要です。</p></td>
<td><p><a href="journaling-exchange-2013-help.md">ジャーナル</a></p></td>
</tr>
<tr class="even">
<td><p>Transport Rules</p></td>
<td><p>トランスポート ルールを使用して、組織を通過するメッセージの特定の条件を見つけ、それらのメッセージを処理することができます。トランスポート ルールによって、電子メール メッセージにメッセージング ポリシーを適用し、メッセージおよびメッセージング システムを保護し、情報漏洩を防ぐことができます。</p></td>
<td><p><a href="mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md">メール フローやトランスポート ルール</a></p></td>
</tr>
<tr class="odd">
<td><p>データ損失防止 (DLP)</p></td>
<td><p>DLP 機能では機密データを保護し、ポリシーおよび規制についてユーザーに通知できます。ユーザーが誤って承認されていない連絡先に機密情報を送信してしまわないように防止することもできます。DLP ポリシーを構成する際、関連付けられたファイルの種類を数多く含むメッセージング システムの内容を分析することにより、機密データを識別して保護することができます。Exchange 2013 で用意されている DLP ポリシー テンプレートは、PII やクレジットカード業界のデータ セキュリティ基準 (PCI) などの規制基準に基づいています。DLP は、組織にとって重要なその他のポリシーをサポートするように拡張できます。さらに、新しいポリシー ヒント機能により、機密データが送信される前にポリシー違反についてユーザーに通知することが可能です。</p></td>
<td><p><a href="technical-overview-of-dlp-data-loss-prevention-in-exchange.md">データ損失防止</a></p></td>
</tr>
<tr class="even">
<td><p>Information Rights Management (IRM)</p></td>
<td><p>Information Rights Management (IRM) は、Active Directory Rights Management サービス (AD RMS) を使用し、電子メール メッセージおよび添付ファイルをオンラインおよびオフラインで永続的に保護します。</p></td>
<td><p><a href="information-rights-management-exchange-2013-help.md">Information Rights Management</a></p></td>
</tr>
<tr class="odd">
<td><p>S/MIME</p></td>
<td><p>S/MIME (Secure/Multipurpose Internet Mail Extensions) により、Office 365 メールボックスと Exchange 2013 および Exchange Online を使用するユーザーは、組織内で署名付きの暗号化された電子メールを送信して、機密情報を保護できます。Office 365 メールボックスの S/MIME を有効にするには、管理者が、Office 365 と社内のサーバーとの間でユーザー証明書を同期してから、S/MIME をサポートするように Outlook Online を構成します。</p></td>
<td><p><a href="s-mime-for-message-signing-and-encryption-exchange-2013-help.md">S/MIME によるメッセージの署名と暗号化</a></p></td>
</tr>
<tr class="even">
<td><p>メールボックスの監査ログの出力</p></td>
<td><p>メールボックスには機密でビジネスへの影響が大きい (HBI) 情報、および PII が含まれている可能性があり、組織内のメールボックスにログオンしたユーザー、および行った操作を追跡することが重要です。メールボックスの所有者 (代理ユーザーと呼ばれます) 以外のユーザーによるメールボックスへのアクセスを追跡することが特に重要です。メールボックス監査ログを使用すると、メールボックスの所有者、代理人 (フル メールボックス アクセスのアクセス許可を持つ管理者を含む)、および管理者によるメールボックスへのアクセスをログに記録できます。</p></td>
<td><p><a href="mailbox-audit-logging-exchange-2013-help.md">メールボックスの監査ログの出力</a></p>
<p><a href="exchange-auditing-reports-exchange-2013-help.md">Exchange 監査レポート</a></p></td>
</tr>
<tr class="odd">
<td><p>管理者監査ログ</p></td>
<td><p>管理者監査ログでは、Exchange サーバーと組織構成、および Exchange 受信者に対して管理者によって行われた変更のログを保持できます。管理者監査ログは、変更管理プロセスの一環として、またはコンプライアンス目的で構成と受信者に対する変更とアクセスを追跡するために使用できます。</p></td>
<td><p><a href="administrator-audit-logging-exchange-2013-help.md">管理者監査ログ</a></p></td>
</tr>
</tbody>
</table>

