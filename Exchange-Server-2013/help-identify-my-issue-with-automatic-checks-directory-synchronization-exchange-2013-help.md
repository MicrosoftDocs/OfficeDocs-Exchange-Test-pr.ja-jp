---
title: '自動チェックを使って問題を特定する: ディレクトリ同期: Exchange 2013 Help'
TOCTitle: '自動チェックを使って問題を特定する: ディレクトリ同期'
ms:assetid: e6ea900a-c382-444c-a8ce-54d392bfeca3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn793977(v=EXCHG.150)
ms:contentKeyID: 62633014
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 自動チェックを使って問題を特定する: ディレクトリ同期

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

以下の自動チェックは、構成を検証し、環境を更新するために使用できます。

Office 365 のユーザー アカウントが既にある場合は、サインインを選択します。Azure ID アカウントは必要ありません。チェックを実行するときにユーザー アカウントの再入力を求められることがあります。その場合は、username@youroffice365login.domain 形式のユーザー アカウントとパスワードを入力してください。


> [!NOTE]
> Office 365 ポータルでの同期警告メッセージ、同期サーバー イベント ログのエラー、または Microsoft Online Services からの異常なディレクトリ同期の通知電子メールを受信した場合は、何らかの種類のディレクトリ同期の問題が発生している可能性があります。<A href="https://aka.ms/dsup">ディレクトリ同期のトラブルシューティング ツール</A>は、一般的な種類の同期障害の識別に役立ち、検出された問題に対する解決策を説明する Web ベースの診断ツールです。ディレクトリ同期のトラブルシューティング ツールはディレクトリ同期サーバーで実行する必要があります。



## 前提条件

Azure Active Directory サインイン アシスタント および Windows PowerShell の Azure Active Directory モジュール がインストールされているかどうかを確認するためのチェックが行われます。

Azure Active Directory サインイン アシスタント には、次の 2 つのバージョンがあります。[32 ビット](https://go.microsoft.com/fwlink/?linkid=286261) および [64 ビット](https://go.microsoft.com/fwlink/?linkid=286262)。

Windows PowerShell の Azure Active Directory モジュール には、次の 2 つのバージョンがあります。[32 ビット](https://go.microsoft.com/fwlink/?linkid=286258) および [64 ビット](https://go.microsoft.com/fwlink/?linkid=286259)。

## ディレクトリ同期のチェック


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
<td><p>ディレクトリ同期</p></td>
<td><p>使用しているすべての Active Directory ユーザー アカウントがディレクトリ同期の要件を満たしているかわかりません。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834884">このチェックを実行します</a></p></td>
</tr>
<tr class="odd">
<td><p>ディレクトリ同期</p></td>
<td><p>使用している Active Directory ドメインの機能レベルが Windows Server 2003 以上に正しく設定されているかわかりません。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834876">このチェックを実行します</a></p></td>
</tr>
<tr class="even">
<td><p>ディレクトリ同期</p></td>
<td><p>ディレクトリ同期が過去 3 時間以内に発生したかどうかがわかりません。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834887">このチェックを実行します</a></p></td>
</tr>
<tr class="odd">
<td><p>ディレクトリ同期</p></td>
<td><p>使用している Active Directory に、ディレクトリ同期をブロックする重複したユーザー属性があるかどうかがわかりません。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834883">このチェックを実行します</a></p></td>
</tr>
<tr class="even">
<td><p>ディレクトリ同期</p></td>
<td><p>ディレクトリ同期が Office 365 で有効であるかどうかがわかりません。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834887">このチェックを実行します</a></p></td>
</tr>
<tr class="odd">
<td><p>ディレクトリ同期</p></td>
<td><p>Office 365 見積もり制限を展開できるかどうかがわかりません。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834920">このチェックを実行します</a></p></td>
</tr>
<tr class="even">
<td><p>ディレクトリ同期</p></td>
<td><p>Office 365 を展開できるかどうか、既定のディレクトリ同期セットアップを使用できるかどうかがわかりません。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834876">このチェックを実行します</a></p></td>
</tr>
<tr class="odd">
<td><p>ディレクトリ同期</p></td>
<td><p>Active Directory を使用してディレクトリ同期をサポートできるかどうかがわかりません。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834886">このチェックを実行します</a></p></td>
</tr>
<tr class="even">
<td><p>ディレクトリ同期</p></td>
<td><p>使用しているすべての Active Directory グループがディレクトリ同期の要件を満たしているかわかりません。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834913">このチェックを実行します</a></p></td>
</tr>
</tbody>
</table>

