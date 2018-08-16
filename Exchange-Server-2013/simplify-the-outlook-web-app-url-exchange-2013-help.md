---
title: 'Outlook Web App の URL を簡略化する: Exchange 2013 Help'
TOCTitle: Outlook Web App の URL を簡略化する
ms:assetid: 5fb6a873-f3cf-4f82-87d1-2ff6e47a0080
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998359(v=EXCHG.150)
ms:contentKeyID: 54652968
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Web App の URL を簡略化する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-07-16_

**概要**:この記事に記載されている手順を実行すると、組織のユーザーが Exchange 2013 の OWA へのアクセスに使う URL を簡略化できます。

ユーザーが各自の Exchange Server 2013 メールボックスへのアクセスに使う MicrosoftOutlook Web App の URL を簡略化できます。

ユーザーの Outlook Web App へのアクセスを簡略化するために、標準的な IIS 内の既定の Web サイトである Outlook Web App Web ページを、自動的にユーザーを https にリダイレクトするように構成することができます。「IIS マネージャーを使用して Outlook Web App の URL を簡略化する」の手順では、http://*server* に対する要求が https://*server*/owa にリダイレクトされます。クライアントとサーバー間で送信される情報をセキュリティ保護するために、インストール時に既定の Web サイトは SSL (Secure Sockets Layer) を必要とするように設定されます。

Windows Server 2008 の最上位ディレクトリにリダイレクトを構成すると、その設定は下位レベルのディレクトリに伝達されます。例えば、\[既定の Web サイト\] のリダイレクトを /owa 仮想ディレクトリに構成すると、/Autodiscover、/Exchange、および /Public などのすべての仮想ディレクトリを表示する \[HTTP リダイレクト\] ページにも構成する設定が表示されます。したがって、リダイレクト対象のディレクトリを除くすべての仮想ディレクトリからリダイレクト指定を削除する必要があります。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 10 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。 「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」トピックの「Outlook Web App のアクセス許可」セクション内の "IIS マネージャー" エントリ。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 手順 1: IIS マネージャーを使用して Outlook Web App の URL を簡略化し、SSL へのリダイレクションを強制する

1.  IIS マネージャーを起動します。

2.  ローカル コンピューターを展開し、<strong>サイト</strong> を展開して、<strong>既定の Web サイト</strong> をクリックします。

3.  \[既定の Web サイトのホーム\] ウィンドウの下部の <strong>機能ビュー</strong> がまだ選択されていない場合は、このオプションをクリックします。

4.  <strong>IIS</strong> セクションで、<strong>HTTP リダイレクト</strong> をダブルクリックします。

5.  <strong>このリダイレクト先に要求をリダイレクト</strong> チェック ボックスをオンにします。

6.  /owa 仮想ディレクトリの絶対パスを入力します。たとえば、「**https://mail.contoso.com/owa**」と入力します。

7.  <strong>リダイレクト動作</strong> で、<strong>要求をこのディレクトリのコンテンツにのみリダイレクト (サブディレクトリにはリダイレクトしない)</strong> チェック ボックスをオンにします。

8.  <strong>状態コード</strong> ボックスの一覧で、<strong>検出 (302)</strong> をクリックします。

9.  \[操作\] ウィンドウで、<strong>適用</strong> をクリックします。

10. <strong>既定の Web サイト</strong> をクリックします。

11. \[既定の Web サイト\] のホーム ウィンドウで、<strong>SSL 設定</strong> をダブルクリックします。

12. <strong>SSL 設定</strong> で、<strong>SSL が必要</strong> をオフにします。
    

    > [!NOTE]
    > <STRONG>[SSL を要求]</STRONG> をオフにしないと、ユーザーがセキュリティで保護されていない URL を入力した場合にリダイレクトされません。ユーザーにはアクセス拒否のエラーが表示されます。



## 手順 2:仮想ディレクトリからリダイレクト指定を削除する

仮想ディレクトリからリダイレクト指定を削除するには、次の手順に従います。

1.  コマンド プロンプト ウィンドウを開きます。

2.  \<*Window ディレクトリ*\>\\System32\\Inetsrv に移動します。

3.  次のコマンドを実行します。
    
    1.  `appcmd set config "Default Web Site/autodiscover" /section:httpredirect /enabled:false -commit:apphost`
    
    2.  `appcmd set config "Default Web Site/ecp" /section:httpredirect /enabled:false -commit:apphost`
    
    3.  `appcmd set config "Default Web Site/ews" /section:httpredirect /enabled:false -commit:apphost`
    
    4.  `appcmd set config "Default Web Site/owa" /section:httpredirect /enabled:false -commit:apphost`
    
    5.  `appcmd set config "Default Web Site/oab" /section:httpredirect /enabled:false -commit:apphost`
    
    6.  `appcmd set config "Default Web Site/powershell" /section:httpredirect /enabled:false -commit:apphost`
    
    7.  `appcmd set config "Default Web Site/rpc" /section:httpredirect /enabled:false -commit:apphost`
    
    8.  `appcmd set config "Default Web Site/rpcwithcert" /section:httpredirect /enabled:false -commit:apphost`
    
    9.  `appcmd set config "Default Web Site/Microsoft-Server-ActiveSync" /section:httpredirect /enabled:false -commit:apphost`

4.  コマンド `iisreset/noforce` を実行して完了します。

最上位ディレクトリからのリダイレクトを構成すると、web.config ファイルが \<*ドライブ*\>\\Program Files\\Microsoft\\Exchange Server\\\<*バージョン*\>\\ClientAccess\\oab の下に作成される場合があります。このとき、後でリダイレクトを削除すると、ユーザーが <strong>送受信</strong> をクリックしたときに Outlook がフリーズする可能性があります。リダイレクト削除後のこの現象を回避するには、\<*ドライブ*\>\\Program Files\\Microsoft\\Exchange Server\\\<*バージョン*\>\\ClientAccess\\oab から web.config ファイルを削除します。

## 正常な動作を確認する方法

Outlook Web App URL の簡略化と SSL 接続へのリダイレクトが成功したかどうかを確認するには、以下の手順を実行します。

1.  Web ブラウザーを開いて、Outlook Web App の新しい URL を http://\<*URL*\> という形式で入力します。

2.  SSL 接続を介して Outlook Web App サインイン・ページにリダイレクトされるはずです。

