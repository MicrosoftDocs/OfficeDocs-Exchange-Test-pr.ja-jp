---
title: 'Azure:自動チェックを使って問題を特定する - DNS レコード: Exchange 2013 Help'
TOCTitle: Azure:自動チェックを使って問題を特定する - DNS レコード
ms:assetid: 1ef42cde-4df4-401a-b8f2-494630996ca8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn793619(v=EXCHG.150)
ms:contentKeyID: 62629997
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Azure:自動チェックを使って問題を特定する - DNS レコード

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2016-12-09_

構成をセットアップする際の最も一般的な問題の 1 つは、DNS レコードを不正確に構成することです。以下にリストされている自動チェックは、構成を検証し、環境を更新するために使用できます。

Office 365 のユーザー アカウントが既にある場合は、サインインを選択します。Azure ID アカウントは必要ありません。チェックを実行するときにユーザー アカウントの再入力を求められることがあります。その場合は、username@youroffice365login.domain 形式のユーザー アカウントとパスワードを入力してください。

## 前提条件

Azure Active Directory サインイン アシスタント および Windows PowerShell の Azure Active Directory モジュール がインストールされているかどうかを確認するためのチェックが行われます。

Azure Active Directory サインイン アシスタント には、次の 2 つのバージョンがあります。[32 ビット](https://go.microsoft.com/fwlink/?linkid=286261) および [64 ビット](https://go.microsoft.com/fwlink/?linkid=286262)。

Windows PowerShell の Azure Active Directory モジュール には、次の 2 つのバージョンがあります。[32 ビット](https://go.microsoft.com/fwlink/?linkid=286258) および [64 ビット](https://go.microsoft.com/fwlink/?linkid=286259)。

## DNS レコードのチェック


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
<td><p>カスタム ドメイン (contoso.com など) が Office 365 で構成されていないと思われます</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">このチェックを実行します</a></p></td>
</tr>
<tr class="odd">
<td><p>ドメイン</p></td>
<td><p>カスタム ドメイン (contoso.com など) が Office 365 で構成されていないと思われます (CNAME レコードを使用した場合)</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">このチェックを実行します</a></p></td>
</tr>
<tr class="even">
<td><p>ドメイン</p></td>
<td><p>カスタム ドメイン (contoso.com など) が Office 365 で構成されていないと思われます (TXT レコードを使用した場合)</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">このチェックを実行します</a></p></td>
</tr>
<tr class="odd">
<td><p>インスタント メッセージング</p></td>
<td><p>ユーザーが Lync クライアントを機能させる際に問題が発生します</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834901">このチェックを実行します</a></p></td>
</tr>
<tr class="even">
<td><p>インスタント メッセージング</p></td>
<td><p>ユーザーが Lync クライアントを他の組織で機能させる際に問題が発生します</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834902">このチェックを実行します</a></p></td>
</tr>
<tr class="odd">
<td><p>メール</p></td>
<td><p>Office 365 用に Outlook を自動構成できません</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834897">このチェックを実行します</a></p></td>
</tr>
<tr class="even">
<td><p>Mail</p></td>
<td><p>電子メールが Office 365 にルーティングされていないと思われます</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834898">このチェックを実行します</a></p></td>
</tr>
<tr class="odd">
<td><p>Mail</p></td>
<td><p>組織に多数のスパムが届きます</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834903">このチェックを実行します</a></p></td>
</tr>
<tr class="even">
<td><p>Mail</p></td>
<td><p>Exchange ハイブリッドを動作させることができそうにありません</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834904">このチェックを実行します</a></p></td>
</tr>
</tbody>
</table>

