---
title: 'キュー ビューアーでのサーバーへの接続: Exchange 2013 Help'
TOCTitle: キュー ビューアーでのサーバーへの接続
ms:assetid: 6c1ad574-9ab5-4dcc-9398-ec10eca4fd11
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998669(v=EXCHG.150)
ms:contentKeyID: 49896298
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# キュー ビューアーでのサーバーへの接続

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-03_

Exchange 組織内部に存在する Microsoft Exchange Server 2013 サーバー上の Exchange ツールボックスでキュー ビューアーを使用すると、他のメールボックス サーバーに接続することができます。 既定では、メールボックス サーバーでキュー ビューアーを開くと、キュー ビューアーがローカル サーバー上のキュー データベースに接続します。 ただし、キュー ビューアーのインスタンスを複数起動して、それぞれのインスタンスが別のサーバーを対象とするように指定することができます。 複数のメールボックス サーバーを同時に簡単に監視できるように、\[キュー ビューアー\] ウィンドウを並べて表示することもできます。

また、リモート PowerShell が指定されたタスクをキュー ビューアーで実行するのに使用するサーバーを指定することもできます。 このサーバーは、キュー ビューアーで管理しているリモート サーバーと一致している必要はありません。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「キュー」。

  - このトピックの手順は、エッジ トランスポート サーバーには適用されません。 エッジ トランスポート サーバーでキュー ビューアーを使用すると、ツールの対象となるサーバーを変更できません。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## Exchange ツールボックスを使用してキュー ビューアーで管理するサーバーを指定する

1.  <strong>スタート</strong> \> <strong>すべてのプログラム</strong> \> <strong>Microsoft Exchange Server 2013</strong> \> <strong>Exchange ツールボックス</strong> の順にクリックします。

2.  <strong>メール フロー ツール</strong> セクションで、<strong>キュー ビューアー</strong> をダブルクリックします。

3.  操作ウィンドウで、<strong>サーバーに接続</strong> をクリックします。

4.  <strong>サーバーに接続</strong> ウィンドウで <strong>参照</strong> をクリックし、利用できるメールボックス サーバーの一覧を表示します。

5.  <strong>Exchange サーバーの選択</strong> ウィンドウで、メールボックス サーバーを選択します。メールボックス サーバーを検索するには、次の手順のいずれかを使用します。
    
      - <strong>検索</strong> ボックスに正確なサーバー名またはサーバー名の最初の数文字を入力し、<strong>検索開始</strong> をクリックします。 結果ウィンドウでサーバーを選択します。
    
      - <strong>表示</strong> メニューの <strong>フィルターを表示</strong> をクリックします。 <strong>名前</strong> 列または <strong>バージョン</strong> 列でフィルター アイコンをクリックし、フィルター演算子を選択します。 <strong>ここにテキストを入力してください</strong> ボックスにフィルター条件を入力します。 Enter キーを押します。 結果ウィンドウでサーバーを選択します。

6.  <strong>OK</strong> をクリックして、<strong>Exchange サーバーの選択</strong> ウィンドウを閉じます。

7.  サーバーを選択した後で、キュー ビューアーを開くたびに最初にこのサーバーが対象となるようにするには、<strong>サーバーに接続</strong> ウィンドウで <strong>既定のサーバーとして設定</strong> チェック ボックスをオンにします。

8.  <strong>サーバーに接続</strong> ウィンドウで、<strong>接続</strong> をクリックします。

## Exchange ツールボックスを使用してキュー ビューアーがリモート PowerShell の実行に使用するサーバーを指定する

1.  <strong>スタート</strong> \> <strong>すべてのプログラム</strong> \> <strong>Microsoft Exchange Server 2013</strong> \> <strong>Exchange ツールボックス</strong> の順にクリックします。

2.  <strong>メール フロー ツール</strong> セクションで、<strong>キュー ビューアー</strong> をダブルクリックします。

3.  操作ウィンドウで <strong>プロパティ</strong> をクリックします。

4.  <strong>キュー ビューアー - \<サーバー名\> プロパティ</strong> ダイアログ ボックスで、次のいずれかのオプションを選択します。
    
      - <strong>自動的に選択されたサーバーに接続する</strong>   リモート PowerShell を実行するために管理されているキューがあるサーバーに自動的に接続するには、このオプションを選択します。
    
      - <strong>接続するサーバーを指定する</strong>   リモート PowerShell を実行するサーバーを指定するには、このオプションを選択します。 このオプションを選択した場合、<strong>参照</strong> をクリックして、<strong>Exchange サーバーの選択</strong> ダイアログ ボックスを開きます。 リモート PowerShell を実行するサーバーを選択して、<strong>OK</strong> をクリックします。

## 正常な動作を確認する方法

指定したメールボックス サーバー上のキューを管理できるはずです。

