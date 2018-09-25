---
title: 'スパム対策スタンプ: Exchange 2013 Help'
TOCTitle: スパム対策スタンプ
ms:assetid: 28d3a5c2-8509-4b25-9876-763536e77c27
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa996878(v=EXCHG.150)
ms:contentKeyID: 49895307
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# スパム対策スタンプ

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

スパム対策スタンプは、スパムに関連する問題を診断するのに役立ちます。この機能は、インターネットからの受信メッセージをフィルタリングするためのスパム対策機能をメッセージが通過するとき、送信者固有の情報、パズル検証の結果、コンテンツ フィルターの結果などの診断メタデータ (スタンプ) を適用することによって、実行されます。スパム対策スタンプには Phishing Confidence Level スタンプ、Spam Confidence Level スタンプ、Sender ID スタンプの 3 種類があります。

スパム対策スタンプを診断ツールとして使用すると、各ユーザーが自分のメールボックスで受信した、誤ってスパムと判断されたメッセージやスパムと疑われるメッセージに対して、どのような処理を行うかを決定できます。

## スパム対策スタンプの表示

スパム対策スタンプは、Microsoft Outlook を使用して表示できます。詳細については、「[Outlook でのスパム対策スタンプの表示](view-anti-spam-stamps-in-outlook-exchange-2013-help.md)」を参照してください。

## スパム対策レポートについて

スパム対策レポートは、メール メッセージに適用されたスパム対策フィルターの結果の要約レポートです。コンテンツ フィルター エージェントは、次のような X-header の形式で、メッセージ エンベロープにこのスタンプを適用します。

```powershell
X-MS-Exchange-Organization-Antispam-Report: DV:<DATVersion>;CW:CustomList;PCL:PhishingVerdict <verdict>;P100:PhishingBlock;PP:Presolve;SID:SenderIDStatus <status>;TIME:<SendReceiveDelta>;MIME:MimeCompliance 
```

次の表は、スパム対策レポートに記載されることがあるフィルター情報を示します。


> [!NOTE]
> スパム対策レポートには、特定のメッセージに適用されたフィルターから得られた情報だけが表示されます。通常、スパム対策レポートには、次の表に示すすべての情報が含まれているわけではありません。たとえば、受信するスパム対策レポートは、次のようになります。<CODE>DV:3.1.3924.1409;SID:SenderIDStatus Fail;PCL:PhishingLevel SUSPICIOUS;CW:CustomList;PP:Presolved;TIME:TimeBasedFeatures</CODE>.



### スパム対策レポート内のフィルター情報

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>スタンプ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SID</p></td>
<td><p>Sender ID (SID) スタンプは、電子メールでのドメインの使用を承認する SPF (Sender Policy Framework) に基づきます。SPF は、メッセージ エンベロープでは <code>Received-SPF</code> として表示されます。Sender ID の評価処理によってメッセージの Sender ID の状態が生成されます。この状態は、次のいずれかの値として返されます。</p>
<ul>
<li><p><strong>Pass   </strong>IP アドレスと PRA (Purported Responsible Address) の両方が Sender ID の検証確認に合格しました。</p></li>
<li><p><strong>Neutral</strong>   発行された Sender ID のデータだけでは判断できないことを示します。</p></li>
<li><p><strong>Soft fail</strong>   PRA の IP アドレスは許可されていないセットに含まれている可能性があります。</p></li>
<li><p><strong>Fail   </strong>IP アドレスが許可されていません。受信メールで PRA が見つからないか、送信ドメインが存在しません。</p></li>
<li><p><strong>None   </strong>送信者の DNS 内に、公開されている SPF データが存在しません。</p></li>
<li><p><strong>TempError</strong>   DNS サーバーが使用できないなど、一時的な DNS エラーが発生しました。</p></li>
<li><p><strong>PermError   </strong>レコードの形式にエラーがあるなど、DNS レコードが無効です。</p></li>
</ul>
<p>Sender ID スタンプは、メッセージ エンベロープでは次のような X-header として表示されます。</p>

```powershell
X-MS-Exchange-Organization-SenderIdResult:<status>
```

<p>Sender ID の詳細については、「<a href="sender-id-exchange-2013-help.md">送信者 ID</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>DV</p></td>
<td><p>DAT バージョン (DV) スタンプは、メッセージのスキャンに使用されたスパム定義ファイルのバージョンを示します。</p></td>
</tr>
<tr class="odd">
<td><p>SA</p></td>
<td><p>署名処理 (SA) スタンプは、メッセージ内で見つかった署名が原因で、そのメッセージが回復または削除されたことを示します。</p></td>
</tr>
<tr class="even">
<td><p>SV</p></td>
<td><p>署名 DAT バージョン (SV) スタンプは、メッセージのスキャンに使用された署名ファイルのバージョンを示します。</p></td>
</tr>
<tr class="odd">
<td><p>PCL</p></td>
<td><p>PCL (Phishing Confidence Level) スタンプは、そのコンテンツに基づいてメッセージのレベルが表示され、コンテンツ フィルター エージェントによってメッセージを処理するときに適用されます。この状態は、次のいずれかの値として返されます。</p>
<ul>
<li><p><strong>Neutral   </strong>メッセージの内容がフィッシングされる可能性が低いことを示します。</p></li>
<li><p><strong>Suspicious   </strong>メッセージの内容がフィッシングされる可能性が高いことを示します。</p></li>
</ul>
<p>PCL 値の範囲は 1 ～ 8 です。 A PCL レベルが 1 ～ 3 の場合、<code>Neutral</code> の状態が返されます。これは、メッセージの内容がフィッシングされる可能性が低いことを意味します。PCL レベルが 4 ～ 8 の場合、<code>Suspicious</code> の状態が返されます。これは、メッセージがフィッシングされる可能性が高いことを意味します。</p>
<p>この値は、Outlook メッセージを処理する内容を決めるために使用されます。Outlook は PCL スタンプを使用し、疑わしいメッセージの内容をブロックします。</p>
<p>PCL スタンプは、メッセージ エンベロープでは次のような X-header として表示されます。</p>

```powershell
X-MS-Exchange-Organization-PCL:<status>
```

</td>
</tr>
<tr class="even">
<td><p>SCL</p></td>
<td><p>メッセージの SCL (Spam Confidence Level) スタンプは、内容に基づいたメッセージの評価レベルを示します。コンテンツ フィルター エージェントは、Microsoft SmartScreen テクノロジを使用してメッセージのコンテンツを評価し、各メッセージに SCL レベルを割り当てます。SCL の値は 0 ～ 9 の間です。0 はスパムである可能性が最も低く、9 はスパムである可能性が最も高いと見なされます。Exchange や Outlook で実行される処理は、SCL しきい値の設定によって異なります。</p>
<p>SCL スタンプは、メッセージ エンベロープでは次のような X-header として表示されます。</p>

```powershell
X-MS-Exchange-Organization-SCL:<status>
```

<p>SCL しきい値と処理の詳細については、「<a href="spam-confidence-level-threshold-exchange-2013-help.md">Spam Confidence Level のしきい値</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>CW</p></td>
<td><p>メッセージのカスタムの重み (CW) スタンプは、承認しない単語や語句がメッセージに含まれており、それらの承認しない単語や語句の SCL 値 (重み) が、最終的な SCL スコアに適用されたことを示します。</p>
<ul>
<li><p>承認しない単語や語句 (禁止語句) の重みは最大であるため、SCL スコアは 9 に変更されます。</p></li>
<li><p>承認する単語や語句 (許可語句) の重みは最小であるため、SCL スコアは 0 に変更されます。</p></li>
</ul>
<p>承認する単語や語句および承認しない単語や語句をコンテンツ フィルター エージェントに追加する方法の詳細については、「<a href="manage-content-filtering-exchange-2013-help.md">コンテンツ フィルターの管理</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>PP</p></td>
<td><p>解決済みパズル (PP) スタンプは、送信者のメッセージに、コンピューターによる解決済みの有効な消印が含まれているかどうかを示します。この消印は、Outlook の電子メールの消印検証機能に基づくもので、その送信者が悪意のある送信者である可能性が低いことを示します。この場合は、コンテンツ フィルター エージェントは SCL レベルを下げます。</p>
<p>電子メールの消印検証機能が有効になっていて、次のいずれかの条件に当てはまる場合、コンテンツ フィルター エージェントは SCL レベルを変更しません。</p>
<ul>
<li><p>受信メッセージにコンピュテーショナル消印ヘッダーが含まれていない。</p></li>
<li><p>コンピュテーショナル消印ヘッダーが無効である。</p></li>
</ul>
<p>消印の検証機能の詳細については、「<a href="content-filtering-exchange-2013-help.md">コンテンツ フィルター</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>TIME: TimeBasedFeatures</p></td>
<td><p>TIME スタンプは、メッセージが送信された時刻と受信された時刻の間に大幅な時間遅延があったことを示します。TIME スタンプは、メッセージの最終的な SCL レベルを決定するために使用されます。</p></td>
</tr>
<tr class="even">
<td><p>MIME:MIMECompliance</p></td>
<td><p>MIME スタンプは、その電子メール メッセージが MIME に準拠していないことを示します。</p></td>
</tr>
<tr class="odd">
<td><p>P100:PhishingBlock</p></td>
<td><p>P100 スタンプは、そのメッセージに、フィッシング定義ファイルに存在する URL が含まれていることを示します。</p></td>
</tr>
<tr class="even">
<td><p>IPOnAllowList</p></td>
<td><p>IPOnAllowList スタンプは、送信者の IP アドレスが IP 許可一覧に含まれていることを示します。IP 許可一覧の詳細については、「<a href="http://go.microsoft.com/fwlink/?linkid=268732">接続フィルターについて</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>MessageSecurityAntispamBypass</p></td>
<td><p>MessageSecurityAntispamBypass スタンプは、メッセージの内容がフィルター処理されなかったことと、送信者にはスパム対策フィルターをバイパスする許可が付与されていたことを示します。</p></td>
</tr>
<tr class="even">
<td><p>SenderBypassed</p></td>
<td><p>SenderBypassed スタンプは、この送信者から受信したメッセージに対して、コンテンツ フィルター エージェントがコンテンツ フィルターを一切適用しないことを示します。詳細については、「<a href="manage-content-filtering-exchange-2013-help.md">コンテンツ フィルターの管理</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>AllRecipientsBypassed</p></td>
<td><p>AllRecipientsBypassed スタンプは、メッセージに列挙されているすべての受信者について、次の条件のいずれかが満たされていることを示します。</p>
<ul>
<li><p>受信者のメールボックスの <em>AntispamBypassedEnabled</em> パラメーターが <code>$true</code> に設定されている。これは、管理者だけが <strong>Set-Mailbox</strong> コマンドレットを使用して設定できる受信者単位の設定です。</p></li>
<li><p>メッセージの送信者が受信者の  差出人セーフ リストに含まれている。差出人セーフ リストの詳細については、「<a href="manage-safelist-aggregation-exchange-2013-help.md">セーフリスト集約を管理する</a>」を参照してください。</p></li>
<li><p>コンテンツ フィルター エージェントが、この受信者に送信されるメッセージに対してコンテンツ フィルターを一切適用していない。受信者の例外の詳細については、「<a href="manage-content-filtering-exchange-2013-help.md">コンテンツ フィルターの管理</a>」を参照してください。</p></li>
</ul></td>
</tr>
</tbody>
</table>

