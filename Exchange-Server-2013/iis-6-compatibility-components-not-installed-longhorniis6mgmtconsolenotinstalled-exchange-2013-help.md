---
title: 'IIS 6 互換性コンポーネントがインストールされていない'
TOCTitle: IIS 6 互換性コンポーネントがインストールされていない_LonghornIIS6MgmtConsoleNotInstalled
ms:assetid: 8358eafb-def7-4b8d-8fe1-623bc5a0e20e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.longhorniis6mgmtconsolenotinstalled(v=EXCHG.150)
ms:contentKeyID: 48269722
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# IIS 6 互換性コンポーネントがインストールされていない\_LonghornIIS6MgmtConsoleNotInstalled

 

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

1.  <strong>スタート</strong> ボタンをクリックし、<strong>管理ツール</strong> をクリックします。次に、<strong>サーバー マネージャー</strong> をクリックします。

2.  ナビゲーション ウィンドウで、<strong>役割</strong> を展開し、<strong>Web サーバー (IIS)</strong> を右クリックします。次に、<strong>役割サービスの追加</strong> を選択します。

3.  <strong>役割サービスの選択</strong> ウィンドウで、<strong>IIS 6 管理互換</strong> まで下にスクロールします。

4.  <strong>IIS 6 メタベース互換</strong>、<strong>IIS 6 WMI 互換性</strong>、および <strong>IIS 6 管理コンソール</strong> チェックボックスをオンにします。

5.  <strong>役割サービスの選択</strong> ウィンドウで、<strong>次へ</strong> をクリックします。

6.  <strong>インストール オプションの確認</strong> ウィンドウで、<strong>インストール</strong> をクリックします。

7.  <strong>閉じる</strong> をクリックして、役割サービスの追加ウィザードを終了します。

**コントロール パネルからの IIS 6.0 管理互換コンポーネントの Windows 7 または Windows Vista へのインストール**

1.  <strong>スタート</strong> ボタンをクリックし、<strong>コントロール パネル</strong> をクリックします。次に、<strong>プログラムと機能</strong> をクリックして、<strong>Windows の機能の有効化または無効化</strong> をクリックします。

2.  <strong>インターネット インフォメーション サービス マネージャー</strong> を開きます。

3.  <strong>Web 管理ツール</strong> を開きます。

4.  <strong>IIS 6 と互換性のある管理</strong> を開きます。

5.  <strong>IIS 6 メタベースおよび IIS 構成互換性</strong>、<strong>IIS 6 WMI 互換姓</strong>、および <strong>IIS 6 管理コンソール</strong> チェックボックスをオンにします。

6.  <strong>OK</strong> をクリックします。

