---
title: '受信コネクタの認証機構: Exchange 2013 Help'
TOCTitle: 受信コネクタの認証機構
ms:assetid: 926424e1-83e3-4c4b-b2dd-bf814d81e877
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657472(v=EXCHG.150)
ms:contentKeyID: 49896371
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 受信コネクタの認証機構

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-03-09_


受信コネクタの認証機構を次に示します。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>認証機構</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>なし</p></td>
<td><p>認証はありません。</p></td>
</tr>
<tr class="even">
<td><p>TLS</p></td>
<td><p>STARTTLS を通知します。TLS を提供するには、サーバー証明書を使用できる必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>統合</p></td>
<td><p>NTLM および Kerberos (統合 Windows 認証)</p></td>
</tr>
<tr class="even">
<td><p>BasicAuth</p></td>
<td><p>基本認証。認証されたログオンが必要です。</p></td>
</tr>
<tr class="odd">
<td><p>BasicAuthRequireTLS</p></td>
<td><p>TLS 経由の基本認証。サーバー証明書が必要です。</p></td>
</tr>
<tr class="even">
<td><p>ExchangeServer</p></td>
<td><p>Exchange Server 認証 (GSS-API (Generic Security Services application programming interface) および相互 GSS-API)</p></td>
</tr>
<tr class="odd">
<td><p>ExternalAuthoritative</p></td>
<td><p>接続は、Exchange の外部のセキュリティ機構を使用して、外部的にセキュリティで保護されていると見なされます。この接続は、インターネット プロトコル セキュリティ (IPsec) アソシエーションまたは仮想プライベート ネットワーク (VPN) になります。または、このサーバーは信頼できる物理的に制御されたネットワークに属している場合があります。<code>ExternalAuthoritative</code> の認証方法を使用するには、<code>ExchangeServers</code> 許可グループが必要です。認証方法とセキュリティ グループをこのように組み合わせることで、このコネクタ経由で受信したメッセージについて、匿名の送信者の電子メール アドレスを解決できます。</p></td>
</tr>
</tbody>
</table>


受信コネクタの認証機構の詳細については、「[New-ReceiveConnector](https://technet.microsoft.com/ja-jp/library/bb125139\(v=exchg.150\))」を参照してください。

