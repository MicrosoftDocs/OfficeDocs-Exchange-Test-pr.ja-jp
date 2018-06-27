---
title: 'Outlook Web App: Exchange 2013 Help'
TOCTitle: Outlook Web App
ms:assetid: 3814b665-01e8-4881-9a44-163f14789ee4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657718(v=EXCHG.150)
ms:contentKeyID: 49896199
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Web App

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2016-12-09_

ここでは、Outlook Web App について説明します。これは、2010 より前のバージョンの Microsoft Exchange では Outlook Web Access と呼ばれていたものです。この記事では簡単な概要を説明し、役に立つ情報へのリンクを掲載します。

既定では、MicrosoftExchange 2013 をインストールすると、Outlook Web App が有効になります。MicrosoftOutlook Web App では、ほとんどの Web ブラウザーから自分の Exchange メールボックスをアクセスできます。

クライアント アクセス サーバーの役割は、Outlook Web App のプロキシ サービスとリダイレクト サービスを提供します。


> [!NOTE]
> Outlook Web App は、Exchange 2010 より前の Microsoft Exchange バージョンでは、Outlook Web Access と呼んでいました。



新機能についての詳細については、「[Exchange 2013 の新機能](what-s-new-in-exchange-2013-exchange-2013-help.md) 」を参照してください 。Exchange 2013 のクライアント アクセス サーバーの役割の詳細については、「[クライアント アクセス サーバー](client-access-server-exchange-2013-help.md)」を参照してください。

## Outlook Web App の概要

完全サポートの Web ブラウザーでは、ユーザーは、スレッド ビュー、受信トレイのルール、閲覧ウィンドウ、スケジュール アシスタントなどの機能にアクセスできます。完全サポートでないブラウザーも利用できますが、表示されるのは Outlook Web App の簡易バージョンであり、機能に制約があります。Outlook Web App の新機能についての詳細については、[Exchange 2013 の Outlook Web App の新機能](what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md) を参照してください。

## Outlook Web App の管理

Exchange 2013 では、最も基本的な Outlook Web App 管理タスクは Exchange 管理センター (EAC) で実行できます。これらすべてのタスク以外にも多くのタスクが、Exchange 管理シェルで実行できます。ただし、SSL (Secure Sockets Layer) の構成やユーザー用の簡易 URL のセットアップなど、タスクによっては必要に応じてインターネット インフォメーション サービス (IIS) マネージャーなどのツールを使用してください。

## Outlook Web App にアクセスする

管理者やユーザーが Outlook Web App にサインインするときは、次のような URL を使用します。**https://\<domain name\>/OWA** または **https://mail.\<domain name\>/OWA**

たとえば、組織のドメインが contoso.com の場合は、https://contoso.com/OWA または https://mail.contoso.com/OWA を使用します。Outlook Web App にアクセスする方法の詳細については、[こちら](https://support.microsoft.com/ja-jp/kb/2897680)を参照してください。別のサインイン URL に変更する場合や、SSL へのリダイレクトを行う場合は、「[Outlook Web App の URL を簡略化する](simplify-the-outlook-web-app-url-exchange-2013-help.md)」を参照してください。

電子メールのために Exchange Online または Office 365 を使用している場合、管理者やユーザーは **outlook.office365.com/owa** から Outlook Web App にアクセスするか、[こちらをクリック](http://go.microsoft.com/fwlink/p/?linkid=402333)してください。詳細については、「[Outlook Web App にサインインする](http://go.microsoft.com/fwlink/p/?linkid=511341)」と「[Office 365 にサインインする場所](http://go.microsoft.com/fwlink/p/?linkid=522691)」を参照してください。

