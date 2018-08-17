---
title: 'Outlook Web App サインイン、言語選択、エラー ページをカスタマイズする: Exchange 2013 Help'
TOCTitle: Outlook Web App サインイン、言語選択、エラー ページをカスタマイズする
ms:assetid: d8d9f735-7181-428f-9049-b9886dce5159
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee633483(v=EXCHG.150)
ms:contentKeyID: 54652985
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Web App サインイン、言語選択、エラー ページをカスタマイズする

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

ここでは、Outlook Web App のサインイン、言語選択、およびエラーの各ページをカスタマイズする方法について説明します。

Outlook Web App サインイン、言語選択、およびエラーのページは、テーマのリソース フォルダー内のグラフィック ファイルと .css ファイルに基づいて作成されます。Outlook Web App では、すべてのテーマに対してサインイン、言語選択、およびエラーの各ページのセットが 1 組だけ使われます。これらのページに対する変更は、すべてのユーザーに表示されます。テーマのリソース フォルダーは、V15\\FrontEnd\\HttpProxy\\owa\\auth\\version\\themes\\resources の Exchange インストール ディレクトリにあります。既定の色を変更するにはテキスト エディター、画像を変更するにはグラフィック エディターが必要です。特定の色に一致させる必要があり、その色を「[色の一覧](https://go.microsoft.com/fwlink/p/?linkid=280679)」で見つけられない場合は、画像編集ツールを使用して色をサンプリングすると、その HTML RGB 値を特定することができます。

複数のサーバーが Outlook Web App をサポートしていて、そのすべてで同じサインイン、言語、およびエラーの各ページを使用するには、修正したファイルを各サーバーにコピーする必要があります。カスタマイズされたファイルのバックアップ コピーも作成する必要があります。Exchange を再インストールまたはアップグレードする場合、テーマ フォルダーにあるすべてのファイルは上書きされます。再インストールまたはアップグレードの完了後に、カスタマイズされたファイルを適切なフォルダーにコピーして戻す必要があります。


> [!IMPORTANT]
> カスタムのサインイン ページとサインアウト ページの作成を開始する前に、変更するすべてのファイルのコピーをバックアップしてください。



カスタム テーマの作成の詳細については、「[Outlook Web App のテーマの作成](create-a-theme-for-outlook-web-app-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - このタスクの予想所要時間:45 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「Outlook Web App のアクセス許可」の「グラフィックス エディター」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## サインイン ページの色をカスタマイズする

1.  Exchange サーバーにログオンして、Windows Explorer を使って Exchange サーバーのインストール ディレクトリに移動し、\\V15\\FrontEnd\\HttpProxy\\owa\\auth\\\<バージョン\>\\themes\\resources を見つけます。

2.  メモ帳などのテキスト エディターを使用して、logon.css ファイルを開きます。

3.  既定の色の値 \#0072c6 を検索して、使用する色の HTML RBG 値と置き換えます。HTML RGB の値は、こちらで確認できます: [色の一覧](https://go.microsoft.com/fwlink/p/?linkid=280679)。

4.  ファイルを保存して閉じます。

## エラー ページの色をカスタマイズする

1.  Exchange サーバーにログオンして、Windows Explorer を使って Exchange サーバーのインストール ディレクトリに移動し、\\V15\\FrontEnd\\HttpProxy\\owa\\auth\\\<バージョン\>\\themes\\resources を見つけます。

2.  メモ帳などのテキスト エディターを使用して、errorFE.css ファイルを開きます。

3.  既定の色の値 \#0072c6 を検索して、使用する色の HTML RBG 値と置き換えます。HTML RGB の値は、こちらで確認できます: [色の一覧](https://go.microsoft.com/fwlink/p/?linkid=280679)。

4.  ファイルを保存して閉じます。

## 言語選択ページの色をカスタマイズする

1.  Exchange サーバーにログオンして、Windows Explorer を使って Exchange サーバーのインストール ディレクトリに移動し、\\V15\\Client Access\\OWA\\version\\Owa2\\resources\\styles を見つけます。

2.  メモ帳などのテキスト エディターを使用して、LanguageSelection.css ファイルを開きます。

3.  既定の色の値 \#0072c6 を検索して、使用する色の HTML RBG 値と置き換えます。HTML RGB の値は、こちらで確認できます: [色の一覧](https://go.microsoft.com/fwlink/p/?linkid=280679)。

4.  ファイルを保存して閉じます。

## サインイン ページとエラー ページの画像をカスタマイズする

画像編集ツールを使って、サインイン ページとエラー ページの作成に使用する画像を開いて編集します。

1.  Exchange サーバーにログオンして、Windows Explorer を使って Exchange サーバーのインストール ディレクトリに移動し、\\V15\\FrontEnd\\HttpProxy\\owa\\auth\\\<バージョン\>\\themes\\resources を見つけます。

2.  グラフィックス エディターを使って、次のファイルを開いて編集します。
    
      - owa\_text\_blue.png ("Outlook Web App" テキスト ロゴを変更します)
    
      - olk\_logo\_white.png (左側のバーのアプリ ロゴを変更します)
    
      - olk\_logo\_white\_cropped.png (エラー ページの左側のウィンドウの画像を変更します)
    
      - sign\_in\_arrow.png (\[サインイン\] ボタンの左側のアイコンを変更します)
    
      - olk\_exchange\_text\_blue.png (tnarrow レイアウトの "Outlook Mobile" ロゴを変更します)
    
      - olk\_logo\_white\_small.png は tnarrow で使われます。
    
      - olk\_exchange\_text\_stacked\_white\_small.png は tnarrow で使われます。

3.  既定の色の値 \#0072c6 を検索して、使用する色の HTML RBG 値と置き換えます。HTML RGB の値は、こちらで確認できます: [色の一覧](https://go.microsoft.com/fwlink/p/?linkid=280679)。

4.  ファイルを保存して閉じます。

## 正常な動作を確認する方法

Internet Explorer で Outlook Web App のサインイン ページを開きます。Outlook Web App 仮想ディレクトリをホストしているサーバーの既定の Web サイトに対する変更をテストしている場合、Internet Explorer を開いて URL に「https://localhost/owa」と入力することで、テストを実行することができます。

変更されない場合は、以下の操作を実行してください。

1.  ツールバーで <strong>設定</strong> \> <strong>インターネット オプション</strong> \> <strong>一般</strong> と選択します。

2.  <strong>閲覧の履歴</strong> の下で <strong>削除</strong> を選択します。

3.  <strong>インターネット一時ファイルと Web サイト ファイル</strong> を選択し、<strong>削除</strong> を選択します。

4.  削除が終了したら、<strong>OK</strong> を選択して、<strong>インターネット オプション</strong> を閉じます。

5.  ブラウザー ウィンドウを更新します。


> [!TIP]
> 変更の効果を確認するには、編集している .css ファイルを開いたままにして、変更するたびにファイルを保存して、ブラウザー ウィンドウを更新します。


