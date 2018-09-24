---
title: '保持タグのエクスポートとインポート: Exchange Online Help'
TOCTitle: 保持タグのエクスポートとインポート
ms:assetid: 18405ea2-7ccc-475e-bd84-8b040e17bf44
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ907307(v=EXCHG.150)
ms:contentKeyID: 51407505
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 保持タグのエクスポートとインポート

 

_**適用先:** Exchange Online, Exchange Server 2013_

保持タグのエクスポートまたはインポートに使用できるシナリオは何種類かあります。

  - 複数フォレストの Exchange 組織ですべてのサーバーに同じアイテム保持ポリシーを適用する

  - メールボックスが社内 Exchange 組織と Exchange Online に存在するハイブリッド環境で同じアイテム保持ポリシーを適用する

  - オンプレミスの Exchange 2010 以降のメールボックスのユーザーがクラウドベースのアーカイブを持っている、Exchange Archiving シナリオでアイテム保持ポリシーを適用する

これらのシナリオにおいて、管理フォルダー アシスタントは、アイテムまたはメールボックスが別の組織に移動した後に保持タグが適用されたアイテムを正しく処理できます。


> [!NOTE]
> 保持タグとアイテム保持ポリシーを 2 つの組織間で常に同期させるには、同期元の組織で保持タグまたはアイテム保持ポリシーを変更するたびに、この手順を実行して同期元の組織から保持タグとアイテム保持ポリシーをエクスポートして、同期先の組織にインポートする必要があります。<BR>特定の保持タグまたはアイテム保持ポリシーを選択してエクスポートすることはできません。Export-RetentionTags.ps1 スクリプトでは、すべての保持タグとアイテム保持ポリシーが組織からエクスポートされます。



メッセージング レコード管理に関連するその他の管理タスクについては、「[メッセージング レコード管理の手順](messaging-records-management-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:10 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「メッセージング レコード管理」。

  - このトピックの手順は、Exchange サーバーの `%ExchangeInstallPath%Scripts` フォルダーにあるこれら 3 つのファイルによって異なります。
    
      - Export-RetentionTags.ps1
    
      - Import-RetentionTags.ps1
    
      - MigrateRetentionTags.strings.psd1

  - 特定の保持タグまたはアイテム保持ポリシーを選択してエクスポートまたはインポートすることはできません。Export-RetentionTags.ps1 スクリプトでは、すべての保持タグとアイテム保持ポリシーが組織からエクスポートされます。Import-RetentionTags.ps1 スクリプトでは、インポート中の XML ファイルのすべての保持タグとアイテム保持ポリシーがインポートされ、Exchange 組織にある既存の保持タグとアイテム保持ポリシーはすべて置き換えられます。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 手順 1: オンプレミスの Exchange 組織から保持タグをエクスポートする

1.  この Exchange 管理シェル コマンドを実行して、ディレクトリを Exchange のインストール先パスの **Scripts** サブディレクトリに変更します。
    
    ```powershell
    Cd $Env:ExchangeInstallPath\Scripts
    ```

2.  Export-RetentionTags.ps1 スクリプトを実行して保持タグを XML ファイルにエクスポートします。
    

    > [!IMPORTANT]
    > 保持タグとアイテム保持ポリシーを Exchange Online にインポートまたはエクスポートする場合は、Windows PowerShell セッションを Exchange Online に接続する必要があります。詳細については、「<A href="https://technet.microsoft.com/ja-jp/library/jj984289(v=exchg.150)">リモート PowerShell による Exchange への接続</A>」を参照してください。

    
    ```powershell
    .\Export-RetentionTags.ps1 "c:\docs\ExportedRetentionTags.xml"
    ```

## 正常な動作を確認する方法

保持タグと保持ポリシーを正常にエクスポートしたことを確認するには、以下を実行します。

1.  エクスポートするコマンドで指定したパスに移動し、指定した名前で XML ファイルが作成されていることを確認します。

2.  テキスト エディターで XML ファイルを開き、内容を検討することもできます。

## 手順 2: 保持タグを Exchange 組織にインポートする

1.  この Exchange 管理シェル コマンドを実行して、ディレクトリを Exchange のインストール先パスの **Scripts** サブディレクトリに変更します。
    
    ```powershell
    Cd $Env:ExchangeInstallPath\Scripts
    ```

2.  Import-RetentionTags.ps1 スクリプトを実行し、以前にエクスポートされた XML ファイルから保持タグをインポートします。
    

    > [!IMPORTANT]
    > 保持タグとアイテム保持ポリシーを Exchange Online にインポートまたはエクスポートする場合は、Windows PowerShell セッションを Exchange Online に接続する必要があります。詳細については、「<A href="https://technet.microsoft.com/ja-jp/library/jj984289(v=exchg.150)">リモート PowerShell による Exchange への接続</A>」を参照してください。

    

    > [!NOTE]
    > このスクリプトを Exchange Online に対して実行すると、信頼されていない発行元からのソフトウェアの実行の確認を求められる可能性があります。発行元の名前が <CODE>CN=Microsoft Corporation, OU=MOPR, O=Microsoft Corporation, L=Redmond, S=Washington, C=US</CODE> と表示されているのを確認してから、<STRONG>[R]</STRONG> をクリックしてスクリプトを 1 回だけ実行するようにするか、<STRONG>[A]</STRONG> をクリックして常に実行するようにします。

    
    ```powershell
    .\Import-RetentionTags.ps1 "c:\docs\ExportedRetentionTags.xml"
    ```

## 正常な動作を確認する方法

保持タグと保持ポリシーを正常にインポートしたことを確認するには、以下を実行します。

1.  EAC で <strong>コンプライアンス管理</strong> \> <strong>保持タグ</strong> の順に移動し、保持タグが正常にインポートされていることを確認します。<strong>コンプライアンス管理</strong> \> <strong>アイテム保持ポリシー</strong> の順に移動し、アイテム保持ポリシーが正常にインポートされていることを確認します。

2.  **Get-RetentionPolicy** コマンドレットと **Get-RetentionPolicyTag** コマンドレットを使用し、タグとポリシーが作成されていることを確認します。保持タグとアイテム保持ポリシーの取得方法の例については、「[Get-RetentionPolicyTag](https://technet.microsoft.com/ja-jp/library/dd298009\(v=exchg.150\))」と「[Get-RetentionPolicy](https://technet.microsoft.com/ja-jp/library/dd298086\(v=exchg.150\))」の例をご確認ください。

