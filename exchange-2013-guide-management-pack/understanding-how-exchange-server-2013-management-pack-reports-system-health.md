---
title: Exchange Server 2013 管理パックによるシステム正常性の報告方法について
TOCTitle: Exchange Server 2013 管理パックによるシステム正常性の報告方法について
ms:assetid: 6ca8847f-93fe-458d-bd43-7afad7fdd2f4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn195910(v=EXCHG.150)
ms:contentKeyID: 53181895
ms.date: 04/03/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Server 2013 管理パックによるシステム正常性の報告方法について

 

_**トピックの最終更新日:**  2015-03-09_

このトピックでは、Exchange Server 2013 管理パックがどのように Exchange システムを監視してその正常性を報告するかについて説明します。Exchange 2013 管理パックでは、正常性状態の情報を簡単な方法でロールアップします。正常性セットが異常になってエスカレート レスポンダーがトリガーされるたびに、Windows イベント ログに次のイベントが記録されます。

## 管理可用性

Exchange Server 2013 では、いくつかのアーキテクチャ上の変更が行われています。主な変更点の 1 つは、問題を検出してサービスの可用性の回復を試みるモニターが Exchange 2013 のすべてのコンポーネントに組み込まれる*管理可用性*機能です。Exchange 2013 管理パックはこの機能に依存しています。自動的に回復できない問題は、Exchange 2013 管理パックにアラートとしてエスカレートされます。Exchange 2013 内の各コンポーネントは、プローブ、モニター、およびレスポンダーと呼ばれる 3 つの基本的なコンポーネントを使用して自分自身を監視します。

![可用性管理](images/Dn195910.dd5febae-d05e-4089-a3f5-1691b2d9a3d7(EXCHG.150).png "可用性管理")

  - **プローブ**   さまざまなコンポーネントを測定するデータ コレクター セットです。プローブには次の 3 種類があります。
    
      - 代理エンドツーエンド ユーザー操作を測定する代理トランザクションと実際のトラフィックを測定するチェック。
    
      - 実際の顧客トラフィックを測定するチェック。
    
      - Exchange に即時対応を許可する通知。この良い例は、証明書が失効したときにトリガーされる通知です。

  - **モニター**   プローブによって収集されたデータはモニターに渡され、そこで、データが特定の条件下で分析され、その条件に応じて、特定のコンポーネントが正常か異常かが判断されます。

  - **レスポンダー**   コンポーネントが異常であるとモニターが判断したときに、レスポンダーがトリガーされます。問題が回復可能である場合、レスポンダーは組み込みロジックを使用してコンポーネントを回復しようとします。コンポーネントごとに複数のレスポンダーが使用可能ですが、Exchange 2013 管理パックに関連するレスポンダーは *Escalate Responder* です。トリガーされた Escalate Responder は、Exchange 2013 管理パックが認識するイベントを生成し、適切な情報をアラートにフィードして、問題への対処に必要な情報を管理者に提供します。

Exchange 2013 内の各コンポーネントは、プローブ、モニター、およびレスポンダーの特定のセットを使用して自分自信を監視します。このプローブとモニターの集合は*正常性セット*と呼ばれています。たとえば、ActiveSync サービスのさまざまな側面に関するデータを収集する複数のプローブがあります。このデータは、適切なレスポンダーをトリガーして ActiveSync サービス内で検出された問題を解決する指定されたモニターのセットによって処理されます。これらのコンポーネントが集まって ActiveSync 正常性セットを構成します。

Exchange 内の正常性セットは、管理パック ダッシュボードに対応する次の 4 つのカテゴリに分類されます。

  - 顧客タッチ ポイント

  - サービス コンポーネント

  - サーバー リソース

  - キーの依存関係

Exchange 正常性セットの完全な一覧については、「[Appendix A: Exchange health sets](appendix-a-exchange-health-sets.md)」を参照してください。

可用性管理の詳細については、「[サーバーの状態とパフォーマンス](https://technet.microsoft.com/ja-jp/library/jj150551\(v=exchg.150\))」を参照してください。

## 正常性のロールアップ方法

このトピックでは、Exchange Server 2013 管理パックがどのように Exchange システムを監視してその正常性を報告するかについて説明します。Exchange 2013 管理パックでは、正常性状態の情報を簡単な方法でロールアップします。正常性セットが異常になってエスカレート レスポンダーがトリガーされるたびに、Windows イベント ログに次のイベントが記録されます。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>ログ名</p></td>
<td><p>Microsoft-Exchange-ManagedAvailability/Monitoring</p></td>
</tr>
<tr class="even">
<td><p>ソース</p></td>
<td><p>ManagedAvailability</p></td>
</tr>
<tr class="odd">
<td><p>日付</p></td>
<td><p>&lt;<em>イベントの日付と時刻</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>イベント ID</p></td>
<td><p>4</p></td>
</tr>
<tr class="odd">
<td><p>タスク カテゴリ</p></td>
<td><p>&quot;Monitoring/監視&quot;</p></td>
</tr>
<tr class="even">
<td><p>レベル</p></td>
<td><p>エラー</p></td>
</tr>
<tr class="odd">
<td><p>キーワード</p></td>
<td><p>&lt;<em>なし</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>ユーザー</p></td>
<td><p>SYSTEM</p></td>
</tr>
<tr class="odd">
<td><p>コンピューター</p></td>
<td><p>&lt;<em>Exchange サーバーの FQDN</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>説明</p></td>
<td><p>&lt;<em>エスカレート レスポンダーによって動的に生成されます</em>&gt;</p></td>
</tr>
</tbody>
</table>


管理パックのエージェントはこのイベントを検出して処理します。可用性管理は、このイベントを使用して、SCOM 内でアラートを生成できます。対応する問題が解決され、正常性セットが正常状態に戻ると、以下のイベントが Windows イベント ログに記録されます。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>ログ名</p></td>
<td><p>Microsoft-Exchange-ManagedAvailability/Monitoring</p></td>
</tr>
<tr class="even">
<td><p>ソース</p></td>
<td><p>ManagedAvailability</p></td>
</tr>
<tr class="odd">
<td><p>日付</p></td>
<td><p>&lt;<em>イベントの日付と時刻</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>イベント ID</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>タスク カテゴリ</p></td>
<td><p>&quot;Monitoring/監視&quot;</p></td>
</tr>
<tr class="even">
<td><p>レベル</p></td>
<td><p>情報</p></td>
</tr>
<tr class="odd">
<td><p>キーワード</p></td>
<td><p>&lt;<em>なし</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>ユーザー</p></td>
<td><p>SYSTEM</p></td>
</tr>
<tr class="odd">
<td><p>コンピューター</p></td>
<td><p>&lt;<em>Exchange サーバーの FQDN</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>説明</p></td>
<td><p>&lt;<em>エスカレート レスポンダーによって動的に生成されます</em>&gt;</p></td>
</tr>
</tbody>
</table>


以前のバージョンの Exchange を監視する管理パックは、完全に集中管理されました。各 Exchange サーバーのエージェントはデータを収集し、集中相関エンジンはエージェントによってレポートされたすべてのデータを比較、評価して全体的なサービス正常性を判断します。大規模環境ではこのプロセスによって相関関係が複雑になり、アラート生成が遅れます。Exchange 2013 では警告の相関関係は使用されません。その代わりに各サーバーが必要に応じて独自の監視を実行して SCOM に警告するため、非常に拡張性の高いアーキテクチャが実現します。

イベントの影響とそれをトリガーする正常性セットに応じて、問題が SCOM コンソール内の別々のカテゴリに表示されます。イベントがユーザーに影響する場合は、顧客タッチ ポイント インジケーターが異常として表示されます。イベントによって OWA などのコンポーネント全体が使用できなくなった場合は、サービス コンポーネント インジケーターが異常として表示されます。特定のサーバーに伴う問題の場合は、対応するサーバー正常性インジケーターが異常として表示されます。最後に、問題が、Exchange が依存しているリソースに関係している場合は、主要依存性インジケーターが異常として表示されます。これらのカテゴリの詳細については、「[Exchange Server 2013 管理パックをお使いになる前に](getting-started-with-exchange-server-2013-management-pack.md)」を参照してください。

