---
title: 'サーバーの役割のインストール中にセットアップ エラーが発生した_InstallWatermark: Exchange 2013 Help'
TOCTitle: サーバーの役割のインストール中にセットアップ エラーが発生した_InstallWatermark
ms:assetid: ad89ebd5-f9bb-40c1-8811-09b145c2b341
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.installwatermark(v=EXCHG.150)
ms:contentKeyID: 48269922
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# サーバーの役割のインストール中にセットアップ エラーが発生した\_InstallWatermark

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2016-12-09_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

サーバーの役割のインストール中に以前のセットアップ エラーが検出されたため、Microsoft Exchange Server 2007 セットアッププログラムを続行できません。

Exchange 2007 セットアップ プログラムを実行するには、他のセットアップ作業を続行する前に、インストールに失敗したサーバーの役割が正しく再インストールされているか、セットアップ処理から削除されている必要があります。

この問題を解決するには、インストールに失敗したサーバーの役割を再インストールするか、サーバーの役割を削除します。

**インストールに失敗したサーバーの役割をコマンド ラインから再インストールするには、次の操作を行います。**

1.  コマンド プロンプト ウィンドウを開き、インストール ファイルに移動します。

2.  次のコマンドを実行します。
    
    ```powershell
    Setup /roles:<Failed Server Role>
    ```
    
    以下の役割から、1 つ以上の役割を選択します。複数の場合はコンマで区切ります。
    
    ClientAccess (CA または C)
    
    EdgeTransport (ET または E)
    

    > [!NOTE]
    > 1 台のコンピューター上でエッジ トランスポート サーバーの役割と他のサーバーの役割を共存させることはできません。

    

    > [!NOTE]
    > エッジ トランスポート サーバーの役割は、境界ネットワーク内および Active Directory&nbsp;フォレストの外側に展開する必要があります。

    
    HubTransport (HT または H)
    
    Mailbox (MB または M)
    
    UnifiedMessaging (UM または U)
    
    ManagementTools (MT または T)
    

    > [!NOTE]
    > ManagementTools を指定すると、Exchange 管理コンソール、Exchange 管理シェル用の Exchange コマンドレット、Exchange ヘルプ ファイル、Exchange ベスト プラクティス アナライザー ツール、Exchange トラブルシューティング アシスタントがインストールされます。その他のサーバーの役割をインストールした場合、管理ツールは自動的にインストールされます。

    
    たとえば、既存のメールボックス サーバーにハブ トランスポート サーバーの役割を追加するには、次のように入力します。**%LocalExchangeInstallationDir%\\bin\\Setup.com /role:HubTransport /Mode:Install**


> [!NOTE]
> いずれかの Exchange Server&nbsp;2007 サーバーの役割が以前に正しくインストールされている場合、セットアップ ウィザードは保守モードで実行されます。以前に正しくインストールされた Exchange 2007 サーバーの役割がない場合、セットアップ ウィザードは停止されたところから開始されます。



**Exchange Server 2007 セットアップ ウィザードを保守モードで使用して、インストールに失敗したサーバーの役割を再インストールするには、次の操作を行います。**

1.  サーバーの役割を再インストールするサーバーにログオンします。

2.  コントロール パネルを開き、<strong>プログラムの追加と削除</strong> をダブルクリックします。

3.  <strong>プログラムの変更と削除</strong> ページで、<strong>Microsoft Exchange Server</strong> を選択し、<strong>変更</strong> をクリックします。

4.  Exchange Server 2007 セットアップ ウィザードの <strong>Exchange 保守モード</strong> ページで、<strong>次へ</strong> をクリックします。

5.  <strong>サーバーの役割の選択</strong> ページで、インストールするサーバーの役割のチェック ボックスをオンにし、<strong>次へ</strong> をクリックします。
    

    > [!NOTE]
    > 1 台のコンピューター上でエッジ トランスポート サーバーの役割と他のサーバーの役割を共存させることはできません。

    

    > [!NOTE]
    > エッジ トランスポート サーバーの役割は、境界ネットワーク内および Active Directory&nbsp;フォレストの外側に展開する必要があります。

    

    > [!NOTE]
    > [管理ツール] を選択すると、Exchange 管理コンソール、Exchange 管理シェル用の Exchange コマンドレット、Exchange ヘルプ ファイルがインストールされます。その他のサーバーの役割をインストールした場合、管理ツールは自動的にインストールされます。



6.  <strong>ハブ トランスポートの役割</strong> を選択し、既存の Exchange Server 2003 組織または Exchange 2000 Server 組織を含むフォレスト内に Exchange 2007 をインストールする場合は、<strong>メール フローの設定</strong> ページでルーティング グループ コネクタの作成対象となる Exchange 2003 または Exchange 2000 のルーティング グループのメンバーである既存の組織内のブリッジヘッド サーバーを選択します。

7.  <strong>インストールの前提条件の確認</strong> ページで、状態を表示して、組織およびサーバーの役割の前提条件の確認が正しく完了したかどうかを確認します。正しく完了した場合は、<strong>インストール</strong> をクリックして Exchange 2007 をインストールします。

8.  <strong>完了</strong> ページで、<strong>終了</strong> をクリックします。

**他のサーバーの役割が以前に正しくインストールされていない場合、Exchange Server 2007 セットアップ ウィザードを使用して、インストールに失敗したサーバーの役割を再インストールするには、次の操作を行います。**

1.  Exchange Server 2007 製品ドキュメントの「Exchange Server 2007 セットアップを使用してカスタム インストールを実行する方法」([https://go.microsoft.com/fwlink/?LinkId=86648](https://go.microsoft.com/fwlink/?linkid=86648)) に記載されている指示に従ってください。

**インストールに失敗したサーバーの役割を削除するには、次の操作を行います。**

1.  Exchange Server 2007 製品ドキュメントの「Exchange 2007 サーバーの役割を削除する方法」([https://go.microsoft.com/fwlink/?LinkId=86649](https://go.microsoft.com/fwlink/?linkid=86649)) に記載されている指示に従ってください。

## 詳細情報

Exchange 2007 を無人モードでインストールする方法の詳細については、「無人モードで Exchange 2007 をインストールする方法」([https://go.microsoft.com/fwlink/?LinkId=86476](https://go.microsoft.com/fwlink/?linkid=86476)) をご覧ください。

