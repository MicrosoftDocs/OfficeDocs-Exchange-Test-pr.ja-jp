---
title: 'IIS 7 .NET 拡張性コンポーネントが必要_LonghornIIS7NetExt: Exchange 2013 Help'
TOCTitle: IIS 7 .NET 拡張性コンポーネントが必要_LonghornIIS7NetExt
ms:assetid: 8b481626-b68a-4fba-b66e-a02c03856bfd
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.longhorniis7netext(v=EXCHG.150)
ms:contentKeyID: 48269761
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# IIS 7 .NET 拡張性コンポーネントが必要\_LonghornIIS7NetExt

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2012-06-05_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft®Exchange Server 2010 セットアップ プログラムを続行できません。

Exchange 2010 が Windows PowerShell リモート処理を使用するには、対象サーバーに IIS 7 .NET 拡張機能コンポーネントがインストールされている必要があります。

このエラーに対処するには、サーバー マネージャーを使用して IIS 7 .NET 拡張機能コンポーネントをこのサーバーにインストールしてから、Exchange 2010 セットアップ プログラムを再度実行します。

**サーバー マネージャー ツールを使用した IIS 7 .NET 拡張性コンポーネントの Windows Server 2008 または Windows Server 2008 R2 へのインストール**

1.  **\[スタート\]** ボタンをクリックし、**\[管理ツール\]** をクリックします。次に、**\[サーバー マネージャー\]** をクリックします。

2.  左側のナビゲーション ウィンドウで、**\[役割\]** を展開し、**\[Web サーバー (IIS)\]** を右クリックします。次に、**\[役割サービスの追加\]** を選択します。

3.  **\[役割サービスの選択\]** ウィンドウで、**\[アプリケーション開発\]** まで下にスクロールします。

4.  **\[.NET 拡張機能\]** のチェック ボックスをオンにします。

5.  **\[役割サービスの選択\]** ウィンドウで **\[次へ\]** をクリックし、**\[インストール選択の確認\]** ウィンドウで **\[インストール\]** をクリックします。

6.  **\[閉じる\]** をクリックして、役割サービスの追加ウィザードを終了します。

