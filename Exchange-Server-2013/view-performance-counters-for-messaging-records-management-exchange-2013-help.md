---
title: 'メッセージング レコード管理用のパフォーマンス カウンターを表示する: Exchange 2013 Help'
TOCTitle: メッセージング レコード管理用のパフォーマンス カウンターを表示する
ms:assetid: ec374d31-2797-4f8b-8c96-3839d01a662c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb397227(v=EXCHG.150)
ms:contentKeyID: 51407593
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メッセージング レコード管理用のパフォーマンス カウンターを表示する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2009-12-09_

Windows 信頼性とパフォーマンス モニター (Perfmon.exe) を使用して、メッセージング レコード管理 (MRM) のパフォーマンス カウンターを選択および表示できます。パフォーマンス カウンターを使用すると、多くのリソースを消費する MRM プロセスの実行時に、管理されたフォルダー アシスタントを監視できます。

MRM のパフォーマンス カウンターの一覧については、「[メッセージング レコード管理用のパフォーマンス カウンター](performance-counters-for-messaging-records-management-exchange-2013-help.md)」を参照してください。

MRM の監視に関連するその他のタスクについては、「[メッセージング レコード管理の監視](monitoring-messaging-records-management-exchange-2013-help.md)」を参照してください。

## Windows の信頼性およびパフォーマンス モニターを使用して、MRM のパフォーマンス カウンターを表示する

この手順を実行するには、使用するアカウントにローカルの Administrators グループのメンバーシップが委任されている必要があります。

1.  Windows 信頼性とパフォーマンス モニターを起動するには、<strong>スタート</strong>、<strong>ファイル名を指定して実行</strong> の順にクリックし、「**perfmon**」と入力します。

2.  コンソール ツリーで、<strong>監視ツール</strong> \> <strong>パフォーマンス モニター</strong> に移動します。

3.  ツール バーのプラス記号 (+) ボタンをクリックします。<strong>カウンターの追加</strong> ダイアログ ボックスが表示されます。

4.  <strong>次のコンピューターからカウンターを選ぶ</strong> 一覧で、次のオプションのうち 1 つを選択します。
    
      - この手順をローカル コンピューターで実行している場合は、<strong>\<ローカル コンピューター\></strong> を選択します。既定ではこのオプションが選択されています。
    
      - この手順をリモートで実行している場合は、監視するサーバーを選択します。

5.  パフォーマンス カウンターの一覧で、<strong>MSExchange Assistants - データベースごと</strong> または <strong>MSExchange 管理フォルダー アシスタント</strong> を展開します。

6.  監視するパフォーマンス カウンターを選択します。

7.  <strong>MSExchange Assistants - データベースごと</strong> のパフォーマンス カウンターの場合、すべてのメールボックス データベースのカウンターを表示するには、<strong>選択したオブジェクトのインスタンス</strong> で、<strong>すべてのインスタンス</strong> をクリックします。または、メールボックス データベースを 1 つ以上指定するには、一覧からインスタンスを選択します。

8.  カウンターが Windows 信頼性とパフォーマンス モニターに表示されるように選択したカウンターを追加し、パフォーマンス データの収集を開始するには、<strong>追加</strong> をクリックします。

