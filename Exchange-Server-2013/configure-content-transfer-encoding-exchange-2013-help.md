---
title: 'コンテンツ転送エンコードの構成: Exchange 2013 Help'
TOCTitle: コンテンツ転送エンコードの構成
ms:assetid: c4922362-18d4-42f7-9189-9076720eb1d8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg144562(v=EXCHG.150)
ms:contentKeyID: 49896462
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# コンテンツ転送エンコードの構成

 

_**適用先:** Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

*コンテンツ転送エンコード*により、電子メール メッセージ データを US-ASCII プレーン テキスト形式に変換するためのエンコード方法が定義されます。この変換により、メッセージは、US-ASCII テキスト形式のメッセージのみをサポートしている古い SMTP メッセージング サーバーを通過できるようになります。コンテンツ転送エンコードは RFC 2045 に定義されています。転送エンコード方法は、メッセージの **Content-Transfer-Encoding** ヘッダー フィールドに格納されます。Microsoft Exchange Server 2013 では、次のコンテンツ転送エンコード方法を使用できます。

  - **7-bit**   この値は、メッセージ本文のデータがすでに US ASCII プレーン テキスト形式であり、メッセージ エンコードがメッセージに対して実行されていないことを示します。

  - **Quoted-printable (QP)**   このエンコーディング方法は、印刷可能な US-ASCII 文字列を使用してメッセージ本文のデータをエンコードします。元のメッセージ テキストの大部分が US-ASCII テキストである場合は、Quoted-printable エンコーディングによってある程度判読できる小サイズの結果が得られます。既定では、Exchange 2013 は QP を使用してバイナリ メッセージ データをエンコードします。

  - **Base64**   このエンコーディング方法は、主に、RFC 1421 で定義されている PEM (Privacy-Enhanced Mail) 標準に基づいています。Base64 エンコーディングでは、PEM で定義されている 64 文字のアルファベットのエンコーディング方法と出力スペース文字を使用して、メッセージ本文のデータをエンコードします。Base64 エンコードは、メッセージのサイズがどの程度増えるかを予測できるため、バイナリ データおよび US-ASCII 形式ではないテキストに最適です。

転送エンコード方法は、**Set-OrganizationConfig** コマンドレットおよび **Set-RemoteDomain** コマンドレット上で *ByteEncoderTypeFor7BitCharsets* パラメーターを使用して構成します。**Set-OrganizationConfig** を使用して構成するコンテンツ転送エンコードの設定は、Exchange 組織におけるすべてのメッセージに適用されます。**Set-RemoteDomain** を使用して構成するコンテンツ転送エンコードの設定は、リモート ドメインの外部受信者に送信されるメッセージにのみ適用されます。

次の表に、転送エンコード方法の設定に使用できる値の一覧を示します。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Set-OrganizationConfig</strong> のパラメーター</th>
<th><strong>Set-RemoteDomain</strong> のパラメーター</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p><code>Use7Bit</code></p></td>
<td><p>HTML およびプレーン テキストに対して、常に 7-bit エンコードを使用します。これは既定の値です。</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p><code>UseQP</code></p></td>
<td><p>HTML およびテキスト形式に対して、常に QP エンコードを使用します。</p></td>
</tr>
<tr class="odd">
<td><p>2</p></td>
<td><p><code>UseBase64</code></p></td>
<td><p>HTML およびテキスト形式に対して、常に Base64 エンコードを使用します。</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p><code>UseQPHtmlDetectTextPlain</code></p></td>
<td><p>HTML に対して QP エンコードを使用し、テキスト形式に対しては、テキストの折り返しが無効である場合に限り QP エンコードを使用します。テキストの折り返しが有効の場合は、テキスト形式に対して 7 ビット エンコードを使用します。</p></td>
</tr>
<tr class="odd">
<td><p>6</p></td>
<td><p><code>UseBase64HtmlDetectTextPlain</code></p></td>
<td><p>HTML に対して Base64 エンコードを使用し、テキスト形式に対しては、テキストの折り返しが無効である場合に限り Base64 エンコードを使用します。テキスト形式でテキストの折り返しが有効の場合は、HTML に対して Base64 エンコードを使用し、テキスト形式に対して 7 ビット エンコードを使用します。</p></td>
</tr>
<tr class="even">
<td><p>13</p></td>
<td><p><code>UseQPHtml7BitTextPlain</code></p></td>
<td><p>HTML に対して、常に QP エンコードを使用します。テキスト形式に対しては、常に 7 ビット エンコードを使用します。</p></td>
</tr>
<tr class="odd">
<td><p>14</p></td>
<td><p><code>UseBase64Html7BitTextPlain</code></p></td>
<td><p>HTML 形式に対して、常に Base64 エンコードを使用します。テキスト形式に対しては、常に 7 ビット エンコードを使用します。</p></td>
</tr>
</tbody>
</table>


**Content-Transfer-Encoding** ヘッダー フィールドの詳細については、「[コンテンツ変換](content-conversion-exchange-2013-help.md)」の「Understanding the structure of email messages」を参照してください。

リモート ドメインの詳細については、「[リモート ドメイン](remote-domains-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「トランスポート サービス」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用して組織のコンテンツ転送エンコード方法を構成する

組織のコンテンツ転送エンコード方法を設定するには、次のコマンドを実行します。

```powershell
Set-OrganizationConfig -ByteEncoderTypeFor7BitCharsets <Integer>
```

たとえば、コンテンツ転送エンコード方法を Base64 に設定するには、次のコマンドを実行します。

```powershell
Set-OrganizationConfig -ByteEncoderTypeFor7BitCharsets 2
```

## シェルを使用してリモート ドメインのコンテンツ転送エンコード方法を構成する

リモート ドメインのすべての受信者のコンテンツ転送エンコード方法を設定するには、次のコマンドを実行します。

```powershell
Set-RemoteDomain -ByteEncoderTypeFor7BitCharsets <Value>
```

たとえば、コンテンツ転送エンコード方法を Base64 に設定するには、次のコマンドを実行します。

```powershell
Set- RemoteDomain -ByteEncoderTypeFor7BitCharsets UseBase64
```

## 正常な動作を確認する方法

コンテンツ転送エンコードの方法が正常に構成されたことを確認するには、次の手順を実行します。

1.  US-ASCII テキストとバイナリ データの組み合わせ、または US-ASCII 以外のテキストを含むテスト メッセージを、内部または外部のテスト アカウントに送信します。内部アカウントを使用して組織の設定をテストし、リモート ドメインの外部アカウントを使用してリモート ドメインの設定をテストします。

2.  電子メール クライアントで、メッセージの **Content-Transfer-Encoding** ヘッダー フィールドを表示し、メッセージに対して使用されたコンテンツ転送エンコード方法が構成した方法と一致していることを確認します。

