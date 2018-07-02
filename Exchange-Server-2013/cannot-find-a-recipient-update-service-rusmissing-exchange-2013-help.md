---
title: '受信者更新サービスが見つからない_RUSMissing: Exchange 2013 Help'
TOCTitle: 受信者更新サービスが見つからない_RUSMissing
ms:assetid: 920fbf51-d5e4-4ac6-869f-7f1c5d9a3024
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.rusmissing(v=EXCHG.150)
ms:contentKeyID: 48269789
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 受信者更新サービスが見つからない\_RUSMissing

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2016-12-15_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

既存の Exchange 組織内のドメインに対して使用される受信者更新サービス (RUS) が見つからないため、Microsoft® Exchange Server 2007 または Exchange Server 2010 のセットアップ プログラムを続行できません。

Microsoft Exchange セットアップ プログラムを実行するには、既存の Exchange 組織内の各ドメインに受信者更新サービスのインスタンスが存在する必要があります。

ドメインの受信者更新サービスのインスタンスが見つからない場合、そのドメイン内で作成される新しいユーザー オブジェクトは、自身宛てに発行される電子メール アドレスを受信できません。

この問題を解決するには、受信者更新サービスのインスタンスが各ドメインに存在することを確認し、インスタンスが存在しないドメインの受信者更新サービスのインスタンスを作成した後、Microsoft Exchange セットアップ プログラムを再実行します。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>ドメインの受信者更新サービスのインスタンスを作成するには、次の操作を行います。</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Exchange システム マネージャーを起動します。</p></li>
<li><p><strong>[受信者]</strong> を展開します。</p></li>
<li><p><strong>[受信者更新サービス]</strong> ノードを右クリックし、<strong>[新規作成]</strong> をクリックして、<strong>[受信者更新サービス]</strong> をクリックします。</p></li>
<li><p>[新しいオブジェクト] ウィンドウで、<strong>[参照]</strong> をクリックして、ドメインの名前を見つけます。</p></li>
<li><p>ドメイン名を選択し、<strong>[OK]</strong> をクリックします。</p></li>
<li><p>[新しいオブジェクト] ウィンドウで、<strong>[次へ]</strong> をクリックし、<strong>[完了]</strong> をクリックします。</p></li>
</ol></td>
</tr>
</tbody>
</table>


受信者更新サービスの詳細については、以下の Microsoft サポート技術情報の文書を参照してください。

  - 「受信者更新サービスで受信者ポリシーを適用する方法」([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=328738](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=328738))

  - 「受信者更新サービスにアドレス一覧を生成させる方法」([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=253828](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=253828))

  - 「Exchange 受信者更新サービスの進行状況を確認する方法」([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=246127](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=246127))

  - 「Exchange 受信者更新サービスで行われるタスク」([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=253770](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=253770))

