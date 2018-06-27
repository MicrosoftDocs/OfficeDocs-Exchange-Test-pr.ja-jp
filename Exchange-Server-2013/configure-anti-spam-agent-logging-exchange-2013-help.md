---
title: 'スパム対策エージェントのログの構成: Exchange 2013 Help'
TOCTitle: スパム対策エージェントのログの構成
ms:assetid: df157ca3-ad8e-4302-acbc-5fbb8570c21d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb691337(v=EXCHG.150)
ms:contentKeyID: 49896517
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# スパム対策エージェントのログの構成

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-04-08_

エージェント ログには、特定の Exchange スパム対策エージェントによって実行された処理が記録されます。エージェント ログに書き込まれる情報は、エージェント、SMTP イベント、およびメッセージに対して実行された処理によって異なります。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「Transport Service (トランスポート サービス)」または「Edge Transport server (エッジ トランスポート サーバー)」。

  - 既定では、メールボックス サーバーのトランスポート サービスでスパム対策機能が有効になっていません。一般的には、Exchange 組織が受信メッセージの受信前にスパム対策フィルターを事前に設定しない場合に限り、スパム対策機能を有効にします。詳細については、「[メールボックス サーバーのスパム対策機能を有効にする](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)」を参照してください。

  - この手順を実行するには、シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用してスパム対策エージェント ログを構成する

次のコマンドを実行します。

    Set-TransportService <ServerIdentity> -AgentLogEnabled <$true | $false> -AgentLogMaxAge <dd.hh:mm:ss> -AgentLogMaxDirectorySize <Size> -AgentLogMaxFileSize <Size> -AgentLogPath <LocalFilePath>

この例では、Mailbox01 というメールボックス サーバーで次のようなエージェント ログ設定を行います。

  -  
    エージェント ログ ファイルの場所を D:\\Anti-Spam Agent Log に設定します。フォルダーが存在しない場合は、新たに作成されます。

  -  
    エージェント ログ ファイルの最大サイズを 20 MB に設定します。

  -  
    エージェント ログ ディレクトリの最大サイズを 400 MB に設定します。

  -  
    エージェント ログ ファイルの最大保存期間を 14 日に設定します。

<!-- end list -->

    Set-TransportService Mailbox01 -AgentLogPath "D:\Anti-Spam Agent Log" -AgentLogMaxFileSize 20MB -AgentLogMaxDirectorySize 400MB -AgentLogMaxAge 14.00:00:00


> [!NOTE]
> <UL>
> <LI>
> <P><EM>AgentLogPath</EM> パラメーターを <CODE>$null</CODE> の値に設定した場合、エージェント ログは無効になります。ただし、<EM>AgentLogPath</EM> を <CODE>$null</CODE> に設定した場合は、<EM>AgentLogEnabled</EM> パラメーターの値を <CODE>$true</CODE> にすると、イベント ログ エラーが発生します。エージェント ログを無効にするための望ましい方法は、<EM>AgentLogEnabled</EM> を <CODE>$false</CODE> に設定することです。</P>
> <LI>
> <P><EM>AgentLogMaxAge</EM> パラメーターを <CODE>00:00:00</CODE> の値に設定すると、エージェント ログ ファイルが保存期間によって自動的に削除されなくなります。</P></LI></UL>



構文およびパラメーターの詳細については、「[Set-TransportService](https://technet.microsoft.com/ja-jp/library/jj215682\(v=exchg.150\))」の *AgentLog* パラメーターを参照してください。

## 正常な動作を確認する方法

スパム対策エージェント ログが正常に構成されたことを確認するには、次の手順を実行します。

1.  シェルで、次のコマンドを実行します。
    
        Get-TransportService <ServerIdentity> | Format-List AgentLog*

2.  表示された値が構成した値であることを確認します。

