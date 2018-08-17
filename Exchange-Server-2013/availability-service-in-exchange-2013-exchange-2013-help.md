---
title: 'Exchange 2013 の可用性サービス: Exchange 2013 Help'
TOCTitle: Exchange 2013 の可用性サービス
ms:assetid: 9722dea2-2bf8-437c-85c0-3ab65b8a07b9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb232134(v=EXCHG.150)
ms:contentKeyID: 52057837
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 の可用性サービス

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

Exchange 2013 可用性サービスにより、Microsoft Outlook および Outlook Web App クライアントが空き時間情報を利用できるようになります。可用性サービスは、セキュリティで保護された一貫性のある最新の空き時間情報を提供することによって、インフォメーション ワーカーの予定表や会議のスケジュール調整の操作を向上させます。

Outlook と Outlook Web App は、以下の処理の実行に可用性サービスを使用します。

  - Exchange 2013 メールボックスの最新の空き時間情報の取得

  - その他の Exchange 2013 組織からの最新の空き時間情報の取得

  - 以前のバージョンの Exchange を持つサーバー上のメールボックスのパブリック フォルダーから発行された空き時間情報の取得

  - 出席者の就業時間の表示

  - 会議時間のお勧めの表示

**目次**

可用性サービスの概要

不在状態に関する情報

可用性サービス API

可用性サービスのネットワーク負荷分散

空き時間情報を取得するために使用する方法

## 可用性サービスの概要

可用性サービスは、空き時間情報を Exchange 2013、Exchange 2010、または Exchange 2007 上のユーザーの対象メールボックスから直接取得しますが、以前のバージョンの Exchange 上のユーザーのために空き時間情報を取得するようにも構成できます。すべてのクライアントが Outlook 2007 以上を実行している Exchange 2007、Exchange 2010、または Exchange 2013 メールボックスを持つトポロジの場合は、空き時間情報を取得するために可用性サービスが使用されます。

Outlook では、Exchange 自動検出サービスを使用して可用性サービスの URL を取得します。自動検出サービスの詳細については、「[自動検出サービス](autodiscover-service-for-exchange-2013.md)」を参照してください。

Exchange 管理シェルを使用して可用性サービスを構成できます。Exchange 管理コンソール (EAC) を使用して可用性サービスを構成することはできません。

## 不在状態に関する情報

可用性サービスは、ユーザーが長期間不在にするときに送信する自動返信メッセージへのアクセスも提供します。

インフォメーション ワーカーは、電子メール メッセージに応答できないとき、Outlook および Outlook Web App の自動返信機能 (以前は不在時機能と呼ばれていました) を使用して他の人に通知できます。これにより、インフォメーション ワーカーと管理者の自動返信メッセージの設定と管理が簡単に行えるようになります。

## 可用性サービス API

可用性サービスは、Exchange 2013 プログラミング インターフェイスの一部です。これは、開発者が統合を目的としてサード パーティのツールを記述できる Web サービスとして使用可能です。

## 可用性サービスのネットワーク負荷分散

可用性サービスを実行しているクライアント アクセス サーバーでネットワーク負荷分散 (NLB) を使用すると、空き時間情報に依存するユーザーのパフォーマンスと信頼性が向上します。Outlook では、自動検出サービスを使用して可用性サービスの URL を検出します。可用性サービスで NLB を使用するには、構成を変更する必要があります。

内部 URL はイントラネットから使用され、外部 URL はインターネットから使用されます。内部のトラフィックと外部のトラフィックの両方に同じ URL を使用する場合は、DNS が、内部のトラフィックを内部の URL に直接ルーティングするように正しく構成されていることを確認してください。また、その URL に、内部と外部の両方からアクセスできることも確認してください。自動検出サービスおよび可用性サービスを正常に動作させるために、DNS を構成して mail.\<*domain name*\>.com および autodiscover.mail.\<*domain name*\>.com が負荷分散ソリューションの仮想 IP (VIP) を指すようにする必要があります。ここで、\<*domain name*\> はドメイン名です。


> [!NOTE]
> 詳細については、「<A href="https://go.microsoft.com/fwlink/p/?linkid=45959">ネットワーク負荷分散のテクニカル リファレンス</A>」および「<A href="https://go.microsoft.com/fwlink/p/?linkid=49315">ネットワーク負荷分散クラスタ</A>」を参照してください。また、サード パーティの負荷分散ソフトウェアの Web サイトを検索することもできます。



## 空き時間情報を取得するために使用する方法

次の表は、さまざまな単一フォレストのトポロジで空き時間情報を取得するために使用される方法を示しています。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>クライアント</th>
<th>空き時間情報を取得しているメールボックスを実行しています。</th>
<th>移動先のメールボックスを実行しています。</th>
<th>空き時間情報の取得方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013</p></td>
<td><p>Exchange 2013、Exchange 2010、または Exchange 2007</p></td>
<td><p>Exchange 2013、Exchange 2010、または Exchange 2007</p></td>
<td><p>可用性サービスが、対象のメールボックスから空き時間情報を読み取ります。</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2007</p></td>
<td><p>Exchange 2013、Exchange 2010、または Exchange 2007</p></td>
<td><p>Exchange 2010 またはExchange 2007</p></td>
<td><p>可用性サービスが、対象のメールボックスから空き時間情報を読み取ります。</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p>Exchange 2010 またはExchange 2007</p></td>
<td><p>Exchange 2003</p></td>
<td><p>可用性サービスが、Exchange 2003 メールボックスの /public 仮想ディレクトリへの HTTP 接続を確立します。</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App</p></td>
<td><p>Exchange 2013、Exchange 2010、または Exchange 2007</p></td>
<td><p>Exchange 2013、Exchange 2010、または Exchange 2007</p></td>
<td><p>Exchange 2010 では Outlook Web App または Exchange 2007 では Outlook Web Access が可用性サービス API を呼び出します。この API が、対象のメールボックスから空き時間情報を読み取ります。</p></td>
</tr>
</tbody>
</table>

