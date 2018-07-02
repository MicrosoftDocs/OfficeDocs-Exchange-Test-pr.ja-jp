---
title: 'Exchange 組織間のフェデレーション共有を構成する: Exchange 2013 Help'
TOCTitle: Exchange 組織間のフェデレーション共有を構成する
ms:assetid: 94e31454-b027-4757-b52f-d3c2ead6d916
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657473(v=EXCHG.150)
ms:contentKeyID: 49896378
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 組織間のフェデレーション共有を構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

フェデレーション共有を使用すると、社内の Exchange 組織のユーザーは、やはりフェデレーション共有を構成されている他の Exchange 組織内の受信者と予定表の空き時間情報を共有できます。空き時間情報の共有は、Exchange 2013 を実行している 2 つの組織間、および Exchange を混在展開している組織間で有効化できます。フェデレーション共有の詳細については、「[共有](sharing-exchange-2013-help.md)」を参照してください。

ここでは、次の一般的な Exchange 展開のうち異なる種類間で空き時間情報の共有を有効化するための要件の概要と、必要な手順を説明します。

  - 2 つの Exchange 2013 組織。

  - Exchange 2013 組織と Exchange 2010 SP2 組織。

  - Exchange 2007 組織 (または Exchange 2007 組織と Exchange 2010 SP2 組織の混在) および Exchange 2013 組織。

  - Exchange 2003 組織 (または Exchange 2003 組織と Exchange 2010 SP2 組織の混在) および Exchange 2013 組織。

フェデレーション共有に関連する追加の管理タスクについては、「[フェデレーションの手順](federation-procedures-exchange-2013-help.md)」を参照してください。


> [!IMPORTANT]
> Exchange Server 2013 のこの機能は、中国で 21Vianet によって運用される Office 365 との完全な互換性を備えておらず、いくつかの機能制限が適用される場合があります。詳細については、「<A href="https://go.microsoft.com/fwlink/?linkid=313640">21Vianet が運用している Office 365 について</A>」を参照してください。



## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:2 時間。

  - このトピックの手順には、特定のアクセス許可が必要です。アクセス許可情報については、各手順を参照してください。

  - このトピックの手順を実行する前に、Exchange 組織間で共有している空き時間情報に関連付けられた制限事項を理解しておいてください。詳細については、「[Limitations of free/busy sharing](sharing-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

## 必要な作業

## Exchange 2013 組織間で空き時間情報の共有を構成する

両方の組織で「[フェデレーション共有の構成](configure-federated-sharing-exchange-2013-help.md)」の手順を完了します。

## Exchange 2013 組織と Exchange 2010 SP2 組織間で空き時間情報の共有を構成する

  - Exchange 2013 組織のフェデレーション共有を構成します。「[フェデレーション共有の構成](configure-federated-sharing-exchange-2013-help.md)」の手順を完了します。

  - Exchange 2010 SP2 組織のフェデレーション委任 (フェデレーション共有の以前の名前) を構成します。「[シナリオ: 空き時間情報の共有を構成する](https://go.microsoft.com/fwlink/p/?linkid=268410)」の手順を完了します。

## Exchange 2013 組織と Exchange 2007 組織間で空き時間情報の共有を構成する

  - Exchange 2013 組織のフェデレーション共有を構成します。「[フェデレーション共有の構成](configure-federated-sharing-exchange-2013-help.md)」の手順を完了します。

  - Exchange 2007 組織で次の手順を完了します。
    
    1.  **Exchange 2010 SP2 サーバーの追加**
        
        クライアント アクセス サーバーの役割を果たす Exchange 2010 SP2 サーバーを、Exchange 2007 組織にスントールする必要があります。他に既存の Exchange 2010 サーバーがある場合、そちらも Exchange 2010 SP2 に更新してください。Exchange 2007 組織での Exchange 2010 のインストールについては、「[Exchange 2007 - アップグレードと共存のロードマップ計画](https://go.microsoft.com/fwlink/p/?linkid=268411)」を参照してください。
    
    2.  **フェデレーション委任の構成**
        
        Exchange 2007 組織のフェデレーション委任を構成します。Exchange 2007 組織の Exchange 2010 SP2 サーバーで、「[フェデレーション委任の構成](https://go.microsoft.com/fwlink/p/?linkid=268410)」の手順を完了します。
    
    3.  **Active Directory の同期の構成**
        
        Active Directory の同期は、組織内で空き時間情報を共有する必要のあるすべてのユーザーに対して構成する必要があります。Active Directory の同期の際、手動で構成することも、自動化された Active Directory 同期サービスを使用して構成することもできます。Active Directory の同期を構成するには、以下の手順を参照してください。
        
          - **前提条件**Active Directory 同期をインストールする前提条件を組織が満たしていることを確認します。
            
            詳細については、「[Active Directory の同期の準備](https://go.microsoft.com/fwlink/p/?linkid=247302)」を参照してください。
        
          - **計画**   Microsoft Online Services ディレクトリ同期ツールおよびインストール ロードマップについて把握します。
            
            詳細については、「[Active Directory Synchronization (Active Directory の同期)」を参照してください。ロードマップ](http://go.microsoft.com/fwlink/p/?linkid=203007)
        
          - **インストールおよび構成**   社内組織と Office 365 テナント サービス組織との間で Active Directory 同期を構成します。
            
            詳細については、「[Microsoft Online Services ディレクトリ同期ツールのインストールとアップグレード](https://go.microsoft.com/fwlink/p/?linkid=247303)」を参照してください。
    
    4.  **可用性アドレス スペースの作成**
        
        Exchange 2007 メールボックス ユーザーから Exchange 2007 組織内の Exchange 2010 SP2 クライアント アクセス サーバーに可用性要求を指示するリモート Exchange 2013 組織に対して可用性アドレス スペースを作成します。この設定により、Exchange 2007 ユーザーから、Exchange 2007 組織内の Exchange 2010 クライアント アクセス サーバーでプロキシ経由されるリモート Exchange 2013 組織内ユーザーへのユーザーの可用性要求を有効化します。Exchange 2007 組織内の Exchange 2010 クライアント アクセス サーバーは、フェデレーション信頼および組織上の関係を使用して、リモート Exchange 2013 組織のフォレスト可用性エンドポイントに可用性要求を送信します。
        
        Exhange 2007 組織内の Exchange 2010 クライアント アクセス サーバー上で可用性アドレス スペースを構成するには、Exchange 管理シェルで次のコマンドを実行します。
        
            Add-AvailabilityAddressSpace -AccessMethod InternalProxy -ProxyUrl https://<Exchange 2010 CAS server name>/ews/exchange.asmx -ForestName <SMTP domain of the remote Exchange organization> -UseServiceAccount $True
        
        構文およびパラメーターの詳細については、「[Add-AvailabilityAddressSpace](https://go.microsoft.com/fwlink/p/?linkid=268413)」を参照してください。

## Exchange 2013 組織と Exchange 2003 組織間で空き時間情報の共有を構成する

  - Exchange 2013 組織のフェデレーション共有を構成します。「[フェデレーション共有の構成](configure-federated-sharing-exchange-2013-help.md)」の手順を完了します。

  - Exchange 2003 組織で次の手順を完了します。
    
    1.  **Exchange 2010 SP2 サーバーの追加**。
        
        クライアント アクセス サーバーの役割を果たす Exchange 2010 SP2 サーバーを、Exchange 2003 組織にスントールする必要があります。他に既存の Exchange 2010 サーバーがある場合、そちらも Exchange 2010 SP2 に更新してください。Exchange 2003 組織での Exchange 2010 のインストールについては、「[Exchange 2003 - アップグレードと共存のロードマップ計画](https://go.microsoft.com/fwlink/?linkid=268414)」を参照してください。
        

        > [!WARNING]
        > Exchange 2013 組織と Exchange 2003 組織間で空き時間情報の共有が正しく動作するには、<STRONG>OU=EXTERNAL (FYDIBOHF25SPDLT)</STRONG> パブリック フォルダーがパブリック フォルダー階層に存在している必要があります。このフォルダーは、Exchange 2010 セットアップ時に Outlook 2003 サポートのクライアント設定の構成の一部としてパブリック フォルダーを作成するオプションを選択した場合にのみ、Exchange 2003 組織内の Exchange 2010 メールボックス サーバー上に自動的に作成されます。また、このオプションは、その Exchange 2010 メールボックス サーバーが組織内で最初にインストールされるメールボックス サーバーである場合にのみ、セットアップ処理時に表示されます。セットアップ時に <STRONG>OU=EXTERNAL (FYDIBOHF25SPDLT)</STRONG> パブリック フォルダーが作成されなかった場合は、手動でこのフォルダーを作成する必要があります。パブリック フォルダーを作成する方法の詳細については、「<A href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=2555008">Microsoft Office 365 for enterprises 環境で Exchange フェデレーションを使用すると発生する空き時間情報 (Free/Busy) に関する問題のトラブルシュート方法</A>」を参照してください。

    
    2.  **フェデレーション委任の構成**。
        
        Exchange 2003 組織のフェデレーション委任を構成します。Exchange 2003 組織の Exchange 2010 SP2 サーバーで、「[フェデレーション委任の構成](https://go.microsoft.com/fwlink/p/?linkid=268410)」の手順を完了します。
    
    3.  **Active Directory の同期の構成**。
        
        Active Directory の同期は、組織内で空き時間情報を共有する必要のあるすべてのユーザーに対して構成する必要があります。Active Directory の同期の際、手動で構成することも、自動化された Active Directory 同期サービスを使用して構成することもできます。Active Directory の同期の詳細については、「[Forefront ID 管理](https://go.microsoft.com/fwlink/?linkid=294645)」を参照してください。
        
          - **前提条件**Active Directory 同期をインストールする前提条件を組織が満たしていることを確認します。
            
            詳細については、「[Active Directory の同期の準備](https://go.microsoft.com/fwlink/p/?linkid=247302)」を参照してください。
        
          - **計画**   Microsoft Online Services ディレクトリ同期ツールおよびインストール ロードマップについて把握します。
            
            詳細については、「[Active Directory Synchronization (Active Directory の同期)」を参照してください。ロードマップ](http://go.microsoft.com/fwlink/p/?linkid=203007)
        
          - **インストールおよび構成**   社内組織と Office 365 テナント サービス組織との間で Active Directory 同期を構成します。
            
            詳細については、「[Microsoft Online Services ディレクトリ同期ツールのインストールとアップグレード](https://go.microsoft.com/fwlink/p/?linkid=247303)」を参照してください。
    
    4.  **Exchange 2003 組織で空き時間情報の共有のパブリック フォルダーを構成します。**
        
        Exchange 2003 サーバー上で次の手順を完了します。
        
          - Exchange システム マネージャーのコンソール ツリーで、**\[管理グループ\]** \> **\[最初の管理グループ\]** \> **\[サーバー\]** に移動します。
        
          - Exchange 2003 サーバーを選択し、**\[最初のストレージ グループ\]** \> **\[パブリック フォルダー ストア\]** \> **\[パブリック フォルダー\]** \> **\[Schedule+ FREE BUSY\]** に移動します。
        
          - 操作ウィンドウで、**\[最初の管理グループ\]** として **\[OU=EXTERNAL (FYDIBOHF25SPDLT)\]** フォルダーを選択します。
        
          - **\[OU=EXTERNAL (FYDIBOHF25SPDLT)\]** フォルダーを右クリックして、**\[プロパティ\]** をクリックします。
        
          - **\[OU=EXTERNAL (FYDIBOHF25SPDLT) のプロパティ\]** で、**\[レプリケーション\]**\] タブを選択します。
        
          - **OU=EXTERNAL (FYDIBOHF25SPDLT)** フォルダーを Exchange 2010 クライアント アクセス/メールボックス サーバーにレプリケートするには、**\[追加\]** をクリックします。
        
          - **\[パブリック フォルダー ストアの選択\]** で、Exchange 2010 クライアント アクセス/メールボックス サーバーの **\[パブリック フォルダー データベース\]** を選択し、**\[OK\]** をクリックします。
            

            > [!NOTE]
            > 既定では、Exchange では、パブリック フォルダー データベースで設定されているレプリケーション スケジュールを使用します。

        
          - **\[OK\]** をクリックして **\[OU=EXTERNAL (FYDIBOHF25SPDLT) のプロパティ\]**\] を閉じ、変更を保存します。
        
          - **OU=Exchange Administrative Group (FYDIBOHF23SPDLT)** フォルダーについても、上記と同じ手順を実行します。
            

            > [!WARNING]
            > パブリック フォルダーのサイズによっては、このレプリケートに数時間かかる場合があります。

        
          - **OU=EXTERNAL (FYDIBOHF25SPDLT)** および **OU=Exchange Administrative Group (FYDIBOHF23SPDLT)** パブリック フォルダーを Exchange 2010 クライアント アクセス/メールボックス サーバーにレプリケートした後は、Exchange 2003 サーバーにあるこれらのパブリック フォルダーのレプリカを削除する必要があります。
    
    5.  **LegacyExchangeDN パラメーターの変更**
        
        リモート Exchange 2013 組織を参照する Exchange 2003 組織のメールが有効なすべてのオブジェクトで *LegacyExchangeDN* パラメーターを変更します。メールが有効なオブジェクトの既存の組織単位 (OU) 値を、**External (FYDIBOHF25SPDLT)** に変更します。たとえば、**LegacyExchangeDN=/o=First Organization/ou=External (FYDIBOHF25SPDLT)/cn=Recipients/cn=User Name** とします。
        
        Exchange 2003 組織でメールが有効なオブジェクトを変更するには、[Active Directory サービス インターフェイス エディター (ADSI Edit) ツール](https://go.microsoft.com/fwlink/?linkid=294644) または [Microsoft Exchange Server LegacyDN ユーティリティ](http://go.microsoft.com/fwlink/?linkid=294643) のいずれかを使用してください。

