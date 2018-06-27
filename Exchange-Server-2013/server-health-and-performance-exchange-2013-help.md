---
title: 'サーバーの状態とパフォーマンス: Exchange 2013 Help'
TOCTitle: サーバーの状態とパフォーマンス
ms:assetid: 9d1fdec8-8273-4c71-88f1-b4edfd542c4f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ150551(v=EXCHG.150)
ms:contentKeyID: 48269858
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# サーバーの状態とパフォーマンス

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-03-09_

パフォーマンスに優れたメッセージング インフラストラクチャの設計と管理には、サーバーの正常性とパフォーマンスについて理解しておくことが重要です。Microsoft Exchange Server 2013 ではサーバーの正常性とパフォーマンスが改善されています。

サーバーの正常性とパフォーマンスに関するすべてのトピックの一覧については、「サーバーの正常性とパフォーマンスに関するドキュメント」を参照してください。

## 可用性管理

Exchange 2013 では、*可用性管理*の概念が導入されています。可用性管理はすべての Exchange 2013 サーバーで実行されます。可用性管理は、Exchange Health Manager Service (MSExchangeHMHost.exe) および Exchange Health Manager Worker プロセス (MSExchangeHMWorker.exe) という 2 つのプロセス、および次の非同期コンポーネントで構成されます。

  - **プローブ エンジン** *プローブ エンジン*は、サーバー上で測定を行います。

  - **監視プローブ エンジン** *監視プローブ エンジン*には、正常な状態を示すビジネス ロジックが保存されます。監視プローブ エンジンはパターン認識エンジンのように機能し、正常な状態とは異なるパターンと測定結果を確認して、コンポーネントまたは機能が正常でないかどうかを評価します。

  - **レスポンダー エンジン** *レスポンダー エンジン*が正常でないコンポーネントに関する警告を受けた場合、最初にそのコンポーネントの修復操作が試行されます。可用性管理によって、複数の段階からなる修復操作が可能になります。最初の試行はアプリケーション プールの再起動、2 回目の試行は対応するサービスの再起動、3 回目の試行はサーバーの再起動になる可能性があります。最後の試行でサーバーをオフラインにし、それ以上トラフィックを受信しないようにします。これらのアクションがすべて失敗すると、ヘルプ デスクに警告が送信されます。

可用性管理の詳細については、「[可用性管理](managed-availability-exchange-2013-help.md)」を参照してください。

## ワークロード管理

Exchange 2013 ワークロード管理には、次のコンポーネントが含まれています。

  - *ユーザー ワークロード管理*とは、Exchange Server 2010 にあったユーザー調整機能の新しい名前です。環境のニーズに応じてこれらの設定をカスタマイズできます。

  - *システム ワークロード管理*は Exchange 2013 の新機能であり、この機能を使用して主要なサーバー リソースの正常性を監視して特定の Exchange ワークロードを自動的に調整します。これらの設定のカスタマイズは、Microsoft カスタマー サービス/サポートの指示によってのみ行ってください。

詳細については、「[Exchange ワークロード管理](exchange-workload-management-exchange-2013-help.md)」を参照してください。

## サーバーの正常性とパフォーマンスに関するドキュメント

次の表には、Exchange 2013 でのサーバーの正常性とパフォーマンスの詳細の確認と管理に役立つトピックへのリンクが含まれています。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="exchange-workload-management-exchange-2013-help.md">Exchange ワークロード管理</a></p></td>
<td><p>個々のユーザーによるリソースの消費状況を制御して Exchange ワークロードを管理する方法について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="managed-availability-exchange-2013-help.md">可用性管理</a></p></td>
<td><p>Exchange 2013 で利用可能な組み込みのリソース監視と回復処理について説明します。</p></td>
</tr>
</tbody>
</table>

