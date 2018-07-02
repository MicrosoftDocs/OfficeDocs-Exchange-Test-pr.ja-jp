---
title: 'Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスを開始する: Exchange 2013 Help'
TOCTitle: Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスを開始する
ms:assetid: 8b7e1a4c-87b3-4477-a95f-6b41cf2d38f0
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ673542(v=EXCHG.150)
ms:contentKeyID: 50555825
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスを開始する

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2012-11-16_

Microsoft 管理コンソール (MMC) でサービス スナップインを、またはコマンド プロンプトで cmd.exe を使用すると、クライアント アクセス サーバー上の MicrosoftExchange ユニファイド メッセージング呼び出しルーター サービスを開始できます。既定では、MicrosoftExchange ユニファイド メッセージング呼び出しルーター サービスは、クライアント アクセス サーバーのインストール後に開始されます。ただし、クライアント アクセス サーバーをオフラインにしていてオンラインに戻す必要がある場合など、MicrosoftExchange ユニファイド メッセージング呼び出しルーター サービスを手動で再開または停止することが必要になることもあります。

クライアント アクセス サーバーで MicrosoftExchange ユニファイド メッセージング呼び出しルーター サービスが開始されると、着信 UM 呼び出しの応答および処理においてクライアント アクセス サーバーを使用できるようになります。

クライアント アクセス サーバーに関連する追加の管理タスクについては、「[UM サービス手順](um-services-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - 以下の手順を実行するには、ローカル Administrators グループのメンバーであるアカウントを使用してクライアント アクセス サーバーにログオンする必要があります。

  - クライアント アクセス サーバーが、メールボックス サーバーと同じコンピューターまたは個別のコンピューターのどちらにインストールされているかを確認します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## MMC サービス スナップインを使用して Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスを開始する

1.  **\[スタート\]** ボタンをクリックし、**\[コントロール パネル\]** をクリックします。

2.  コントロール パネルで、**\[管理ツール\]** をダブルクリックします。

3.  **\[管理ツール\]** で、**\[サービス\]** をダブルクリックします。

4.  **\[サービス\]** 詳細ウィンドウで、**\[Microsoft Exchange ユニファイド メッセージング呼び出しルーター\]** を右クリックし、**\[開始\]** をクリックします。

## コマンド プロンプトを使用して Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスを開始する

1.  **\[スタート\]** ボタンをクリックし、**\[ファイル名を指定して実行\]** をクリックします。

2.  **\[開く\]** ボックスに次のコマンドを入力し、Enter キーを押します。
    
        net start MSExchangeUMCR

