---
title: 'バック プレッシャ: Exchange 2013 Help'
TOCTitle: バック プレッシャ
ms:assetid: 03003544-e802-4988-9427-5fc4da64dcb8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb201658(v=EXCHG.150)
ms:contentKeyID: 52057792
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# バック プレッシャ

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-03-09_

バック プレッシャは、Microsoft Exchange 2013 メールボックス サーバーとエッジ トランスポート サーバーに存在する、Microsoft Exchange トランスポート サービスのシステム リソース監視機能です。

Exchange は、使用可能なハード ドライブ領域やメモリなどの重要なリソースが圧迫されていて、サービスが利用不可になるのを防止するために対応策を取る時点を検出できます。バック プレッシャにより、システム リソースに最大の負荷がかかるのを防止でき、Exchange サーバーは既存のメッセージを処理してから新しいメッセージを受け入れようとします。システム リソースの使用率が通常のレベルに戻ると、Exchange サーバーは段階的に通常の動作を再開し、新しいメッセージを再び受け入れ始めます。

Exchange 2013 では、メールボックス サーバーまたはエッジ トランスポート サーバーのトランスポート サービスでリソースが圧迫されていると、受信接続は受け入れられますが、この接続による受信メッセージは低速で受け入れられるか拒否されます。リソースが圧迫されている Exchange サーバーに SMTP ホストが接続しようとすると、接続は正常に処理されます。ただし、ホストが **MAIL FROM** コマンドを実行してメッセージを送信すると、圧迫されているリソースに応じて、トランスポート サービスでは **MAIL FROM** コマンドの受信確認が遅れるか接続が拒否されます。

**目次**

監視対象リソース

リソースが圧迫されている状態で Exchange Transport が実行する処理

EdgeTransport.exe.config ファイルのバック プレッシャ構成オプション

バック プレッシャのログ情報

## 監視対象リソース

バック プレッシャ機能の一部として、次のシステム リソースが監視されます。

  - メッセージ キュー データベースを格納するハード ドライブの空き容量

  - メッセージ キュー データベース トランザクション ログを格納するハード ドライブの空き容量

  - メモリ内に存在するコミットされていないメッセージ キュー データベース トランザクションの数

  - EdgeTransport.exe プロセスで使用されているメモリ

  - 他のすべてのプロセスで使用されているメモリ

  - 送信キュー内のメッセージの数。

メールボックス サーバーまたはエッジ トランスポート サーバー上の監視対象の各システム リソースに対して、次の 3 つのリソース使用率レベルが適用されます。

  - **標準**   リソースは適度に使用されています。サーバーは、新しい接続およびメッセージを受け付けます。

  - **中**   リソースの使用率が若干高くなっています。サーバーには、限定されたバック プレッシャが適用されます。権限のあるドメイン内の送信者からのメールは処理されます。ただし圧迫されている特定のリソースによっては、サーバーはタールピットを使用してサーバーの応答を遅らせるか、他のソースから受信する **MAIL FROM** コマンドを拒否します。

  - **高**   リソースが過度に使用されています。完全なバック プレッシャが適用されます。すべてのメッセージ フローが停止し、サーバーはすべての新しい受信 **MAIL FROM** コマンドを拒否します。

次のセクションでは、特定のリソースが圧迫されている場合に、Exchange が状況を処理する方法について説明します。

## メッセージ キュー データベースのハード ドライブ空き容量

既定では、メッセージ キュー データベースは %ExchangeInstallPath%TransportRoles\\data\\Queue に格納されます。Exchange は、この場所のハード ドライブ空き容量を監視します。次の数式を使用して、ハード ドライブ容量の高レベルの使用率が計算されます。

100 \* (*hard disk size* - *fixed constant*) / *hard drive size*

*fixed constant*の値は 500 メガバイト (MB) です。

この数式の結果は、使用されている合計のハード ドライブ容量の割合として表されます。数式の結果は、常に最も近い整数に切り捨てられます。既定では、ハード ドライブの中レベルの使用率は、高レベルより 2% 小さい値になります。既定では、ハード ドライブの標準レベルの使用率は、高レベルより 4% 小さい値になります。

ページのトップへ

## メッセージ キュー データベース トランザクション ログ用のハード ドライブ空き容量

既定では、メッセージ キュー データベース トランザクション ログは %ExchangeInstallPath%TransportRoles\\data\\Queue に格納されます。Exchange は、この場所のハード ドライブ空き容量を監視します。%ExchangeInstallPath%Bin\\EdgeTransport.exe.config アプリケーション構成ファイルには *DatabaseCheckPointDepthMax* キーが含まれ、既定値は 384 MB になっています。このキーは、ハード ドライブ上に存在するコミットされていないすべてのトランザクション ログの許可された合計サイズを制御します。このキーは、ハード ドライブの使用率を計算する数式で使用されます。


> [!NOTE]
> <EM>DatabaseCheckPointDepthMax</EM> キーの値は、メールボックス サーバーまたはエッジ トランスポート サーバー上に存在するトランスポート関連のすべての Extensible Storage Engine (ESE) データベースに適用されます。これには、メッセージ キュー データベースや IP フィルター データベースが含まれます。



既定では、次の数式を使用して、ディスクの高レベルの使用率が計算されます。

100 \* (*hard drive size* - Min(5 GB, 3\**DatabaseCheckPointDepthMax*)) / *hard drive size*

数式の結果は、常に最も近い整数に切り捨てられます。既定では、ハード ドライブの中レベルの使用率は、高レベルより 2% 小さい値になります。ハード ドライブの標準レベルの使用率は、高レベルより 4% 小さい値になります。

ページのトップへ

## メモリ内のコミットされていないメッセージ キュー データベース トランザクションの数

メッセージ キュー データベースに加えられた変更の一覧は、それらの変更をトランザクション ログにコミットできるようになるまでメモリ内に保持されます。その時点で、この一覧はメッセージ キュー データベース自体にコミットされます。メモリ内に保持されるこれらの未処理のメッセージ キュー データベース トランザクションを、*バージョンのバケット*と呼びます。予想以上に大量の受信メッセージ、スパム攻撃、メッセージ キュー データベースの整合性に関する問題、またはハード ドライブのパフォーマンスが原因で、バージョンのバケット数が許容できないほど高いレベルに増加することがあります。

Exchange がメッセージの受信を開始すると、これらのメッセージはバッチにグループ化され、バージョン バケットとして準備されます。受信メッセージの添付ファイルのサイズが大きい場合は、複数のバッチに分けることができます。処理されているこれらのバッチは、*バッチ ポイント*と呼ばれます。大きな添付ファイルが原因で受信メッセージのサイズが予想以上に大きい場合、未処理のバッチ ポイントが、設定されたしきい値を超える可能性があります。

バージョン バケットやバッチ ポイントが圧迫されている場合、Exchange サーバーは受信メッセージの受信確認を遅らせることで受信接続の調整を開始します。Exchange はタールピットによって受信メッセージ フロー率を低くし、その結果 **MAIL FROM** コマンドの遅延が生じます。リソースが圧迫される状態が引き続き発生する場合、Exchange は徐々にタールピットの遅延を増やします。リソース使用率が通常に戻ると、Exchange は段階的に受信確認の遅延を減らし、通常の処理に戻していきます。既定では、Exchange はリソースが圧迫されていると、10 秒間のメッセージ受信確認遅延を開始します。リソース圧迫の状態が続くと、遅延は 5 秒単位で最長 55 秒まで増加していきます。

Exchange は、バージョン バケットとバッチ ポイントのリソース使用率の履歴を保持します。ポーリング間隔が特定の値 (履歴の深さとも呼ばれる) であるためにリソース使用率が通常レベルまで減らない場合、Exchange はタールピット遅延を停止し、リソース使用率が通常に戻るまで受信メッセージを拒否し始めます。既定では、バージョン バケットとバッチ ポイントの履歴の深さは、それぞれ 10 および 300 のポーリング間隔です。

ページのトップへ

## EdgeTransport.exe プロセスで使用されているメモリ

既定では、次の数式を使用して、EdgeTransport.exe プロセスによる高レベルのメモリ使用率が計算されます。

物理メモリの合計の 75% または 1 TB のどちらか小さい方

この計算には、ハード ドライブのページング ファイル内で使用できる仮想メモリや、他のプロセスで使用されているメモリは含まれません。この数式の結果は、EdgeTransport.exe プロセスで使用されている合計メモリの割合として表されます。数式の結果は、常に最も近い整数に切り捨てられます。

既定では、EdgeTransport.exe ファイルによる中レベルのメモリ使用率は、物理メモリの合計の 73%、または高レベルの値より 2% 小さい値のどちらか小さい方になります。既定では、EdgeTransport.exe ファイルによる標準レベルのメモリ使用率は、物理メモリの合計の 71%、または高レベルの値より 4% 小さい値のどちらか小さい方になります。

EdgeTransport.exe プロセスのメモリ使用率が指定された標準レベルを超えている場合は、*ガーベジ コレクション*が強制的に実行されます。ガーベジ コレクションとは、メモリ内に存在する未使用のオブジェクトをチェックし、それらの未使用のオブジェクトで使用されているメモリを再利用するプロセスです。

Exchange は EdgeTransport.exe プロセスのメモリ使用率の履歴を保持します。ポーリング間隔が特定の値 (履歴の深さとも呼ばれる) であるためにリソース使用率が通常レベルまで減らない場合、Exchange はリソース使用率が通常に戻るまで受信メッセージを拒否し始めます。既定では、EdgeTransport.exe のメモリ使用率の履歴の深さは、ポーリング間隔 30 です。

ページのトップへ

## すべてのプロセスで使用されているメモリ

既定では、すべてのプロセスによる高レベルのメモリ使用率は、物理メモリの合計の 94% になります。この値には、ハード ドライブのページング ファイル内で使用できる仮想メモリは含まれません。

指定したメモリ使用率のレベルに達すると、*メッセージの退避*が発生します。メッセージの退避とは、メモリ内にキャッシュされているキュー内のメッセージの不要な要素を削除する処理です。パフォーマンスを向上させるために、メッセージ全体がメモリ内にキャッシュされます。キューに格納されているメッセージの MIME コンテンツをメモリから削除すると、そのメッセージがメッセージ キュー データベースから直接読み取られるため、使用されるメモリは少なくなりますが、待ち時間は長くなります。メッセージの退避は、既定で有効になっています。

ページのトップへ

## 送信キュー内のメッセージの数

送信キューは、Exchange 2013 メールボックス サーバーとエッジ トランスポート サーバー上のトランスポート サービスとに関連付けられています。カテゴライザーは送信キュー内の各メッセージを処理します。この分類により、メッセージは配信キューに入ります。詳細については、「[メール フロー](mail-flow-exchange-2013-help.md)」および「[キュー](queues-exchange-2013-help.md)」を参照してください。送信キューにメッセージが多数ある状態は、カテゴライザーがメッセージを適切に処理できていないことを意味します。

送信キューが圧迫されているとき、Exchange サーバーは受信メッセージの受信確認を遅らせて受信接続の調整を開始します。Exchange はタールピットによって受信メッセージ フロー率を低くし、その結果 **MAIL FROM** コマンドの遅延が生じます。送信キューが圧迫される状態が引き続き発生する場合、Exchange は徐々にタールピットの遅延を増やします。送信キュー使用率が通常に戻ると、Exchange は段階的に受信確認の遅延を減らし、通常の処理に戻していきます。既定では、Exchange は送信キューが圧迫されていると、10 秒間のメッセージ受信確認遅延を開始します。送信キューが圧迫されている状態が続くと、遅延は 5 秒単位で最長 55 秒まで増加していきます。

Exchange は送信キューの使用率の履歴を保持します。ポーリング間隔が特定の値 (履歴の深さとも呼ばれる) であるために送信キュー使用率が通常レベルまで減らない場合、Exchange はタールピット遅延を停止し、送信使用率が通常に戻るまで受信メッセージを拒否し始めます。既定では、送信キューの履歴の深さはポーリング 300 回以内です。

## リソースが圧迫されている状態で Exchange Transport が実行する処理

次の表に、特定のリソースが圧迫されている場合の Exchange Transport による処理を示します。

### リソースの圧迫に応答するメールボックス サーバーとエッジ トランスポート サーバーによるバック プレッシャ アクション

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>圧迫されているリソース</th>
<th>使用率レベル</th>
<th>実行された処理</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>メッセージ キュー データベース用のハード ドライブ空き容量</p></td>
<td><p>中</p></td>
<td><ul>
<li><p>Exchange 以外のサーバーからの受信メッセージを拒否</p></li>
<li><p>ピックアップ ディレクトリおよび再生ディレクトリからのメッセージを拒否</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>メッセージ キュー データベース用のハード ドライブ空き容量</p></td>
<td><p>高</p></td>
<td><ul>
<li><p>他の Exchange サーバーからの受信メッセージを拒否</p></li>
<li><p>メールボックス サーバーのメールボックス トランスポート送信サービスによる、メールボックス データベースからのメッセージ送信を拒否</p></li>
<li><p>Exchange 以外のサーバーからの受信メッセージを拒否</p></li>
<li><p>ピックアップ ディレクトリおよび再生ディレクトリからのメッセージを拒否</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>メッセージ キュー データベース トランザクション ログ用のハード ドライブ空き容量</p></td>
<td><p>中</p></td>
<td><ul>
<li><p>Exchange 以外のサーバーからの受信メッセージを拒否</p></li>
<li><p>ピックアップ ディレクトリおよび再生ディレクトリからのメッセージを拒否</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>メッセージ キュー データベース トランザクション ログ用のハード ドライブ空き容量</p></td>
<td><p>高</p></td>
<td><ul>
<li><p>他の Exchange サーバーからの受信メッセージを拒否</p></li>
<li><p>メールボックス サーバーのメールボックス トランスポート送信サービスによる、メールボックス データベースからのメッセージ送信を拒否</p></li>
<li><p>Exchange 以外のサーバーからの受信メッセージを拒否</p></li>
<li><p>ピックアップ ディレクトリおよび再生ディレクトリからのメッセージを拒否</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>バージョン バケット</p></td>
<td><p>中</p></td>
<td><p>受信メッセージへのタールピット遅延が導入されるか、増加します。バージョン バケット全体の履歴の深さが通常レベルに達しない場合は、次の処理を実行します。</p>
<ul>
<li><p>Exchange 以外のサーバーからの受信メッセージを拒否</p></li>
<li><p>ピックアップ ディレクトリおよび再生ディレクトリからのメッセージを拒否</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>バージョン バケット</p></td>
<td><p>高</p></td>
<td><p>受信メッセージへのタールピット遅延が導入されるか、増加します。バージョン バケット全体の履歴の深さが通常レベルに達しない場合は、次の処理を実行します。</p>
<ul>
<li><p>他の Exchange サーバーからの受信メッセージを拒否</p></li>
<li><p>メールボックス サーバーのメールボックス トランスポート送信サービスによる、メールボックス データベースからのメッセージ送信を拒否</p></li>
<li><p>Exchange 以外のサーバーからの受信メッセージを拒否</p></li>
<li><p>ピックアップ ディレクトリおよび再生ディレクトリからのメッセージを拒否</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>バッチ ポイント</p></td>
<td><p>中</p></td>
<td><p>受信メッセージへのタールピット遅延が導入されるか、増加します。バッチ ポイント全体の履歴の深さが通常レベルに達しない場合は、次の処理を実行します。</p>
<ul>
<li><p>Exchange 以外のサーバーからの受信メッセージを拒否</p></li>
<li><p>ピックアップ ディレクトリおよび再生ディレクトリからのメッセージを拒否</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>バッチ ポイント</p></td>
<td><p>高</p></td>
<td><p>受信メッセージへのタールピット遅延が導入されるか、増加します。バッチ ポイント全体の履歴の深さが通常レベルに達しない場合は、次の処理を実行します。</p>
<ul>
<li><p>他の Exchange サーバーからの受信メッセージを拒否</p></li>
<li><p>メールボックス サーバーのメールボックス トランスポート送信サービスによる、メールボックス データベースからのメッセージ送信を拒否</p></li>
<li><p>Exchange 以外のサーバーからの受信メッセージを拒否</p></li>
<li><p>ピックアップ ディレクトリおよび再生ディレクトリからのメッセージを拒否</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>EdgeTransport.exe のプロセスによって使用されるメモリ</p></td>
<td><p>中</p></td>
<td><ul>
<li><p>Exchange 以外のサーバーからの受信メッセージを拒否</p></li>
<li><p>ピックアップ ディレクトリおよび再生ディレクトリからのメッセージを拒否</p></li>
<li><p>ガベージ コレクションの強制</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe のプロセスによって使用されるメモリ</p></td>
<td><p>高</p></td>
<td><ul>
<li><p>他の Exchange サーバーからの受信メッセージを拒否</p></li>
<li><p>メールボックス サーバーのメールボックス トランスポート送信サービスによる、メールボックス データベースからのメッセージ送信を拒否</p></li>
<li><p>Exchange 以外のサーバーからの受信メッセージを拒否</p></li>
<li><p>ピックアップ ディレクトリおよび再生ディレクトリからのメッセージを拒否</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>すべてのプロセスで使用されているメモリ</p></td>
<td><p>中</p></td>
<td><ul>
<li><p>Exchange 以外のサーバーからの受信メッセージを拒否</p></li>
<li><p>ピックアップ ディレクトリおよび再生ディレクトリからのメッセージを拒否</p></li>
<li><p>ガベージ コレクションの強制</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>すべてのプロセスで使用されているメモリ</p></td>
<td><p>高</p></td>
<td><ul>
<li><p>他の Exchange サーバーからの受信メッセージを拒否</p></li>
<li><p>メールボックス サーバーのメールボックス トランスポート送信サービスによる、メールボックス データベースからのメッセージ送信を拒否</p></li>
<li><p>Exchange 以外のサーバーからの受信メッセージを拒否</p></li>
<li><p>ピックアップ ディレクトリおよび再生ディレクトリからのメッセージを拒否</p></li>
<li><p>拡張 DNS キャッシュをメモリからフラッシュ</p></li>
<li><p>メッセージの退避を開始する</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>送信キュー内のメッセージの数</p></td>
<td><p>中</p></td>
<td><p>受信メッセージへのタールピット遅延が導入されるか、増加します。送信キュー全体の履歴の深さが通常レベルに達しない場合は、次の処理を実行します。</p>
<ul>
<li><p>Exchange 以外のサーバーからの受信メッセージを拒否</p></li>
<li><p>ピックアップ ディレクトリおよび再生ディレクトリからのメッセージを拒否</p></li>
<li><p>ガベージ コレクションの強制</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>送信キュー内のメッセージの数</p></td>
<td><p>高</p></td>
<td><p>受信メッセージへのタールピット遅延が導入されるか、増加します。送信キュー全体の履歴の深さが通常レベルに達しない場合は、次の処理を実行します。</p>
<ul>
<li><p>他の Exchange サーバーからの受信メッセージを拒否</p></li>
<li><p>メールボックス サーバーのメールボックス トランスポート送信サービスによる、メールボックス データベースからのメッセージ送信を拒否</p></li>
<li><p>Exchange 以外のサーバーからの受信メッセージを拒否</p></li>
<li><p>ピックアップ ディレクトリおよび再生ディレクトリからのメッセージを拒否</p></li>
<li><p>拡張 DNS キャッシュをメモリからフラッシュ</p></li>
<li><p>メッセージの退避を開始する</p></li>
</ul></td>
</tr>
</tbody>
</table>


ページのトップへ

## EdgeTransport.exe.config ファイルのバック プレッシャ構成オプション

バック プレッシャの構成オプションはすべて、%ExchangeInstallPath%Bin\\EdgeTransport.exe.config XML アプリケーション構成ファイルで使用できます。


> [!NOTE]
> これらの設定は、参照用としてのみ表示されます。EdgeTransport.exe.config ファイルのバック プレッシャの設定は変更しないことを強くお勧めします。バック プレッシャの設定を変更すると、パフォーマンスの低下やデータの損失が発生する可能性があります。発生するバック プレッシャ イベントは、すべて根本原因を調べて修正することをお勧めします。



### バック プレッシャ構成オプション

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>キーの名前</th>
<th>既定値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>EnableResourceMonitoring</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="even">
<td><p><em>ResourceMonitoringInterval</em></p></td>
<td><p><code>00:00:02</code> (2 秒)</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseDiskSpaceUsedHighThreshold</em></p></td>
<td><p>0. この値は、既定の数式が使用されることを示します。</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseDiskSpaceUsedMediumThreshold</em></p></td>
<td><p>0. この値は、実際の値が <em>PercentageDatabaseDiskSpaceUsedHighThreshold</em> の値より 2% 小さいことを示します。</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseDiskSpaceUsedNormalThreshold</em></p></td>
<td><p>0. この値は、実際の値が <em>PercentageDatabaseDiskSpaceUsedMediumThreshold</em> の値より 2% 小さいことを示します。</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedHighThreshold</em></p></td>
<td><p>0. この値は、既定の数式が使用されることを示します。</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedMediumThreshold</em></p></td>
<td><p>0. この値は、実際の値が <em>PercentageDatabaseLoggingDiskSpaceUsedHighThreshold</em> の値より 2% 小さいことを示します。</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedNormalThreshold</em></p></td>
<td><p>0. この値は、実際の値が <em>PercentageDatabaseLoggingDiskSpaceUsedMediumThreshold</em> の値より 2% 小さいことを示します。</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentagePrivateBytesUsedHighThreshold</em></p></td>
<td><p>0. この値は、既定の計算が使用されることを示します。</p></td>
</tr>
<tr class="even">
<td><p><em>PercentagePrivateBytesUsedMediumThreshold</em></p></td>
<td><p>0. この値は、実際の値が <em>PercentagePrivateBytesUsedHighThreshold</em> の値より 2% 小さいことを示します。</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentagePrivateBytesUsedNormalThreshold</em></p></td>
<td><p>0. この値は、実際の値が <em>PercentagePrivateBytesUsedMediumThreshold</em> の値より 2% 小さいことを示します。</p></td>
</tr>
<tr class="even">
<td><p><em>VersionBucketsHighThreshold</em></p></td>
<td><p>200</p></td>
</tr>
<tr class="odd">
<td><p><em>VersionBucketsMediumThreshold</em></p></td>
<td><p>120</p></td>
</tr>
<tr class="even">
<td><p><em>VersionBucketsNormalThreshold</em></p></td>
<td><p>80</p></td>
</tr>
<tr class="odd">
<td><p><em>VersionBucketsHistoryDepth</em></p></td>
<td><p>10</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointHighThreshold</em></p></td>
<td><p>4000</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointMediumThreshold</em></p></td>
<td><p>2000</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointNormalThreshold</em></p></td>
<td><p>1000</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointHistoryDepth</em></p></td>
<td><p>300</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointUseCostForPressure</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointBatchSize</em></p></td>
<td><p>40</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointBatchTimeout</em></p></td>
<td><p><code>00:00:00.100</code> (0.1 秒)</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointItemExpiryInterval</em></p></td>
<td><p><code>00:05:00</code> (5 分)</p></td>
</tr>
<tr class="even">
<td><p><em>SMTPBaseThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:00</code></p></td>
</tr>
<tr class="odd">
<td><p><em>SMTPMaxThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:55</code> (55 秒)</p></td>
</tr>
<tr class="even">
<td><p><em>SMTPStepThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:05</code> (5 秒)</p></td>
</tr>
<tr class="odd">
<td><p><em>SMTPStartThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:10</code> (10 秒)</p></td>
</tr>
<tr class="even">
<td><p><em>PercentagePhysicalMemoryUsedLimit</em></p></td>
<td><p>94</p></td>
</tr>
<tr class="odd">
<td><p><em>DehydrateMessagesUnderMemoryPressure</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="even">
<td><p><em>PrivateBytesHistoryDepth</em></p></td>
<td><p>30</p></td>
</tr>
<tr class="odd">
<td><p><em>SubmissionQueueHighThreshold</em></p></td>
<td><p>10000</p></td>
</tr>
<tr class="even">
<td><p><em>SubmissionQueueMediumThreshold</em></p></td>
<td><p>4000</p></td>
</tr>
<tr class="odd">
<td><p><em>SubmissionQueueNormalThreshold</em></p></td>
<td><p>2000</p></td>
</tr>
<tr class="even">
<td><p><em>SubmissionQueueHistoryDepth</em></p></td>
<td><p>300</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## バック プレッシャのログ情報

次の一覧は、Exchange の特定のバック プレッシャ イベントによって生成されるイベント ログ エントリに関する説明です。

  - **リソース使用率レベルが増加した場合のイベント ログ エントリ**
    
    イベントの種類: エラー
    
    イベント ソース: MSExchangeTransport
    
    イベント カテゴリ: リソース マネージャー
    
    イベント ID: 15004
    
    説明: リソースの圧迫が*Previous Utilization Level*から*Current Utilization Level*に増加しました。

  - **リソース使用率レベルが減少した場合のイベント ログ エントリ**
    
    イベントの種類: 情報
    
    イベント ソース: MSExchangeTransport
    
    イベント カテゴリ: リソース マネージャー
    
    イベント ID: 15005
    
    説明: リソースの圧迫が*Previous Utilization Level*から*Current Utilization Level*に減少しました。

  - **利用可能なディスク領域が著しく不足した場合のイベント ログ エントリ**
    
    イベントの種類: エラー
    
    イベント ソース: MSExchangeTransport
    
    イベント カテゴリ: リソース マネージャー
    
    イベント ID: 15006
    
    説明: Microsoft Exchange Transport サービスは、利用可能なディスク領域が構成されたしきい値を下回るため、メッセージを拒否しています。運用を続けるには、サービスの空きディスク領域を増やすための管理操作が必要な場合があります。

  - **利用可能なメモリが著しく不足した場合のイベント ログ エントリ**
    
    イベントの種類: エラー
    
    イベント ソース: MSExchangeTransport
    
    イベント カテゴリ: リソース マネージャー
    
    イベント ID: 15007
    
    説明 : サービスが、構成されているしきい値を超えるメモリ量を消費し続けているため、Microsoft Exchange Transport サービスはメッセージの送信を拒否しています。これにより、通常の運用を続けるには、このサービスを再起動する必要がある場合があります。

ページのトップへ

