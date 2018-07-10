---
title: '無人モードを使用した Exchange 2013 のインストール: Exchange 2013 Help'
TOCTitle: 無人モードを使用した Exchange 2013 のインストール
ms:assetid: 386465e9-41da-4e26-9816-b3b69be1f8bf
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997281(v=EXCHG.150)
ms:contentKeyID: 48269369
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 無人モードを使用した Exchange 2013 のインストール

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-06-19_

無人セットアップを実行するには、コマンド プロンプトから Microsoft Exchange Server 2013 をインストールします。Exchange 2013 の計画および展開の詳細については、「[計画と展開](planning-and-deployment-for-exchange-2013-installation-instructions.md)」を参照してください。

エッジ トランスポートの役割は、組織内部の Active Directory フォレストの外側にある境界ネットワークにインストールすることをお勧めします。エッジ トランスポート サーバーの役割をドメインによって結合されたコンピューターにインストールできますが、これにより可能になるのは Windows の機能と設定のドメイン管理のみです。エッジ トランスポートの役割自体は Active Directory を使用しません。その代わりに、構成と受信者情報を格納するActive Directoryライトウェイト ディレクトリ サービス (AD LDS) Windows機能を使用します。エッジ トランスポートの役割について、詳細は「[エッジ トランスポート サーバー](edge-transport-servers-exchange-2013-help.md)」を参照してください。


> [!TIP]
> Exchange Server 展開アシスタントについて聞いたことがありますか。これは、いくつかの質問を通して特別にカスタマイズされた展開チェックリストを作成することにより、組織への Exchange 2013 の迅速な展開を支援する無料のオンライン ツールです。この詳細については、「<A href="exchange-server-deployment-assistant-exchange-2013-help.md">Exchange Server 展開アシスタント</A>」にアクセスしてください。




> [!NOTE]
> Exchange 2013 を実行しているコンピューターにいずれかのサーバーの役割をインストールした後は、Exchange 2013 セットアップ ウィザードを使用して他のサーバーの役割をこのコンピューターに追加することはできません。サーバーの役割をコンピューターに追加する必要がある場合は、コントロール パネルの [プログラムの追加と削除] を使用するか、コマンド プロンプト ウィンドウで Setup.exe を使用する必要があります。<BR>エッジ トランスポートの役割は、メールボックスやクライアント アクセスのサーバーの役割と同じコンピューター上にインストールすることはできません。



インストール後に実行するタスクの詳細については、「[Exchange 2013 のインストール後のタスク](exchange-2013-post-installation-tasks-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

次の情報は、Exchange 2013 サーバーのすべての役割に適用されます。

  - Exchange 2013 をインストールする前に、リリース ノートを読んだことを確認してださい。詳細については、「[Exchange 2013 のリリース ノート](release-notes-for-exchange-2013-exchange-2013-help.md)」を参照してください。

  - Exchange 2013 をインストールするコンピューターは、サポートされているオペレーティング システム (Windows Server 2008 R2 と Service Pack 1 (SP1)、Windows Server 2012 R2、または Windows Server 2012) が搭載され、十分な空きディスク領域を備え、その他の要件も満たしている必要があります。システム要件の詳細については、「[Exchange 2013 のシステム要件](exchange-2013-system-requirements-exchange-2013-help.md)」を参照してください。

  - Exchange 2013 セットアップを実行するには、Microsoft .NET Framework 4.5、Windows Management Framework、およびその他の必要なソフトウェアをインストールしておく必要があります。すべてのサーバーの役割の前提条件を理解するには、「[Exchange 2013 の前提条件](exchange-2013-prerequisites-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!NOTE]
> サーバーに Exchange をインストールした後は、サーバー名を変更しないでください。Exchange のサーバーの役割をインストールした後でサーバーの名前を変更することは、サポートされていません。



次の情報は、Exchange 2013 メールボックスおよびクライアント アクセス サーバーの役割に適用されます。

  - 予想所要時間 : 60 分

  - 各組織では、Active Directory フォレスト内に最低でも 1 つのクライアント アクセス サーバーと 1 つのメールボックス サーバーが必要です。また、メールボックス サーバーを含む各 Active Directory サイトには、クライアント アクセス サーバーが少なくとも 1 つ含まれている必要があります。サーバーの役割を分離している場合は、最初にメールボックス サーバーの役割をインストールすることをお勧めします。

  - Exchange 2013 をインストールするコンピューターは、Active Directory ドメインのメンバーである必要があります。

  - 次の手順を実行するには、これまでに Active Directory スキーマを準備していない場合、使用するアカウントに Schema Admins グループのメンバーシップが委任されていることを確認する必要があります。組織に最初の Exchange 2013 サーバーをインストールしている場合は、Enterprise Admins グループのメンバーシップを持つアカウントを使用する必要があります。既にスキーマを準備していて、組織に最初の Exchange 2013 サーバーをインストールしていない場合は、Exchange 2013 "Organization Management/組織の管理" 管理役割グループのメンバーのアカウントを使用します。
    
    "Delegated Setup/委任されたセットアップ" 役割グループのメンバーである管理者は、"Organization Management/組織の管理" 役割グループのメンバーによって既に準備された Exchange 2013 サーバーを展開できます。

次の情報は、Exchange 2013 エッジ トランスポート サーバーの役割に適用されます。

  - 予想所要時間: 40 分

  - エッジ トランスポートの役割は、Exchange 2013 SP1 以上で利用可能です。

  - コンピューター上でプライマリ DNS サフィックスを構成する必要があります。たとえば、コンピューターの完全修飾ドメイン名が edge.contoso.com の場合、コンピューターの DNS サフィックスは contoso.com です。詳細は「[プライマリ DNS サフィックスに \[ms.exch.setupreadiness.FqdnMissing\] が存在しない](primary-dns-suffix-is-missing-exchange-2013-help.md)」を参照してください。

  - Exchange 2007 および Exchange 2010 ハブ トランスポート サーバーは、Exchange 2013 エッジ トランスポート サーバーとの間に EdgeSync サブスクリプションを作成する前に更新する必要があります。この更新プログラムをインストールしていない場合、EdgeSync サブスクリプションは正しく動作しません。詳細は、「[Exchange 2013 のシステム要件](exchange-2013-system-requirements-exchange-2013-help.md)」の「サポートされる共存シナリオ」セクションを参照してください。

  - ご使用のアカウントがエッジ トランスポートの役割をインストールしているコンピューターのローカル管理者グループのメンバーであることを確認してください。

## Setup.exe を使用して無人モードで Exchange 2013 をインストールする


> [!NOTE]
> Exchange 2013 の最新バージョンをダウンロードするには、「<A href="updates-for-exchange-2013-exchange-2013-help.md">Exchange 2013 の更新プログラム</A>」を参照してください。



1.  Exchange 2013 をインストールするコンピューターにログオンします。

2.  Exchange 2013 インストール ファイルが格納されているネットワーク上の場所に移動します。

3.  コマンド プロンプトで、組織の該当するコマンドを実行します。
    

    > [!IMPORTANT]
    > ユーザー アクセス コントロール (UAC) を有効にした場合は、昇格したコマンド プロンプトから <CODE>Setup.exe</CODE> を実行してください。

    
        Setup.exe [/Mode:<setup mode>] [/IAcceptExchangeServerLicenseTerms]
        [/Roles:<server roles to install>] [/InstallWindowsComponents] 
        [/OrganizationName:<name for the new Exchange organization>] 
        [/TargetDir:<target directory>] [/SourceDir:<source directory>]
        [/UpdatesDir:<directory from which to install updates>] 
        [/DomainController:<FQDN of domain controller>] [/DisableAMFiltering]
        [/AnswerFile:<filename>] [/DoNotStartTransport] 
        [/EnableErrorReporting] [/CustomerFeedbackEnabled:<True | False>] 
        [/AddUmLanguagePack:<UM language pack name>] 
        [/RemoveUmLanguagePack:<UM language pack name>] 
        [/NewProvisionedServer:<server>] [/RemoveProvisionedServer:<server>] 
        [/MdbName:<mailbox database name>] [/DbFilePath:<Edb file path>] 
        [/LogFolderPath:<log folder path>] [/ActiveDirectorySplitPermissions:<True | False>]
        [/TenantOrganizationConfig:<path>]

4.  セットアップによって、Exchange 2013 をインストールするコンピューターのローカルにセットアップ ファイルがコピーされます。

5.  インストールするサーバーの役割に固有のすべての前提条件を含め、前提条件が確認されます。すべての前提条件を満たしていない場合、セットアップは失敗し、失敗の理由を説明するエラー メッセージが返されます。すべての前提条件を満たしている場合は、Exchange 2013 がインストールされます。

6.  Exchange 2013 のインストールの完了後、コンピューターを再起動します。

7.  「[Exchange 2013 のインストール後のタスク](exchange-2013-post-installation-tasks-exchange-2013-help.md)」に記述されているタスクを実行して、展開を完了します。

## 例

Setup.exe の使用例を以下に示します。

  - **Setup.exe /mode:Install /role:ClientAccess,Mailbox /OrganizationName:MyOrg /IAcceptExchangeServerLicenseTerms**
    
    このコマンドは、Active Directory 内に MyOrg という名前の Exchange 2013 組織を作成し、クライアント、アクセス サーバーの役割とメールボックス サーバーの役割、および管理ツールをインストールします。また、Exchange 2013 ライセンス条項に同意したものとみなします。

  - **Setup.exe /mode:Install /role:ClientAccess,Mailbox /TargetDir:"C:\\Exchange Server" /IAcceptExchangeServerLicenseTerms**
    
    このコマンドは、クライアント アクセス サーバーの役割、メールボックス サーバーの役割、および管理ツールを "C:\\Exchange Server" ディレクトリにインストールします。このコマンドは、Exchange 2013 組織が既に準備されているとみなします。

  - **Setup.exe /mode:Install /r:CA,MB /IAcceptExchangeServerLicenseTerms**
    
    このコマンドは、クライアント アクセス サーバーの役割、メールボックス サーバーの役割、および管理ツールを既定のインストール場所にインストールします。

  - **Setup.exe /mode:Install /r:EdgeTransport /IAcceptExchangeServerLicenseTerms**
    
    このコマンドは、既定のインストール場所に、エッジ トランスポート サーバーの役割と管理ツールをインストールします。

  - **Setup.exe /mode:Install /r:ET /IAcceptExchangeServerLicenseTerms**
    
    このコマンドは、既定のインストール場所に、エッジ トランスポート サーバーの役割と管理ツールをインストールします。

  - **Setup.exe /mode:Uninstall /IAcceptExchangeServerLicenseTerms**
    
    このコマンドは、Exchange 2013 をサーバーから完全に削除し、このサーバーの Exchange の構成を Active Directory から削除します。

  - **Setup.exe /PrepareAD /on:"My Org" /IAcceptExchangeServerLicenseTerms**
    
    このコマンドは、My Org という名前の Exchange 組織を作成し、Exchange 2013 用に Active Directory を準備します。

  - **C:\\ExchangeServer\\bin\\Setup.exe /m:Install /r:ClientAccess /SourceDir:d:\\amd64 /IAcceptExchangeServerLicenseTerms**
    
    このコマンドは、インストール元ディレクトリとして D:\\amd64 を使用し、クライアント アクセス サーバーの役割を既存の Exchange 2013 サーバーに追加します。

  - **Setup.exe /role:ClientAccess,Mailbox /UpdatesDir:"C:\\ExchangeServer\\New Patches" /IAcceptExchangeServerLicenseTerms**
    
    このコマンドは、指定したディレクトリの修正プログラムを使用して ExchangeServer.msi を更新し、その後クライアント アクセス サーバーの役割、メールボックス サーバーの役割、および管理ツールをインストールします。言語パック バンドルがこのディレクトリに含まれている場合は、その言語パックもインストールされます。

  - **Setup.exe /mode:Install /role:ClientAccess,Mailbox /DomainController:DC01 /IAcceptExchangeServerLicenseTerms**
    
    このコマンドは、ドメイン コントローラー DC01 を使用して Active Directory への照会と変更を行いながら、クライアント アクセス サーバーの役割、メールボックス サーバーの役割、および管理ツールをインストールします。

  - **Setup.exe /mode:Install /role:ClientAccess /AnswerFile:c:\\ExchangeConfig.txt /IAcceptExchangeServerLicenseTerms**
    
    このコマンドは、ExchangeConfig.txt ファイルの設定を使用して、クライアント アクセス サーバーの役割をインストールします。

  - **Setup.exe /rprs:Exchange03 /IAcceptExchangeServerLicenseTerms**
    
    このコマンドは、Active Directory からオブジェクト Exchange03 を削除します。

  - **Setup.exe /AddUmLanguagePack:ko-KR /IAcceptExchangeServerLicenseTerms**
    
    このコマンドは、韓国語のユニファイド メッセージング言語パックを %ExchangeSourceDir%\\ServerRoles\\UnifiedMessaging ディレクトリからインストールします。

## 正常な動作を確認する方法

Exchange 2013 が正常にインストールされたことを確認するには、「[Exchange 2013 のインストールの確認](verify-an-exchange-2013-installation-exchange-2013-help.md)」を参照してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

探しているものは見つかりましたか？検索したい情報に関する[フィードバックを送信](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback)してください。

