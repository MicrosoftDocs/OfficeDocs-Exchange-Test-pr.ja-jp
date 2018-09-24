---
title: 'フェールオーバー クラスター コマンド インターフェイス Windows 機能がインストールされていない: Exchange 2013 Help'
TOCTitle: フェールオーバー クラスター コマンド インターフェイス Windows 機能がインストールされていない
ms:assetid: 0d839514-5ab7-497d-8945-41392b4c3980
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.rsatclusteringcmdinterfaceinstalled(v=EXCHG.150)
ms:contentKeyID: 51407500
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# フェールオーバー クラスター コマンド インターフェイス Windows 機能がインストールされていない

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2014-12-03_

ローカル コンピューターに必要な Windows 機能がないため、Microsoft Exchange Server 2013 のセットアップを続行できません。Exchange 2013 を続行する前に、この Windows 機能をインストールする必要があります。

Exchange 2013 セットアップがインストールを続行できるようにするには、**フェールオーバー クラスター コマンド インターフェイス** Windows 機能をコンピューターにインストールする必要があります。

このコンピューターに Windows の機能をインストールするには、次を実行します。この機能のインストールを完了するために再起動が必要な場合は、Exchange 2013 のセットアップを終了し、再起動してから、セットアップを再び起動します。


> [!NOTE]
> Exchange 2013 のセットアップを続行する前に、追加の Windows 機能または更新プログラムのインストールが必要になる場合があります。必要な Windows の機能と更新プログラムの完全な一覧については、「<A href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 の前提条件</A>」を確認してください。



1.  ローカル コンピューターで Windows PowerShell を開きます。

2.  次のコマンドを実行して、必要な Windows 機能をインストールします。
    
    ```powershell
    Install-WindowsFeature RSAT-Clustering-CmdInterface
    ```

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

探しているものは見つかりましたか？検索したい情報に関する[フィードバックを送信](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback)してください。

