---
title: 'Exchange 2013 の前提条件: Exchange 2013 Help'
TOCTitle: Exchange 2013 の前提条件
ms:assetid: e21cf744-7813-48b3-9293-5cecd89a6c25
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb691354(v=EXCHG.150)
ms:contentKeyID: 48270156
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 の前提条件

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2017-03-20_

このトピックでは、Microsoft Exchange 2013 メールボックス、クライアント アクセス、およびエッジ トランスポート サーバーの役割で前提条件となる、必須の Windows Server 2012 R2、Windows Server 2012、および Windows Server 2008 R2 with Service Pack 1 (SP1) オペレーティング システムのインストール手順を説明します。また、Windows 8、Windows 8.1、および Windows 7 クライアント コンピューターに Exchange 2013 をインストールするために必要な前提条件についても説明します。

  - 始める前に把握しておくべき情報

  - Active Directory の準備

  - Windows Server 2012 R2 と Windows Server 2012 の前提条件
    
      - メールボックスまたはクライアント アクセス サーバーの役割
    
      - エッジ トランスポート サーバーの役割

  - Windows Server 2008 R2 SP1 の前提条件
    
      - メールボックスまたはクライアント アクセス サーバーの役割
    
      - エッジ トランスポート サーバーの役割

  - Windows 7 の前提条件 (管理ツールのみ) (管理ツールのみ)

  - Windows 8 と Windows 8.1 の前提条件 (管理ツールのみ) (管理ツールのみ)

## 始める前に把握しておくべき情報

  - このトピックの情報は、Exchange 2013 の Service Pack 1 以降のバージョンに適用されます。

  - エッジ トランスポート サーバーの役割は、Exchange 2013 SP1 以降で使用できます。

  - フォレストの機能レベルが最低でも Windows Server 2003 であり、スキーマ マスターによって Service Pack 2 以降のバージョンの Windows Server 2003 が実行されていることを確認します。Windows の機能レベルの詳細については、「[ドメインとフォレストの管理](https://go.microsoft.com/fwlink/p/?linkid=137037)」を参照してください。

  - Windows Server 2012 R2、Windows Server 2012、および Windows Server 2008 R2 SP1 の完全インストール オプションは、Exchange 2013 のサーバーの役割または管理ツールを実行するすべてのサーバーで使用される必要があります。

  - 最初に、コンピューターを適切な内部 Active Directory フォレストとドメインに結合する必要があります。

  - 一部の前提条件では、インストールを完了するためにサーバーを再起動する必要があります。

  - 最新の Windows 更新プログラムをコンピューターにインストールします。詳細については、「[展開のセキュリティ チェックリスト](deployment-security-checklist-exchange-2013-help.md)」を参照してください。
    

    > [!NOTE]
    > メールボックス サーバーの役割をインストールしていて、そのサーバーをデータベース可用性グループ (DAG) のメンバーにする場合は、Windows Server 2012 R2 Standard (または Datacenter) Edition、Windows Server 2012 Standard (または Datacenter) Edition、または Windows Server 2008 R2 SP1 Enterprise Edition を実行している必要があります。Windows Server 2008 R2 SP 1 Standard Edition では、DAG に必要な機能がサポートされていません。<BR>サーバーに Exchange がインストールされている場合は、Windows をアップグレードできません。<BR>Microsoft Unified Communications Managed API (UCMA) 4.0 にアップグレードするには、まずインストールされている以前のバージョンの UCMA を <STRONG>[アプリケーションの追加と削除]</STRONG> を使用してアンインストールする必要があります。




> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## Active Directory の準備

Active Directory for Exchange 2013 を準備するために使用するコンピューターには、満たされる必要のある特定の前提条件があります。

Active Directory の準備に使用するコンピューターに、次のソフトウェアを、示された順序でインストールします。

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)

2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234) (Windows Server 2012 R2 に含まれている)

上記のソフトウェアをインストールした後に、次の手順を完了して Remote Tools Administration Pack をインストールします。Remote Tools Administration Pack をインストールすると、Active Directory の準備にコンピューターを使用できるようになります。Active Directory の準備方法の詳細については、「[Active Directory とドメインを準備する](prepare-active-directory-and-domains-exchange-2013-help.md)」を参照してください。

1.  Windows PowerShell を開きます。

2.  Remote Tools Administration Pack をインストールします。
    
      - Windows Server 2012 R2 または Windows Server 2012 コンピューター上で、以下のコマンドを実行します。
        
        ```powershell
Install-WindowsFeature RSAT-ADDS
```
    
      - Windows Server 2008 R2 SP1 コンピューター上で、以下のコマンドを実行します。
        
        ```powershell
Add-WindowsFeature RSAT-ADDS
```

## Windows Server 2012 R2 と Windows Server 2012 の前提条件

Exchange 2013 を Windows Server 2012 R2 または Windows Server 2012 コンピューターにインストールするために必要な前提条件は、インストールする Exchange の役割によって異なります。インストールする役割に一致するセクションを読んでください。

## メールボックスまたはクライアント アクセス サーバーの役割

次のいずれかを行う Windows Server 2012 R2 または Windows Server 2012 コンピューターに前提条件をインストールするには、このセクションの手順に従います。

  - メールボックス サーバーの役割のみをコンピューターにインストールします。

  - クライアント アクセス サーバーの役割のみをコンピューターにインストールします。

  - メールボックス サーバーとクライアント アクセス サーバーの両方の役割を同一コンピューターにインストールします。

必要な Windows の役割および機能をインストールするには、次の操作を行います。

1.  Windows PowerShell を開きます。

2.  次のコマンドを実行して、必要な Windows コンポーネントをインストールします。
    
        Install-WindowsFeature AS-HTTP-Activation, Desktop-Experience, NET-Framework-45-Features, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Clustering-CmdInterface, RSAT-Clustering-Mgmt, RSAT-Clustering-PowerShell, Web-Mgmt-Console, WAS-Process-Model, Web-Asp-Net45, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext45, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, Windows-Identity-Foundation, RSAT-ADDS

オペレーティング システムの役割と機能をインストールした後で、次のソフトウェアを表示されている順序でインストールします。

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    

    > [!IMPORTANT]
    > Exchange 2013 CU16 以降には .NET Framework 4.6.2 が<STRONG>必要です</STRONG>。先にサーバーを .NET Framework 4.6.2 にアップグレードしてから Exchange 2013 CU16 をインストールしてください。そうしないと、エラーが発生します。.NET Framework 4.5.2 が Exchange サーバーにインストールされている場合は, .NET Framework 4.6.2 をインストールする前に、サーバーを Exchange 2013 CU15 にアップグレードします。



2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234) (Windows Server 2012 R2 に含まれている)

3.  [Microsoft Unified Communications Managed API 4.0 コア ランタイム 64 ビット](https://go.microsoft.com/fwlink/p/?linkid=258269)

## エッジ トランスポート サーバーの役割

コンピューターにエッジ トランスポート サーバーの役割をインストールする Windows Server 2012 R2 または Windows Server 2012 コンピューターに前提条件をインストールするには、このセクションの手順に従います。

必要な Windows の役割および機能をインストールするには、次の操作を行います。

1.  Windows PowerShell を開きます。

2.  次のコマンドを実行して、必要な Windows コンポーネントをインストールします。
    
    ```powershell
Install-WindowsFeature ADLDS
```

インストール中の Exchange 2013 のバージョンに対応する Microsoft .NET Framework のバージョンをインストールします。

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    

    > [!IMPORTANT]
    > Exchange 2013 CU16 以降には .NET Framework 4.6.2 が<STRONG>必要です</STRONG>。先にサーバーを .NET Framework 4.6.2 にアップグレードしてから Exchange 2013 CU16 をインストールしてください。そうしないと、エラーが発生します。.NET Framework 4.5.2 が Exchange サーバーにインストールされている場合は, .NET Framework 4.6.2 をインストールする前に、サーバーを Exchange 2013 CU15 にアップグレードします。



2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234) (Windows Server 2012 R2 に含まれている)

## Windows Server 2008 R2 SP1 の前提条件

Exchange 2013 を Windows Server 2008 R2 SP1 コンピューター上にインストールするために必要な前提条件は、インストールする Exchange の役割によって異なります。インストールする役割に一致するセクションを読んでください。

## メールボックスまたはクライアント アクセス サーバーの役割

次のいずれかを行う Windows Server 2008 R2 SP1 コンピューターに前提条件をインストールするには、このセクションの手順に従います。

  - メールボックス サーバーの役割のみをコンピューターにインストールします。

  - クライアント アクセス サーバーの役割のみをコンピューターにインストールします。

  - メールボックス サーバーとクライアント アクセス サーバーの両方の役割を同一コンピューターにインストールします。

必要な Windows の役割および機能をインストールするには、次の操作を行います。

1.  Windows PowerShell を開きます。

2.  次のコマンドを実行して、サーバー マネージャー モジュールをロードします。
    
    ```powershell
Import-Module ServerManager
```

3.  次のコマンドを実行して、必要な Windows コンポーネントをインストールします。
    
        Add-WindowsFeature Desktop-Experience, NET-Framework, NET-HTTP-Activation, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Web-Server, WAS-Process-Model, Web-Asp-Net, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, RSAT-ADDS

オペレーティング システムの役割と機能をインストールした後で、次のソフトウェアを表示されている順序でインストールします。

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    

    > [!IMPORTANT]
    > Exchange 2013 CU16 以降には .NET Framework 4.6.2 が<STRONG>必要です</STRONG>。先にサーバーを .NET Framework 4.6.2 にアップグレードしてから Exchange 2013 CU16 をインストールしてください。そうしないと、エラーが発生します。.NET Framework 4.5.2 が Exchange サーバーにインストールされている場合は, .NET Framework 4.6.2 をインストールする前に、サーバーを Exchange 2013 CU15 にアップグレードします。



2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)

3.  [Microsoft Unified Communications Managed API 4.0 コア ランタイム 64 ビット](https://go.microsoft.com/fwlink/p/?linkid=258269)

4.  [Microsoft サポート技術情報の記事 KB974405 (Windows Identity Foundation)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=974405)

5.  [サポート技術情報の記事 KB2619234 (RPC over HTTP で使用する関連の Cookie/GUID を Windows 7 および Windows Server 2008 R2 の RPC 層でも使用できるようにする)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=2619234)

6.  [サポート技術情報の記事 KB2533623 (安全でないライブラリの読み込みにより、リモートでコードが実行される)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=2533623)
    

    > [!NOTE]
    > コンピューターにセキュリティ更新プログラムをインストールするように Windows Update を構成した場合、この修正プログラムはすでにインストールされていることがあります。



## エッジ トランスポート サーバーの役割

コンピューターにエッジ トランスポート サーバーの役割をインストールする Windows Server 2008 R2 SP1 コンピューターに前提条件をインストールするには、このセクションの手順に従います。

必要な Windows の役割および機能をインストールするには、次の操作を行います。

1.  Windows PowerShell を開きます。

2.  次のコマンドを実行して、サーバー マネージャー モジュールをロードします。
    
    ```powershell
Import-Module ServerManager
```

3.  次のコマンドを実行して、必要な Windows コンポーネントをインストールします。
    
    ```powershell
Add-WindowsFeature NET-Framework, ADLDS
```

オペレーティング システムの役割と機能をインストールした後で、次のソフトウェアを表示されている順序でインストールします。

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    

    > [!IMPORTANT]
    > Exchange 2013 CU16 以降には .NET Framework 4.6.2 が<STRONG>必要です</STRONG>。先にサーバーを .NET Framework 4.6.2 にアップグレードしてから Exchange 2013 CU16 をインストールしてください。そうしないと、エラーが発生します。.NET Framework 4.5.2 が Exchange サーバーにインストールされている場合は, .NET Framework 4.6.2 をインストールする前に、サーバーを Exchange 2013 CU15 にアップグレードします。



2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)

3.  [Microsoft Unified Communications Managed API 4.0 コア ランタイム 64 ビット](https://go.microsoft.com/fwlink/p/?linkid=258269)

## Windows 7 の前提条件 (管理ツールのみ)

Exchange 管理ツールをインストールするドメイン参加済みの Windows 7 64 ビット コンピューターに前提条件をインストールするには、このセクションの手順に従います。

1.  <strong>コントロール パネル</strong> を開き、<strong>プログラム</strong> をクリックします。

2.  <strong>Windows の機能の有効化または無効化</strong> をクリックします。

3.  <strong>インターネット インフォメーション サービス (IIS)</strong> \> <strong>Web 管理ツール</strong> \> <strong>IIS 6 と互換性のある管理</strong> の順に移動します。

4.  <strong>IIS 6 管理コンソール</strong> のチェック ボックスをオンにし、<strong>OK</strong> をクリックします。

オペレーティング システムの機能をインストールした後で、次のソフトウェアを表示されている順序でインストールします。

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)

2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)

3.  [サポート技術情報の記事 KB974405 (Windows Identity Foundation)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=974405)

## Windows 8 と Windows 8.1 の前提条件 (管理ツールのみ)

[.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)

