---
title: '自動チェックを使用して問題の特定を支援する - 移行: Exchange 2013 Help'
TOCTitle: 自動チェックを使用して問題の特定を支援する - 移行
ms:assetid: c1cd235d-8e8b-44a8-862d-9d36dc3a44c3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn793980(v=EXCHG.150)
ms:contentKeyID: 62633012
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 自動チェックを使用して問題の特定を支援する - 移行

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2016-12-09_

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
<td><p>メールボックス サイズ</p></td>
<td><p>ユーザーが組織の既定のメールボックス サイズを使用しているかどうかを特定することによって、最適な移行計画が立てられるようにしたい。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834877">このチェックを実行します</a></p></td>
</tr>
<tr class="odd">
<td><p>単一フォレスト</p></td>
<td><p>ディレクトリ同期を使用してユーザーのアカウントを移行できるかどうかを評価したい。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834875">このチェックを実行します</a></p></td>
</tr>
<tr class="even">
<td><p>ドメイン機能モード</p></td>
<td><p>ADFS 2.0/シングル サインオンの統合準備ができているかどうかがわからない。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834876">このチェックを実行します</a></p></td>
</tr>
<tr class="odd">
<td><p>パブリック フォルダー</p></td>
<td><p>Office 365 に移行するためのパブリック フォルダーが存在するかどうかがわからない。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834896">このチェックを実行します</a></p></td>
</tr>
</tbody>
</table>

