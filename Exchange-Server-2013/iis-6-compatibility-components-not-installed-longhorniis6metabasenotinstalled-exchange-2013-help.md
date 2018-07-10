---
title: 'IIS 6 互換性コンポーネントがインストールされていない_LonghornIIS6MetabaseNotInstalled: Exchange 2013 Help'
TOCTitle: IIS 6 互換性コンポーネントがインストールされていない_LonghornIIS6MetabaseNotInstalled
ms:assetid: 0bd52987-d3cc-496c-ac8c-d35591405195
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.longhorniis6metabasenotinstalled(v=EXCHG.150)
ms:contentKeyID: 48269169
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# IIS 6 互換性コンポーネントがインストールされていない\_LonghornIIS6MetabaseNotInstalled

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2012-06-05_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft®Exchange Server 2007 セットアップ プログラムは、以下の Windows オペレーティング システムでは、クライアント アクセス サーバーのサーバーの役割、メールボックス サーバーの役割、または Exchange 2007 管理ツールのインストール試行を続行できません。

  - Windows Server 2008 R2

  - Windows Server 2008

  - Windows 7 (管理ツールのみ）

  - Windows Vista (管理ツールのみ）

この問題は、Internet Information Server (IIS) 6 メタベース互換コンポーネントと IIS 6 管理コンソール コンポーネントがインストールされていないために発生します。

Exchange 2007 セットアップ プログラムを実行するには、Exchange 2007 クライアント アクセス サーバーの役割、メールボックス サーバーの役割、または Exchange 2007 管理ツールをインストールするコンピューターに、IIS 6 メタベース互換コンポーネントと IIS 6 管理コンソール コンポーネントがインストールされている必要があります。

この問題を解決するには、IIS 6 メタベース互換コンポーネントを対象のコンピューターにインストールしてから、Microsoft Exchange セットアップ プログラムに戻ります。

**サーバー マネージャー ツールを使用した IIS 6.0 管理互換コンポーネントの Windows Server 2008 R2 または Windows Server へのインストール**

1.  **\[スタート\]** ボタンをクリックし、**\[管理ツール\]** をクリックします。次に、**\[サーバー マネージャー\]** をクリックします。

2.  ナビゲーション ウィンドウで、**\[役割\]** を展開し、**\[Web サーバー (IIS)\]** を右クリックします。次に、**\[役割サービスの追加\]** を選択します。

3.  **\[役割サービスの選択\]** ウィンドウで、**\[IIS 6 管理互換\]** まで下にスクロールします。

4.  **\[IIS 6 メタベース互換\]**、**\[IIS 6 WMI 互換性\]**、および **\[IIS 6 管理コンソール\]** チェックボックスをオンにします。

5.  **\[役割サービスの選択\]** ウィンドウで、**\[次へ\]** をクリックします。

6.  **\[インストール オプションの確認\]** ウィンドウで、**\[インストール\]** をクリックします。

7.  **\[閉じる\]** をクリックして、役割サービスの追加ウィザードを終了します。

**コントロール パネルからの IIS 6.0 管理互換コンポーネントの Windows 7 または Windows Vista へのインストール**

1.  **\[スタート\]** ボタンをクリックし、**\[コントロール パネル\]** をクリックします。次に、**\[プログラムと機能\]** をクリックして、**\[Windows の機能の有効化または無効化\]** をクリックします。

2.  **\[インターネット インフォメーション サービス マネージャー\]** を開きます。

3.  **\[Web 管理ツール\]** を開きます。

4.  **\[IIS 6 と互換性のある管理\]** を開きます。

5.  **\[IIS 6 メタベースおよび IIS 構成互換性\]**、**\[IIS 6 WMI 互換姓\]**、および **\[IIS 6 管理コンソール\]** チェックボックスをオンにします。

6.  **\[OK\]** をクリックします。

