---
title: 'World Wide Web Publishing Service が無効または見つからない_ShouldReRunSetupForW3SVC: Exchange 2013 Help'
TOCTitle: World Wide Web Publishing Service が無効または見つからない_ShouldReRunSetupForW3SVC
ms:assetid: f1815a6d-d16b-4271-9fab-84087465529e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.shouldrerunsetupforw3svc(v=EXCHG.150)
ms:contentKeyID: 48270232
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# World Wide Web Publishing Service が無効または見つからない\_ShouldReRunSetupForW3SVC

 

_**適用先:**Exchange Server_

_**トピックの最終更新日:**2012-06-05_

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

