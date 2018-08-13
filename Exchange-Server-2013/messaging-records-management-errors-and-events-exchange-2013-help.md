---
title: 'メッセージング レコード管理のエラーおよびイベント: Exchange 2013 Help'
TOCTitle: メッセージング レコード管理のエラーおよびイベント
ms:assetid: 8bc3f5ae-403b-45af-86c1-b2fccab34e63
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb310783(v=EXCHG.150)
ms:contentKeyID: 51407555
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メッセージング レコード管理のエラーおよびイベント

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

メッセージング レコード管理 (MRM) では、生成されるイベントをイベント ビューアーで表示できます。これによって、管理フォルダー アシスタントのパフォーマンスをトラブルシューティングおよび確認することができます。イベント ビューアーでは、重要度に基づいて次に示す種類のイベントが次の順序で記録されます。

1.  エラー イベント

2.  警告イベント

3.  情報イベント

## MRM のエラーおよびイベント

次の表に、MRM のトラブルシューティングに使用できるイベントの一覧を示します。ログ出力の種類には、次のものがあります。

  - **\[LogAlways\]** のラベルが付けられたイベントは常に個別にログ出力されます。

  - **\[LogPeriodic\]** のラベルが付けられたイベントは発生するたびにログ出力されるのではなく、5 分間に 1 回だけログ出力されます。これによって、ログ エントリが過剰に出力されることを防ぎます。

### 管理フォルダー アシスタント カテゴリの MRM イベント

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>イベント ID</strong></th>
<th><strong>カテゴリ</strong></th>
<th><strong>イベントの種類</strong></th>
<th><strong>ログ</strong></th>
<th><strong>値または説明</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>10003</p></td>
<td><p>管理フォルダー アシスタント</p></td>
<td><p>エラー</p></td>
<td><p>LogPeriodic</p></td>
<td><p>Active Directory からサーバーの構成オブジェクトを取得できませんでした。&lt;<em>例外の詳細</em>&gt;。ドメイン コントローラーのネットワーク接続に問題がないかどうか、または DNS の構成が正しいかどうかを確認してください。</p></td>
</tr>
<tr class="even">
<td><p>10004</p></td>
<td><p>管理フォルダー アシスタント</p></td>
<td><p>エラー</p></td>
<td><p>LogAlways</p></td>
<td><p>メールボックス &lt;<em>メールボックス</em>&gt; のフォルダー &lt;<em>フォルダー</em>&gt; のアイテム保持ポリシーは適用されません。管理フォルダー アシスタントは、管理フォルダー &lt;<em>管理フォルダー</em>&gt; に対する管理コンテンツの設定 &lt;<em>コンテンツの設定</em>&gt; を処理できません。RetentionAction は MoveToFolder ですが、移動先のフォルダーが指定されていませんでした。移動先となるフォルダーを指定してください。</p></td>
</tr>
<tr class="odd">
<td><p>10005</p></td>
<td><p>管理フォルダー アシスタント</p></td>
<td><p>エラー</p></td>
<td><p>常に出力</p></td>
<td><p>メールボックス &lt;<em>メールボックス</em>&gt; のフォルダー &lt;<em>フォルダー</em>&gt; に対して、アイテム保持ポリシーは適用されません。管理フォルダー &lt;<em>管理フォルダー</em>&gt; に対する管理コンテンツの設定 &lt;<em>コンテンツの設定</em>&gt; を処理できません。RetentionAction は MoveToFolder ですが、移動先のフォルダー &lt;<em>フォルダー</em>&gt; が移動元のフォルダー &lt;<em>フォルダー</em>&gt; と同じです。移動元のフォルダーとは異なる移動先のフォルダーを指定してください。</p></td>
</tr>
<tr class="even">
<td><p>10009</p></td>
<td><p>管理フォルダー アシスタント</p></td>
<td><p>エラー</p></td>
<td><p>常に出力</p></td>
<td><p>管理フォルダー アシスタントは Active Directory から監査ログのパラメーターを読み取ることができなかったため、ローカル サーバーですべてのデータベースの処理をスキップしました。スケジュールされた時間帯に、後で再試行します。現在のデータベース:&lt;<em>データベース</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>10010</p></td>
<td><p>管理フォルダー アシスタント</p></td>
<td><p>エラー</p></td>
<td><p>常に出力</p></td>
<td><p>監査ログは有効になっていますが、監査ログへのパスが Active Directory にないため、管理フォルダー アシスタントはローカル サーバーですべてのデータベースの処理をスキップしました。スケジュールされた時間帯に、後で再試行します。現在のデータベース:&lt;<em>データベース</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>10011</p></td>
<td><p>管理フォルダー アシスタント</p></td>
<td><p>エラー</p></td>
<td><p>常に出力</p></td>
<td><p>管理フォルダー アシスタントは監査ログを構成できませんでした。現在のデータベースの処理は中止されます:'%1'. スケジュールされた時間帯に、後で再試行します。例外の詳細: &lt;<em>詳細</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>10012</p></td>
<td><p>管理フォルダー アシスタント</p></td>
<td><p>エラー</p></td>
<td><p>常に出力</p></td>
<td><p>管理フォルダー アシスタントは監査ログへの書き込みを行いませんでした。現在のデータベースの処理は中止されます:&lt;<em>データベース</em>&gt;。監査ログへの書き込みは、スケジュールされた時間帯に後で再試行されます。例外の詳細: &lt;<em>詳細</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>10017</p></td>
<td><p>管理フォルダー アシスタント</p></td>
<td><p>エラー</p></td>
<td><p>常に出力</p></td>
<td><p>メールボックス:&lt;<em>メールボックス</em>&gt; フォルダー:名前 : &lt;<em>フォルダー名</em>&gt; ID:&lt;<em>フォルダー ID</em>&gt; 項目:ID:&lt;<em>ID</em>&gt;。例外：&lt;<em>例外</em>&gt; を処理しているときに、管理フォルダー アシスタントで例外が発生しました。</p></td>
</tr>
</tbody>
</table>


### アシスタント カテゴリの MRM イベント

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>イベント ID</strong></th>
<th><strong>カテゴリ</strong></th>
<th><strong>イベントの種類</strong></th>
<th><strong>ログ出力</strong></th>
<th><strong>値または説明</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>9004</p></td>
<td><p>アシスタント</p></td>
<td><p>警告</p></td>
<td><p>常に出力</p></td>
<td><p>サービス &lt;<em>サービス</em>&gt;。&lt;<em>サービス</em>&gt; は、メールボックス &lt;<em>メールボックス</em>&gt; を処理できませんでした。次の例外がエラーの原因です。&lt;<em>例外</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9014</p></td>
<td><p>アシスタント</p></td>
<td><p>警告</p></td>
<td><p>常に出力</p></td>
<td><p>サービス &lt;<em>サービス</em>&gt;。スケジュールの変更を処理できません。次の例外がエラーの原因です。&lt;<em>例外</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9017</p></td>
<td><p>アシスタント</p></td>
<td><p>情報</p></td>
<td><p>常に出力</p></td>
<td><p>サービス &lt;<em>サービス</em>&gt;。データベース &lt;<em>データベース</em>&gt; の &lt;<em>サービス</em>&gt; を行う時間帯に入りました。処理が必要なメールボックスが &lt;<em>数</em>&gt; 個あります。</p></td>
</tr>
<tr class="even">
<td><p>9018</p></td>
<td><p>アシスタント</p></td>
<td><p>情報</p></td>
<td><p>常に出力</p></td>
<td><p>サービス &lt;<em>サービス</em>&gt;。データベース &lt;<em>データベース</em>&gt; の &lt;<em>サービス</em>&gt; はスケジュールされた時間帯を抜けようとしています。&lt;<em>数</em>&gt; 個の中の &lt;<em>数</em>&gt; 個のメールボックスが正常に処理されました。&lt;<em>数</em>&gt; 個のメールボックスがエラーのためスキップされました。&lt;<em>数</em>&gt; 個のメールボックスが個別に処理されました。&lt;<em>数</em>&gt; 個のメールボックスが時間不足のため処理されませんでした。</p>

> [!NOTE]
> 管理フォルダー アシスタントは次回の処理実行時に前回処理を中断したところから再開します。


</td>
</tr>
<tr class="odd">
<td><p>9019</p></td>
<td><p>アシスタント</p></td>
<td><p>警告</p></td>
<td><p>定期的に出力</p></td>
<td><p>サービス &lt;<em>サービス</em>&gt;。データベース &lt;<em>データベース</em>&gt; の &lt;<em>サービス</em>&gt; の進行状況を保存できません (アシスタントは次回の再開時に前回処理を中断したところから再開できるように中断したところを保存できませんでした)。次の例外がエラーの原因です。&lt;<em>例外</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9020</p></td>
<td><p>アシスタント</p></td>
<td><p>警告</p></td>
<td><p>常に出力</p></td>
<td><p>サービス &lt;<em>サービス</em>&gt;。データベース &lt;<em>データベース</em>&gt; に対して &lt;<em>アシスタント名</em>&gt; を開始できませんでした。次の例外がエラーの原因です。&lt;<em>例外</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9021</p></td>
<td><p>アシスタント</p></td>
<td><p>情報</p></td>
<td><p>常に出力</p></td>
<td><p>サービス &lt;<em>サービス</em>&gt;。データベース &lt;<em>データベース</em>&gt; の &lt;<em>サービス</em>&gt; は、オンデマンド要求を処理しています。処理が必要なメールボックスが &lt;<em>数</em>&gt; 個あります。</p></td>
</tr>
<tr class="even">
<td><p>9022</p></td>
<td><p>アシスタント</p></td>
<td><p>情報</p></td>
<td><p>常に出力</p></td>
<td><p>サービス &lt;<em>サービス</em>&gt;。データベース &lt;<em>データベース</em>&gt; の &lt;<em>サービス</em>&gt; がオンデマンド要求を終了しました。&lt;<em>数</em>&gt; 個の中の &lt;<em>数</em>&gt; 個のメールボックスが正常に処理されました。&lt;<em>数</em>&gt; 個のメールボックスがエラーのためスキップされました。</p></td>
</tr>
<tr class="odd">
<td><p>9023</p></td>
<td><p>アシスタント</p></td>
<td><p>警告</p></td>
<td><p>常に出力</p></td>
<td><p>サービス &lt;<em>サービス</em>&gt;。&lt;<em>サービス</em>&gt; はデータベース &lt;<em>データベース</em>&gt; に対するタイム ウィンドウ処理を開始できませんでした。次の例外がエラーの原因です。&lt;<em>例外</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9025</p></td>
<td><p>アシスタント</p></td>
<td><p>情報</p></td>
<td><p>常に出力</p></td>
<td><p>サービス &lt;<em>サービス</em>&gt;。&lt;<em>サービス</em>&gt; は、データベース &lt;<em>データベース</em>&gt; の &lt;<em>数</em>&gt; 個のメールボックスをスキップしました。メールボックス : &lt;<em>メールボックス</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9026</p></td>
<td><p>アシスタント</p></td>
<td><p>警告</p></td>
<td><p>常に出力</p></td>
<td><p>サービス &lt;<em>サービス</em>&gt;。&lt;<em>サービス</em>&gt; はデータベース &lt;<em>データベース</em>&gt; に対するオンデマンド処理を開始できませんでした。次の例外がエラーの原因です。&lt;<em>例外</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9027</p></td>
<td><p>アシスタント</p></td>
<td><p>エラー</p></td>
<td><p>常に出力</p></td>
<td><p>サービス &lt;<em>サービス</em>&gt;。データベース &lt;<em>データベース</em>&gt; のメールボックス &lt;<em>メールボックス</em>&gt; を処理しているときに、&lt;<em>サービス</em>&gt; によりプロセスが &lt;<em>数</em>&gt; 回終了しました。このメールボックスは、要求されたタイム ウィンドウまたはオンデマンド要求で処理されません。次の例外がエラーの原因です。&lt;<em>例外</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9028</p></td>
<td><p>アシスタント</p></td>
<td><p>警告</p></td>
<td><p>常に出力</p></td>
<td><p>サービス &lt;<em>サービス</em>&gt;。データベース &lt;<em>データベース</em>&gt; のメールボックス &lt;<em>メールボックス</em>&gt; を処理しているときに、&lt;<em>サービス</em>&gt; によりプロセスが &lt;<em>数</em>&gt; 回終了しました。次の例外がエラーの原因です。&lt;<em>例外</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9033</p></td>
<td><p>アシスタント</p></td>
<td><p>警告</p></td>
<td><p>常に出力</p></td>
<td><p>サービス &lt;<em>サービス</em>&gt;。データベース &lt;<em>データベース</em>&gt; の &lt;<em>サービス</em>&gt; は、オンデマンド要求を受信しました。ただし、処理するメールボックスがありません。</p></td>
</tr>
<tr class="odd">
<td><p>9034</p></td>
<td><p>アシスタント</p></td>
<td><p>情報</p></td>
<td><p>常に出力</p></td>
<td><p>サービス &lt;<em>サービス</em>&gt; は、データベース &lt;<em>データベース</em>&gt; での管理フォルダー アシスタントに対する時間ベースの処理を中止しました。</p></td>
</tr>
<tr class="even">
<td><p>9035</p></td>
<td><p>アシスタント</p></td>
<td><p>警告</p></td>
<td><p>常に出力</p></td>
<td><p>サービス &lt;<em>サービス</em>&gt;。時間不足のため、&lt;<em>アシスタント名</em>&gt; は &lt;<em>数</em>&gt; 個のメールボックスを処理できませんでした。</p></td>
</tr>
<tr class="odd">
<td><p>9037</p></td>
<td><p>アシスタント</p></td>
<td><p>エラー</p></td>
<td><p>常に出力</p></td>
<td><p>サービス &lt;<em>サービス</em>&gt;。RPC を処理しているときに例外が発生しました。方法:&lt;<em>方法</em>&gt; 例外:&lt;<em>例外</em>&gt;</p></td>
</tr>
</tbody>
</table>

