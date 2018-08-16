---
title: 'リモート ドメイン用にサポートされている文字セット: Exchange Online Help'
TOCTitle: リモート ドメイン用にサポートされている文字セット
ms:assetid: 66023a62-1fd3-4019-be2b-4e7147db148a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998600(v=EXCHG.150)
ms:contentKeyID: 52057437
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# リモート ドメイン用にサポートされている文字セット

 

_**適用先:** Exchange Online, Exchange Server 2013_

リモート ドメインに送信されるメッセージに次の文字セットを指定できます。

  - Exchange 管理センター (EAC) の <strong>リモート ドメイン</strong> の設定ページで、<strong>MIME 文字セット</strong> および <strong>非 MIME 文字セット</strong> ドロップダウン リストから名前を選択します。

  - シェルでは、[Set-RemoteDomain](https://technet.microsoft.com/ja-jp/library/aa997857\(v=exchg.150\)) コマンドレット内の *CharacterSet* パラメーターまたは *NonMimeCharacterSet* パラメーターに関する次の表内の \[名前\] 列内の値を使用します。

### リモート ドメインの構成でサポートされる文字セット

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>名前</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>big5</p></td>
<td><p>繁体字中国語 (Big5)</p></td>
</tr>
<tr class="even">
<td><p>DIN_66003</p></td>
<td><p>ドイツ語 (IA5)</p></td>
</tr>
<tr class="odd">
<td><p>euc-jp</p></td>
<td><p>日本語 (EUC)</p></td>
</tr>
<tr class="even">
<td><p>euc-kr</p></td>
<td><p>韓国語 (EUC)</p></td>
</tr>
<tr class="odd">
<td><p>GB18030</p></td>
<td><p>簡体字中国語 (GB18030)</p></td>
</tr>
<tr class="even">
<td><p>gb2312</p></td>
<td><p>簡体字中国語 (GB2312)</p></td>
</tr>
<tr class="odd">
<td><p>hz-gb-2312</p></td>
<td><p>簡体字中国語 (HZ)</p></td>
</tr>
<tr class="even">
<td><p>iso-2022-jp</p></td>
<td><p>日本語 (JIS)</p></td>
</tr>
<tr class="odd">
<td><p>iso-2022-kr</p></td>
<td><p>韓国語 (ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-1</p></td>
<td><p>西ヨーロッパ言語 (ISO)</p></td>
</tr>
<tr class="odd">
<td><p>iso-8859-2</p></td>
<td><p>中央ヨーロッパ言語 (ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-3</p></td>
<td><p>ラテン 3 (ISO)</p></td>
</tr>
<tr class="odd">
<td><p>iso-8859-4</p></td>
<td><p>バルト言語 (ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-5</p></td>
<td><p>キリル言語 (ISO)</p></td>
</tr>
<tr class="odd">
<td><p>iso-8859-6</p></td>
<td><p>アラビア語 (ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-7</p></td>
<td><p>ギリシャ語 (ISO)</p></td>
</tr>
<tr class="odd">
<td><p>iso-8859-8</p></td>
<td><p>ヘブライ語 (ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-9</p></td>
<td><p>トルコ語 (ISO)</p></td>
</tr>
<tr class="odd">
<td><p>iso-8859-13</p></td>
<td><p>エストニア語 (ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-15</p></td>
<td><p>ラテン 9 (ISO)</p></td>
</tr>
<tr class="odd">
<td><p>koi8-r</p></td>
<td><p>キリル言語 (KOI8-R)</p></td>
</tr>
<tr class="even">
<td><p>koi8-u</p></td>
<td><p>キリル言語 (KOI8-U)</p></td>
</tr>
<tr class="odd">
<td><p>ks_c_5601-1987</p></td>
<td><p>韓国語 (Windows)</p></td>
</tr>
<tr class="even">
<td><p>NS_4551-1</p></td>
<td><p>ノルウェー語 (IA5)</p></td>
</tr>
<tr class="odd">
<td><p>SEN_850200_B</p></td>
<td><p>スウェーデン語 (IA5)</p></td>
</tr>
<tr class="even">
<td><p>shift_jis</p></td>
<td><p>日本語 (Shift-JIS)</p></td>
</tr>
<tr class="odd">
<td><p>utf-8</p></td>
<td><p>Unicode (UTF-8)</p></td>
</tr>
<tr class="even">
<td><p>windows-1250</p></td>
<td><p>中央ヨーロッパ言語 (Windows)</p></td>
</tr>
<tr class="odd">
<td><p>windows-1251</p></td>
<td><p>キリル言語 (Windows)</p></td>
</tr>
<tr class="even">
<td><p>windows-1252</p></td>
<td><p>西ヨーロッパ言語 (Windows)</p></td>
</tr>
<tr class="odd">
<td><p>windows-1253</p></td>
<td><p>ギリシャ語 (Windows)</p></td>
</tr>
<tr class="even">
<td><p>windows-1254</p></td>
<td><p>トルコ語 (Windows)</p></td>
</tr>
<tr class="odd">
<td><p>windows-1255</p></td>
<td><p>ヘブライ語 (Windows)</p></td>
</tr>
<tr class="even">
<td><p>windows-1256</p></td>
<td><p>アラビア語 (Windows)</p></td>
</tr>
<tr class="odd">
<td><p>windows-1257</p></td>
<td><p>バルト言語 (Windows)</p></td>
</tr>
<tr class="even">
<td><p>windows-1258</p></td>
<td><p>ベトナム語 (Windows)</p></td>
</tr>
<tr class="odd">
<td><p>windows-874</p></td>
<td><p>タイ語 (Windows)</p></td>
</tr>
</tbody>
</table>

