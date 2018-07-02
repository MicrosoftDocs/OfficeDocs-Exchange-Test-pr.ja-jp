---
title: 'メッセージ サイズの制限: Exchange 2013 Help'
TOCTitle: メッセージ サイズの制限
ms:assetid: b6a3840d-b821-4e53-877b-59c16be77206
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124345(v=EXCHG.150)
ms:contentKeyID: 49896431
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メッセージ サイズの制限

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-08-20_

Microsoft Exchange Server 2013 組織を通過するメッセージに制限を適用できます。メッセージの合計サイズ、またはメッセージ ヘッダーやメッセージの添付ファイル、受信者数などのメッセージの個々のコンポーネントのサイズを制限できます。制限は、Exchange 組織全体にグローバルに適用することも、特定のコネクタまたはユーザー オブジェクトに限定して適用することもできます。

Exchange 組織のメッセージ サイズの制限を計画するときには、以下の点を考慮してください。

  - すべての受信メッセージに対し、どの程度のサイズ制限を設定する必要があるか。

  - すべての送信メッセージに対し、どの程度のサイズ制限を設定する必要があるか。

  - Exchange 組織のメールボックスのクォータはいくらか。

  - 設定したメッセージ サイズの制限が、メールボックス クォータのサイズとどのように関連するか。

  - Exchange 組織に、指定した許容サイズを超えるメッセージの送受信を必要とするユーザーがいるか。

  - Exchange ネットワーク トポロジに、他のメッセージング システムや、異なるメッセージ サイズの制限が指定されている完全に個別のビジネス単位が含まれているかどうか。

このトピックでは、これらの事項の検討に役立つガイダンスを示します。

**目次**

メッセージ サイズの制限の種類

制限の適用範囲

メッセージ サイズの制限の優先順位

サイズ制限が適用されないメッセージ

## メッセージ サイズの制限の種類

以下は、個別のメッセージに使用可能なサイズ制限の基本的なカテゴリです。

  - **メッセージ ヘッダーのサイズ制限**   この制限は、メッセージ内のすべてのメッセージ ヘッダー フィールドの合計サイズに適用されます。メッセージ本文や添付ファイルのサイズは考慮されません。ヘッダー フィールドはプレーン テキストであるため、ヘッダーのサイズは各ヘッダー フィールドの文字数とヘッダー フィールドの合計数によって決定されます。テキストの 1 文字のサイズは 1 バイトです。
    

    > [!NOTE]
    > 一部のサード パーティ製のファイアウォールまたはプロキシ サーバーでは、独自のメッセージ ヘッダーのサイズ制限が適用されます。これらのサード パーティ製のファイアウォールまたはプロキシ サーバーでは、50 文字を超える添付ファイル名、または US-ASCII 形式ではない文字が含まれる添付ファイル名を含むメッセージが処理しにくい場合があります。



  - **メッセージ サイズの制限**   この制限は、メッセージ ヘッダー、メッセージ本文、添付ファイルを含めたメッセージの合計サイズに適用されます。メッセージ サイズの制限は、受信メッセージおよび送信メッセージのいずれにも設定できます。内部のメッセージ フローでは、Exchange 組織にメッセージが到着したときに、Exchange がカスタムの `X-MS-Exchange-Organization-OriginalSize:` メッセージ ヘッダーを使用して元のメッセージのサイズを記録します。指定したメッセージ サイズの制限に照らしてメッセージをチェックする場合、現在のメッセージ サイズと上記の元のメッセージ サイズ ヘッダーの値のうち小さい方の値が使用されます。コンテンツ変換、エンコード、およびエージェント処理によって、メッセージのサイズが変わる場合があります。

  - **添付ファイルのサイズ制限**   この制限は、メッセージ内の単一の添付ファイルの最大許容サイズに適用されます。メッセージには、メッセージ全体のサイズを大幅に上回る添付ファイルが多数含まれる場合があります。ただし、添付ファイルのサイズの制限は、個々の添付ファイルのサイズにのみ適用されます。

  - **受信者の制限**   この制限は、メッセージの受信者の合計数に適用されます。メッセージの最初の作成時には、受信者は `To:`、`Cc:`、および `Bcc:` ヘッダー フィールドに設定されます。メッセージが配信のために送信される際に、メッセージの受信者はメッセージ エンベロープ内の `RCPT TO:` エントリに変換されます。メッセージの送信時には、配布グループは単一の受信者としてカウントされます。

ページのトップへ

## 制限の適用範囲

各メッセージに使用可能な制限の適用範囲は、次の基本的なカテゴリに分類されます。

  - **組織における制限**   この制限は、組織内に存在するすべてのExchange 2013 メールボックス サーバー、およびExchange 2010 と Exchange 2007 のハブ トランスポート サーバーに適用されます。境界ネットワークにエッジ トランスポート サーバーが設置されている場合、指定された制限がそのサーバーに適用されます。

  - **コネクタにおける制限**   この制限は、指定した送信コネクタ、受信コネクタ、配信エージェント コネクタ、または外部コネクタをメッセージ配信のために使用するすべてのメッセージに適用されます。送信コネクタは、メールボックス サーバー上およびエッジ トランスポート サーバー上のトランスポート サービスで定義されます。受信コネクタは、メールボックス サーバー上、クライアント アクセス サーバー上のフロント エンド トランスポート サービス内、およびエッジ トランスポート サーバー上にあるトランスポート サービスで定義されます。

  - **"Active Directory サイト リンク"** メールボックス サーバー上のトランスポート サービスは、Active Directory サイト、および Active Directory IP サイト リンクに割り当てられたコストを、組織内のメールボックス サーバー間での最小コストのルーティング パスを決定する要因の 1 つとして使用します。組織内の Active Directory サイト リンクには、特定のメッセージ サイズの制限を割り当てることができます。

  - **サーバーにおける制限**   この制限は、特定のメールボックス サーバーまたはエッジ トランスポート サーバーに適用されます。このメッセージ制限は、それぞれのメールボックス サーバーまたはエッジ トランスポート サーバーで個別に設定できます。
    
    Outlook Web App では、クライアント アクセス サーバーに設定される HTTP 要求の最大サイズ制限は、Outlook Web App ユーザーが送信できるメッセージのサイズも制御します。

  - **ユーザーにおける制限**   この制限は、メールボックス、連絡先、配布グループ、パブリック フォルダーなどの特定のユーザー オブジェクトに適用されます。

次の表は、各メッセージ制限（Exchange 管理シェルまたはExchange 管理センター (EAC)での制限の構成方法に関する情報を含む）を示しています。

### 組織における制限

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>サイズの制限</th>
<th>既定値</th>
<th>シェル構成</th>
<th>EAC の構成</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>受信されるメッセージの最大サイズ</p></td>
<td><p>10 MB</p></td>
<td><p>コマンドレット: <strong>Set-TransportConfig</strong></p>
<p>パラメーター: <em>MaxReceiveSize</em></p></td>
<td><p><strong>[メール フロー]</strong> &gt; <strong>[受信コネクタ]</strong> &gt; <strong>[その他のオプション]</strong><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="[その他のオプション] アイコン" alt="[その他のオプション] アイコン" /> &gt; <strong>[組織のトランスポート設定]</strong> &gt; <strong>[制限]</strong> タブ &gt; <strong>[最大受信メッセージ サイズ]</strong></p></td>
</tr>
<tr class="even">
<td><p>送信されるメッセージの最大サイズ</p></td>
<td><p>10 MB</p></td>
<td><p>コマンドレット: <strong>Set-TransportConfig</strong></p>
<p>パラメーター: <em>MaxSendSize</em></p></td>
<td><p><strong>[メール フロー]</strong> &gt; <strong>[受信コネクタ]</strong> &gt; <strong>[その他のオプション]</strong><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="[その他のオプション] アイコン" alt="[その他のオプション] アイコン" /> &gt; <strong>[組織のトランスポート設定]</strong> &gt; <strong>[制限]</strong> タブ &gt; <strong>[最大送信メッセージ サイズ]</strong></p></td>
</tr>
<tr class="odd">
<td><p>メッセージあたりの最大受信者数</p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ126338.note(EXCHG.150).gif" title="メモ" alt="メモ" />メモ:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td></td>
</tr>
</tbody>
</table>

</td>
<td><p>5000</p></td>
<td><p>コマンドレット: <strong>Set-TransportConfig</strong></p>
<p>パラメーター: <em>MaxRecipientEnvelopeLimit</em></p></td>
<td><p><strong>[メール フロー]</strong> &gt; <strong>[受信コネクタ]</strong> &gt; <strong>[その他のオプション]</strong><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="[その他のオプション] アイコン" alt="[その他のオプション] アイコン" /> &gt; <strong>[組織のトランスポート設定]</strong> &gt; <strong>[制限]</strong> タブ &gt; <strong>[最大受信者数]</strong></p></td>
</tr>
<tr class="even">
<td><p>組織内のすべてのメールボックス サーバーに適用されるトランスポート ルールの最大添付ファイル サイズ</p></td>
<td><p>未構成</p></td>
<td><p>コマンドレット:<strong>New-TransportRule</strong>、<strong>Set-TransportRule</strong></p>
<p>パラメーター: <em>AttachmentSizeOver</em></p></td>
<td><p><strong>[メール フロー]</strong> &gt; <strong>[ルール]</strong> &gt; <strong>[追加]</strong><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="[追加] アイコン" alt="[追加] アイコン" /> または <strong>[編集]</strong><img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="編集アイコン" alt="編集アイコン" />。</p>
<p>述語 <strong>[次の場合にこのルールを適用]</strong> &gt; <strong>[いずれかの添付ファイル]</strong> &gt; <strong>[次のサイズ以上]</strong> を使用します。</p>
<p>述語 <strong>[次の場合にこのルールを適用]</strong> &gt; <strong>[メッセージ]</strong> &gt; <strong>[次のサイズ以上]</strong> を使用します</p></td>
</tr>
<tr class="odd">
<td><p>組織内のすべてのメールボックス サーバーに適用されるトランスポート ルールの最大メッセージ サイズ</p></td>
<td><p></p></td>
<td><p>コマンドレット:<strong>New-TransportRule</strong>、<strong>Set-TransportRule</strong></p>
<p>パラメーター: <em>MessageSizeOver</em></p></td>
<td><p><strong>[メール フロー]</strong> &gt; <strong>[ルール]</strong> &gt; <strong>[追加]</strong><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="[追加] アイコン" alt="[追加] アイコン" /> または <strong>[編集]</strong><img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="編集アイコン" alt="編集アイコン" />。</p>
<p>述語 <strong>[次の場合にこのルールを適用]</strong> &gt; <strong>[メッセージ]</strong> &gt; <strong>[次のサイズ以上]</strong> を使用します。</p></td>
</tr>
</tbody>
</table>


ページのトップへ

### コネクタ制限

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>サイズの制限</th>
<th>既定値</th>
<th>シェル構成</th>
<th>EAC の構成</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>受信コネクタを通過する最大ヘッダー サイズ</p></td>
<td><p>128 KB</p></td>
<td><p>コマンドレット:<strong>New-ReceiveConnector</strong>、<strong>Set-ReceiveConnector</strong></p>
<p>パラメーター: <em>MaxHeaderSize</em></p></td>
<td><p>該当なし</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>受信コネクタを通過する最大メッセージ サイズ</p>

> [!NOTE]
> 実際のメッセージ サイズは、メッセージ エンコーディングおよびコンテンツ変換のため、これより小さい場合があります。


</td>
<td><p><strong>メールボックス サーバー上のトランスポート サービス</strong></p>
<p>既定およびクライアント プロキシ受信コネクタ: 35 MB</p>
<p><strong>クライアント アクセス サーバー上のフロント エンド トランスポート サービス</strong></p>
<p>既定のフロント エンドおよび送信プロキシ フロント エンド受信コネクタ: 36 MB</p>
<p>クライアント フロント エンド受信コネクタ: 35 MB</p></td>
<td><p>コマンドレット:<strong>New-ReceiveConnector</strong>、<strong>Set-ReceiveConnector</strong></p>
<p>パラメーター: <em>MaxMessageSize</em></p></td>
<td><p><strong>[メール フロー]</strong> &gt; <strong>[受信コネクタ]</strong> &gt; <strong>[編集]</strong><img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="編集アイコン" alt="編集アイコン" /> &gt; <strong>[全般]</strong> タブ &gt; <strong>[最大受信メッセージ サイズ]</strong></p></td>
</tr>
<tr class="odd">
<td><p>受信コネクタを通過するメッセージあたりの最大受信者数</p></td>
<td><p><strong>メールボックス サーバー上のトランスポート サービス</strong></p>
<p>既定の受信コネクタ: 5,000</p>
<p>クライアント プロキシ受信コネクタ: 200</p>
<p><strong>クライアント アクセス サーバー上のフロント エンド トランスポート サービス</strong></p>
<p>既定のフロント エンド、クライアント フロント エンド、クライアント プロキシ フロント エンド受信コネクタ: 200</p>

> [!NOTE]
> 匿名の送信者の場合にこの受信者数を超えると、最初の 200&nbsp;人の受信者に対するメッセージが受け付けられます。ほとんどの SMTP メッセージング サーバーは、受信者の制限が有効になっていることを検出します。SMTP メッセージング サーバーは、そのメッセージがすべての受信者に配信されるまで、200 人の受信者のグループでメッセージを繰り返し再送信します。


</td>
<td><p>コマンドレット:<strong>New-ReceiveConnector</strong>、<strong>Set-ReceiveConnector</strong></p>
<p>パラメーター: <em>MaxRecipientsPerMessage</em></p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="even">
<td><p>送信コネクタを通過する最大メッセージ サイズ</p></td>
<td><p>10 MB</p></td>
<td><p>コマンドレット:<strong>New-SendConnector</strong>、<strong>Set-SendConnector</strong></p>
<p>パラメーター: <em>MaxMessageSize</em></p></td>
<td><p><strong>[メール フロー]</strong> &gt; <strong>[送信コネクタ]</strong> &gt; <strong>[編集]</strong><img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="編集アイコン" alt="編集アイコン" /> &gt; <strong>[全般]</strong> タブ &gt; <strong>[最大送信メッセージ サイズ]</strong></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Active Directory サイト リンクを通過する最大メッセージ サイズ</p></td>
<td><p>無制限</p></td>
<td><p>コマンドレット: <strong>Set-AdSiteLink</strong></p>
<p>パラメーター: <em>MaxMessageSize</em></p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="even">
<td><p>配信エージェント コネクタを通過する最大メッセージ サイズ</p></td>
<td><p>無制限</p></td>
<td><p>コマンドレット:<strong>New-DeliveryAgentConnector</strong>、<strong>Set-DeliveryAgentConnector</strong></p>
<p>パラメーター: <em>MaxMessageSize</em></p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="odd">
<td><p>外部コネクタを通過する最大メッセージ サイズ</p></td>
<td><p>無制限</p></td>
<td><p><strong>Cmdlet: Set-ForeignConnector</strong> パラメーター:<em>MaxMessageSize</em></p></td>
<td><p>該当なし</p></td>
</tr>
</tbody>
</table>


ページのトップへ

### サーバー制限

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>サイズの制限</th>
<th>既定値</th>
<th>シェル構成</th>
<th>EAC の構成</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ピックアップ ディレクトリ内のメッセージの最大ヘッダー サイズ</p></td>
<td><p>64 KB</p></td>
<td><p>コマンドレット: <strong>Set-TransportService</strong></p>
<p>パラメーター: <em>PickupDirectoryMaxHeaderSize</em></p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="even">
<td><p>ピックアップ ディレクトリ内のメッセージのメッセージあたりの最大受信者数</p></td>
<td><p>100</p></td>
<td><p>コマンドレット: <strong>Set-TransportService</strong></p>
<p>パラメーター: <em>PickupDirectoryMaxRecipientsPerMessage</em></p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="odd">
<td><p>Outlook Web App、Exchange ActiveSync、および Exchange Web サービスのクライアントごとの最大メッセージ サイズ制限</p></td>
<td><p>Outlook Web App   35 MB</p>
<p>Exchange ActiveSync   10 MB</p>
<p>Exchange Web サービス   64 MB</p>

> [!NOTE]
> これらの値は、Base64 エンコードに関連するオーバーヘッドにより、使用可能な実際の最大メッセージ サイズより約 33% 大きくなります。


</td>
<td><p>これらの値は、クライアント アクセス サーバーの適切な web.config XML アプリケーション構成ファイルで構成できます。詳細については、「<a href="configure-client-specific-message-size-limits-exchange-2013-help.md">クライアント固有のメッセージのサイズ制限を構成する</a>」を参照してください。</p></td>
<td><p>該当なし</p></td>
</tr>
</tbody>
</table>


ページのトップへ

### ユーザー制限

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>サイズの制限</th>
<th>既定値</th>
<th>シェル構成</th>
<th>EAC の構成</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>この受信者が送信可能な最大メッセージ サイズ</p></td>
<td><p>無制限</p></td>
<td><p>コマンドレット:</p>
<p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-RemoteMailbox</strong></p>
<p>パラメーター: <em>MaxSendSize</em></p></td>
<td><p>メールボックスの場合:</p>
<p><strong>[受信者]</strong> &gt; <strong>[メールボックス]</strong> &gt; <strong>[編集]</strong><img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="編集アイコン" alt="編集アイコン" /> &gt; <strong>[メールボックスの機能]</strong> &gt; <strong>[メール フロー]</strong> &gt; <strong>[メッセージのサイズ制限]</strong> &gt; <strong>[詳細の表示]</strong> &gt; <strong>[送信済みメッセージ]</strong></p>

> [!NOTE]
> 他の受信者タイプについては、EAC を使用してこの設定を構成することはできません。


</td>
</tr>
<tr class="even">
<td><p>この受信者に送信可能な最大メッセージ サイズ</p></td>
<td><p>無制限</p>
<p>サイト メールボックスのプロビジョニング ポリシー: 36 MB</p></td>
<td><p>コマンドレット:</p>
<p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>New-SiteMailboxProvisioningPolicy</strong></p>
<p><strong>Set-SiteMailboxProvisioningPolicy</strong></p>
<p>パラメーター: <em>MaxReceiveSize</em></p></td>
<td><p>メールボックスの場合:</p>
<p><strong>[受信者]</strong> &gt; <strong>[メールボックス]</strong> &gt; <strong>[編集]</strong><img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="編集アイコン" alt="編集アイコン" /> &gt; <strong>[メールボックスの機能]</strong> &gt; <strong>[メール フロー]</strong> &gt; <strong>[メッセージのサイズ制限]</strong> &gt; <strong>[詳細の表示]</strong> &gt; <strong>[受信メッセージ]</strong></p>

> [!NOTE]
> 他の受信者タイプについては、EAC を使用してこの設定を構成することはできません。


</td>
</tr>
<tr class="odd">
<td><p>この受信者が送信するメッセージあたりの最大受信者数</p></td>
<td><p>無制限</p></td>
<td><p>コマンドレット:</p>
<p><strong>Set-Mailbox</strong>, <strong>Set-MailUser</strong></p>
<p>パラメーター: <em>RecipientLimits</em></p>
<p></p></td>
<td><p>該当なし</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## メッセージ サイズの制限の優先順位

Exchange 組織では、異なるメッセージ サイズの制限をさまざまなレベルで設定できます。メッセージはトランスポート インフラストラクチャ内をルーティングされる間、さまざまなメッセージ サイズの制限の影響を受けます。トランスポート パイプライン内のメッセージがメッセージ サイズの制限に違反する場合は、できるだけ早い段階でそのメッセージが拒否されるように、メッセージ サイズの制限を計画する必要があります。一般的に言えば、メッセージがインフラストラチャ内に入るポイントで、より厳しい制限を設定する必要があります。たとえば、インターネットからメッセージを受信するエッジ サーバーの受信コネクタに対するすべてのメッセージ サイズの制限は、内部の Exchange 組織について構成するメッセージ サイズの制限以下にする必要があります。Exchange サーバーが受信し、処理したインターネットからのメッセージを、メールボックス サーバー上のトランスポート サービスが拒否することはシステム リソースの浪費になります。組織、サーバー、コネクタにおける制限は、メッセージの不要な処理を最小限にするように構成する必要があります。

この考え方の例外はユーザー制限です。ユーザー レベルの制限は、他のメッセージ サイズの制限より優先されます。したがって、組織の既定のメッセージ サイズの制限を超えるようにユーザーを構成できます。たとえば、ユーザー メールボックスの特定のグループに対しカスタムの送受信の制限を構成することで、そのメールボックスが、組織の他の部分よりサイズの大きなメッセージを送信できるようになります。

ユーザー制限の例外は、認証されたユーザー間でのメッセージ交換のみに適用されます。メッセージがインターネットで受信者に送信されるか、受信者によって受信される場合は、組織における制限が適用されます。たとえばメッセージ サイズの制限が 10 MB の組織で、マーケティング部門のユーザーを 50 MB までのメッセージを送受信するように構成したとします。このユーザーは大容量メッセージを相互に交換できますが、インターネット ユーザーから大容量メッセージを受信することはできません。これは、この場合のメッセージが、認証されていない送信者からのものであるためです。

ページのトップへ

## サイズ制限が適用されないメッセージ

次の一覧は、メールボックス サーバーまたはエッジ トランスポート サーバーによって生成され、すべてのメッセージ サイズの制限が適用されないメッセージの種類を示しています。

  - システム メッセージ

  - エージェントが生成するメッセージ

  - 配信状態通知 (DSN) メッセージ

  - ジャーナル レポート メッセージ

  - 隔離されたメッセージ

ただし、メッセージあたりの最大受信者数の組織における制限は、これらのメッセージにも適用されます。

ページのトップへ

