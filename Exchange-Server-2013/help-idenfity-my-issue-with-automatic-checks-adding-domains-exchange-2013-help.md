---
title: '自動チェックを使って問題を特定する: ドメインの追加: Exchange 2013 Help'
TOCTitle: '自動チェックを使って問題を特定する: ドメインの追加'
ms:assetid: ea90a24b-7c9c-48d5-9475-0eb7777452f3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn793981(v=EXCHG.150)
ms:contentKeyID: 62633015
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 自動チェックを使って問題を特定する: ドメインの追加

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

このページのチェックを実行すると、最もよく見られる構成の問題を確認できます。以下の自動チェックを使用して、構成を検証し、環境を更新することができます。

Office 365 のユーザー アカウントを既にお持ちの場合は、**\[サインイン\]** を選択してください。Azure ID アカウントは必要ありません。チェックを実行するときにユーザー アカウントの再入力を求められることがあります。その場合は、username@youroffice365login.domain 形式のユーザー アカウントとパスワードを入力してください。

## 前提条件

Azure Active Directory サインイン アシスタント および Windows PowerShell の Azure Active Directory モジュール がインストールされているかどうかを確認するためのチェックが行われます。

Azure Active Directory サインイン アシスタント には、次の 2 つのバージョンがあります。[32 ビット](https://go.microsoft.com/fwlink/?linkid=286261) および [64 ビット](https://go.microsoft.com/fwlink/?linkid=286262)。

Windows PowerShell の Azure Active Directory モジュール には、次の 2 つのバージョンがあります。[32 ビット](https://go.microsoft.com/fwlink/?linkid=286258) および [64 ビット](https://go.microsoft.com/fwlink/?linkid=286259)。

## ドメインの追加のチェック


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>アプリケーション</p></td>
<td><p>現象</p></td>
<td><p>チェック</p></td>
</tr>
<tr class="even">
<td><p>ドメイン</p></td>
<td><p>社内に設置されたドメインを特定したい、または所有しているドメインがわかりません。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834925">このチェックを実行します</a></p></td>
</tr>
<tr class="odd">
<td><p>ドメイン</p></td>
<td><p>追加して検証したのが自分のテナントに適した正しいドメインであるかどうかがわかりません。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">このチェックを実行します</a></p></td>
</tr>
<tr class="even">
<td><p>ドメイン</p></td>
<td><p>使用しているすべての DNS レコードが Office 365 に適した正しいものであるかどうかを確認する方法がわかりません。</p></td>
<td><ol>
<li><p><a href="https://portal.microsoftonline.com/">Office 365 にサインインします</a></p></li>
<li><p><a href="https://portal.microsoftonline.com/tools">ツール</a>を選択します</p></li>
<li><p>[<strong>Office 365 ベスト プラクティス アナライザーで社内の PC を確認する</strong>] を選択します。</p></li>
</ol></td>
</tr>
</tbody>
</table>

