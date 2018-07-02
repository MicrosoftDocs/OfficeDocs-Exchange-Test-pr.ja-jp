---
title: '接続ログを構成する: Exchange 2013 Help'
TOCTitle: 接続ログを構成する
ms:assetid: 24e46a79-33ea-44e9-b03c-549db1c86a6f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa996827(v=EXCHG.150)
ms:contentKeyID: 49895300
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 接続ログを構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2013-02-18_

接続ログは、Exchange サーバーのトランスポート サービスからメッセージを送信するときに使用する送信接続アクティビティを記録します。接続ログは、接続元、接続先、送信したメッセージ数とバイト数、接続エラー情報を記録します。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md) トピックの「トランスポート サービス」、「フロント エンド トランスポート サービス」、「メールボックス トランスポート サービス」エントリ。

  - Exchange 管理センター (EAC) では、接続ログの有効化や無効化、あるいはトランスポート サービス専用の接続ログのパスの設定が可能です。他のトランスポート サービスのその他すべての接続ログ オプションについては、シェルを使用してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EAC を使用してトランスポート サービスの接続ログを構成する

1.  EAC で **\[サーバー\]** \> **\[サーバー\]** に移動します。

2.  構成するメールボックス サーバーを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  サーバー プロパティ ページで、**\[トランスポート ログ\]** をクリックします。

4.  **\[接続ログ\]** セクションで、以下のいずれかの変更を行います。
    
      - **\[接続ログを有効にする\]**   サーバーで接続ログを無効にするには、このチェック ボックスをオフにします。サーバーで接続ログを有効にするには、このチェック ボックスを選択します。
    
      - **\[接続ログのパス\]**   ローカル Exchange サーバー上の値を指定してください。そのフォルダーが存在しない場合は、**\[保存\]** をクリックすると作成されます。
    
    完了したら、**\[保存\]** をクリックします。

## シェルを使用して接続ログを構成する

循環ログを構成するには、次のコマンドを実行します。

    <Set-TransportService | Set-MailboxTransportService | Set-FrontEndTransportService> <ServerIdentity> -ConnectivityLogEnabled <$true | $false> -ConnectivityLogMaxAge <dd.hh:mm:ss> -ConnectivityLogMaxDirectorySize <Size> -ConnectivityLogMaxFileSize <Size> -ConnectivityLogPath <LocalFilePath>

この例では、メールボックス サーバー Mailbox01 のトランスポート サービスに以下のように接続ログを設定します。

  -  
    接続ログ ファイルの場所は D:\\Hub Connectivity Log に設定します。フォルダーが存在しない場合は、新たに作成されます。

  -  
    接続ログ ファイルの最大サイズは 20 MB に設定します。

  -  
    接続ログ ディレクトリの最大サイズは 1.5 GB に設定します。

  -  
    接続ログ ファイルの最大保存期間は 45 日に設定します。

<!-- end list -->

    Set-TransportService Mailbox01 -ConnectivityLogPath "D:\Hub Connectivity Log" -ConnectivityLogMaxFileSize 20MB -ConnectivityLogMaxDirectorySize 1.5GB -ConnectivityLogMaxAge 45.00:00:00


> [!NOTE]
> <UL>
> <LI>
> <P>メールボックス サーバーでメールボックス トランスポート サービスの接続ログ設定を構成するには、<STRONG>Set-MailboxTransportService</STRONG> コマンドレットを使用します。クライアント アクセス サーバーでフロント エンド トランスポート サービスの接続ログ設定を構成するには、<STRONG>Set-FrontEndTransportService</STRONG> コマンドレットを使用します。</P>
> <LI>
> <P><EM>ConnectivityLogPath</EM> パラメーターの値を <CODE>$null</CODE> に設定すると、接続ログは事実上無効になります。ただし、<EM>ConnectivityLogEnabled</EM> パラメーターの値が <CODE>$true</CODE> の場合、イベント ログ エラーが生成されます。</P>
> <LI>
> <P><EM>ConnectivityLogMaxAge</EM> パラメーターの値を <CODE>00:00:00</CODE> に設定すると、接続ログ ファイルが保存期間をもとに自動的に削除されることがなくなります。</P></LI></UL>



## 正常な動作を確認する方法

接続ログが正しく構成されたことを確認するには、以下の手順を実行します。

1.  シェルで、次のコマンドを実行します。
    
        <Get-TransportService | Get-FrontEndTransportService | Get-MailboxTransportService> <ServerIdentity> | Format-List ConnectivityLog*

2.  表示された値が構成した値であることを確認します。

