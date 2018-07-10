---
title: '受信コネクタのアクセス許可: Exchange 2013 Help'
TOCTitle: 受信コネクタのアクセス許可
ms:assetid: 31af7139-6823-411b-81b3-e42edd83ee6c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ673053(v=EXCHG.150)
ms:contentKeyID: 49896182
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 受信コネクタのアクセス許可

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-07_

次の表は、各アクセス許可の種類と説明を示しています。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>受信コネクタのアクセス許可</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-SMTP-Submit</p></td>
<td><p>セッションにはこのアクセス許可を与える必要があります。そうしないと、セッションはこの受信コネクタにメッセージを送信できません。セッションがこのアクセス許可を持っていない場合、MAIL FROM および AUTH コマンドは失敗します。</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-SMTP-Accept-Any-Recipient</p></td>
<td><p>このアクセス許可によって、セッションはこのコネクタを介してメッセージを中継できます。このアクセス許可が与えられていない場合、このコネクタでは、承認済みドメイン内の受信者宛てのメッセージのみが受け付けられます。</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-SMTP-Accept-Any-Sender</p></td>
<td><p>このアクセス許可によって、セッションは送信者アドレスのスプーフィング チェックを省略できます。</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-SMTP-Accept-Authoritative-Domain-Sender</p></td>
<td><p>このアクセス許可によって、権限のあるドメインに電子メール アドレスを持つ送信者はこの受信コネクタとのセッションを確立できます。</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-SMTP-Accept-Authentication-Flag</p></td>
<td><p>このアクセス許可によって、Exchange 2003 サーバーは内部の送信者からのメッセージを送信できます。Exchange 2010 は、このメッセージが内部のメッセージであると認識します。送信者はメッセージを &quot;信頼できる&quot; と宣言することができます。匿名の発信を通じて Exchange システムに入ってきたメッセージは、このフラグが信頼されていない状態に設定されて、Exchange 組織経由で中継されます。</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Accept-Headers-Routing</p></td>
<td><p>このアクセス許可によって、セッションは、すべての受信ヘッダーが変更されていないメッセージを送信できます。このアクセス許可が与えられていない場合、サーバーはすべての受信ヘッダーを削除します。</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Accept-Headers-Organization</p></td>
<td><p>このアクセス許可によって、セッションは、すべての組織ヘッダーが変更されていないメッセージを送信できます。組織ヘッダーはすべて、<strong>X-MS-Exchange-Organization-</strong> で始まります。このアクセス許可が与えられていない場合、受信側のサーバーはすべての組織ヘッダーを削除します。</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Accept-Headers-Forest</p></td>
<td><p>このアクセス許可によって、セッションは、すべてのフォレスト ヘッダーが変更されていないメッセージを送信できます。フォレスト ヘッダーはすべて、<strong>X-MS-Exchange-Forest-</strong> で始まります。このアクセス許可が与えられていない場合、受信側のサーバーはすべてのフォレスト ヘッダーを削除します。</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Accept-Exch50</p></td>
<td><p>このアクセス許可によって、セッションは XEXCH50 コマンドが含まれたメッセージを送信できます。このコマンドは、Exchange 2003 との相互運用に必要です。XEXCH50 コマンドは、メッセージの SCL (Spam Confidence Level) などのデータを提供します。</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Bypass-Message-Size-Limit</p></td>
<td><p>このアクセス許可によって、セッションは、コネクタで構成されているメッセージのサイズ制限を超えるメッセージを送信できます。</p></td>
</tr>
<tr class="odd">
<td><p>Ms-Exch-Bypass-Anti-Spam</p></td>
<td><p>このアクセス許可によって、セッションはスパム対策フィルターをバイパスできます。</p></td>
</tr>
</tbody>
</table>

