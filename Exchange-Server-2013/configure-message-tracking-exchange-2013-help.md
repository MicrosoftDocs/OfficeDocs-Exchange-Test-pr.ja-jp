---
title: 'メッセージ追跡を構成する: Exchange 2013 Help'
TOCTitle: メッセージ追跡を構成する
ms:assetid: 50eb5213-cf27-4179-b427-38d751ee4a70
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997984(v=EXCHG.150)
ms:contentKeyID: 51407527
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メッセージ追跡を構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2013-02-18_

メッセージ追跡は、Microsoft Exchange Server 2013 メールボックス サーバー上のトランスポート サービスまたはメールボックスとの間で転送されるすべてのメッセージの SMTP トランスポート アクティビティを記録します。メッセージ追跡ログを使用して、メッセージ フォレンシック、メール フロー分析、レポート、およびトラブルシューティングを行うことができます。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「トランスポート サービス」または「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「メールボックス サーバーの構成」。

  - Exchange 管理センター (EAC) を使用すると、メッセージ追跡を有効または無効にしたり、メッセージ追跡ログのパスを設定したりできます。その他すべてのメッセージ追跡オプションについては、Exchange 管理シェルを使用する必要があります。

  - Exchange 2013 メールボックス サーバーでは、**Set-TransportService** コマンドレットまたは **Set-MailboxServer** コマンドレットのいずれかを使用してメッセージ追跡オプションを構成できます。このトピックの手順では、**Set-TransportService** コマンドレットを使用します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## EAC を使用してメールボックス サーバーのメッセージ追跡を構成する

1.  EAC で <strong>サーバー</strong> \> <strong>サーバー</strong> に移動します。

2.  構成するメールボックス サーバーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  サーバー プロパティ ページで、<strong>トランスポート ログ</strong> をクリックします。

4.  <strong>メッセージ追跡ログ</strong> セクションで、以下のいずれかを変更します。
    
      - <strong>メッセージ追跡ログを有効にする</strong>   サーバーでメッセージ追跡ログを無効にするには、このチェック ボックスをオフにします。サーバーでメッセージ追跡を有効にするには、チェック ボックスをオンにします。
    
      - <strong>メッセージ追跡ログのパス</strong>   ローカル Exchange サーバー上の値を指定します。フォルダーが存在しない場合は、<strong>保存</strong> をクリックするとフォルダーが作成されます。

5.  <strong>保存</strong> をクリックします。

## シェルを使用してメッセージ追跡を構成する

メッセージ追跡を構成するには、次のコマンドを実行します。

    Set-TransportService <ServerIdentity> -MessageTrackingLogEnabled <$true | $false> -MessageTrackingLogMaxAge <dd.hh:mm:ss> -MessageTrackingLogMaxDirectorySize <Size> -MessageTrackingLogMaxFileSize <Size> -MessageTrackingLogPath <LocalFilePath> -MessageTrackingLogSubjectLoggingEnabled <$true|$false>

この例では、Mailbox01 というメールボックス サーバーで次のようなメッセージ追跡ログ設定を行います。

  -  メッセージ追跡のログ ファイルの場所を D:\\Message Tracking Log に設定します。フォルダーが存在しない場合は、新たに作成されます。

  -  メッセージ追跡ログ ファイルの最大サイズを 20 MB に設定します。

  -  メッセージ追跡ログ ディレクトリの最大サイズを 1.5 GB に設定します。

  -  メッセージ追跡ログ ファイルの最大保存期間を 45 日に設定します。

<!-- end list -->

    Set-TransportService Mailbox01 -MessageTrackingLogPath "D:\Hub Message Tracking Log" -MessageTrackingLogMaxFileSize 20MB -MessageTrackingLogMaxDirectorySize 1.5GB -MessageTrackingLogMaxAge 45.00:00:00


> [!NOTE]
> <UL>
> <LI>
> <P><EM>MessageTrackingLogPath</EM> パラメーターの値を <CODE>$null</CODE> に設定すると、メッセージ追跡は事実上無効になります。ただし、<EM>MessageTrackingLogEnabled</EM> パラメーターの値が <CODE>$true</CODE> の場合、イベント ログ エラーが生成されます。</P>
> <LI>
> <P><EM>MessageTrackingLogMaxAge</EM> パラメーターの値を <CODE>00:00:00</CODE> に設定すると、メッセージ追跡ログ ファイルが保存期間によって自動的に削除されなくなります。</P>
> <LI>
> <P>Exchange 2013 メールボックス サーバーでは、メッセージ追跡ログ ディレクトリの最大サイズは、<EM>MessageTrackingLogMaxDirectorySize</EM> パラメーターの値の 3 倍になります。異なる 4 つのサービスによって生成されるメッセージ追跡ログ ファイルは、それぞれ異なるファイル名プレフィックスを持っていますが、<STRONG>MSGTRKMA</STRONG> ログ ファイルに書き込まれるデータの量と頻度は、他の 3 つに比べてごくわずかなものです。詳細については、「<A href="message-tracking-exchange-2013-help.md">メッセージ追跡</A>」の「メッセージ追跡ログ ファイルの構造」を参照してください。</P></LI></UL>



この例では、Mailbox01 という名前のメールボックス サーバーのメッセージ追跡ログで、メッセージの件名のログを無効にします。

```powershell
Set-TransportService Mailbox01 -MessageTrackingLogSubjectLoggingEnabled $false
```

この例では、Mailbox01 という名前のメールボックス サーバーのメッセージ追跡を無効にします。

```powershell
Set-TransportService Mailbox01 -MessageTrackingLogEnabled $false
```

## 正常な動作を確認する方法

メッセージ追跡が正常に構成されたことを確認するには、次の手順を実行します。

1.  シェルで、次のコマンドを実行します。
    
        Get-TransportService <ServerIdentity> | Format-List MessageTrackingLog*

2.  表示された値が構成した値であることを確認します。

