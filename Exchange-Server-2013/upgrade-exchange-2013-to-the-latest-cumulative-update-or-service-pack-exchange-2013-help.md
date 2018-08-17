---
title: 'Exchange 2013 から最新の累積更新プログラムまたは Service Pack へのアップグレード: Exchange 2013 Help'
TOCTitle: Exchange 2013 から最新の累積更新プログラムまたは Service Pack へのアップグレード
ms:assetid: 928a4a0b-0082-4d50-a696-bfaf2782f42d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ983803(v=EXCHG.150)
ms:contentKeyID: 52057833
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 から最新の累積更新プログラムまたは Service Pack へのアップグレード

 

_**適用先:** Exchange Online, Exchange Server, Exchange Server 2013_

_**トピックの最終更新日:** 2015-09-04_

Microsoft Exchange Server 2013 がインストールされている場合、それを最新の Exchange 2013 累積更新プログラムまたは Service Pack にアップグレードできます。Exchange 2013 セットアップ ウィザードを使用すると、Exchange 2013 の現在のバージョンをアップグレードできます。最新の Exchange 2013 累積更新プログラムまたは Service Pack の詳細については、「[Exchange 2013 の更新プログラム](updates-for-exchange-2013-exchange-2013-help.md)」を参照してください。Exchange 2013 の詳細については、「[Exchange 2013 の新機能](what-s-new-in-exchange-2013-exchange-2013-help.md)」を参照してください。


> [!WARNING]
> Exchange 2013 をより新しい累積更新プログラムまたは Service Pack にアップグレードした後、新しいバージョンをアンインストールして前のバージョンに戻すことはできません。新しいバージョンをアンインストールすると、サーバーから Exchange が削除されることになります。



## 始める前に把握しておくべき情報

  - 予想所要時間 : 60 分

  - Exchange 2013 をアンインストールする前に、リリース ノートをお読みください。詳細については、「[Exchange 2013 のリリース ノート](release-notes-for-exchange-2013-exchange-2013-help.md)」を参照してください。

  - 累積更新プログラムまたは Service Pack をインストールする予定のサーバーが、システム要件および前提条件を満たしていることを確認してください。詳細については、「[Exchange 2013 のシステム要件](exchange-2013-system-requirements-exchange-2013-help.md)」および「[Exchange 2013 の前提条件](exchange-2013-prerequisites-exchange-2013-help.md)」を参照してください。
    

    > [!WARNING]
    > Exchange XML アプリケーション構成ファイルで行うカスタマイズ済みのサーバーごとの設定 (クライアント アクセス サーバーの web.config ファイルまたはメールボックス サーバーの EdgeTransport.exe.config ファイルなど) は、Exchange 累積更新プログラム (CU) のインストール時に上書きされます。インストール後にサーバーを簡単に再構成できるよう、必ずこの情報を保存しておいてください。これらの設定は、Exchange 累積更新プログラムのインストール後に構成し直す必要があります。



  - 累積更新プログラムまたは Service Pack をインストールした後、レジストリとオペレーティング システムに実際に変更が加えられるようにするため、コンピューターを再起動する必要があります。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## Exchange 2013 の累積更新プログラムまたは Service Pack のインストール

Exchange 2013 の累積更新プログラムまたは Service Pack は、セットアップ ウィザードを使用しても、無人モードでもインストールできます。具体的な手順は、以下のトピックを参照してください。

  - [セットアップ ウィザードを使用した Exchange 2013 のインストール](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)

  - [無人モードを使用した Exchange 2013 のインストール](install-exchange-2013-using-unattended-mode-exchange-2013-help.md)

サービス パックや累積的な更新プログラムをインストールしたコンピューターが、データベース可用性グループ (DAG) のメンバーである場合、「[データベース可用性グループの管理](managing-database-availability-groups-exchange-2013-help.md)」トピックの「[DAG メンバーに対するメンテナンスの実行](managing-database-availability-groups-exchange-2013-help.md)」セクションの手順に従ってください。

