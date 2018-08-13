---
title: 'Outlook Web App のテーマの作成: Exchange 2013 Help'
TOCTitle: Outlook Web App のテーマの作成
ms:assetid: 7e1fa13c-3de3-45c2-b1fa-e74fc8487bda
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb201700(v=EXCHG.150)
ms:contentKeyID: 54652976
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Web App のテーマの作成

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

*テーマ*は、MicrosoftOutlook Web App が使用する背景色、フォント、強調表示色、アイコン、およびヘッダーを定義します。メディア ファイルとカスケード スタイル シート (css) ファイルの集合がテーマで、これらのファイルは、MicrosoftExchange のインストール ディレクトリ内の \\Client Access\\OWA\\prem\\*version*\\resources\\themes に格納されています。各テーマは、\\themes の独自のサブディレクトリに格納されています。

既定のテーマは、\\Client Access\\OWA\\prem\\*version*\\resources\\themes\\base に格納されています。各テーマ フォルダーには、テーマを定義するために必要なすべてのファイルが格納されています。これらのファイルには、CSS ファイル、グラフィック、およびテーマの名前を定義する .xml ファイルが含まれています。1 つのテーマからすべてのファイルを新しいフォルダーにコピーし、必要に応じてそれらのファイルを変更することで、追加のテーマを作成できます。

既定では、Exchange Server 2013 のインストール時に、次のように複数のテーマがインストールされます。

  - CSS (.css) ファイルは、色、グラデーション、およびフォントを定義します。

  - 画像 (.png) ファイルはアイコンおよび他のグラフィック要素を提供します。アイコンを編集する場合は、そのサイズを変更しないでください。いずれかのグラフィック要素のサイズを変更した場合は、変更内容をテストして、要素が所定の範囲に収まることを確認してください。

これらのファイルは、クライアント アクセス サーバーのインストール ディレクトリ内の \\Client Access\\OWA\\prem\\*\<version\>*\\resources\\themes に格納されます。各テーマは、テーマのサブディレクトリに格納されます。既存のテーマをコピーし、そのコピー内容を変更すれば、追加のテーマを作成することができます。

テーマを作成した後で、[Outlook Web App サインイン、言語選択、エラー ページをカスタマイズする](customize-the-outlook-web-app-sign-in-language-selection-and-error-pages-exchange-2013-help.md) 操作も実行できます。


> [!NOTE]
> Light バージョンの Outlook Web App は、テーマをサポートしていません。




> [!NOTE]
> Outlook Web App をサポートしている複数のサーバーがある場合、各サーバーにカスタム テーマをコピーする必要があります。また、カスタム テーマのバックアップ コピーを作成することも必要です。Exchange を再インストールまたはアップグレードする場合、テーマ フォルダーにあるすべてのファイルは上書きされます。再インストールまたはアップグレードの完了後に、テーマを適切なフォルダーにコピーして戻す必要があります。<BR>カスタム テーマの作成を開始する前に、変更するすべてのファイルのバックアップ コピーを作成してください。



## 始める前に把握しておくべき情報

  - このタスクの予想所要時間: 60 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。 [クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md) トピックの「Outlook Web App 仮想ディレクトリ」エントリ。

  - これらの手順を実行するには、ローカル サーバー管理者アクセスが必要です。

  - 既定の色を変更するのにはテキスト エディターとイメージを変更するのには、グラフィックス エディター必要があります。特定の色を一致させる必要があり、[カラー テーブル](https://go.microsoft.com/fwlink/p/?linkid=280679)での一致が見つからない場合は、カラーをサンプリングし、その HTML RGB 値を決定する画像編集ツールを使用できます。

  - ベスト プラクティスとして、Outlook Web App テーマを変更または作成するときは、以下のガイドラインを利用することをお勧めします。
    
      - 既存のテーマを編集する際は、編集を開始する前に、元のファイルのバックアップ コピーを作成します。
    
      - \\Client Access\\OWA\\prem\\*version*\\resources\\themes\\base フォルダー、またはこのフォルダー内にあるファイルはどれも削除しないでください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 実行方法

## 手順 1: 新しい Outlook Web App テーマを作成する

開始するには、新しいテーマのフォルダーを作成してから、既存のテーマから新しいフォルダーにファイルをコピーします。

1.  ローカルの Administrators グループのメンバーシップが委任されているアカウントを使用して、Outlook Web App 仮想ディレクトリをホストしている Exchange サーバーにログオンします。

2.  Windows エクスプローラーを開き、Exchange サーバー インストール ディレクトリを見つけます。

3.  \\Client Access\\OWA\\prem\\*version*\\resources\\themes に、新しいフォルダーを作成して名前 (Fourth Coffee など) を付けます。

4.  すべてのファイルを別のテーマ フォルダーから新しいフォルダーにコピーします。

## 手順 2: 新しいテーマに名前を付ける

新しいテーマに表示名を設定するには、以下の操作を行います。

1.  作成したカスタム テーマ フォルダー内の themeinfo.xml のコピーを開きます。

2.  テーマの `displayname` の値を見つけ、この値を使用する名前に変更します。たとえば `displayname = "Fourth Coffee Theme"` などです。

3.  themeinfo.xml を保存して閉じます。

## 手順 3: 新しいテーマのソート順を変更する (オプション)

必要に応じて、themeinfo.xml ファイルを編集することで、新しいテーマのソート順を変更できます。ソート順により、\[設定\] メニューの **\[テーマの変更\]** パネル内でのテーマの位置が決まります。

themeinfo.xml ファイルを使用して新しいテーマのソート順を変更するには、次の操作を行います。

1.  カスタム テーマ フォルダー内の themeinfo.xml のコピーを開きます。

2.  テーマの `sortorder` の値を見つけ、リスト内での新しいテーマの表示位置を反映するように、この値を変更します。テーマは、数値の昇順に並べられます。既定では、基本テーマが最初のテーマであり、その `sortorder` 値は "0" です。たとえば `sortorder="<number>"` などです。

3.  themeinfo.xml を保存して閉じます。

## 手順 4: 新しいテーマを変更する

ファイルをコピーし、テーマに名前を付けたので、テーマをカスタマイズできます。Outlook Web App テーマでは、次の要素をカスタマイズできます。

  - 画像ファイル。ヘッダー領域とアイコンを定義します。

  - CSS ファイル。フォントと色を定義します。

## 画像ファイル

テーマの画像は、\\themes*\\\<theme name\>*\\images\\ にある 2 つのフォルダーに格納されます。\\images\\0 フォルダーには、左から右へ読まれる言語 (英語など) で使われる画像が格納され、右から左へ読まれる言語では \\images\\rtl フォルダーの画像が使用されます。


> [!NOTE]
> \images\rtl フォルダーの画像の一部は \images\0 フォルダーの画像と同じですが、左右が逆転しています。



テーマをカスタマイズするには、画像編集ツールを使用して次の画像を開き、変更します。

  - Headerbgmain.png
    
      - これはメインのヘッダー画像です。画像は、ヘッダーの高さである 30 ピクセル以下にすることをお勧めします。既存のテーマは背景画像を使わないため、この画像は透明です。カスタム背景画像を持つテーマの例については、**Blueprint** テーマ フォルダーの画像を参照してください。

  - Headerbgright.png
    
      - これは、ヘッダーの後ろにタイル状に並べられる画像として使われます。既存のテーマは背景にタイル状に並べられる画像を使わないため、この画像は透明です。タイル状に並べられるカスタム背景画像を持つテーマの例については、**Blueprint** テーマ フォルダーの画像を参照してください。

  - sprite1.mouse.png
    
      - このファイルには、テーマで使われるほとんどの画像が格納されています。テーマに合わせて画像の色を変更したり、既定の Outlook Web App テキスト ロゴを変更することもできます。
    
      - 問題を回避するため、スプライト内の個々のアイコンのサイズは変更しないでください。また、必ず透過的な .png ファイルとして保存してください。

  - themepreview.png
    
      - この画像は、Outlook Web App の \[設定\] メニューの **\[テーマの変更\]** パネル内にあるテーマを表すために使われます。

## 色とフォント

カスケード スタイル シート (.css) ファイルは、テーマで使われる色とフォントを定義し、\\themes\\*\<theme name\>* の下の複数のフォルダーに格納されます。\\*\<theme name\>*\\0 フォルダーには、左から右へ読まれる言語 (英語など) で使われる .css ファイルが格納され、右から左へ読まれる言語では \\*\<theme name\>*\\rtl フォルダーの .css ファイルが使用されます。また言語固有のフォルダー (\\ja、\\ko、\\zhs、\\zht など) もあります。これらのフォルダーには、その言語で使われる .css ファイルが格納されます。

最初に \\*\<theme name\>*\\images\\0 フォルダーを変更します。各テーマでは 4 つの色が使われていますが、これらの色はカスタマイズ可能です。

  - BrandColor: \#0072C6

  - NavBarHoverColor: \#4C9CD7

  - UnreadColor: \#2A8DD4

  - FocusColor: \#DFEDFA

メモ帳などのテキスト エディターを使って、次の 2 つのファイル内のテーマの色に関して、上記値のすべてのインスタンスを検索して置換することができます。owa2styles.mouseCSS と owa2styles2.mouseCSSこれは、対象となる .css ファイルを格納する、新しいテーマの全フォルダーで実行する必要があります。

## 手順 5: 既定の Outlook Web App テーマを設定する

新しい既定テーマを設定すると、Outlook Web App の \[設定\] メニューからテーマを変更していないユーザーにだけ反映されます。

すべてのユーザーが既定のテーマを使用するように設定するには、既定のテーマを設定した上で、テーマ選択を無効にする必要があります。

## シェルを使用して Outlook Web App の既定のテーマを設定する

この例では、Outlook Web App の既定のテーマを設定します。ここでは、サーバー名が `fourthcoffee`、仮想ディレクトリ名が `owa`、Web サイト名が `default web site`、およびテーマが `Custom` という名前のフォルダー内にあります。

    set-owavirtualdirectory -identity "fourthcoffee\owa (default web site)" -defaulttheme Custom 

構文およびパラメーターの詳細については、「[Set-OwaVirtualDirectory](https://technet.microsoft.com/ja-jp/library/bb123515\(v=exchg.150\))」を参照してください。

## シェルを使用して Outlook Web App テーマ選択を無効にする

この例では、Outlook Web App のテーマ選択を無効にします。ここでは、サーバー名が `fourthcoffee`、仮想ディレクトリ名が `owa`、および Web サイト名が `default web site` です。

    set-owavirtualdirectory -identity "fourthcoffee\owa (default web site)" -themeselectionenabled $false 

また、次の例に示すように、両方のコマンドを同時に実行することもできます。

    set-owavirtualdirectory -identity "fourthcoffee\owa (default web site)" -defaulttheme Custom -themeselectionenabled $false

構文およびパラメーターの詳細については、「[Set-OwaVirtualDirectory](https://technet.microsoft.com/ja-jp/library/bb123515\(v=exchg.150\))」を参照してください。

## 手順 6: iisreset/noforce を実行してクリックして変更を保存する

テーマの追加または変更、テーマの名前変更、またはテーマのソート順の変更を行う場合、変更内容を有効にするには、インターネット インフォメーション サービス (IIS) を停止して始動する必要があります。この操作を行うには、新しいテーマを作成したサーバーで \[コマンド プロンプト\] ウィンドウを開き、**iisresest /nforce** コマンドを実行します。

## このタスクの検証方法

1.  新しいテーマを作成したサーバー上の仮想ディレクトリを使って、Outlook Web App にサインインします。Outlook Web App 仮想ディレクトリをホストしている Exchange サーバーの既定の Web サイトに対する変更をテストしている場合、Internet Explorer を開いて URL に「https://localhost/owa」と入力することで、テーマをテストすることができます。

2.  \[設定\] メニュー \> **\[テーマの変更\]** を選択し、カスタム テーマを選択して、カスタム テーマに切り替えます。

## 最新の変更が有効にならない場合は、iisreset/noforce を実行してください。

1.  Internet Explorer ツールバーで \[設定\]メニュー \> **\[インターネット オプション\]** と選択します。

2.  **\[全般\]** タブで、**\[閲覧の履歴\]** の下の **\[削除\]** を選択し、**\[インターネット一時ファイルと Web サイト ファイル\]** がオンであることを確認します。次に **\[削除\]** を選択して、これらのファイルを削除します。

3.  **\[OK\]** を選択して、**\[インターネット オプション\]** を閉じます。

4.  **\[最新の情報に更新\]** を選択すると変更が反映されます。

テーマ ファイルに変更を加えるたびに、これらの手順を繰り返して変更を確認する必要がある場合もあります。複数の箇所を変更する場合、Outlook Web App を開いたままにして、必要に応じて、サーバー上での **iisreset/noforce** の実行と、Internet Explorer からの一時ファイルの削除を繰り返し実行します。

