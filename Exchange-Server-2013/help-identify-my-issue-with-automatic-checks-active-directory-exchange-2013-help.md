---
title: '自動チェックで問題を特定する方法 - Active Directory: Exchange 2013 Help'
TOCTitle: 自動チェックで問題を特定する方法 - Active Directory
ms:assetid: af08e7a1-775a-4e56-a6fe-4ffc10460514
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn793979(v=EXCHG.150)
ms:contentKeyID: 62633011
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 自動チェックで問題を特定する方法 - Active Directory

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2016-12-09_

このページのチェックを実行すると、最もよく見られる構成の問題を確認できます。以下の自動チェックを使用して、構成を検証し、環境を更新することができます。

Office 365 のユーザー アカウントを既にお持ちの場合は、**\[サインイン\]** を選択してください。Azure ID アカウントは必要ありません。チェックを実行するときにユーザー アカウントの再入力を求められることがあります。その場合は、username@youroffice365login.domain 形式のユーザー アカウントとパスワードを入力してください。

## 前提条件

Azure Active Directory サインイン アシスタント および Windows PowerShell の Azure Active Directory モジュール がインストールされているかどうかを確認するためのチェックが行われます。

Azure Active Directory サインイン アシスタント には、次の 2 つのバージョンがあります。[32 ビット](https://go.microsoft.com/fwlink/?linkid=286261) および [64 ビット](https://go.microsoft.com/fwlink/?linkid=286262)。

Windows PowerShell の Azure Active Directory モジュール には、次の 2 つのバージョンがあります。[32 ビット](https://go.microsoft.com/fwlink/?linkid=286258) および [64 ビット](https://go.microsoft.com/fwlink/?linkid=286259)。

## Active Directory のチェック


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
<td><p>Exchange バージョン</p></td>
<td><p>Exchange Server が社内にインストールされているかどうかがわからない、または、どのバージョンを所有しているのかがわからない。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834879">このチェックを実行します</a></p></td>
</tr>
<tr class="odd">
<td><p>資格情報</p></td>
<td><p>Office 365 に移行するのに適切な資格情報を持っているかどうかがわからない。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834880">このチェックを実行します</a></p></td>
</tr>
<tr class="even">
<td><p>サード パーティ製のツール</p></td>
<td><p>メッセージング環境にサード パーティ製のどの統合/アプリケーションをインストールしたかがわからない。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834907">このチェックを実行します</a></p></td>
</tr>
<tr class="odd">
<td><p>共有メールボックス</p></td>
<td><p>他のユーザー (代理人) のメールボックスの管理者を特定したい。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834917">このチェックを実行します</a></p></td>
</tr>
</tbody>
</table>

