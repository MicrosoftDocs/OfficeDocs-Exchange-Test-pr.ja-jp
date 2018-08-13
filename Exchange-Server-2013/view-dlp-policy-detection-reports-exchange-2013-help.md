---
title: 'DLP ポリシー検出のレポートの表示: Exchange 2013 Help'
TOCTitle: DLP ポリシー検出のレポートの表示
ms:assetid: 5c3f1cf6-d8c7-4d83-bb24-641ea9d50cbc
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ150520(v=EXCHG.150)
ms:contentKeyID: 48269029
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# DLP ポリシー検出のレポートの表示

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-16_

データ損失防止 (DLP) ポリシー検出管理では、組織が DLP ポリシー違反を特定、調査し、解決するために実行するアクティビティを広範に定義します。インシデントを管理するには、DLP ポリシーが検出した内容を特定する情報にアクセスする必要があります。この検出情報は既存の Microsoft Exchange Server 2013 データおよびログ形式と統合されるため、すでに存在する豊富なデータ システムを活用してメール フロー インシデントを管理できます。

単一のポリシー検出イベントに沿ったインシデント レポートの作成方法の詳細については、「[DLP ポリシー検出のインシデント レポートの作成](create-incident-reports-for-dlp-policy-detections-exchange-2013-help.md)」を参照してください。メッセージ ログの詳細については、「[配信レポートによるメッセージの追跡](track-messages-with-delivery-reports-exchange-2013-help.md)」を参照してください。


> [!NOTE]
> Exchange 2013: DLP は、Exchange エンタープライズ クライアント アクセス ライセンス (CAL) が必要なプレミアム機能です。CAL とサーバー ライセンスの詳細については、「<A href="https://go.microsoft.com/fwlink/p/?linkid=237292">Project のヘルプ</A>」を参照してください。



## 監査情報

Exchange での DLP 検出管理に関連するデータは、配信レポートとも呼ばれるメッセージ追跡ログに統合されています。この機能は、システムで使用可能な既存のロギング フレームワークの多くを再利用します。メッセージ追跡ログ ファイルの構造を含む概要については、「[メッセージ追跡について](message-tracking-exchange-2013-help.md)」または「[配信レポートによるメッセージの追跡](track-messages-with-delivery-reports-exchange-2013-help.md)」にある内容を確認してください。

配信レポートは、メールボックス サーバー上でトランスポート サービスを実行しているコンピューターの間でメッセージが転送されるときのすべてのメッセージ アクティビティに関する詳細なログです。メッセージ追跡ログは、Exchange 管理シェルを介して **Get-MessageTrackingLog** コマンドレットを使用するとアクセスできます。DLP データは、既存のデータ形式および規則に従い、配信レポートに統合されます。

## データ ログの書式

メッセージ追跡ログには、メール フロー コンテンツの処理に関与するエージェントからのデータが含まれています。DLP では、トランスポート ルール エージェント (TRA) を使用して、ディープ メッセージ コンテンツ スキャンを呼び出し、ETR の一部として定義されたポリシーを適用します。メッセージ追跡ログに DLP 関連エントリを追加するには、既存の AgentInfo イベントを使用します。

AgentInfo イベントにおけるエージェント名は **TRA** (**トランスポート ルール エージェント**) です。メッセージに適用された DLP 処理を説明するメッセージごとに、1 つの AgentInfo イベントがログに記録されます。メッセージ追跡ログ エントリ フィールドの **CustomData** フィールドには、トランスポート ルール エージェントによって記録された DLP データが表示されます。このフィールドは、複数のエントリを含めることができます。メッセージ内のデータ分類ごとにデータ分類/クライアント情報が 1 行、メッセージに適用されるルールごとにルール情報が 1 行、読み込み時間または実行時間のしきい値を超過するルールごとに状態監視情報が 1 行あります。

以下は、DLP ログ エントリの例です。出力の書式は、文字列を別々の行に表示し、行と行の間を 1 行空けるように設定されています。

ソース : AGENT

EventId:AGENTINFO

CustomData:S:TRA=DC|dcid=41BFDBC6C9D811E0816A3CD34824019B|count=10|conf=77;

S:TRA=DC|dcid=C7ECCBA0CA0011E0B6C00B124924019B|count=3|conf=81;

S:TRA=CI|sndOverride=or|just=Business Reason;

S:TRA=CI|sndOverride=fp;

S:TRA=ETR|ruleId=FC2AA60C9D811E0AFC076D34824019B|dlpid=1B81CC82C9DB11E09052C5D64824019B|st=2010-11-03 15:30T|action=PrependSubject|action=Encrypt|sev=2|mode=audit|dcid=41BFDBC6C9D811E0816A3CD34824019B|sndOverride=or;

S:TRA=ETR|ruleId=AB2AA60C9D811E0AFC076D34824019B|dlpid=1B81CC82C9DB11E09052C5D64824019B|st=2010-11-03 15:30T|action=Encrypt|sev=1|mode=enabled|dcid=C7ECCBA0CA0011E0B6C00B124924019B|sndOverride=fp;

S:TRA=ETRP|ruleId=C27D21EECA0311E0BCB896154924019B|LoadW=200|LoadC=100|ExecW=5500|ExecC=200;

トランスポート ルール エージェントでは、ルール ID (ログ行内の "TRA=ETR" で示されます) に基づいて、ルール ID、DLP ポリシー ID (オプション)、最終変更日時、アクション、重大度、モード、検出されたデータ分類 (オプション)、および送信者上書き (オプション) をグループ化する必要があります。また、データ分類 ID、カウント、および分類の信頼レベルも、分類名 (ログ行内の "TRA=DC" で示されます) でグループ化する必要があります。

さらに、クライアント上で検出されたすべての分類データの分類 ID (ログ行内の "TRA=CI" で示されます) に基づいて、データ分類 ID、送信者上書き (オプション)、および上書きの妥当性 (オプション) もグループ化する必要があります。トランスポート ルール エージェントでは、ルール ID、読み込みウォール クロック (オプション)、読み込み CPU クロック (オプション)、および実行 CPU クロック (オプション) のグループ化が要求されます。このグループ化は、読み込み/実行ウォール クロックのしきい値または CPU クロックのしきい値を超過するすべてのルールについて、ルール ID をもとに行われます (ログ行内の "TRA=ETRP" で示されます)。

以下は、すべてのデータ フィールドの一覧です。メッセージ追跡ログ内のすべてのデータは文字列型です。形式列は、メッセージ追跡ログ内の各フィールドの認識方法についての説明です。オプション フィールド列には、ルールに一致してもログに記録されない可能性があるフィールドが記されています。DLP 固有列には、DLP 機能に固有のフィールドが記されています。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>フィールド名</strong></p></td>
<td><p><strong>説明</strong></p></td>
<td><p><strong>形式</strong></p></td>
<td><p><strong>オプション フィールド</strong></p></td>
<td><p><strong>DLP 固有</strong></p></td>
</tr>
<tr class="even">
<td><p>TRA</p></td>
<td><p>トランスポート ルール エージェント (AgentName 型)</p></td>
<td><p>TRA=DC、ETR、CI、または ETRP</p></td>
<td><p>必須</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>DC</p></td>
<td><p>データ分類 (groupName 型)</p></td>
<td><p>TRA=DC</p></td>
<td><p>省略可能</p></td>
<td><p>○</p></td>
</tr>
<tr class="even">
<td><p>ETR</p></td>
<td><p>Exchange トランスポート ルール (groupName 型)</p></td>
<td><p>TRA=ETR</p></td>
<td><p>必須</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>CI</p></td>
<td><p>クライアント情報 (groupName 型)</p></td>
<td><p>TRA=CI</p></td>
<td><p>省略可能</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p>ETRP</p></td>
<td><p>Exchange トランスポート ルール パフォーマンス (groupName 型)</p></td>
<td><p>TRA=ETRP</p></td>
<td><p>省略可能</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>dcid</p></td>
<td><p>データ分類の ID</p></td>
<td><p>dcid=GUID</p></td>
<td><p>省略可能</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p>count</p></td>
<td><p>データ分類のカウント</p></td>
<td><p>count= 整数</p></td>
<td><p>省略可能</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p>conf</p></td>
<td><p>データ分類の信頼レベル</p></td>
<td><p>conf= 整数 (%)</p></td>
<td><p>省略可能</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p>sndOverride</p></td>
<td><p>送信者の上書き。省略可能フィールド。</p>
<p>TRA=CI 行で、フィールドが &quot;or&quot; に設定されている場合、データ分類が上書きされたことを示します。フィールドが &quot;fp&quot; に設定されている場合、データ分類が誤検知として通知されたことを示します。</p>
<p>TRA=ETR 行で、フィールドが &quot;or&quot; に設定されている場合、ルールまたはルールの一部が上書きされたことを示します。フィールドが &quot;fp&quot; に設定されている場合、ルールまたはルールの一部が誤検知として通知されたことを示します。</p></td>
<td><p>sndOverride=or または fp</p>
<p>ここで、&quot;or&quot; は上書きを表し、&quot;fp&quot; は誤検知を意味します。sndOverride フィールドは、エンド ユーザーがルールに対して上書きまたは誤検出を報告した場合に、表示されます。</p></td>
<td><p>省略可能</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p>just</p></td>
<td><p>正当性。省略可能フィールド。送信者の上書きフィールドが TRA=CI 行内の &quot;or&quot; に等しい場合にのみ利用できます。エンド ユーザーがデータ分類を上書きする正当な理由を提供するテキスト。</p></td>
<td><p>just=IW (正当な理由の文字列を入力)</p>
<p>正当性フィールドは、エンド ユーザーが上書きを報告した場合にのみログに記録されます。</p></td>
<td><p>省略可能</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p>ruleId</p></td>
<td><p>ルールの ID</p></td>
<td><p>ruleId=GUID</p></td>
<td><p>必須</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>dlpId</p></td>
<td><p>DLP ポリシーの ID。フィールドは省略可能です。dlpId が存在しない場合、ルールは DLP ポリシーに属しません。</p></td>
<td><p>dlpId=GUID</p></td>
<td><p>省略可能</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p>st</p></td>
<td><p>ルールの最終変更日時</p></td>
<td><p>st=UTC 日時</p></td>
<td><p>必須</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>アクション</p></td>
<td><p>ルールによって実行されるアクション。1 つのルールに対して複数のアクションが実行される場合があります。</p></td>
<td><p>action=1 つのアクション</p>
<p>1 つのルールに対して複数のアクションが存在する場合、複数のアクション フィールドが存在します。</p></td>
<td><p>必須</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>sev</p></td>
<td><p>ルールの監査重要度</p></td>
<td><p>sev=1、2、または 3</p>
<p>ここで、1 は &quot;低&quot;、2 は &quot;中&quot;、3 は &quot;高&quot; を表します。</p></td>
<td><p>省略可能</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>mode</p></td>
<td><p>ルールが該当したときのルールの状態 (enforcement、audit、または auditandnotify)。</p></td>
<td><p>mode=audit、auditandnotify、または enforcement</p></td>
<td><p>必須</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>loadW</p></td>
<td><p>読み込みウォール クロック。省略可能フィールド</p></td>
<td><p>loadW= 時間 (ミリ秒)</p></td>
<td><p>省略可能</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>loadC</p></td>
<td><p>読み込み CPU クロック。省略可能フィールド</p></td>
<td><p>loadC= 時間 (ミリ秒)</p></td>
<td><p>省略可能</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>execW</p></td>
<td><p>実行ウォール クロック。省略可能フィールド</p></td>
<td><p>execW= 時間 (ミリ秒)</p></td>
<td><p>省略可能</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>execC</p></td>
<td><p>実行 CPU クロック。省略可能フィールド</p></td>
<td><p>execC= 時間 (ミリ秒)</p></td>
<td><p>省略可能</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>message-id</p></td>
<td><p>メッセージの ID</p></td>
<td><p>message-id= メッセージの ID</p></td>
<td><p>必須</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>date-time</p></td>
<td><p>メッセージが送信された日時 (UTC)</p></td>
<td><p>date-time=UTC 日時</p></td>
<td><p>必須</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>sender-address</p></td>
<td><p>送信者フィールドに指定された電子メール アドレス</p></td>
<td><p>sender-address= 電子メール アドレス</p></td>
<td><p>必須</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>recipient-address</p></td>
<td><p>メッセージ受信者の電子メール アドレス</p></td>
<td><p>recipient-address= 電子メール アドレス</p></td>
<td><p>必須</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>message-subject</p></td>
<td><p>メッセージの件名フィールド内のデータ</p></td>
<td><p>message-subject= エンドユーザーが入力する件名文字列</p></td>
<td><p>必須</p></td>
<td><p>いいえ</p></td>
</tr>
</tbody>
</table>


## 詳細情報

[データ損失防止](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[DLP ポリシー検出のインシデント レポートの作成](create-incident-reports-for-dlp-policy-detections-exchange-2013-help.md)

[配信レポートによるメッセージの追跡](track-messages-with-delivery-reports-exchange-2013-help.md)

