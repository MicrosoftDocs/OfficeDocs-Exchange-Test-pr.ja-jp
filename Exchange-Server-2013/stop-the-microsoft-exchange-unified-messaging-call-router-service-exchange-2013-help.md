---
title: 'Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスの停止: Exchange 2013 Help'
TOCTitle: Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスの停止
ms:assetid: 79935528-1a8c-4f22-826c-8f9a60f4f6f4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ673535(v=EXCHG.150)
ms:contentKeyID: 50555800
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスの停止

 

_**適用先:**Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:**2012-11-16_

Microsoft 管理コンソール (MMC) でサービス スナップインを、またはコマンド プロンプトで cmd.exe を使用すると、クライアント アクセス サーバー上の MicrosoftExchange ユニファイド メッセージング呼び出しルーター サービスを停止できます。このサービスを停止する必要のある場合もあります。たとえば、クライアント アクセス サーバーをオフラインにする必要のあるときなどです。MicrosoftExchange ユニファイド メッセージング呼び出しルーター サービスを停止すると、クライアント アクセス サーバーは、着信呼び出しを受け付けて処理することができなくなります。

クライアント アクセス サーバーに関連する追加の管理タスクについては、「[UM サービス手順](um-services-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - 以下の手順を実行するには、ローカル Administrators グループのメンバーであるアカウントを使用してクライアント アクセス サーバーにログオンする必要があります。

  - クライアント アクセス サーバーが、メールボックス サーバーと同じコンピューターまたは個別のコンピューターのどちらにインストールされているかを確認します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## MMC サービス スナップインを使用して Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスを停止する

1.  **\[スタート\]** ボタンをクリックし、**\[コントロール パネル\]** をクリックします。

2.  コントロール パネルで、**\[管理ツール\]** をダブルクリックします。

3.  **\[管理ツール\]** で、**\[サービス\]** をダブルクリックします。

4.  **\[サービス\]** 詳細ウィンドウで、**\[Microsoft Exchange ユニファイド メッセージング呼び出しルーター\]** を右クリックし、**\[停止\]** をクリックします。

## コマンド プロンプトを使用して Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスを停止する

1.  **\[スタート\]** ボタンをクリックし、**\[ファイル名を指定して実行\]** をクリックします。

2.  **\[開く\]** ボックスに次のコマンドを入力し、Enter キーを押します。
    
        net stop MSExchangeUMCR

