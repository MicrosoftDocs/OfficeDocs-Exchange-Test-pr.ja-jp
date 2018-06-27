---
title: '展開のセキュリティ チェックリスト: Exchange 2013 Help'
TOCTitle: 展開のセキュリティ チェックリスト
ms:assetid: 0cbfad59-f503-48a0-8184-6ca999d89e61
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa996026(v=EXCHG.150)
ms:contentKeyID: 49115905
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 展開のセキュリティ チェックリスト

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2016-12-09_

Microsoft Exchange Server 2013 の機能は、メッセージング環境のセキュリティを向上させるために設計されています。通常、Exchange 2013では以下の条件が当てはまります。

  - Exchange 2013 によって使用されるアカウントは、特定の一連のタスクを実行するために最低限必要な権限を持ちます。

  - 既定では、サービスは必要な場合にのみ開始されます。

  - Exchange オブジェクトに対するアクセス制御リスト (ACL) の権限は、最小限になっています。

  - 管理アクセス許可は、特定の変更で必要とされるオブジェクトの変更範囲に従って設定されます。

  - 既定では、内部の既定のメッセージ パスはすべて暗号化されます。

このトピックでは、Microsoft Exchange のインストール前にメッセージング環境を強化するために実行する推奨手順について説明します。新しい Exchange サーバーの役割をインストールするたびに、このチェックリストを参照することをお勧めします。

Exchange 2013 をインストールする前に、以下の手順を実行します。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>手順</th>
<th>完了?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=54836">Microsoft Update</a> を実行します。</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>MicrosoftWindows 悪意のあるソフトウェアの削除ツールを実行します。悪意のあるソフトウェアの削除ツールは、Microsoft Update に含まれています。このツールの詳細については、<a href="http://go.microsoft.com/fwlink/p/?linkid=73452">悪意のあるソフトウェアの削除ツールについてのページ</a> を参照してください (このサイトは英語の場合があります)。</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=16526">Microsoft Baseline Security Analyzer</a> を実行します。</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>

