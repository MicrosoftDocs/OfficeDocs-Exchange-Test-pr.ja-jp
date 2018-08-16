---
title: 'Windows Server バックアップを使用して Exchange のバックアップを復元する: Exchange 2013 Help'
TOCTitle: Windows Server バックアップを使用して Exchange のバックアップを復元する
ms:assetid: 2d0f31dc-eb32-451a-8852-591269026506
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd876864(v=EXCHG.150)
ms:contentKeyID: 48269310
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Windows Server バックアップを使用して Exchange のバックアップを復元する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-06-18_

Windows Server Backup を使用して、Exchange データベースのバックアップと復元を行うことができます。Exchange には、ボリューム シャドウ コピー サービス (VSS) ベースで Exchange データのバックアップの作成と復元ができる Windows Server Backup のプラグインが組み込まれています。詳細については、「[Windows Server バックアップを使用した Exchange データのバックアップと復元](using-windows-server-backup-to-back-up-and-restore-exchange-data-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分にデータの復元にかかる時間を合計した時間

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「メールボックス回復」。

  - Windows Server Backup 機能はローカル コンピューターにインストールする必要があります。

  - データベースを元の場所に復元する場合、データベースをダーティ シャットダウン状態のままにして、システムによってマウントできるようにできます。(回復用のデータベースを使用する準備などで) 代わりの場所に復元する場合は、Exchange サーバー データベース ユーティリティ (Eseutil.exe) を使用して手動でクリーン シャットダウン状態にする必要があります。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## Windows Server バックアップを使用して Exchange のバックアップを復元する

1.  Windows Server Backup を起動します。

2.  <strong>ローカル バックアップ</strong> を選択します。

3.  操作ウィンドウで <strong>回復...</strong> をクリックすると、回復ウィザードが開始します。

4.  <strong>作業の開始</strong> ページで、以下のいずれかの操作を行います。
    
      - 回復するデータをローカル サーバーにバックアップした場合は、<strong>このサーバー (サーバー名)</strong> を選択してから <strong>次へ</strong> をクリックします。
    
      - 回復するデータが他のサーバーからのデータである場合、または回復するバックアップが別のコンピューターにある場合は、<strong>別のサーバー</strong> を選択し、<strong>次へ</strong> をクリックします。<strong>バックアップの場所の種類指定</strong> ページで、<strong>ローカル ドライブ</strong> または <strong>リモート共有フォルダー</strong> を選択し、<strong>次へ</strong> をクリックします。<strong>ローカル ドライブ</strong> を選択した場合は、<strong>バックアップの場所の選択</strong> ページでバックアップを含むドライブを選択し、<strong>次へ</strong> をクリックします。<strong>リモート共有フォルダー</strong> を選択した場合は、<strong>リモート フォルダーの指定</strong> ページでバックアップ データの UNC パスを入力し、<strong>次へ</strong> をクリックします。

5.  <strong>バックアップの日付の選択</strong> ページで、回復するバックアップの日時を選択し、<strong>次へ</strong> をクリックします。

6.  <strong>回復の種類の選択</strong> ページで、<strong>アプリケーション</strong> を選択し、<strong>次へ</strong> をクリックします。
    

    > [!NOTE]
    > 選択肢として<STRONG>[アプリケーション]</STRONG> が使用できない場合は、復元用に選択したバックアップはフォルダー レベルのバックアップで、ボリューム レベルのバックアップではないことが示されます。Windows Server Backup で Exchange データをバックアップする場合は、ボリューム レベルでバックアップを実行する必要があります。



7.  <strong>アプリケーションの選択</strong> ページで、Exchange が <strong>アプリケーション</strong> フィールドで選択されていることを確認します。<strong>詳細の表示</strong> をクリックして、バックアップのアプリケーション コンポーネントを表示します。回復するバックアップが最新のものである場合は、<strong>アプリケーション データベースのロールフォワード回復を実行しない</strong> チェック ボックスが表示されます。コミットしていないトランザクション ログをすべてコミットすることで、Windows Server Backup が回復するデータベースをロール フォワードしないようにするには、このチェック ボックスをオンにします。<strong>次へ</strong> をクリックします。

8.  <strong>回復オプションの指定</strong> ページで、データの回復先の場所を次のように指定し、<strong>次へ</strong> をクリックします。
    
      - Exchange データを直接元の場所に復元する場合は、<strong>元の場所に回復する</strong> を選択します。このオプションを使用する場合、どのデータベースを復元するかを選択することはできません。ボリューム上でバックアップされたデータベースはすべて元の場所に復元されます。
    
      - 個別のデータベースおよびファイルを指定の場所に回復する場合は、<strong>別の場所に回復する</strong> を選択します。別の場所を指定するには、<strong>参照</strong> をクリックします。このオプションを使用すると、どのデータベースを復元するかを選択できます。回復したデータ ファイルは、その後回復用データベースに移動したり、手動で元の場所に移動したり、[データベースの移植性](database-portability-exchange-2013-help.md) を使用して Exchange 組織内の別の場所にマウントすることができます。データベースを代替の場所に回復する場合、回復したデータベースはダーティ シャットダウン状態になります。復元処理が完了したら、Eseutil.exe を使用してデータベースを手動でクリーン シャットダウン状態にする必要があります。

9.  <strong>確認</strong> ページで、回復の設定を確認し、<strong>回復</strong> をクリックします。

10. <strong>回復の進行状況</strong> ページで、回復操作の状態と進行状況を確認できます。

11. 回復操作が完了したら、<strong>閉じる</strong> をクリックします。

## 正常な動作を確認する方法

<strong>回復の進行状況</strong> ページに、回復処理が正常に完了したかどうかが示されます。さらにデータを正常に復元できたことを確認するには、次のいずれかを実行します。

  - バックアップ先のディレクトリを調べ、復元されたデータがあることを確認します。

  - Windows Server バックアップを実行したサーバーで、バックアップ ログを表示して、ジョブが正常に完了したことを確認します。

  - イベント ビューアーを開いて、復元完了イベントがアプリケーション イベント ログに記録されたことを確認します。

