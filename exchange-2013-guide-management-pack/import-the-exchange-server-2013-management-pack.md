---
title: Exchange Server 2013 管理パックのインポート
TOCTitle: Exchange Server 2013 管理パックのインポート
ms:assetid: dc929928-61b8-448b-9ae5-d3fa73a18ee9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn195914(v=EXCHG.150)
ms:contentKeyID: 53181898
ms.date: 04/03/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Server 2013 管理パックのインポート

 

_**トピックの最終更新日:**  2013-03-30_

最初に管理パックを SCOM 展開にインポートしましょう。

## 前提条件

管理パックをインポートする前に、次の条件を満たしていることを確認します。

  - 組織には、以下のいずれかのバージョンの System Center Operations Manager が導入されています。
    
      - System Center Operations Manager 2012 RMT 以降
    
      - System Center Operations Manager 2007 R2 以降

  - Exchange サーバーには既に SCOM エージェントが導入されています。[エージェントの展開状態を確認する](procedures-related-to-deployment.md).

  - Exchange サーバー上の SCOM エージェントは、ローカル システム アカウントで実行されています。[エージェントのセキュリティ構成を確認する](procedures-related-to-deployment.md).

  - Exchange サーバー上の SCOM エージェントはプロキシとして動作し、他のコンピューターの管理オブジェクトを検出するように構成されています。[エージェントのプロキシ構成を確認する](procedures-related-to-deployment.md).

  - ユーザー アカウントは、Operations Manager 管理者役割のメンバーです。

## Exchange Server 2013 管理パックのインポート

Exchange Server 2013 管理パックをインポートする手順は次のとおりです。この手順では、System Center Operations Manager (SCOM) サーバーのローカル ドライブに管理パックの内容を展開したと想定しています。Exchange Server 2013 管理パックを以下からダウンロードできます。

1.  SCOM サーバーにログオンして、[Microsoft ダウンロード センター](http://go.microsoft.com/fwlink/p/?linkid=268587)」から、Exchange Server 2013 管理パックをダウンロードします。

2.  `ExchangeServerManagementPack.msi` ファイルを実行して、管理パックの内容をシステム上のフォルダーに抽出します。

3.  SCOM コンソールを起動します。SCOM コンソールで **\[管理\]** をクリックします。

4.  **\[管理パック\]** を右クリックし、**\[管理パックのインポート\]** をクリックします。

5.  管理パックのインポート ウィザードを開きます。**\[追加\]** をクリックし、次に**\[ディスクから追加\]** をクリックします。

6.  **\[インポートする管理パックの選択\]** ダイアログ ボックスが表示されます。管理パックを抽出したたディレクトリを参照します。`Microsoft.Exchange.15.mp` ファイルをクリックし、**\[開く\]** をクリックします。

7.  **\[管理パックの選択\]** ページに Exchange Server 2013 管理パックが表示されます。**\[インストール\]** をクリックします。

8.  **\[管理パックのインポート\]** ページが表示され、進行状況が示されます。インポート プロセスのいずれかの段階で問題が発生した場合は、一覧内で管理パックを選択して状態の詳細を確認します。

9.  インポートが完了したら、**\[閉じる\]** をクリックします。

10. **\[表示\]**、**\[更新\]** とクリックするか、F5 を押して、管理パック一覧に Microsoft Exchange Server 2013 管理パックを表示します。

これで管理パックがインストールされました。新しいダッシュボードの詳細は、「[Exchange Server 2013 管理パックをお使いになる前に](getting-started-with-exchange-server-2013-management-pack.md)」を参照してください。

