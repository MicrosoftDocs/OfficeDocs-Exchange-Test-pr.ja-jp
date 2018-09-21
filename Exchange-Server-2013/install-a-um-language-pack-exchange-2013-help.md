---
title: 'UM 言語パックをインストールする: Exchange 2013 Help'
TOCTitle: UM 言語パックをインストールする
ms:assetid: ed14ffa5-c9b0-4367-b5da-564024b360ff
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd876951(v=EXCHG.150)
ms:contentKeyID: 49896541
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM 言語パックをインストールする

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2016-12-09_

UM ダイヤル プランまたは UM 自動応答で利用可能なユニファイド メッセージング言語の一覧に言語が表示されるようにするには、まず適切な UM 言語パックをインストールする必要があります。言語固有の自己解凍実行ファイルまたは **setup.exe /AddUmLanguagePack** コマンドを使用して、Microsoft Exchange ユニファイド メッセージング サービスを実行するメールボックス サーバーに言語パックをインストールします。UM 言語パックをインストールする前に、まずメールボックス サーバーのローカル フォルダーに言語パックをダウンロードする必要があります。UM 言語パックは、「[Exchange Server 2013 UM 言語パック](https://go.microsoft.com/fwlink/p/?linkid=266542)」からダウンロードできます。実行ファイルは、言語ごとに用意されています。

適切な UM 言語パックをインストールしたら、UM ダイヤル プランの <strong>設定</strong> ページのドロップダウン リストまたは UM 自動応答の <strong>全般</strong> ページの <strong>自動音声インターフェイスの言語</strong> ドロップダウン リストを表示することでインストールされている UM 言語パックの一覧を参照できます。また、UM ダイヤル プランおよび自動応答の既定の言語を英語 (en-US) 以外の言語にすることもできます。


> [!NOTE]
> Microsoft Exchange Server 2007 または Exchange&nbsp;2007 Service Pack 1 (SP1)、SP2、または SP3、あるいは Exchange 2010 Service Pack 1 SP1、SP2、または SP3 の UM 言語パックは、Exchange 2013 メールボックス サーバーで使用することはできません。



UM 言語に関連した追加タスクについては、「[UM 言語、プロンプト、および案内応答の手順](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間: 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「メールボックス サーバー (UM サービス)」。

  - メールボックス サーバーがクライアント アクセス サーバーとは別のコンピューターにインストールされているのか、それともクライアント アクセス サーバーおよびメールボックス サーバーが同じハードウェア上にあるのかを確認します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## UM 言語パックのインストール (.exe) ファイルを使用して UM 言語パックをインストールする

1.  「[Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/p/?linkid=266542)」から、メールボックス サーバーのローカル フォルダーに言語固有の UM 言語パック (.exe) ファイルをダウンロードします。

2.  UMLanguagePack.*\<CultureCode\>.exe* ファイルをダブルクリックします。たとえば、ドイツ語の UM 言語パックの場合、UMLanguagePack.de-DE.exe という名前のファイルをダウンロードします。

3.  
    
    Exchange 2013 セットアップ ウィザードの <strong>使用許諾契約書</strong> ページで、契約の条項を読んで、<strong>使用許諾契約書に同意します</strong> を選択し、<strong>次へ</strong> をクリックします。

4.  
    
    <strong>ユニファイド メッセージング言語パック</strong> ページで、<strong>次のユニファイド メッセージング言語パックがインストールされます。</strong> ウィンドウに正しい言語が表示されていることを確認し、<strong>インストール</strong> をクリックします。

5.  <strong>完了</strong> をクリックし、UM 言語パックのインストールを終了します。

## setup.exe を使用して UM 言語パックをインストールする

この例では、メールボックス サーバーの D:\\Exchange\\UMLanguagePacks フォルダーにダウンロードした日本語 (ja-JP) の UM 言語パックをインストールします。

```powershell
setup.exe /AddUmLanguagePack:ja-JP /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms
```

この例では、メールボックス サーバーの D:\\Exchange\\UMLanguagePacks フォルダーにダウンロードしたメキシコのスペイン語 (es-MX) の UM 言語パックおよびドイツ語 (de-DE) の UM 言語パックをインストールします。

    setup.exe /AddUmLanguagePack:es-MX,de-DE /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms


> [!WARNING]
> /IAcceptExchangeServerLicenseTerms パラメーターを使用しないと、次のエラーが表示されます。Microsoft Exchange Server 2013 無人セットアップへようこそ。Microsoft Exchange Server 2013 をインストールするには、ライセンス条項に同意する必要があります。使用許諾契約書を読むには、http://go.microsoft.com/fwlink/p/?LinkId=150127 にアクセスしてください。使用許諾契約書に同意するには、実行中のコマンドに /IAcceptExchangeServerLicenseTerms パラメーターを追加してください。詳細については、setup /? を実行してください。



利用可能な UM 言語およびカルチャー コードの詳細については、「[UM 言語、プロンプト、および案内応答](um-languages-prompts-and-greetings-exchange-2013-help.md)」をご覧ください。

