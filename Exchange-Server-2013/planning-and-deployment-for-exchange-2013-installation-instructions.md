---
title: '計画と展開: Exchange 2013 Help'
TOCTitle: 計画と展開
ms:assetid: 692c59e3-f0b0-4cef-a66e-751aa740abae
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998636(v=EXCHG.150)
ms:contentKeyID: 48269611
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 計画と展開

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

Exchange のインストールを行う上でガイダンスが必要ですか。この記事では、Microsoft Exchange Server 2013 の展開を計画するためのガイダンスと展開で必要となる記事へのリンクを提供します。

次のセクションには、Microsoft Exchange Server 2013 の計画と、その後の展開についての情報へのリンクが記載されています。


> [!IMPORTANT]
> 展開を開始する前に、「<A href="release-notes-for-exchange-2013-exchange-2013-help.md">Exchange 2013 のリリース ノート</A>」トピックをお読みください。リリース ノートには、展開中および展開後に発生する可能性のある問題について、重要な情報が含まれています。



**内容**

Exchange 2013 の計画

Exchange 2013 のインストールの展開

Exchange 2013 セットアップについて

詳細情報

## Exchange 2013 の計画

Exchange Server 2013 を組織に展開する計画に役立つ情報にアクセスするには、次のリンクを使用します。


> [!IMPORTANT]
> テスト環境への Exchange 2013 のインストールについては、後述する「テスト環境を確立する」を参照してください。



  - [メールボックスおよびクライアント アクセス サーバー](mailbox-and-client-access-servers-exchange-2013-help.md)  
    Exchange 2013 に含まれるメールボックス サーバーおよびクライアント アクセス サーバーの役割の詳細情報について。

<!-- end list -->

  - [Exchange 2013 のシステム要件](exchange-2013-system-requirements-exchange-2013-help.md)  
    Exchange 2013 をインストールする前に、満たす必要のある組織のシステム用件について理解します。

<!-- end list -->

  - [Exchange 2013 の前提条件](exchange-2013-prerequisites-exchange-2013-help.md)  
    Exchange 2013 の正しいインストールを実行するためにインストールする必要のある、Windows Server 2008 R2 Service Pack 1 (SP1) または Windows Server 2012 の機能、および他のソフトウェアについて理解します。

<!-- end list -->

  - [Exchange Server 展開アシスタント](exchange-server-deployment-assistant-exchange-2013-help.md)  
    このツールを使用して、計画、インストール、または Exchange 2013 へのアップグレードで使用するカスタマイズされたチェックリストを生成します。社内展開、ハイブリッド展開、またはクラウド展開を含む、複数のシナリオに合わせたガイダンスを利用できます。

<!-- end list -->

  - [Active Directory](active-directory-exchange-2013-help.md)  
    Exchange 2013 による Active Directory の使用法、および Active Directory の展開が Exchange の展開に与える影響については、このトピックをお読みください。

<!-- end list -->

  - [マルウェア対策保護](anti-malware-protection-exchange-2013-help.md)  
    Exchange 2013 のマルウェア対策保護オプションを理解するには、このトピックをお読みください。

<!-- end list -->

  - [Exchange Server のハイブリッド展開](https://technet.microsoft.com/ja-jp/library/jj200581\(v=exchg.150\))  
    Microsoft Office 365 と社内の Exchange 2013 組織のハイブリッド展開の計画に役立てるために、このトピックをお読みください。

<!-- end list -->

  - [高可用性とサイトの復元計画](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)  
    高可用性とビジネスの維持の実現を計画するために役立つ情報については、このトピックをお読みください。

<!-- end list -->

  - [SharePoint および Lync との統合](integration-with-sharepoint-and-lync-exchange-2013-help.md)  
    Exchange 2013、Microsoft SharePoint 2013、および Microsoft Lync 2013 の統合による製品をまたいでのアーカイブ、保持、電子情報開示、サイト メールボックス、認証、Lync のプレゼンス、その他を可能にする方法に関する詳細については、このトピックをお読みください。

<!-- end list -->

  - [ユニファイド メッセージングの計画](planning-for-unified-messaging-exchange-2013-help.md)  
    Exchange 2013 のユニファイド メッセージングの計画に関する詳細については、このトピックをお読みください。

<!-- end list -->

  - [Exchange 2013 記憶域構成オプション](exchange-2013-storage-configuration-options-exchange-2013-help.md)  
    Exchange 2013 メールボックス サーバーの役割がサポートする記憶域アーキテクチャ、ディスクの種類、および記憶域構成については、このトピックをお読みください。

<!-- end list -->

  - [Exchange 2013 仮想化](exchange-2013-virtualization-exchange-2013-help.md)  
    このトピックでは、仮想化環境における Exchange 2013 の展開方法の詳細を説明します。

<!-- end list -->

  - [Exchange 2013 でのマルチテナント機能](multi-tenancy-in-exchange-2013-exchange-2013-help.md)  
    Exchange 2013 を構成して、通常は電子メール、データ、ユーザー、グローバル アドレス一覧 (GAL)、またはその他の一般に使用される Exchange オブジェクトを共有しない、複数に分離した組織またはビジネス単位をホストする方法については、このトピックをお読みください。

<!-- end list -->

  - [Exchange 開発技術](https://go.microsoft.com/fwlink/p/?linkid=268448)  
    このトピックは、Exchange 2013 を使用するアプリケーション向けに利用できるアプリケーション プログラミング インターフェイス (API) に関する重要な情報を含みます。

## テスト環境を確立する

Exchange 2013 を初めてインストールする前に、隔離されたテスト環境にインストールすることを推奨します。このアプローチにより、エンドユーザーのダウンタイムの危険性と、運用環境への悪影響が軽減されます。

テスト環境は、運用環境への展開前に、新しい Exchange 2013 設計の「概念実証」として機能し、どのような実装の実施と取り消しも可能にします。検証とテスト用に専用のテスト環境を設けることにより、今後の運用環境に向けたインストール前チェックを行えるようになります。最初にテスト環境にインストールすることで、組織は、完全な運用実装でより確実に成果を上げることが可能になります。

運用環境を複製する必要があることから、ほとんどの組織にとってテスト ラボを構築するコストは高価になる可能性があります。プロトタイプ ラボに関連するハードウェア コストを削減するため、Windows Server 2008 R2 または Windows Server 2012 の Hyper-V テクノロジを使用した仮想化を使用することを推奨します。Hyper-V により、サーバーの仮想化が可能となるため、単一の物理マシン上で複数の仮想オペレーティング システムを実行できるようになります。

Hyper-V の詳細については、「[サーバー仮想化](https://go.microsoft.com/fwlink/p/?linkid=117704)」を参照してください (このサイトは英語の場合があります)。ハードウェア仮想化ソフトウェアでの、運用状態の Exchange 2013 の Microsoft サポートについては、「[Exchange 2013 のシステム要件](exchange-2013-system-requirements-exchange-2013-help.md)」の「ハードウェア仮想化」を参照してください。

## Exchange 2013 のインストールの展開

展開の段階とは、組織に Exchange 2013 をインストールする期間です。展開の段階を開始する前に、Exchange 組織を計画する必要があります。詳細については、前述の「Exchange 2013 の計画」を参照してください。

次のリンクを使用して、Exchange 2013 の展開で必要な情報にアクセスします。

  - [Active Directory とドメインを準備する](prepare-active-directory-and-domains-exchange-2013-help.md)  
    Exchange 2013 のために Active Directory フォレスト、およびフォレストに対して Exchange が行う変更について準備するために必要な手順について理解します。

<!-- end list -->

  - [セットアップ ウィザードを使用した Exchange 2013 のインストール](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)  
    このトピックの手順に従い、Exchange 2013 セットアップ ウィザードを使用して Exchange 2013 を新規の Exchange の組織にインストールします。

<!-- end list -->

  - [無人モードを使用した Exchange 2013 のインストール](install-exchange-2013-using-unattended-mode-exchange-2013-help.md)  
    このトピックの手順に従い、Exchange 2013 無人セットアップを使用して Exchange 2013 を新規の Exchange の組織にインストールします。

<!-- end list -->

  - [セットアップ ウィザードを使用して Exchange 2013 エッジ トランスポートの役割をインストールする](install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md)  
    このトピックの手順に従い、Exchange 2013 セットアップ ウィザードを使用して Exchange 2013 エッジ トランスポートの役割を境界ネットワークにインストールします。

<!-- end list -->

  - [Exchange 2013 から最新の累積更新プログラムまたは Service Pack へのアップグレード](upgrade-exchange-2013-to-the-latest-cumulative-update-or-service-pack-exchange-2013-help.md)  
    このトピックの手順に従い、最新の累積更新プログラムまたは Service Pack を組織の Exchange 2013 サーバーに適用します。

<!-- end list -->

  - [Exchange 2010 から Exchange 2013 へのアップグレード](upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md)  
    このトピックの手順に従い、Exchange 2013 を既存の Exchange 2010 組織にインストールします。

<!-- end list -->

  - [Exchange 2007 から Exchange 2013 へのアップグレード](upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md)  
    このトピックの手順に従い、Exchange 2013 を既存の Exchange 2007 組織にインストールします。

<!-- end list -->

  - [複数のフォレスト トポロジを Exchange 2013 に展開する](deploy-multiple-forest-topologies-for-exchange-2013-exchange-2013-help.md)  
    Active Directory フォレストが複数存在する組織に Exchange 2013 を展開する場合に役立つ情報については、このトピックをお読みください。

<!-- end list -->

  - [ボイス メールと UM の展開](deploying-voice-mail-and-um-exchange-2013-help.md)  
    Exchange 2013 ユニファイド メッセージングの展開 (新規展開またはアップグレード) については、このトピックをお読みください。

<!-- end list -->

  - [ハイブリッド展開の手順](https://technet.microsoft.com/ja-jp/library/jj200788\(v=exchg.150\))  
    既存のハイブリッド展開での Exchange 2013 の展開については、このトピックをお読みください。

<!-- end list -->

  - [Exchange 2013 のインストール後のタスク](exchange-2013-post-installation-tasks-exchange-2013-help.md)  
    Exchange 2013 のインストールを完了するための、インストール後のタスクについて理解します。

## Exchange 2013 セットアップについて

さまざまなエディションとバージョンの Exchange 2013 をインストールして管理するため、Exchange 2013 セットアップでは個別の種類とモードを使用できます。

## Exchange のエディションおよびバージョン

Exchange 2013 には、Standard Edition と Enterprise Edition の 2 つのサーバー エディションがあります。これらはプロダクト キーによって定義されるライセンス エディションです。詳細については、「[Exchange Server の使用許諾契約書](https://go.microsoft.com/fwlink/p/?linkid=237292)」を参照してください。

## Exchange セットアップの種類

Exchange 2013 セットアップには、以下のオプションがあります。

  - **Exchange のセットアップ UI**   Setup.exe をコマンドライン スイッチを使用せずに実行すると、Exchange 2013 セットアップ ウィザードの指示に従いながら対話形式でセットアップすることができます。

  - **Exchange 無人セットアップ**   Setup.exe をコマンドライン スイッチを使用して実行すると、Exchange を対話式のコマンドラインから、またはスクリプトを通してインストールすることができます。

Setup.exe は、Exchange 2013 の DVD またはダウンロードしたソース ファイルから入手できます。

## Exchange セットアップのモード

Exchange 2013 のセットアップには、次のような複数のインストール モードがあります。

  - **Install**   新しいサーバーの役割をインストールしたり、既存のインストールにサーバーの役割を追加したりする場合 (メンテナンス モード) は、このモードを使用します。このモードは、Exchange セットアップ ウィザードおよび無人インストールの両方から利用できます。

  - **Uninstall**   インストール済み Exchange をコンピューターから除去するには、このモードを使用します。このモードは、Exchange セットアップ ウィザードおよび無人インストールの両方から利用できます。

  - **Upgrade**   Exchange の既存のインストールがある場合に、累積更新プログラムまたは Service Pack をインストールするには、このモードを選択します。このモードは、Exchange セットアップ ウィザードおよび無人インストールの両方から利用できます。
    

    > [!NOTE]
    > Exchange 2013 では、Exchange の以前のバージョンからの社内アップグレードはサポートされていません。このモードは、累積更新プログラムまたは Service Pack をインストールする場合にのみ使用されます。



  - **RecoverServer**   サーバーに致命的な障害が発生し、データを回復する必要がある場合にはこのモードを使用します。障害の発生したサーバーと同じ完全修飾ドメイン名 (FQDN) を使用してサーバーをインストールし、**/m:RecoverServer** スイッチを指定してセットアップ実行する必要があります。復元する役割は指定しないでください。セットアップ プログラムは、Active Directory 内の Exchange Server オブジェクトを検出し、対応するファイルと構成を自動的にインストールします。サーバーを回復した後、データベースを復元し、追加設定を再構成できます。**RecoverServer** モードで実行する場合、サーバーに Exchange をインストールしておくことはできません。Exchange サーバー オブジェクトは Active Directory に存在している必要があります。このモードは、無人インストール中にのみ使用できます。


> [!NOTE]
> セットアップのモードは、他のモードを使用する前に終了しておく必要があります。



## 詳細情報

[Exchange 2013 での IPv6 サポート](ipv6-support-in-exchange-2013-exchange-2013-help.md)

[Exchange 2013 の Exchange 管理者センター](exchange-admin-center-in-exchange-2013-exchange-2013-help.md)

[Exchange 2013 の言語サポート](exchange-2013-language-support-exchange-2013-help.md)

[Exchange 2013 インストールの前提条件の確認](exchange-2013-readiness-checks-exchange-2013-help.md)

