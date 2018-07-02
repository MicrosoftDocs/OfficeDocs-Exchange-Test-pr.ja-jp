---
title: 'ユーザー メールボックスが Exchange 2013 サーバー上に存在するレガシ パブリック フォルダーを構成する: Exchange 2013 Help'
TOCTitle: ユーザー メールボックスが Exchange 2013 サーバー上に存在するレガシ パブリック フォルダーを構成する
ms:assetid: 1d5ca19e-696e-4054-a634-15dd34d952b7
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn690134(v=EXCHG.150)
ms:contentKeyID: 62281135
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# ユーザー メールボックスが Exchange 2013 サーバー上に存在するレガシ パブリック フォルダーを構成する

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2017-03-27_

Exchange 2013 または 2016 の Exchange ユーザーが Exchange 2010 のアクセスまたはそれ以前のパブリック フォルダー (従来のパブリック フォルダーとも呼ばれます) を有効にする方法です。

## 始める前に把握しておくべき情報

Exchange Server 2013 や 2016 の Exchange Server 上にメールボックスのユーザーが Outlook Web App、web 上の Outlook または Outlook for mac から従来のパブリック フォルダーにアクセスできません。この資料の手順は、Exchange 2013 と Exchange 2016 の両方の機能です。


> [!NOTE]
> この記事の手順を実行すると、Outlook 2016 for Mac のユーザーは従来のパブリック フォルダーにアクセスできます。組織内のクライアントが Outlook 2016 for Mac を使用している場合は、2016 年 4 月の更新プログラムをインストールしていることをご確認ください。さもないと、それらのユーザーは共存またはハイブリッド トポロジ内のパブリック フォルダーにアクセスすることができません。詳細については、「<A href="accessing-public-folders-with-outlook-2016-for-mac-exchange-2013-help.md">Outlook 2016 for Mac によるパブリック フォルダーへのアクセス</A>」をご覧ください。



## 手順 1: Exchange 2010 パブリック フォルダーを検出可能にする

1.  パブリック フォルダーが Exchange 2010 以降のサーバー上に存在する場合、クライアント アクセス サーバーの役割を、パブリック フォルダー データベースが存在するすべてのメールボックス サーバーにインストールする必要があります。これにより、Microsoft Exchange RpcClientAccess サービスの実行が可能になり、すべてのクライアントがパブリック フォルダーにアクセスできるようになります。Exchange 2007 パブリック フォルダー サーバーにはクライアント アクセスの役割は不要で、この手順は必要ありません。詳細については、「[Exchange Server 2010 のインストール](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)」を参照してください。
    

    > [!NOTE]
    > このサーバーは、クライアント アクセスの負荷分散に関与する必要はありません。詳細については、「<A href="https://technet.microsoft.com/ja-jp/library/ff625247(v=exchg.141).aspx">Exchange 2010 の負荷分散について</A>」を参照してください。



2.  各パブリック フォルダー サーバーに、空のメールボックス データベースを作成します。
    
    Exchange 2010 では、次のコマンドを実行します。このコマンドは、メールボックス データベースをメールボックス プロビジョニング ロードバランサーから除外します。これにより、このデータベースに新しいメールボックスが自動的に追加されなくなります。
    
        New-MailboxDatabase -Server <PFServerName_with_CASRole> -Name <NewMDBforPFs> -IsExcludedFromProvisioning $true 
    
    Exchange 2007 では、次のコマンドを実行します。
    
        New-MailboxDatabase -StorageGroup "<PFServerName>\StorageGroup>" -Name <NewMDBforPFs>
    

    > [!NOTE]
    > 手順 3 で作成するプロキシ メールボックスのみをこのデータベースに追加することをお勧めします。このメールボックス データベースに、その他のメールボックスを作成しないでください。



3.  新しいメールボックス データベース内にプロキシ メールボックスを作成し、アドレス帳でこのメールボックスを非表示にします。このメールボックスの SMTP は自動検出によって *DefaultPublicFolderMailbox* SMTP として返されます。この SMTP を解決することで、クライアントは従来の Exchange サーバーに接続して、パブリック フォルダーにアクセスできます。
    
        New-Mailbox -Name <PFMailbox1> -Database <NewMDBforPFs> 
    
        Set-Mailbox -Identity <PFMailbox1> -HiddenFromAddressListsEnabled $true

4.  Exchange 2010 では、プロキシ パブリック フォルダー メールボックスを返すように、自動検出を有効にします。この手順は Exchange 2007 には必要ありません。
    
        Set-MailboxDatabase <NewMDBforPFs> -RPCClientAccessServer <PFServerName_with_CASRole>

5.  組織内のすべてのパブリック フォルダー サーバーに対して、前述の手順を繰り返します。

## 手順 2: レガシ パブリック フォルダーにアクセスするようにユーザー メールボックスを構成する

この手順の最終ステップは、社内のレガシ パブリック フォルダーにアクセスできるようにユーザー メールボックスを構成することです。

Exchange Server 2013 の社内ユーザーがレガシ パブリック フォルダーにアクセスできるようにします。[Step 2: Make remote public folders discoverable](configure-legacy-on-premises-public-folders-for-a-hybrid-deployment-exchange-2013-help.md) で作成したすべてのプロキシ パブリック フォルダー メールボックスを指すことになります。CU5 以降の更新プログラムがインストールされた Exchange 2013 サーバーから次のコマンドを実行します。

    Set-OrganizationConfig -PublicFoldersEnabled Remote -RemotePublicFolderMailboxes ProxyMailbox1,ProxyMailbox2,ProxyMailbox3


> [!NOTE]
> 変更を確認するには、Active Directory の同期が完了するまで待つ必要があります。この処理には数時間かかる場合があります。



## 設定が適用されたことを確認する方法

メールボックスが Exchange Server 2013 CU5 以降のサーバー上に存在するユーザーとして Outlook にログオンし、次のパブリック フォルダー テストを実行します。

1.  Outlook クライアントが実行されていることを確認します。

2.  Windows のタスク バーの右側にある通知領域で、CTRL キーを押したまま、Outlook アイコンを右クリックします。

3.  **\[電子メールの自動構成のテスト\]** を選択します。

4.  電子メール自動構成テスト ツールが XML タブに次の情報を返すことを確認します。
    
      - \<PublicFolderInformation\>
    
      - \<SmtpAddress\>\<SMTP Address for public folder mailbox\</SmtpAddress\>
    
      - \</PublicFolderInformation\>

5.  Outlook クライアントで、次のタスクを実行します。
    
      - パブリック フォルダー階層を表示します。
    
      - アクセス許可を確認します。
    
      - パブリック フォルダーの作成と削除
    
      - パブリック フォルダーに対する内容の追加と削除

