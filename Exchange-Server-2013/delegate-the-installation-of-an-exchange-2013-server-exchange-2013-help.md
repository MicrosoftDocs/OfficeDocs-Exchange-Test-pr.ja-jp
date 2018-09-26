---
title: 'Exchange 2013 サーバーのインストールの委任: Exchange 2013 Help'
TOCTitle: Exchange 2013 サーバーのインストールの委任
ms:assetid: f2fc8680-0c7c-4a29-b8f5-d77404fec280
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb201741(v=EXCHG.150)
ms:contentKeyID: 62614005
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 サーバーのインストールの委任

 

_**適用先:** Exchange Online, Exchange Server, Exchange Server 2013_

_**トピックの最終更新日:** 2014-07-31_

Exchange Server 2013 によって、Exchange サーバーのインストールを Exchange 2013 組織の管理役割グループのメンバーではないユーザーに委任できます。これは、サーバーをインストールしてセットアップするユーザーと Exchange などのサービスを管理するユーザーが異なるような規模の大きい企業で役立ちます。実行したいことと一致するようであれば、このトピックをお読みください。

通常、Exchange をインストールする場合、インストールするユーザーは[組織の管理](organization-management-exchange-2013-help.md)役割グループのメンバーである必要があります。これは、Exchange をインストールする時には Active Directory に変更が加えられますが、それらの変更を加えることができるのは、組織の管理役割グループのメンバーである Exchange 管理者だけだからです。加えられる変更の一覧を以下に示します。

  - サーバー オブジェクトが **CN=Servers,CN=Exchange Administrative Group (FYDIBOHF23SPDLT),CN=Administrative Groups,CN=\<Organization Name\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<Root Domain\>** 構成パーティションに作成されます。

  - 以下のアクセス制御エントリ (ACE) が、委任セットアップ役割グループの構成パーティション内のサーバー オブジェクトに追加されます。
    
      - サーバー オブジェクトおよびその子オブジェクトに対するフル コントロール
    
      - Send As 拡張権利に対する拒否のアクセス制御エントリ
    
      - Receive As 拡張権利に対する拒否のアクセス制御エントリ
    
      - Exchange パブリック フォルダー ストア オブジェクトの "CreateChild" および "DeleteChild" アクセス許可に対する "拒否"
    

    > [!NOTE]
    > パブリック フォルダーは組織レベルで管理されるため、パブリック フォルダー ストアの作成および削除は、Exchange 管理者に制限されます。



  - サーバーの Active Directory コンピューター アカウントが、Exchange サーバー グループに追加されます。

  - サーバーが、Exchange アドミン センターで準備されたサーバーとして追加されます。

規模の大きい企業では、新規サーバーをインストールおよびセットアップするユーザーが Exchange 管理者ではない場合があります。それらのユーザーが Exchange をインストールできるようにするため、Exchange 管理者は Active Directory にサーバーを*準備*できます。サーバーを準備する際、コンピューターへの Exchange の実際のインストールとは別に、新規 Exchange サーバーが機能するために必要なすべての変更を Active Directory に加えます。Exchange 管理者は、Exchange を新しいコンピューターにインストールする数時間前または数日前に Active Directory に新規サーバーを準備することができます。サーバーが準備できたら、後はインストールを実行するユーザーが[委任されたセットアップ](delegated-setup-exchange-2013-help.md)役割グループのメンバーでありさえすれば、Exchange をインストールできます。委任セットアップ役割グループは、準備されたサーバーのインストールをメンバーにのみ許可します。

委任セットアップの使用を検討する際、以下を念頭においてください。

  - 追加のサーバーのインストールを委任するには、その前に少なくとも 1 つの Exchange 2013 サーバーがインストールされている必要があります。最初のサーバーをインストールするユーザーは、Exchange 管理者である必要があります。詳細については、「[チェックリスト: Exchange 2013 の新規インストールを実行する](checklist-perform-a-new-installation-of-exchange-2013-exchange-2013-help.md)」を参照してください。

  - 委任されたユーザーは、Exchange サーバーをアンインストールすることはできません。Exchange サーバーをアンインストールするには、Exchange 管理者である必要があります。

## Exchange 2013 サーバーを準備する方法

Exchange 用のサーバーを準備するには、Exchange 2013 コマンドライン セットアップを使用する必要があります。Windows コマンド プロンプトにあまり精通していない場合でも、心配しないでください。このトピックでは、実行する必要のある事柄を順を追って説明します。始める前に、念頭に置いておくべき 2 つの点を以下に示します。

  - サーバーを準備するには、組織の管理役割グループのメンバーである必要があります。

  - Exchange 2013 の最新リリースが必要です。「[Exchange 2013 の更新プログラム](updates-for-exchange-2013-exchange-2013-help.md)」からダウンロード リンクを利用できます。

サーバーを準備するために使用する必要のあるコマンドは、準備を行うコンピューターからセットアップ プログラムを実行するか、別のコンピューターから実行するかに応じて異なります。以下の手順では、セットアップ プログラムを実行する場所に一致するコマンドを選択してください。

1.  Windows キーと R キーを押して、<strong>ファイル名を指定して実行</strong> ウィンドウを開きます。

2.  <strong>名前</strong> に **cmd.exe** を入力して Enter キーを押し、<strong>Windows コマンド プロンプト</strong> を開きます。

3.  Exchange 2013 インストール ファイルをダウンロードして展開した場所にディレクトリを変更します。インストール ファイルが `C:\Downloads\Exchange 2013` にある場合、次のコマンドを使用します。
    
    ```powershell
    CD "C:\Downloads\Exchange 2013"
    ```

4.  セットアップ プログラムを実行する場所に一致するコマンドを選択します。
    
      - **準備を行うコンピューターでセットアップ プログラムを実行する場合**、次のコマンドを実行します。
        
        ```powershell
        Setup.exe /NewProvisionedServer /IAcceptExchangeServerLicenseTerms
        ```
    
      - **別のコンピューターでセットアップ プログラムを実行する場合**、次のコマンドを実行します。
        
        ```powershell
        Setup.exe /NewProvisionedServer:<ComputerName> /IAcceptExchangeServerLicenseTerms
        ```

5.  サーバーを準備した後、準備したサーバーで Exchange をインストールできるユーザーを委任セットアップ役割グループに追加したことを確認する必要があります。ユーザーを役割グループに追加する方法については、「[Add members to a role group](manage-role-group-members-exchange-2013-help.md)」を参照してください。

これらの手順を完了したら、コンピューターに Exchange をインストールする準備が整いました。「[セットアップ ウィザードを使用した Exchange 2013 のインストール](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)」にある手順を使用して、準備したサーバーに Exchange 2013 をインストールすることができます。

## 設定が適用されたことを確認する方法

Exchange 用にサーバーが適切に準備されたことを確認するには、以下を実行します。

1.  <strong>スタート</strong> \> <strong>管理ツール</strong> に移動し、<strong>Active Directory ユーザーとコンピューター</strong> を開きます。

2.  <strong>Microsoft Exchange セキュリティ グループ</strong> を選択して、<strong>Exchange サーバー</strong> をダブルクリックし、<strong>メンバー</strong> タブを選択します。

3.  <strong>メンバー</strong> タブで、準備したサーバーがセキュリティ グループのメンバーとしてリストされているかを確認します。

サーバーが Exchange サーバー セキュリティ グループのメンバーとしてリストされている場合、そのサーバーは適切に準備されています。委任セットアップ役割グループのメンバーであるユーザーは、そのサーバー上に Exchange をインストールできます。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

探しているものは見つかりましたか？検索したい情報に関する[フィードバックを送信](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback)してください。

