---
title: 'キュー ビューアーのオプションを設定する: Exchange 2013 Help'
TOCTitle: キュー ビューアーのオプションを設定する
ms:assetid: 03a9134c-0714-4c13-b286-92bccc7ec05e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa995934(v=EXCHG.150)
ms:contentKeyID: 49895217
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# キュー ビューアーのオプションを設定する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-03_

キュー ビューアーのオプションを設定すると、ページに表示されるアイテムの数と自動更新の間隔を調整できます。自動更新の間隔によって、キュー ビューアーの結果が更新される頻度が決まります。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 10 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「キュー」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!WARNING]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## Exchange ツールボックスを使用してキュー ビューアーのオプションを設定する

1.  <strong>スタート</strong> \> <strong>すべてのプログラム</strong> \> <strong>Microsoft Exchange Server 2013</strong> \> <strong>Exchange ツールボックス</strong> の順にクリックします。

2.  <strong>メール フロー ツール</strong> セクションで、<strong>キュー ビューアー</strong> をダブルクリックします。

3.  キュー ビューアーで、<strong>表示</strong> \> <strong>オプション</strong> をクリックして、<strong>キュー ビューアーのオプション</strong> ダイアログ ボックスで次の設定を構成します。
    
    1.  **"更新間隔 (秒)"** フィールドに、キュー ビューアーの表示を更新する頻度を入力します。
        

        > [!NOTE]
        > 既定の自動更新の間隔は 30 秒です。これより短い時間に設定することはできません。<STRONG>[キュー ビューアーのオプション]</STRONG> ページの <STRONG>[画面の自動更新]</STRONG> チェック ボックスをオフにして自動更新機能を無効にした場合は、[<STRONG>最新の情報に更新</STRONG>] をクリックして、キュー ビューアーに表示される結果を手動で更新する必要があります。

    
    2.  \[**1 ページに表示するアイテム数**\] フィールドに、キュー ビューアーに表示するアイテムの最大数を入力します。この数は 1 ～ 10,000 である必要があります。この制限値を超えるアイテム数がある場合は、アイテムの最大数ごとにグループに分けて表示されます。たとえば次の図では、1 ページに 10 個のアイテムを表示するように構成されたキュー ビューアーに、14 個のメッセージを持つキューが表示されています。ページ上のオブジェクト数が右上に表示されています。ページの下部には、キュー内のアイテムの合計数が表示されています。ナビゲーション コントロールを使用して、キューに含まれている他のアイテムを表示できます。

4.  完了したら、<strong>OK</strong> をクリックします。
    
    **キュー ビューアー**
    
    ![アイテム制限よりもアイテムが多いキュー ビューアー](images/Aa995934.e82196e6-002a-4e9e-823d-b244b0bd25e2(EXCHG.150).gif "アイテム制限よりもアイテムが多いキュー ビューアー")  

## 正常な動作を確認する方法

キュー ビューアーが更新間隔とページごとのアイテム数の設定を使用していれば、この手順が機能したことがわかります。

