---
title: 'Windows プロセス アクティブ化サービス - プロセス モデル コンポーネントが必要'
TOCTitle: Windows プロセス アクティブ化サービス - プロセス モデル コンポーネントが必要_LonghornWASProcessModelInstalled
ms:assetid: 8cc13dbb-4921-4c07-8602-d26613d7730a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.longhornwasprocessmodelinstalled(v=EXCHG.150)
ms:contentKeyID: 48269765
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Windows プロセス アクティブ化サービス - プロセス モデル コンポーネントが必要\_LonghornWASProcessModelInstalled

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2015-04-07_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Windows プロセス アクティブ化サービス - プロセス モデル機能がサーバーにインストールされていないため、Exchange Server 2010 セットアップ プログラムは Windows Server 2008 または Windows Server 2008 R2 ベースのコンピューターでインストールを続行できません。

Windows プロセス アクティブ化サービスは、インターネット インフォメーション サービス (IIS) プロセス モデルを一般化して、HTTP への依存を取り除きます。以前は HTTP アプリケーションでのみ利用可能だった IIS のすべての機能が、非 HTTP プロトコルを使用して、Windows Communication Foundation (WCF) サービスをホストするアプリケーションで使用できるようになりました。IIS 7.0 もまた、HTTP を介したメッセージ ベースのアクティブ化に Windows プロセス アクティブ化サービスを使用します。

プロセス モデルは Web サービスおよび WCF サービスをホストします。IIS 6.0 で導入されたプロセス モデルは、迅速な障害保護、正常性の監視、およびリサイクル機能を備えた新しいアーキテクチャです。

この問題を解決するには、このサーバーに Windows プロセス アクティブ化サービス - プロセス モデル機能をインストールして、Exchange 2010 セットアップ プログラムを再実行します。

**サーバー マネージャー ツールを使用した Windows プロセス アクティブ化サービス - プロセス モデルのインストール**

1.  **\[スタート\]** ボタンをクリックし、**\[管理ツール\]** をクリックします。次に、**\[サーバー マネージャー\]** をクリックします。

2.  左側のナビゲーション ウィンドウで、**\[機能\]** を右クリックし、**\[機能の追加\]** をクリックします。

3.  **\[機能の選択\]** ウィンドウで、**\[Windows プロセス アクティブ化サービス\]** まで下にスクロールします。

4.  **\[プロセス モデル\]** のチェック ボックスをオンにします。

5.  **\[機能の選択\]** ウィンドウで **\[次へ\]** をクリックし、**\[インストール オプションの確認\]** ウィンドウで **\[インストール\]** をクリックします。

6.  **\[閉じる\]** をクリックして、役割サービスの追加ウィザードを終了します。

