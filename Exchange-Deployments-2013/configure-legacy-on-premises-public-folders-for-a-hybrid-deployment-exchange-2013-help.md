---
title: 'ハイブリッド展開用に従来の社内パブリック フォルダーを構成する: Exchange 2013 Help'
TOCTitle: ハイブリッド展開用に従来の社内パブリック フォルダーを構成する
ms:assetid: bcb0ac98-2949-486b-a8ab-8549c021651b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn249373(v=EXCHG.150)
ms:contentKeyID: 54913224
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ハイブリッド展開用に従来の社内パブリック フォルダーを構成する

 

_**適用先:**Exchange Online, Exchange Server 2010, Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:**2018-05-22_

**概要**:この記事内の手順を使用して、Office 365 と Exchange 2007 または Exchange 2010 オンプレミス展開の間でパブリック フォルダーを同期します。

ハイブリッド展開では、ユーザーは Exchange Online、オンプレミスのいずれか一方または両方に配置され、パブリック フォルダーは Exchange Online またはオンプレミスのいずれかに配置されます。パブリック フォルダーを配置できるのは 1 か所だけです。このため、パブリック フォルダーを Exchange Online またはオンプレミスのいずれに配置するかを決定する必要があります。パブリック フォルダーを両方の場所に配置することはできません。パブリック フォルダー メールボックスは、ディレクトリ同期サービスによって、Exchange Online に同期します。ただし、メール対応のパブリック フォルダーが異なる場所間で同期されることはありません。

このトピックでは、ユーザーが Office 365 内に存在し、Exchange 2010 SP3 または Exchange 2007 SP3 RU10 のパブリック フォルダーがオンプレミスの場合の、メール対応パブリック フォルダーの同期方法について説明します。ただし、オンプレミス (ターゲットのパブリック フォルダー階層に対してローカル) の MailUser オブジェクトで表現されない Office 365 ユーザーは、従来のまたは Exchange 2013 オンプレミスのパブリック フォルダーにアクセスできません。


> [!NOTE]
> このトピックでは、Exchange 2010 SP3 サーバーと Exchange 2007 SP3 RU10 サーバーを<EM>従来の Exchange サーバー</EM>と呼びます。



次のスクリプトを使って、電子メール対応パブリック フォルダーを同期します。これらのスクリプトは社内環境で実行される Windows タスクによって開始されます。

1.  `Sync-MailPublicFolders.ps1`   このスクリプトは、メール対応パブリック フォルダー オブジェクトをローカルの Exchange オンプレミス展開と Office 365 の間で同期します。また、ローカルの Exchange オンプレミス展開をマスターとして使用して、O365 に適用する必要のある変更を確認します。このスクリプトは、ローカルのオンプレミス Exchange 展開内に存在するものに基づいて、O365 Active Directory 上のメール対応パブリック フォルダー オブジェクトを作成、更新、または削除します。

2.  `SyncMailPublicFolders.strings.psd1`    これは、前述の同期スクリプトで使用されるサポート ファイルで、前述のスクリプトと同じ場所にコピーする必要があります。

この手順が完了すると、社内ユーザーと Office 365 ユーザーは、同じ社内パブリック フォルダー インフラストラクチャにアクセスできるようになります。

## パブリック フォルダーと併用できる Exchange のハイブリッド バージョン

次の表に、サポートされているユーザー メールボックスとパブリック フォルダーのバージョンと場所の組み合わせを示します。「ハイブリッド適用不可」はサポート対象のシナリオではありますが、パブリック フォルダーとユーザーの両方が同じ場所に存在しているため、ハイブリッド シナリオとは見なされません。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>   </th>
<th>社内 Exchange 2007 または Exchange 2010 のユーザー メールボックス</th>
<th>社内 Exchange 2013 のユーザー メールボックス</th>
<th>Exchange Online のユーザー メールボックス</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>社内 Exchange 2007 または Exchange 2010 のパブリック フォルダー</p></td>
<td><p>ハイブリッド適用不可</p></td>
<td><p>ハイブリッド適用不可</p></td>
<td><p>サポート</p></td>
</tr>
<tr class="even">
<td><p>社内 Exchange 2013 のパブリック フォルダー</p></td>
<td><p>ハイブリッド適用不可</p></td>
<td><p>ハイブリッド適用不可</p></td>
<td><p>サポート</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Online のパブリック フォルダー</p></td>
<td><p>非サポート</p></td>
<td><p>サポート</p></td>
<td><p>ハイブリッド適用不可</p></td>
</tr>
</tbody>
</table>


Exchange 2003 パブリック フォルダーでのハイブリッド構成はサポートされません。組織で Exchange 2003 を実行している場合、すべてのパブリック フォルダー データベースとレプリカを Exchange 2007 SP3 RU10 以降に移動する必要があります。Exchange 2003 でパブリック フォルダーのレプリカを保持することはできません。


> [!NOTE]
> Outlook 2016 は、Exchange 2007 のレガシ パブリック フォルダーへのアクセスをサポートしていません。Outlook 2016 のユーザーが含まれている場合、お使いのパブリック フォルダーを、より新しいバージョンの Exchange に移動する必要があります。Outlook 2016 および Office 2016 と、Exchange 2007 以前のバージョンの互換性についての詳細は、<A href="https://go.microsoft.com/fwlink/p/?linkid=849053">こちらの記事</A>でご覧いただけます。



## 手順 1: 始める前に把握しておくべき情報

1.  以下の手順では、ハイブリッド構成ウィザードを使って、社内環境と Exchange Online 環境の構成と同期を行うこと、およびほとんどのユーザーの自動検出に使われる DNS レコードが社内のエンドポイントを参照していることを前提としています。詳細については、「[ハイブリッド構成ウィザード](hybrid-configuration-wizard-exchange-2013-help.md)」を参照してください。

2.  これらの指示は、従来の社内 Exchange サーバー上で Outlook Anywhere が有効になっており、機能していることを前提としています。Outlook Anywhere を有効にする方法については、「[Outlook Anywhere](https://technet.microsoft.com/ja-jp/library/bb123741\(v=exchg.150\))」を参照してください。

3.  Exchange と Office 365 のハイブリッド展開における従来のパブリック フォルダー共存の実装では、インポート手順中の競合を修正することが必要になる場合があります。競合は、メールを有効にしたパブリック フォルダーに割り当てられた、経路指定できない電子メール アドレス、Office 365 の他のユーザーや グループとの競合、その他の属性により発生する可能性があります。

4.  以下の手順では、Exchange Online 組織がパブリック フォルダーをサポートしているバージョンにアップグレードされていることを前提としています。

5.  Exchange Online で組織の管理役割グループのメンバーになっている必要があります。この役割グループは、Exchange Online にサブスクライブした場合に割り当てられるアクセス許可とは異なるものです。組織の管理役割グループを有効にする方法の詳細については、「[役割グループの管理](https://technet.microsoft.com/ja-jp/library/jj657480\(v=exchg.150\))」を参照してください。

6.  Exchange 2010 では、組織の管理役割グループまたはサーバーの管理 RBAC 役割グループのメンバーになっている必要があります。詳細については、「[役割グループにメンバーを追加する](https://go.microsoft.com/fwlink/?linkid=299212)」を参照してください。

7.  Exchange 2007 では、Exchange 組織管理者または Exchange サーバー管理者の役割を割り当てられる必要があります。さらに、対象サーバーのパブリック フォルダー管理者の役割およびローカルの Administrators グループを割り当てる必要があります。詳細については、「[管理者の役割にユーザーまたはグループを追加する方法](https://go.microsoft.com/fwlink/p/?linkid=81779)」を参照してください。

8.  Windows Server 2008 x64 で Exchange Server 2007 を実行している場合、[Windows PowerShell 2.0 および WinRM 2.0 for Windows Server 2008 x64 Edition](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=968930) にアップグレードする必要があります。Windows Server 2003 x64 で Exchange Server 2007 を実行している場合、Windows PowerShell 2.0 にアップグレードする必要があります。詳細については、「[Windows Server 2003 x64 Edition 用更新プログラム](https://www.microsoft.com/ja-jp/download/details.aspx?id=10512)」を参照してください。

9.  複数の場所にまたがってパブリック フォルダーにアクセスするには、Outlook クライアントを 2012 年 11 月以降の Oooklook パブリック更新プログラムにアップグレードする必要があります。
    
    1.  Outlook 2010 用の 2012 年 11 月の Oooklook 更新プログラムをダウンロードするには、「[Microsoft Outlook 2010 (KB2687623) 32 ビット版の更新プログラム](https://www.microsoft.com/ja-jp/download/details.aspx?id=35702)」を参照してください。
    
    2.  Outlook 2007 用の 2012 年 11 月の Outlook 更新プログラムをダウンロードするには、「[Microsoft Office Outlook 2007 (KB2687404) の更新プログラム](https://www.microsoft.com/ja-jp/download/details.aspx?id=35718)」を参照してください。

10. Outlook 2016 for Mac (と以前のバージョン) および Outlook for Mac for Office 365 では、クロスプレミスでの従来のパブリック フォルダーがサポートされていません。Outlook for Mac または Outlook for Mac for Office 365 を利用してパブリック フォルダーにアクセスする場合、ユーザーはパブリック フォルダーと同じ場所にいる必要があります。また、メールボックスが Exchange Online にあるユーザーは、Outlook Web App を使用してオンプレミスのパブリック フォルダーにアクセスできなくなります。

11. この記事内の手順に従ってハイブリッド展開用にオンプレミスのパブリック フォルダーを構成した後は、追加のステップを実行しない限り、組織の外部にいるユーザーはオンプレミスのパブリック フォルダーにメッセージを送信することはできません。パブリック フォルダーの承認済みドメインを、内部の中継に設定する (詳細については「[Exchange Online で承認済みドメインを管理する](https://technet.microsoft.com/ja-jp/library/jj945194\(v=exchg.150\))」を参照) か、または「[ディレクトリ ベースのエッジ ブロックを使用して無効な受信者に送信されたメッセージを拒否する](https://technet.microsoft.com/ja-jp/library/dn600322\(v=exchg.150\))」で説明されているように、ディレクトリ ベースのエッジ ブロック (DBEB) を無効にすることができます。

## 手順 2: リモート パブリック フォルダーを検出可能にする

1.  パブリック フォルダーが Exchange 2010 以降のサーバー上に存在する場合、クライアント アクセス サーバーの役割を、パブリック フォルダー データベースが存在するすべてのメールボックス サーバーにインストールする必要があります。これにより、Microsoft Exchange RpcClientAccess サービスの実行が可能になり、すべてのクライアントがパブリック フォルダーにアクセスできるようになります。Exchange 2007 パブリック フォルダー サーバーにはクライアント アクセスの役割は不要で、この手順は必要ありません。詳細については、「[Exchange Server 2010 のインストール](https://technet.microsoft.com/ja-jp/library/bb124778\(v=exchg.141\).aspx)」を参照してください。この手順は、Exchange 2007 パブリック フォルダーでは必要ありません。
    

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

## 手順 3: スクリプトをダウンロードする

1.  次のファイルを、「[Mail-enabled Public Folders - directory sync script](https://www.microsoft.com/en-us/download/details.aspx?id=46381)」からダウンロードします。
    
      - `Sync-MailPublicFolders.ps1`
    
      - `SyncMailPublicFolders.strings.psd1`

2.  PowerShell を実行するローカル コンピューターにファイルを保存します。たとえば C:\\Archive などです。

## 手順 4: ディレクトリ同期を構成する

ディレクトリ同期サービスでは、メール対応パブリック フォルダーは同期されません。次のスクリプトを実行すると、施設全体でメール対応パブリック フォルダーが同期されます。ハイブリッド展開シナリオではクロスプレミス アクセス許可がサポートされないため、メール対応パブリック フォルダーに割り当てられる特殊なアクセス許可をクラウド内で再作成する必要があります。詳細については、「[Exchange Server 2013 のハイブリッド展開](exchange-server-hybrid-deployments-exchange-2013-help.md)」を参照してください。


> [!NOTE]
> 同期されたメール対応パブリック フォルダーは、メール フロー用のメール連絡先オブジェクトとして認識されますが、Exchange 管理センターでは表示できません。Get-MailPublicFolder コマンドをご覧ください。クラウド内で SendAs アクセス許可を再作成するには、Add-RecipientPermission コマンドを使用します。



1.  従来の Exchange サーバーでは、次のコマンドを実行して、メール対応パブリック フォルダーをローカルのオンプレミス Active Directory から O365 に同期させます。
    
        Sync-MailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
    ここで、`Credential` は Office 365 のユーザー名とパスワードで、`CsvSummaryFile` は同期操作やエラーを .CSV 形式で記録するためのパスです。


> [!NOTE]
> スクリプトを実行する前に、前述したように <CODE>-WhatIf</CODE> パラメーターを指定して実行することにより、スクリプトが環境内で実行するアクションをシミュレートすることをお勧めします。<BR>また、このスクリプトを毎日実行してメール対応パブリック フォルダーを同期させることもお勧めします。



## 手順 5: Exchange Online ユーザーを構成して、オンプレミスのパブリック フォルダーにアクセスできるようにする

この操作の最後の手順は、Exchange Online 組織を構成して、オンプレミスのレガシ パブリック フォルダーにアクセスできるようにすることです。

Exchange Online 組織から社内パブリック フォルダーにアクセスできるようにします。手順 2: リモート パブリック フォルダーを検出可能にするで作成した、すべてのプロキシ パブリック フォルダー メールボックスをポイントします。

**Windows PowerShell** で次のコマンドを実行します。

    Set-OrganizationConfig -PublicFoldersEnabled Remote -RemotePublicFolderMailboxes PFMailbox1,PFMailbox2,PFMailbox3

変更を確認するには、Active Directory の同期が完了するまで待つ必要があります。この処理は、完了するまで最大 3 時間かかります。3 時間ごとに繰り返される同期処理を待機できない場合は、任意の時点でディレクトリの同期を強制実行できます。ディレクトリの同期を強制実行する詳細な手順については、「[ディレクトリを同期する](http://technet.microsoft.com/ja-jp/library/jj151771.aspx)」を参照してください。Office 365 は、このコマンドで指定されるパブリック フォルダー メールボックスの 1 つをランダムに選択します。


> [!IMPORTANT]
> オンプレミス (ターゲットのパブリック フォルダー階層に対してローカル) の MailUser オブジェクトで表現されない Office 365 ユーザーは、従来のまたは Exchange 2013 オンプレミスのパブリック フォルダーにアクセスできません。解決方法については、サポート技術情報の記事「<A href="https://go.microsoft.com/fwlink/p/?linkid=699451">Exchange Online ユーザーがレガシ パブリック フォルダーにアクセスできない</A>」を参照してください。



## 設定が適用されたことを確認する方法

1.  Exchange Online 内にいるユーザーの Outlook にログオンし、次のパブリック フォルダー テストを実行します。
    
      - 階層の表示
    
      - アクセス許可のチェック
    
      - パブリック フォルダーの作成と削除
    
      - パブリック フォルダーに対する内容の追加と削除

## Office 365 を初めて使用する場合


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/JJ200581.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="LinkedIn Learning の小さいアイコン" alt="LinkedIn Learning の小さいアイコン" /> <strong>Office 365 を初めて使用する場合は、</strong><br />
LinkedIn Learning が提供する <a href="https://support.office.com/ja-jp/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a> のための無料のビデオ コースをご覧ください。</p></td>
</tr>
</tbody>
</table>

