---
title: 'キューのフィルター: Exchange 2013 Help'
TOCTitle: キューのフィルター
ms:assetid: fbfbdcab-e0d2-4ed9-8f7f-e5fa2c87360d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb125237(v=EXCHG.150)
ms:contentKeyID: 49896566
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# キューのフィルター

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

フィルターにより、さまざまなキューのビューが生成されます。フィルター オプションとして、キューのプロパティを使用します。フィルター条件を指定することにより、すばやくキューを見つけ出し、それに対する処理を実行することができます。以下のシナリオは、キューのフィルター処理を使用してメール フローを管理する方法の例です。

  - Microsoft System Center Operations Manager から、キューの長さが設定されたしきい値を超えたことを示すメッセージを受け取りました。メール フローに関する問題がサーバー全体に存在しているのかどうかを調べる必要があります。
    
    この場合、メッセージ数が標準と考えられる数を超えているキューがすべて表示されるフィルターを作成できます。メール フローに関する問題が示された場合、フィルターの結果の中からすべてのキューを選択し、調査を継続している間、キューを一時的に中断することができます。

  - メール フローに関する問題の原因を調査するために、いくつかのキューを中断します。コネクタの構成が正しくないことが問題の原因であったことが判明し、修正されました。
    
    状態が "中断" になっているキューがすべて表示されるフィルターを作成し、フィルターの結果からすべてのキューを選択して、再開することができます。

## キューのフィルター処理に使用するキューのプロパティ

フィルターを作成して、特定の条件を満たすキューを見つけるために、キューのプロパティを使用することができます。キュー ビューアーで、またはキュー管理コマンドレットの *Filter* パラメーターを使用してフィルターを作成できます。なお、キュー管理コマンドレットは、キュー ビューアーより多くのフィルター処理可能なプロパティをサポートしています。次の表に、フィルターに使用できるキュー プロパティとそれぞれの有効な値を示します。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>キュー ビューアーのキュー プロパティ</th>
<th>シェルのキュー プロパティ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>該当なし</p></td>
<td><p><code>DeferredMessageCount</code></p></td>
<td><p>このプロパティは、受信者の解決中に発生した一時エラーのために、送信キューに戻されたメッセージの数を示します。延期されたメッセージの詳細については、「<a href="recipient-resolution-exchange-2013-help.md">受信者の解決</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong>[配信の種類]</strong></p></td>
<td><p><code>DeliveryType</code></p></td>
<td><p><strong>DeliveryType</strong> の有効な値については、「<a href="queues-exchange-2013-help.md">キュー</a>」の「NextHopSolutionKey」セクションで説明します。</p></td>
</tr>
<tr class="odd">
<td><p>該当なし</p></td>
<td><p><code>Identity</code></p></td>
<td><p>このプロパティは、<em>&lt;Server&gt;\&lt;Queue&gt;</em> の形式のキューの ID です。詳細については、「<a href="queues-exchange-2013-help.md">キュー</a>」の「キュー ID」セクションを参照してください。</p></td>
</tr>
<tr class="even">
<td><p>該当なし</p></td>
<td><p><code>IncomingRate</code></p></td>
<td><p>このプロパティは、メッセージがキューに入る速度を算出した数値です。詳細については、「<a href="queues-exchange-2013-help.md">キュー</a>」の「IncomingRate、OutgoingRate、および Velocity」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>[最新のエラー]</strong></p></td>
<td><p><code>LastError</code></p></td>
<td><p>このプロパティは、キューに関して記録された最新のエラーのテキスト文字列を示します。</p></td>
</tr>
<tr class="even">
<td><p><strong>[最終再試行時刻]</strong></p></td>
<td><p><code>LastRetryTime</code></p></td>
<td><p>このプロパティは、状態が &quot;<code>Retry</code>&quot; になっているキューに対して最後に接続を試行した日時を示します。</p></td>
</tr>
<tr class="odd">
<td><p>該当なし</p></td>
<td><p><code>LockedMessageCount</code></p></td>
<td><p>このプロパティは、Microsoft の内部使用目的に予約されており、社内 Exchange 2013 組織では使用されません。</p></td>
</tr>
<tr class="even">
<td><p><strong>[メッセージ数]</strong></p></td>
<td><p><code>MessageCount</code></p></td>
<td><p>このプロパティは、キューに入っているメッセージの数を示します。</p></td>
</tr>
<tr class="odd">
<td><p>該当なし</p></td>
<td><p><code>NextHopCategory</code></p></td>
<td><p>このプロパティは、キューの次ホップを <code>Internal</code> または <code>External</code> として指定し、キューの <strong>DeliveryType</strong> プロパティの値に基づきます。詳細については、「<a href="queues-exchange-2013-help.md">キュー</a>」の「NextHopSolutionKey」セクションを参照してください。</p></td>
</tr>
<tr class="even">
<td><p>該当なし</p></td>
<td><p><code>NextHopConnector</code></p></td>
<td><p>このプロパティは、次ホップの GUID で、キューの <strong>DeliveryType</strong> プロパティの値に基づきます。詳細については、「<a href="queues-exchange-2013-help.md">キュー</a>」の「NextHopSolutionKey」セクションを参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>[次ホップ ドメイン]</strong></p></td>
<td><p><code>NextHopDomain</code></p></td>
<td><p>このプロパティは、次ホップの名前で、キューの <strong>DeliveryType</strong> プロパティの値に基づきます。詳細については、「<a href="queues-exchange-2013-help.md">キュー</a>」の「NextHopSolutionKey」セクションを参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong>[次の再試行時刻]</strong></p></td>
<td><p><code>NextRetryTime</code></p></td>
<td><p>このプロパティは、状態が &quot;<code>Retry</code>&quot; になっているキューに対して次に接続を試行する日時を示します。</p></td>
</tr>
<tr class="odd">
<td><p>該当なし</p></td>
<td><p><code>OutgoingRate</code></p></td>
<td><p>このプロパティは、メッセージがキューから出ていく速度を算出した数値です。詳細については、「<a href="queues-exchange-2013-help.md">キュー</a>」の「IncomingRate、OutgoingRate、および Velocity」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>該当なし</p></td>
<td><p><code>RiskLevel</code></p></td>
<td><p>このプロパティは、Microsoft の内部使用目的に予約されており、社内 Exchange 2013 組織では使用されません。</p></td>
</tr>
<tr class="odd">
<td><p><strong>状態</strong></p></td>
<td><p><code>Status</code></p></td>
<td><p>このプロパティは、現在のキューの状態を示します。キューの状態値は、アクティブ、接続中、なし、中断、準備完了、または再試行のいずれかになります。詳細については、「<a href="queues-exchange-2013-help.md">キュー</a>」の「キューの状態」セクションを参照してください。</p></td>
</tr>
<tr class="even">
<td><p>該当なし</p></td>
<td><p><code>TlsDomain</code></p></td>
<td><p>ドメインにドメイン セキュリティが構成されている場合、このプロパティには送信先ドメインの FQDN が含まれます。</p></td>
</tr>
<tr class="odd">
<td><p>該当なし</p></td>
<td><p><code>Velocity</code></p></td>
<td><p>このプロパティには、キューがどの程度効率的にドレインしているかを算出した数値が含まれます。詳細については、「<a href="queues-exchange-2013-help.md">キュー</a>」の「IncomingRate、OutgoingRate、および Velocity」を参照してください。</p></td>
</tr>
</tbody>
</table>

