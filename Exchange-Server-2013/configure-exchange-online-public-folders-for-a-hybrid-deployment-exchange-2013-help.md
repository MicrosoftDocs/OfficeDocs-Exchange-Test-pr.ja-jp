---
title: 'ハイブリッド展開用に Exchange Online パブリック フォルダーを構成する: Exchange Online Help'
TOCTitle: ハイブリッド展開用に Exchange Online パブリック フォルダーを構成する
ms:assetid: d979edb3-967b-4431-8beb-0c236bf7f56d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Mt729076(v=EXCHG.150)
ms:contentKeyID: 72768739
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ハイブリッド展開用に Exchange Online パブリック フォルダーを構成する

 

_**適用先:**Exchange Server 2013_

**概要:** オンプレミスの Exchange 2013 ユーザーが、Exchange Online のパブリック フォルダーにアクセスできるようにするための手順。

ハイブリッド展開では、ユーザーは Exchange Online と Exchange オンプレミスのいずれか一方または両方に配置され、パブリック フォルダーは Exchange Online か Exchange オンプレミスのいずれかに配置されます。オンライン ユーザーが、Exchange Server 2013 のオンプレミス環境のパブリック フォルダーにアクセスすることが必要な場合があります。同様に、Exchange 2013 ユーザーが、Office 365 または Exchange Online のパブリック フォルダーにアクセスすることが必要な場合もあります。

この記事では、お使いの Exchange 2013 オンプレミス環境のユーザーが、Exchange Online/Office 365 のパブリック フォルダーにアクセスできるようにする方法について説明します。Exchange Online/Office 365 のユーザーがオンプレミス Exchange 2013 のパブリック フォルダーにアクセスできるようにする方法については、「[ハイブリッド展開用に Exchange 2013 パブリック フォルダーを構成する](configure-exchange-2013-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)」を参照してください。


> [!NOTE]
> Exchange 2010 または Exchange 2007 のパブリック フォルダーがある場合は、「<A href="configure-legacy-on-premises-public-folders-for-a-hybrid-deployment-exchange-2013-help.md">ハイブリッド展開用に従来の社内パブリック フォルダーを構成する</A>」をご覧ください。



## 始める前に把握しておくべき情報

1.  以下の手順では、ハイブリッド構成ウィザードを使って、社内環境と Exchange Online 環境の構成と同期を行うこと、およびほとんどのユーザーの自動検出に使われる DNS レコードが社内のエンドポイントを参照していることを前提としています。詳細については、「[ハイブリッド構成ウィザード](https://technet.microsoft.com/ja-jp/library/hh529921\(v=exchg.150\))」を参照してください。

2.  これらの手順は、オンプレミスの Exchange サーバー上で Outlook Anywhere が有効になっており、機能していることを前提としています。Outlook Anywhere を有効にする方法については、「[Outlook Anywhere](outlook-anywhere-exchange-2013-help.md)」をご覧ください。

3.  Exchange と Office 365 のハイブリッド展開におけるパブリック フォルダーの共存の実装では、インポート手順中の競合を修正することが必要になる場合があります。競合は、メールを有効にしたパブリック フォルダーにルーティング不可能な電子メール アドレスが割り当てられていることや、Office 365 の他のユーザーまたはグループとの競合、あるいはその他の原因により発生する可能性があります。

4.  複数の場所にまたがってパブリック フォルダーにアクセスするには、Outlook クライアントを 2012 年 11 月以降の Oooklook パブリック更新プログラムにアップグレードする必要があります。
    
    1.  Outlook 2010 用の 2012 年 11 月の Oooklook 更新プログラムをダウンロードするには、「[Microsoft Outlook 2010 (KB2687623) 32 ビット版の更新プログラム](https://www.microsoft.com/ja-jp/download/details.aspx?id=35702)」を参照してください。
    
    2.  Outlook 2007 用の 2012 年 11 月の Outlook 更新プログラムをダウンロードするには、「[Microsoft Office Outlook 2007 (KB2687404) の更新プログラム](https://www.microsoft.com/ja-jp/download/details.aspx?id=35718)」を参照してください。

5.  Outlook 2011 for Mac および Outlook for Mac for Office 365 ではクロスプレミスでのパブリック フォルダーがサポートされていません。Outlook 2011 for Mac または Outlook for Mac for Office 365 を利用してパブリック フォルダーにアクセスする場合、ユーザーはパブリック フォルダーと同じ場所にいる必要があります。また、メールボックスが Exchange Online にあるユーザーは、Outlook Web App を使用してオンプレミスのパブリック フォルダーにアクセスできなくなります。
    

    > [!NOTE]
    > Outlook 2016 for Mac はクロスプレミスのパブリック フォルダー用にサポートされています。組織内のクライアントが Outlook 2016 for Mac を使用している場合は、2016 年 4 月の更新プログラムをインストールしていることを確認してください。そうしないと、それらのユーザーは共存またはハイブリッド トポロジ内のパブリック フォルダーにアクセスすることができません。詳細については、「<A href="accessing-public-folders-with-outlook-2016-for-mac-exchange-2013-help.md">Outlook 2016 for Mac によるパブリック フォルダーへのアクセス</A>」を参照してください。



## 手順 1: スクリプトをダウンロードする

1.  以下のファイルを、[メールが有効なパブリック フォルダー - EXO からオンプレミスへのディレクトリ同期スクリプト](https://go.microsoft.com/fwlink/p/?linkid=797795) からダウンロードします。
    
      - `Import-PublicFolderMailboxes.ps1`
    
      - `ImportPublicFolderMailboxes.strings.psd1`
    
      - `Sync-MailPublicFoldersCloudToOnprem.ps1`
    
      - `Sync-MailPublicFoldersCloudToOnprem.strings.psd1`

2.  PowerShell を実行するローカル コンピューターにファイルを保存します。たとえば C:\\Archive などです。

## 手順 2: ディレクトリ同期を構成する

スクリプト `Sync-MailPublicFoldersCloudToOnprem.ps1` を実行すると、Exchange Online とお使いの Exchange 2013 オンプレミス環境間で、メール対応パブリック フォルダーが同期されます。ハイブリッド展開シナリオではクロスプレミス アクセス許可がサポートされないため、メール対応パブリック フォルダーに割り当てられる特殊なアクセス許可をクラウド内で再作成する必要があります。詳細については、「[Exchange Server 2013 のハイブリッド展開](https://technet.microsoft.com/ja-jp/59e32000-4fcf-417f-a491-f1d8f9aeef9b\(exchg.150\)#doc)」を参照してください。


> [!NOTE]
> 同期されたメール対応パブリック フォルダーは、メール フロー用のメール連絡先オブジェクトとして認識されますが、Exchange 管理センターでは表示できません。Get-MailPublicFolder コマンドを参照してください。クラウド内で SendAs アクセス許可を再作成するには、Add-RecipientPermission コマンドを使用します。



1.  Exchange 2013 サーバーでは、次のコマンドを実行して、メール対応パブリック フォルダーを Exchange Online/Office 365 からお使いのローカル オンプレミス Active Directory に同期させます。
    
        Sync-MailPublicFoldersCloudToOnprem.ps1 -Credential (Get-Credential)
    
    `Credential` は、Office 365 のためのユーザー名とパスワードです。


> [!NOTE]
> このスクリプトを毎日実行してメール対応パブリック フォルダーを同期させることもお勧めします。



## 手順 3: オンプレミス ユーザーを構成して、Exchange Online パブリック フォルダーにアクセスできるようにする

この手順の最終ステップとして、Exchange 2013 オンプレミス組織を構成して、Exchange Online パブリック フォルダーにアクセスできるようにします。

スクリプト `Import-PublicFolderMailboxes.ps1` を実行すると、メール対応ユーザーとして、クラウドからパブリック フォルダーのメールボックス オブジェクトをお使いのオンプレミス環境にインポートします。また、スクリプトは、インポートされたオブジェクトをリモート パブリック フォルダーのメールボックスとして構成します。

1.  Exchange 2013 サーバーでは、次のコマンドを実行して、パブリック フォルダーのメールボックス オブジェクトをクラウドからお使いのオンプレミス Active Directory にインポートします。
    
        Import-PublicFolderMailboxes.ps1 -Credential (Get-Credential)
    
    `Credential` は、Office 365 のためのユーザー名とパスワードです。
    

    > [!NOTE]
    > このスクリプトを毎日実行して、パブリック フォルダーのメールボックス オブジェクトをインポートすることをお勧めします。パブリック フォルダーのメールボックスがその容量の閾値に到達すると、自動的に複数の新しいメールボックスに分割してしまうためです。そのため、クラウドから最新のパブリック フォルダーのメールボックスをインポートしたことを常に確認します。



2.  Exchange 2013 オンプレミス組織から Exchange Online パブリック フォルダーにアクセスできるようにします。
    
        Set-OrganizationConfig -PublicFoldersEnabled Remote


> [!NOTE]
> 変更を確認するには、Active Directory の同期が完了するまで待つ必要があります。この処理は、完了するまで最大 3 時間かかります。3 時間ごとに繰り返される同期処理を待機できない場合は、任意の時点でディレクトリの同期を強制実行できます。ディレクトリの同期を強制実行する詳細な手順については、「<A href="http://technet.microsoft.com/ja-jp/library/jj151771.aspx">ディレクトリを同期する</A>」を参照してください。



## 設定が適用されたことを確認する方法

1.  Exchange Online 内にいるユーザーの Outlook にログオンし、次のパブリック フォルダー テストを実行します。
    
      - 階層の表示
    
      - アクセス許可のチェック
    
      - パブリック フォルダーの作成と削除
    
      - パブリック フォルダーに対する内容の追加と削除

