---
title: 'サンプル コードを使用してフォレスト間のメールボックス移動を準備する: Exchange 2013 Help'
TOCTitle: サンプル コードを使用してフォレスト間のメールボックス移動を準備する
ms:assetid: f35ac7a5-bb84-4653-b6d0-65906e93627b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee861124(v=EXCHG.150)
ms:contentKeyID: 49896553
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# サンプル コードを使用してフォレスト間のメールボックス移動を準備する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

Microsoft Exchange 2013 では、**New-MoveRequest** および **New-MigrationBatch** コマンドレットを使用してメールボックスの移動および移行ができます。Exchange 管理センター (EAC) 経由でメールボックスを移動することもできます。移動元の Exchange フォレストから移動先の Exchange 2010 フォレストにメールボックスを移動できます。

**New-MoveRequest** を実行するには、メール ユーザーが移動先 Exchange フォレストに存在し、最低限必要な Active Directory 属性の集合を持っている必要があります。Microsoft アイデンティティのライフサイクル Manager (ILM) 2007 の展開をカスタマイズすることで、必要なメール ユーザーを移動先 Exchange フォレストに作成することができます。ここで説明している ILM ベースのルールの拡張のサンプル コードは、現在の ILM の展開をカスタマイズして、必要となるメールが有効なユーザーを移動先 Exchange 2013 フォレストに作成する方法を示しています。

必要な Active Directory 属性の説明などの、フォレスト間の移動の準備の詳細については、「[メールボックスでフォレスト間の移動要求の準備を行う](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - Microsoft ダウンロード センターの「[メールボックスのオンライン移動の準備](https://go.microsoft.com/fwlink/p/?linkid=177882)」ページからサンプル コードをダウンロードします。

  - サンプル コードを実行するには、ILM 2007 Feature Pack 1 Service Pack 1 (SP1) が必要です。Feature Pack をダウンロードするには、Microsoft サポート技術情報の文書番号 977791「[Service Pack 1 (ビルド 3.3.1139.2) アイデンティティのライフサイクル Manager 2007 機能 Pack 1 用には](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=977791)」を参照してください。

  - 次のものも必要です。
    
      - 現在メールボックスが存在し、Exchange 2013 を実行している移動元のフォレスト。
    
      - メールボックスの移動先となる、Exchange 2013 がインストールされた移動先のフォレスト。

  - Exchange 2013 移動先フォレストに接続するには、**UpdateRecipient** コマンドレットを呼び出すための適切なアクセス許可を持つ必要があります。必要なアクセス許可を確認するには、「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「受信者プロビジョニングのアクセス許可」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 実行方法

## 手順 1:ILM のサンプル コードをインストールする

1.  Microsoft Visual Studio 2008 で、Microsoft.Exchange.Sample.OneWayGALSync.sln を開いて、サンプル コードを表示します。サンプル コードは、次を含みます。
    
      - Microsoft.MetadirectoryServicesEx.dll は ILM 2007 FP1 SP1 に付属しているバイナリ ファイルで、\\Program Files\\Microsoft Identity Integration Server\\Bin\\Assemblies の下にあります。これはサンプル コードで参照されています。
    
      - OneWaySync.xml は、サンプル コードで参照されています。
    
      - ILMServerConfig フォルダーには、移動元管理エージェント (MA)、移動先 MA、および ILM メタバース (MV) 用の ILM 構成ファイルが含まれます。
    
      - Microsoft.Exchange.Sample.OneWayGALSync.MARules.dll および Microsoft.Exchange.Sample.OneWayGALSync.MVRules.dll (サンプル コードからビルド) は、\\obj\\Debug の下にあります。

2.  ILM サーバーで、次のものを \\Program Files\\Microsoft Identity Integration Server\\Extensions にコピーします。
    
      - OneWaySync.xml
    
      - Microsoft.Exchange.Sample.OneWayGALSync.MARules.dll
    
      - Microsoft.Exchange.Sample.OneWayGALSync.MVRules.dll

3.  手順 1 で ILM Extensions フォルダーにコピーした OneWaySync.xml ファイルを編集し、メール ユーザーを作成する移動先 Exchange フォレストに TargetOU コンテナーの distinguishedName (DN) を指定します。名前がわからない場合には、LDP.exe または ADSIEdit.exe を使用して TargetOU コンテナーを参照することができます。
    

    > [!NOTE]
    > このサンプルを ILM GalSync 2007 と共に使用している場合、このコンテナーを GalSync2007 が管理するコンテナーの一覧から除外します。



4.  ILM Identity Manager コンソールで、<strong>ファイル</strong> \> <strong>サーバー構成のインポート</strong> の順にクリックして、ILMServerConfig フォルダーから ILM サーバー構成をインポートします。この操作により、2 つの Active Directory 管理エージェントがメタバース スキーマおよびプロビジョニング ルールと共にインポートされます。
    

    > [!NOTE]
    > インポート中に、フォレスト名と資格情報を指定し、インポートされた Active Directory 管理エージェント (ADMA) のパーティションを、移動元および移動先 ADMA の両方の構成内のパーティション名に一致させる必要があります。



5.  Exchange 2013 移動先フォレストをサポートする ADMA に対し、<strong>管理エージェントの作成</strong> ページの <strong>拡張の構成</strong> ウィンドウで、<strong>プロビジョニング対象</strong> ドロップダウン リストから <strong>Exchange 2013</strong> を選択し、Exchange 2010 クライアント アクセス サーバーのリモート Windows PowerShell の URI を <strong>Exchange 2013 RPS URI</strong> に入力します。
    
    <strong>管理エージェントの作成\] ページ**
    
    ![管理エージェントの Exchange 2010 プロビジョニング](images/Aa998597.8f403cda-e5e4-4edf-887f-c1ed46cee3f5(EXCHG.150).gif "管理エージェントの Exchange 2010 プロビジョニング")  

6.  ILM Identity Manager コンソールの <strong>管理エージェントの作成</strong> ウィンドウで、移動元フォレストの管理エージェントの <strong>プロパティ</strong> を開きます。<strong>ディレクトリ パーティションの構成</strong> ウィザードを選択し、<strong>コンテナー</strong> をクリックして、移動先フォレストに移動中のメールボックスを含むコンテナーを選択します。他のすべてのコンテナーの選択をオフにして、管理エージェントのスコープをこの 1 つのコンテナーの管理だけにします。同様に、移動先フォレストの MA に対し、メールが有効なユーザーがプロビジョニングされるコンテナー、つまり手順 2 で指定した TargetOU を選択します。
    

    > [!NOTE]
    > このサンプルを ILM GalSync 2007 と共に使用している場合、この両方のコンテナーを GalSync2007 が管理するコンテナーの一覧から除外します。



7.  ILM が手順 2 で指定した TargetOU を検出できるように、移動先の MA で最初のフル インポート (ステージングのみ) を実行します。

## 手順 2:移動先 Exchange フォレストにメール ユーザーを作成する

これでサンプル コードのインストールが終了しました。次の手順を使用して、移動先 Exchange フォレストに必要なメール ユーザーを作成し、**New-MoveRequest** を実行してオンラインのメールボックス移動を実行できるようにします。

1.  移動元フォレストで、Exchange 管理センターを使用して、「ILM のサンプル コードをインストールする」のステップ 4 で選択したコンテナーにメールボックス ユーザーを作成します。Active Directory のユーザーとコンピューターを使用し、既存のメールボックス ユーザーをコンテナーに移動することもできます。

2.  移動元の MA でデルタ インポートおよびデルタ同期を実行し、移動元コンテナーに追加されたメールボックスを検出し、メール ユーザーを移動先の MA にプロビジョニングします。

3.  移動先の MA でエクスポートを実行し、手順 1 でプロビジョニングされたメール ユーザーを移動先 Active Directory へエクスポートします。

4.  移動先の MA でデルタ インポートを実行し、手順 2 でエクスポートされた変更を確認します。

5.  移動先フォレストで、Exchange 管理シェルを開き、**New-MoveRequest** コマンドレットを使用して移動元フォレストからメールボックスを移動します。

## 正常な動作を確認する方法

移行が正常に完了したことを確認するには、次の手順を実行します。

  - 移動先フォレストで、移動元フォレストから移動したユーザーが移動先フォレストに存在することを確認します。

