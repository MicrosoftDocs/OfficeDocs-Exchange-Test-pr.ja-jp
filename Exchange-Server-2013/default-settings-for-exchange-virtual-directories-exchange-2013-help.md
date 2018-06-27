---
title: 'Exchange 仮想ディレクトリの既定の設定: Exchange 2013 Help'
TOCTitle: Exchange 仮想ディレクトリの既定の設定
ms:assetid: d2d89ce6-4721-4737-a325-fba5ad9422e0
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg247612(v=EXCHG.150)
ms:contentKeyID: 52057863
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 仮想ディレクトリの既定の設定

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-04-07_

Exchange Server 2013 は、インストール中、複数のインターネット インフォメーション サービス (IIS) 仮想ディレクトリを構成します。ここでは、クライアント アクセス サーバーとメールボックス サーバーの既定の IIS 認証設定、および既定の Secure Sockets Layer (SSL) 設定について説明します。

## クライアント アクセス サーバー

次の表は、スタンドアロン Exchange 2013 クライアント アクセス サーバーの既定の設定の一覧です。

### 既定のクライアント アクセス サーバーの IIS の認証と SSL の設定

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>仮想ディレクトリ</th>
<th>認証方法</th>
<th>SSL 設定</th>
<th>管理方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>既定の Web サイト</p></td>
<td><ul>
<li><p>Anonymous</p></li>
</ul></td>
<td><ul>
<li><p>必要</p></li>
</ul></td>
<td><p>IIS 管理コンソール</p></td>
</tr>
<tr class="even">
<td><p>aspnet_client</p></td>
<td><ul>
<li><p>匿名認証</p></li>
</ul></td>
<td><ul>
<li><p>SSL が必要</p></li>
<li><p>128 ビット暗号化が必要</p></li>
</ul></td>
<td><p>IIS 管理コンソール</p></td>
</tr>
<tr class="odd">
<td><p>自動検出</p></td>
<td><ul>
<li><p>匿名認証</p></li>
<li><p>基本認証</p></li>
<li><p>Windows 認証</p></li>
</ul></td>
<td><ul>
<li><p>SSL が必要</p></li>
<li><p>128 ビット暗号化が必要</p></li>
</ul></td>
<td><p>Exchange 管理シェル (シェル)</p></td>
</tr>
<tr class="even">
<td><p>ecp</p></td>
<td><ul>
<li><p>匿名認証</p></li>
<li><p>基本認証</p></li>
</ul></td>
<td><ul>
<li><p>SSL が必要</p></li>
<li><p>128 ビット暗号化が必要</p></li>
</ul></td>
<td><p>Exchange 管理センター (EAC) またはシェル</p></td>
</tr>
<tr class="odd">
<td><p>EWS</p></td>
<td><ul>
<li><p>匿名認証</p></li>
<li><p>Windows 認証</p></li>
</ul></td>
<td><ul>
<li><p>SSL が必要</p></li>
<li><p>128 ビット暗号化が必要</p></li>
</ul></td>
<td><p>シェル</p></td>
</tr>
<tr class="even">
<td><p>Microsoft-Server-ActiveSync</p></td>
<td><ul>
<li><p>基本認証</p></li>
</ul></td>
<td><ul>
<li><p>SSL が必要</p></li>
<li><p>128 ビット暗号化が必要</p></li>
</ul></td>
<td><p>EAC またはシェル</p></td>
</tr>
<tr class="odd">
<td><p>OAB</p></td>
<td><ul>
<li><p>Windows 認証</p></li>
</ul></td>
<td><ul>
<li><p>必要なし</p></li>
</ul></td>
<td><p>EAC またはシェル</p></td>
</tr>
<tr class="even">
<td><p>owa</p></td>
<td><ul>
<li><p>基本認証</p></li>
</ul></td>
<td><ul>
<li><p>SSL が必要</p></li>
<li><p>128 ビット暗号化が必要</p></li>
</ul></td>
<td><p>EAC またはシェル</p></td>
</tr>
<tr class="odd">
<td><p>PowerShell</p></td>
<td><ul>
<li><p>匿名認証</p></li>
</ul></td>
<td><ul>
<li><p>必要なし</p></li>
</ul></td>
<td><p>シェル</p></td>
</tr>
<tr class="even">
<td><p>Rpc</p></td>
<td><ul>
<li><p>基本認証</p></li>
<li><p>Windows 認証</p></li>
</ul></td>
<td><ul>
<li><p>SSL が必要</p></li>
<li><p>128 ビット暗号化が必要</p></li>
</ul></td>
<td><p>シェル</p></td>
</tr>
<tr class="odd">
<td><p>RpcWithCert</p></td>
<td><p>既定では、すべての認証方法が無効になっています。</p></td>
<td><ul>
<li><p>必須かどうか</p></li>
</ul></td>
<td><p> </p></td>
</tr>
</tbody>
</table>


## メールボックス サーバー

次の表は、スタンドアロン Exchange 2013 メールボックス サーバーの既定の設定の一覧です。

### 既定のメールボックス サーバーの IIS の認証と SSL の設定

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>仮想ディレクトリ</th>
<th>認証方法</th>
<th>SSL 設定</th>
<th>管理方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>既定の Web サイト</p></td>
<td><ul>
<li><p>匿名認証</p></li>
</ul></td>
<td><ul>
<li><p>SSL が必要</p></li>
<li><p>128 ビット暗号化が必要</p></li>
</ul></td>
<td><p>ユーザーがこの仮想ディレクトリを構成することはできません。</p></td>
</tr>
<tr class="even">
<td><p>PowerShell</p></td>
<td><ul>
<li><p>匿名認証</p></li>
</ul></td>
<td><ul>
<li><p>必要なし</p></li>
</ul></td>
<td><p>シェル</p></td>
</tr>
</tbody>
</table>

