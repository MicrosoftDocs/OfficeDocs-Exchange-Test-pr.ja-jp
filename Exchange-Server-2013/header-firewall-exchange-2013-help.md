---
title: 'ヘッダー ファイアウォール: Exchange 2013 Help'
TOCTitle: ヘッダー ファイアウォール
ms:assetid: 9b148f7b-47a9-4379-a55b-8d5310c1772f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb232136(v=EXCHG.150)
ms:contentKeyID: 52057838
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- ヘッダー ファイアウォール, ヘッダー ファイアウォールのアクセス許可
- ヘッダー ファイアウォール, トランスポート アーキテクチャ
- ヘッダー ファイアウォール, ルーティング ヘッダー
- ヘッダー ファイアウォール, フォレスト X-Header
- ヘッダー ファイアウォール, X-Header
- ヘッダー ファイアウォール, 組織 X-Header
ms.translationtype: HT
---

# ヘッダー ファイアウォール

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-03-09_

Microsoft Exchange Server 2013 の*ヘッダー ファイアウォール*は、受信および送信メッセージから特定のヘッダー フィールドを削除するメカニズムです。ヘッダー ファイアウォールの影響を受けるヘッダー フィールドは、次の 2 種類です。

  - **X-Header**   *X-Header* は、ユーザーが定義した非公式なヘッダー フィールドです。X-Header は、RFC 2822 では特に言及されていませんが、先頭に **X-** が付く未定義のヘッダー フィールドの使用は、メッセージに非公式のヘッダー フィールドを追加する方法として許容されるようになりました。メッセージング アプリケーション (スパム対策、ウイルス対策、およびメッセージング サーバーなど) は、メッセージに独自の X-Header を追加することができます。Exchange の X-Header フィールドには、SCL (Spam Confidence Level)、コンテンツ フィルターの結果、ルールの処理状態など、トランスポート サービスがメッセージに対して実行する処理についての詳細が含まれます。権限のない送信元にこの情報が漏れると、セキュリティ上のリスクを抱える可能性があります。

  - **ルーティング ヘッダー**   ルーティング ヘッダーは、RFC 2821 および RFC 2822 で定義されている標準の SMTP ヘッダー フィールドです。ルーティング ヘッダーは、メッセージを受信者に配信するために使用されたさまざまなメッセージング サーバーの情報を使用してメッセージにスタンプします。悪意のあるユーザーによってメッセージに挿入されたルーティング ヘッダーは、メッセージが受信者に到達するまでのルーティング パスを偽る可能性があります。

ヘッダー ファイアウォールは、信頼できない送信元から Exchange 組織に送られてきた受信メッセージから Exchange 関連の X-Header を削除することによって、X-Header を利用したスプーフィングを防止します。ヘッダー ファイアウォールは、Exchange 組織外の信頼できない送信元に送信された送信メッセージから Exchange 関連の X-Header を削除することによって、X-Header を利用した漏洩を防止します。ヘッダー ファイアウォールは、メッセージのルーティング履歴の追跡に使用される標準ルーティング ヘッダーのスプーフィングも防止します。

**目次**

Exchange でヘッダー ファイアウォールの影響を受けるメッセージ ヘッダー フィールド

受信コネクタと送信コネクタへのヘッダー ファイアウォールの適用方法

受信コネクタ上の受信メッセージに対するヘッダー ファイアウォール

送信コネクタ上の送信メッセージに対するヘッダー ファイアウォール

その他のメッセージ ソースに対するヘッダー ファイアウォール

Exchange の組織 X-Header およびフォレスト X-Header

## Exchange でヘッダー ファイアウォールの影響を受けるメッセージ ヘッダー フィールド

次の種類の X-Header とルーティング ヘッダーは、ファイアウォールの影響を受けます。

  - **組織 X-Header**   これらの X-Header フィールドはすべて **X-MS-Exchange-Organization-** で始まります。

  - **フォレスト X-Header**   これらの X-Header フィールドはすべて **X-MS-Exchange-Forest-** で始まります。
    
    組織 X-Header およびフォレスト X-Header の例については、このトピックの最後にある「Exchange の組織 X-Header およびフォレスト X-Header」セクションを参照してください。

  - **Received:ルーティング ヘッダー**   このヘッダー フィールドの個々のインスタンスは、受信者宛てのメッセージを受け付けて転送したすべてのメッセージング サーバーによってメッセージ ヘッダーに追加されます。**Received:**ヘッダーには、通常、メッセージング サーバーの名前と日付タイムスタンプが含まれます。

  - **Resent-\*:ルーティング ヘッダー**   Resent ヘッダー フィールドは、メッセージがユーザーによって転送されたかどうかを判断するために使用できる情報ヘッダー フィールドです。以下の Resent ヘッダー フィールドを利用できます。**Resent-Date:**、**Resent-From:**、**Resent-Sender:**、**Resent-To:**、**Resent-Cc:**、**Resent-Bcc:**、および **Resent-Message-ID:**。**Resent-** フィールドは、受信者にとってメッセージが元の送信者から直接送信されたように見えるようにするために使用されます。受信者は、メッセージ ヘッダーを参照して、メッセージを転送したのはだれかを確認することができます。

Exchange は 2 種類の方法を使用して、メッセージ内の組織 X-Header、フォレスト X-Header、およびルーティング ヘッダーにヘッダー ファイアウォールを適用します。

  - メッセージがコネクタを通過する際にメッセージ内の特定の種類のヘッダーを保持または削除するために使用できる送信コネクタまたは受信コネクタに、アクセス許可が割り当てられます。

  - その他の種類のメッセージ送信中、メッセージ内の特定の種類のヘッダーに対してヘッダー ファイアウォールは自動的に実装されます。

ページのトップへ

## 受信コネクタと送信コネクタへのヘッダー ファイアウォールの適用方法

コネクタに割り当てられている特定のアクセス許可に基づいて、送信コネクタと受信コネクタを通過するメッセージにヘッダー ファイアウォールが適用されます。

アクセス許可が受信コネクタまたは送信コネクタに割り当てられると、そのコネクタを通過するメッセージにはヘッダー ファイアウォールは適用されません。影響を受けるヘッダー フィールドがそのメッセージに保存されます。

アクセス許可が受信コネクタまたは送信コネクタに割り当てられないと、そのコネクタを通過するメッセージにヘッダー ファイアウォールが適用されます。影響を受けるヘッダー フィールドがそのメッセージから削除されます。

次の表は、ヘッダー ファイアウォールの適用に使用される送信コネクタおよび受信コネクタのアクセス許可と影響を受けるヘッダー フィールドを示しています。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>コネクタの種類</th>
<th>アクセス許可</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>受信コネクタ</p></td>
<td><p><strong>Ms-Exch-Accept-Headers-Organization</strong></p></td>
<td><p>このアクセス許可は、受信メッセージの <strong>X-MS-Exchange-Organization-</strong> で始まる組織 X-Header フィールドに影響します。</p></td>
</tr>
<tr class="even">
<td><p>受信コネクタ</p></td>
<td><p><strong>Ms-Exch-Accept-Headers-Forest</strong></p></td>
<td><p>このアクセス許可は、受信メッセージの <strong>X-MS-Exchange-Forest-</strong> で始まるフォレスト X-Header フィールドに影響します。</p></td>
</tr>
<tr class="odd">
<td><p>受信コネクタ</p></td>
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>このアクセス許可は、受信メッセージの <strong>Received:</strong>および <strong>Resent-*:</strong>ルーティング ヘッダー フィールドに影響します。</p></td>
</tr>
<tr class="even">
<td><p>送信コネクタ</p></td>
<td><p><strong>Ms-Exch-Send-Headers-Organization</strong></p></td>
<td><p>このアクセス許可は、送信メッセージの <strong>X-MS-Exchange-Organization-</strong> で始まる組織 X-Header フィールドに影響します。</p></td>
</tr>
<tr class="odd">
<td><p>送信コネクタ</p></td>
<td><p><strong>Ms-Exch-Send-Headers-Forest</strong></p></td>
<td><p>このアクセス許可は、送信メッセージの <strong>X-MS-Exchange-Forest-</strong> で始まるフォレスト X-Header フィールドに影響します。</p></td>
</tr>
<tr class="even">
<td><p>送信コネクタ</p></td>
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><p>このアクセス許可は、送信メッセージの <strong>Received:</strong>および <strong>Resent-*:</strong>ルーティング ヘッダー フィールドに影響します。</p></td>
</tr>
</tbody>
</table>


## 受信コネクタ上の受信メッセージに対するヘッダー ファイアウォール

次の表は、受信コネクタ上のヘッダー ファイアウォール アクセス許可の既定のアプリケーションを示しています。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>アクセス許可</th>
<th>アクセス許可が割り当てられた既定の Exchange セキュリティ プリンシパル</th>
<th>メンバーとしてのセキュリティ プリンシパルを持つ許可グループ</th>
<th>受信コネクタに許可グループを割り当てる既定の使用法の種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Ms-Exch-Accept-Headers-Organization</strong> と <strong>Ms-Exch-Accept-Headers-Forest</strong></p></td>
<td><ul>
<li><p>ハブ トランスポート サーバー</p></li>
<li><p>エッジ トランスポート サーバー</p></li>
<li><p>Exchange サーバー</p>

> [!NOTE]
> ハブ トランスポート サーバー上のみ


</li>
</ul></td>
<td><p><strong>ExchangeServers</strong></p></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>匿名ユーザー アカウント</p></td>
<td><p><strong>Anonymous</strong></p></td>
<td><p><code>Internet</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>認証されたユーザー アカウント</p></td>
<td><p><strong>ExchangeUsers</strong></p></td>
<td><p><code>Client</code> (エッジ トランスポート サーバーでは使用できません)</p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><ul>
<li><p>ハブ トランスポート サーバー</p></li>
<li><p>エッジ トランスポート サーバー</p></li>
<li><p>Exchange サーバー</p>

> [!NOTE]
> ハブ トランスポート サーバーのみ


</li>
<li><p>外部的にセキュリティで保護されたサーバー</p></li>
</ul></td>
<td><p><strong>ExchangeServers</strong></p></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>パートナー サーバー アカウント</p></td>
<td><p><strong>Partner</strong></p></td>
<td><p><code>Internet</code> および<code>Partner</code></p></td>
</tr>
</tbody>
</table>


ページのトップへ

## カスタム受信コネクタ上のヘッダー ファイアウォール

カスタム受信コネクタを使用する場合にメッセージにヘッダー ファイアウォールを適用するには、以下の方法を使用します。

  - メッセージにヘッダー ファイアウォールを自動的に適用する使用法の種類で受信コネクタを作成します。受信コネクタを作成する場合に限りこの使用法の種類を設定できることに注意してください。
    
      - メッセージから組織 X-Header またはフォレスト X-Header を削除するには、受信コネクタを作成し、`Internal` 以外の使用法の種類を選択します。
    
      - メッセージからルーティング ヘッダーを削除するには、次のいずれかの操作を行います。
        
          - 受信コネクタを作成し、使用法の種類として `Custom` を選択します。受信コネクタには許可グループを割り当てないでください。
        
          - 既存の受信コネクタを変更し、*PermissionGroups* パラメーターの値を `None` に設定します。
        
        アクセス許可が割り当てられていない受信コネクタがある場合は、最後の手順の説明に従って受信コネクタにセキュリティ プリンシパルを追加する必要がありますので注意してください。

  - 受信コネクタで構成されているセキュリティ プリンシパルから **Ms-Exch-Accept-Headers-Organization** アクセス許可、**Ms-Exch-Accept-Headers-Forest** アクセス許可、および **Ms-Exch-Accept-Headers-Routing** アクセス許可を削除するには、**Remove-ADPermission** コマンドレットを使用します。受信コネクタのアクセス許可グループを使用してセキュリティ プリンシパルにアクセス許可が割り当てられていない場合、アクセス許可グループのアクセス許可割り当てまたはグループ メンバーシップを変更できないため、この方法は機能しません。

  - 受信コネクタのメール フローで必要とする適切なセキュリティ プリンシパルを追加するには、**Add-ADPermission** コマンドレットを使用します。セキュリティ プリンシパルに **Ms-Exch-Accept-Headers-Organization** アクセス許可、**Ms-Exch-Accept-Headers-Forest** アクセス許可、および **Ms-Exch-Accept-Headers-Routing** アクセス許可が割り当てられないようにしてください。必要に応じて、**Add-ADPermission** コマンドレットを使用し、受信コネクタで構成されているセキュリティ プリンシパルへの **Ms-Exch-Accept-Headers-Organization** アクセス許可、**Ms-Exch-Accept-Headers-Forest** アクセス許可、および **Ms-Exch-Accept-Headers-Routing** アクセス許可を拒否します。

詳細については、以下のトピックを参照してください。

  - [受信コネクタ](receive-connectors-exchange-2013-help.md)

  - [Add-ADPermission](https://technet.microsoft.com/ja-jp/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/ja-jp/library/aa996048\(v=exchg.150\))

ページのトップへ

## 送信コネクタ上の送信メッセージに対するヘッダー ファイアウォール

次の表は、送信コネクタ上のヘッダー ファイアウォール アクセス許可の既定のアプリケーションを示しています。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>アクセス許可</th>
<th>アクセス許可が割り当てられた既定の Exchange セキュリティ プリンシパル</th>
<th>送信コネクタにセキュリティ プリンシパルを割り当てる既定の使用法の種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Ms-Exch-Send-Headers-Organization</strong> と <strong>Ms-Exch-Send-Headers-Forest</strong></p></td>
<td><ul>
<li><p>ハブ トランスポート サーバー</p></li>
<li><p>エッジ トランスポート サーバー</p></li>
<li><p>Exchange サーバー</p>

> [!NOTE]
> ハブ トランスポート サーバー上のみ


</li>
<li><p>外部的にセキュリティで保護されたサーバー</p></li>
<li><p><strong>ExchangeLegacyInterop</strong> ユニバーサル セキュリティ グループ</p></li>
</ul></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><ul>
<li><p>ハブ トランスポート サーバー</p></li>
<li><p>エッジ トランスポート サーバー</p></li>
<li><p>Exchange サーバー</p>

> [!NOTE]
> ハブ トランスポート サーバー上のみ


</li>
<li><p>外部的にセキュリティで保護されたサーバー</p></li>
<li><p><strong>ExchangeLegacyInterop</strong> ユニバーサル セキュリティ グループ</p></li>
</ul></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><p>匿名ユーザー アカウント</p></td>
<td><p><code>Internet</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><p>パートナー サーバー</p></td>
<td><p><code>Partner</code></p></td>
</tr>
</tbody>
</table>


ページのトップへ

## カスタム送信コネクタ上のヘッダー ファイアウォール

カスタム送信コネクタを使用する場合にメッセージにヘッダー ファイアウォールを適用するには、以下の方法を使用します。

  - メッセージにヘッダー ファイアウォールを自動的に適用する使用法の種類で送信コネクタを作成します。送信コネクタを作成する場合に限りこの使用法の種類を設定できることに注意してください。
    
      - メッセージから組織 X-Header またはフォレスト X-Header を削除するには、送信コネクタを作成し、`Internal` または `Partner` 以外の使用法の種類を選択します。
    
      - メッセージからルーティング ヘッダーを削除するには、送信コネクタを作成し、`Custom` の使用法の種類を選択します。**Ms-Exch-Send-Headers-Routing** アクセス許可は、`Custom` 以外のすべての送信コネクタの使用法の種類に割り当てられます。

  - コネクタから **Ms-Exch-Send-Headers-Organization** アクセス許可、**Ms-Exch-Send-Headers-Forest** アクセス許可、および **Ms-Exch-Send-Headers-Routing** アクセス許可を割り当てるセキュリティ プリンシパルを削除します。

  - 送信コネクタで構成されているいずれかのセキュリティ プリンシパルから **Ms-Exch-Send-Headers-Organization** アクセス許可、**Ms-Exch-Send-Headers-Forest** アクセス許可、および **Ms-Exch-Send-Headers-Routing** アクセス許可を削除するには、**Remove-ADPermission** コマンドレットを使用します。

  - 送信コネクタで構成されているいずれかのセキュリティ プリンシパルへの **Ms-Exch-Send-Headers-Organization** アクセス許可、**Ms-Exch-Send-Headers-Forest** アクセス許可、および **Ms-Exch-Send-Headers-Routing** アクセス許可を拒否するには、**Add-ADPermission** コマンドレットを使用します。

詳細については、以下のトピックを参照してください。

  - [送信コネクタ](send-connectors-exchange-2013-help.md)

  - [Add-ADPermission](https://technet.microsoft.com/ja-jp/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/ja-jp/library/aa996048\(v=exchg.150\))

ページのトップへ

## その他のメッセージ ソースに対するヘッダー ファイアウォール

送信コネクタや受信コネクタを使用せずに、メッセージがメールボックス サーバーまたはエッジ トランスポート サーバーのトランスポート パイプラインに入ってくることがあります。このようなその他のメッセージ ソースには、次の説明のようにヘッダー ファイアウォールが適用されます。

  - **ピックアップ ディレクトリと再生ディレクトリ**   ピックアップ ディレクトリは、メッセージ ファイルを送信するために管理者またはアプリケーションによって使用されます。再生ディレクトリは、Exchange メッセージ キューからエクスポートされたメッセージを再送信するために使用します。ピックアップ ディレクトリと再生ディレクトリの詳細については、「[ピックアップ ディレクトリと再生ディレクトリ](pickup-directory-and-replay-directory-exchange-2013-help.md)」を参照してください。
    
    組織 X-Header、フォレスト X-Header、およびルーティング ヘッダーは、ピックアップ ディレクトリのメッセージ ファイルから削除されます。
    
    ルーティング ヘッダーは、再生ディレクトリによって送信されたメッセージに保持されます。
    
    組織 X-Header およびフォレスト X-Header が再生ディレクトリ内のメッセージに保持されるか削除されるかは、メッセージ ファイルの **X-CreatedBy:**ヘッダー フィールドによって次のように制御されます。
    
      - **X-CreatedBy:** の値が`MSExchange15` の場合、組織 X-Header およびフォレスト X-Header はメッセージに保持されます。
    
      - **X-CreatedBy:** の値が`MSExchange15` でない場合、組織 X-Header およびフォレスト X-Header はメッセージから削除されます。
    
      - **X-CreatedBy:**ヘッダー フィールドがメッセージ ファイル内にない場合、組織 X-Header およびフォレスト X-Header はメッセージから削除されます。

  - **ドロップ ディレクトリ**   ドロップ ディレクトリは、メッセージ転送に SMTP を使用しないメッセージング サーバーにメッセージを送信するために、メールボックス サーバー上の外部コネクタによって使用されます。外部コネクタの詳細については、「[外部コネクタ](foreign-connectors-exchange-2013-help.md)」を参照してください。
    
    ドロップ ディレクトリに格納される前に、メッセージ ファイルから組織 X-Header およびフォレスト X-Header は削除されます。
    
    ルーティング ヘッダーは、ドロップ ディレクトリに送信されたメッセージに保持されます。

  - **メールボックス トランスポート**   メールボックス トランスポート サービスは、メールボックス サーバーのメールボックスとの間でメッセージを送受信するメールボックス サービス上にあります。メールボックス トランスポート サービスの詳細については、「[メール フロー](mail-flow-exchange-2013-help.md)」を参照してください。
    
    組織 X-Header、フォレスト X-Header、およびルーティング ヘッダーは、メールボックス トランスポート送信サービスによってメールボックスから送信される送信メッセージから削除されます。
    
    ルーティング ヘッダーは、メールボックス トランスポート配信サービスによってメールボックス受信者への受信メッセージのために保持されます。次の組織 X-Header は、メールボックス トランスポート配信サービスによってメールボックス受信者への受信メッセージのために保持されます。
    
      - **X-MS-Exchange-Organization-SCL**
    
      - **X-MS-Exchange-Organization-AuthDomain**
    
      - **X-MS-Exchange-Organization-AuthMechanism**
    
      - **X-MS-Exchange-Organization-AuthSource**
    
      - **X-MS-Exchange-Organization-AuthAs**
    
      - **X-MS-Exchange-Organization-OriginalArrivalTime**
    
      - **X-MS-Exchange-Organization-OriginalSize**

  - **DSN メッセージ**   組織 X-Header、フォレスト X-Header、およびルーティング ヘッダーは、DSN メッセージに添付される元のメッセージまたは元のメッセージ ヘッダーから削除されます。DSN メッセージの詳細については、「[Exchange 2013 の DSN と NDR](dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md)」を参照してください。

  - **トランスポート エージェントによる送信**   組織 X-Header、フォレスト X-Header、およびルーティング ヘッダーは、トランスポート エージェントによって送信されるメッセージに保持されます。

ページのトップへ

## Exchange の組織 X-Header およびフォレスト X-Header

メールボックス サーバーまたはエッジ トランスポート サーバーのトランスポート サービスは、メッセージ ヘッダーにカスタム X-Header フィールドを挿入します。

組織 X-Header はすべて **X-MS-Exchange-Organization-** で始まります。フォレスト X-Header はすべて **X-MS-Exchange-Forest-** で始まります。次の表は、Exchange 組織内のメッセージで使用される組織 X-Header およびフォレスト X-Header の一部を示しています。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>X-Header</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Forest-RulesExecuted</strong></p></td>
<td><p>メッセージを処理するトランスポート ルール。</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-Antispam-Report</strong></p></td>
<td><p>コンテンツ フィルター エージェントによってメッセージに適用されたスパム対策フィルター結果の要約レポートです。</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-AuthAs</strong></p></td>
<td><p>認証元を指定します。この X-Header は、メッセージのセキュリティが評価されている場合は常に存在します。指定できる値は、<code>Anonymous</code>、<code>Internal</code>、<code>External</code>、または <code>Partner</code> です。</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-AuthDomain</strong></p></td>
<td><p>ドメイン セキュリティで保護された認証中に入力されます。値は、リモート認証されたドメインの FQDN です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-AuthMechanism</strong></p></td>
<td><p>メッセージを送信する際の認証メカニズムを指定します。値は、2 桁の 16 進数です。</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-AuthSource</strong></p></td>
<td><p>組織の代理でメッセージの認証を評価したサーバー コンピューターの FQDN を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Journal-Report</strong></p></td>
<td><p>トランスポートのジャーナル レポートを識別します。トランスポート サービスからメッセージが送信されるとすぐに、ヘッダーは <strong>X-MS-Journal-Report</strong> になります。</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-OriginalArrivalTime</strong></p></td>
<td><p>メッセージが最初に Exchange 組織に入った時刻を識別します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Original-Sender</strong></p></td>
<td><p>検疫されたメッセージが最初に Exchange 組織に入ったときに元の送信者を識別します。</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-OriginalSize</strong></p></td>
<td><p>検疫されたメッセージが最初に Exchange 組織に入ったときに元のサイズを識別します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Original-Scl</strong></p></td>
<td><p>検疫されたメッセージが最初に Exchange 組織に入ったときに元の SCL を識別します。</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-PCL</strong></p></td>
<td><p>フィッシング詐欺検出機能の信頼レベルを識別します。指定できる PCL 値は 1 ～ 8 です。値が大きくなるほど、疑わしいメッセージであることを示します。詳細については、「<a href="anti-spam-stamps-exchange-2013-help.md">スパム対策スタンプ</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Quarantine</strong></p></td>
<td><p>メッセージがスパム検疫メールボックスで検疫され、配信状態通知 (DSN) が送信されたことを示します。または、メッセージが管理者によって検疫されて解放されたことを示します。この X-Header フィールドを使用すると、解放されたメッセージは再びスパム検疫メールボックスに送信されません。詳細については、「<a href="release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md">検疫済みメッセージをスパム検疫メールボックスから解放する</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-SCL</strong></p></td>
<td><p>メッセージの SCL を識別します。指定できる SCL 値は 0 ～ 9 です。値が大きくなるほど、疑わしいメッセージであることを示します。特別な値である -1 を指定すると、メッセージはコンテンツ フィルター エージェントによる処理から除外されます。詳細については、「<a href="content-filtering-exchange-2013-help.md">コンテンツ フィルター</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-SenderIdResult</strong></p></td>
<td><p>Sender ID エージェントの結果が含まれています。Sender ID エージェントは、SPF (Sender Policy Framework) を使用して、メッセージの送信元 IP アドレスと、送信者の電子メール アドレスに使用されているドメインを比較します。Sender ID の結果は、メッセージの SCL を計算するのに使用されます。詳細については、「<a href="sender-id-exchange-2013-help.md">送信者 ID</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>


ページのトップへ

