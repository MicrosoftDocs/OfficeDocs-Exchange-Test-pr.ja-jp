---
title: 'フェデレーション信頼のための信頼されたルート証明機関: Exchange 2013 Help'
TOCTitle: フェデレーション信頼のための信頼されたルート証明機関
ms:assetid: d4224bf5-69b3-484c-8a70-4f230d3dbdd9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee332350(v=EXCHG.150)
ms:contentKeyID: 48270091
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# フェデレーション信頼のための信頼されたルート証明機関

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2017-07-26_

Microsoft Exchange Server 2013 組織と [Azure Active Directory 認証システム](https://go.microsoft.com/fwlink/p/?linkid=135986)の間でフェデレーション信頼を確立するには、デジタル証明書を、信頼の作成に使用する Exchange サーバーにインストールする必要があります。自己署名証明書を使用することを強くお勧めします。自己署名証明書は、Exchange 管理センター (EAC) で **\[フェデレーションの信頼を有効にする\]** ウィザードを使用すると、自動的に作成されインストールされます。

推奨する自己署名証明書を使用しない場合は、Microsoft によって信頼されている証明機関 (CA) からの X.509 SSL (Secure Sockets Layer) 証明書を要求してインストールする必要があります。他の CA により発行された証明書であっても Azure AD 認証システムとのフェデレーション信頼を確立するのに使用できますが、これまでに Microsoft により認定されたものはありません。

次の表は、現在 Microsoft によって信頼されている CA の一覧です。これらの CA は Exchange 2013 での使用をテスト済みです。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>CA のフレンドリ名</th>
<th>発行元</th>
<th>目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Autoridade Certificadora Raiz Brasileira</p></td>
<td><p>Autoridade Certificadora Raiz Brasileira</p></td>
<td><p>サーバー認証、クライアント認証</p></td>
</tr>
<tr class="even">
<td><p>Comodo</p></td>
<td><p>Comodo Certification Authority</p></td>
<td><p>サーバー認証、クライアント認証</p></td>
</tr>
<tr class="odd">
<td><p>CyberTrust</p></td>
<td><p>Baltimore CyberTrust Root Certificate Authority</p></td>
<td><p>サーバー認証、クライアント認証</p></td>
</tr>
<tr class="even">
<td><p>Digicert</p></td>
<td><p>Digicert Global Root Certification Authority</p></td>
<td><p>サーバー認証、クライアント認証</p></td>
</tr>
<tr class="odd">
<td><p>Digicert High Assurance EV</p></td>
<td><p>Digicert Global Root Certification Authority</p></td>
<td><p>サーバー認証、クライアント認証</p></td>
</tr>
<tr class="even">
<td><p>Entrust</p></td>
<td><p>Entrust.net Secure Server Certification Authority</p></td>
<td><p>サーバー認証、クライアント認証</p></td>
</tr>
<tr class="odd">
<td><p>Entrust (2048)</p></td>
<td><p>Entrust.net Secure Server Certification Authority</p></td>
<td><p>サーバー認証、クライアント認証</p></td>
</tr>
<tr class="even">
<td><p>Equifax</p></td>
<td><p>Equifax Secure Certification Authority</p></td>
<td><p>サーバー認証、クライアント認証</p></td>
</tr>
<tr class="odd">
<td><p>GlobalSign</p></td>
<td><p>GlobalSign Certification Authority</p></td>
<td><p>サーバー認証、クライアント認証</p></td>
</tr>
<tr class="even">
<td><p>Go Daddy</p></td>
<td><p>Go Daddy Class 2 Certification Authority</p></td>
<td><p>サーバー認証、クライアント認証</p></td>
</tr>
<tr class="odd">
<td><p>Network Solutions</p></td>
<td><p>Network Solutions Certification Authority</p></td>
<td><p>サーバー認証、クライアント認証</p></td>
</tr>
<tr class="even">
<td><p>PositiveSSL</p></td>
<td><p>Comodo Certification Authority</p></td>
<td><p>サーバー認証、クライアント認証</p></td>
</tr>
<tr class="odd">
<td><p>SECOM</p></td>
<td><p>セコムトラストシステムズ証明機関</p></td>
<td><p>サーバー認証、クライアント認証</p></td>
</tr>
<tr class="even">
<td><p>UTN-UserFirst-Hardware</p></td>
<td><p>Comodo Certification Authority</p></td>
<td><p>サーバー認証、クライアント認証</p></td>
</tr>
<tr class="odd">
<td><p>VeriSign</p></td>
<td><p>Class 3 Public Primary Certification Authority</p></td>
<td><p>サーバー認証、クライアント認証</p></td>
</tr>
<tr class="even">
<td><p>VeriSign</p></td>
<td><p>VeriSign Trust Network</p></td>
<td><p>サーバー認証、クライアント認証</p></td>
</tr>
</tbody>
</table>


フェデレーション用の証明書の要件の詳細については、「[フェデレーション](federation-exchange-2013-help.md)」を参照してください。

