---
title: 'World Wide Web 発行サービスが無効または見つからない'
TOCTitle: World Wide Web Publishing Service が無効または見つからない_W3SVCDisabledOrNotInstalled
ms:assetid: 2d26d778-ddf1-4225-b5e2-f6b49d819c94
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.w3svcdisabledornotinstalled(v=EXCHG.150)
ms:contentKeyID: 48269311
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# World Wide Web Publishing Service が無効または見つからない\_W3SVCDisabledOrNotInstalled

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2012-06-05_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

メールボックス サーバーの役割またはクライアント アクセスの役割をインストールしようとしたときに、このコンピューターで World Wide Web Publishing サービスが無効になっているかまたはインストールされていないことが検出されたため、Microsoft® Exchange Server 2007 セットアップ プログラムを続行できません。

Exchange 2007 セットアップ プログラムを実行するには、Microsoft Exchange をインストールするコンピューターに World Wide Web Publishing サービスがインストールされ、無効以外の状態に設定されている必要があります。

この問題を解決するには、ローカル コンピューターに World Wide Web Publishing サービスがインストールされ、無効以外の状態になっていることを確認した後、Microsoft Exchange セットアップ プログラムを再実行します。

**World Wide Web Publishing サービスがインストールされ、無効以外の状態になっていることを確認するには、次の操作を行います。**

1.  デスクトップの **\[マイ コンピューター\]** を右クリックし、**\[管理\]** をクリックします。

2.  **\[サービスとアプリケーション\]** ノードを展開し、**\[サービス\]** ノードをクリックします。

3.  右側のペインで、**\[World Wide Web Publishing Service\]** を見つけます。
    
    インストールされているサービスの一覧に **\[World Wide Web Publishing Service\]** が表示されない場合は、以下の手順を実行してインストールします。

4.  **\[World Wide Web Publishing Service\]** が表示されても、状態が **\[開始\]** になっていない場合は、以下の手順を実行して開始します。

5.  **\[World Wide Web Publishing Service\]** を右クリックし、**\[プロパティ\]** をクリックします。

6.  **\[スタートアップの種類\]** が **\[自動\]** に設定され、**\[サービスの状態\]** が **\[開始\]** に設定されていることを確認します。

7.  **\[適用\]** をクリックし、**\[OK\]** をクリックします。

**World Wide Web Publishing サービスをインストールするには、次の操作を行います。**

1.  **\[スタート\]** ボタンをクリックし、**\[設定\]** をポイントします。次に、**\[コントロール パネル\]** をポイントし、**\[プログラムの追加と削除\]** をクリックします。

2.  **\[Windows コンポーネントの追加と削除\]** をクリックします。

3.  **\[コンポーネント\]** ボックスの一覧で、**\[アプリケーション サーバー\]** チェック ボックスをオンにし、**\[詳細\]** をクリックします。

4.  **\[インターネット インフォメーション サービス マネージャー\]** を選択し、**\[詳細\]** をクリックします。

5.  **\[WWW (World Wide Web) サービス\]** を選択し、チェック ボックスをオンにします。

6.  **\[OK\]** を 2 回クリックして **\[コンポーネント\]** ボックスの一覧に戻り、**\[次へ\]** をクリックします。

7.  IIS サービスがインストールされたら、**\[完了\]** をクリックします。

