---
title: 'IMAP4 の接続タイムアウト制限を設定する: Exchange 2013 Help'
TOCTitle: IMAP4 の接続タイムアウト制限を設定する
ms:assetid: 6b6a5bd1-a878-4a70-8e21-14d5042a58f1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998665(v=EXCHG.150)
ms:contentKeyID: 50555806
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# IMAP4 の接続タイムアウト制限を設定する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-11-28_

認証済みまたは認証されていない IMAP4 のアイドル接続に対する接続タイムアウト制限を構成するには、EAC またはシェルを使用します。

IMAP4 に関連する詳細情報については、「[Exchange Server 2013 での POP3 と IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間: 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「IMAP4 の設定」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して IMAP4 の接続タイムアウト制限を設定する

1.  EAC で **\[サーバー\]\>\[サーバー\]** に移動します。

2.  サーバーの一覧でクライアント アクセス サーバーを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  サーバーのプロパティ ページで、**\[IMAP4\]** をクリックします。

4.  下にスクロールして、**\[その他のオプション\]** をクリックします。

5.  **\[タイムアウト設定\]** で、次の設定を使用します。
    
      - **認証されたタイムアウト (秒)**    アイドル状態の認証済み接続を閉じるまでの待機時間を指定します。既定値は 1,800 です。指定できる値は 30 ～ 86,400 です。
    
      - **認証されていないタイムアウト (秒)**    アイドル状態の認証されていない接続を閉じるまでの待機時間を指定します。既定値は 60 です。指定できる値は 30 ～ 3,600 です。

6.  **\[適用\]** をクリックし、**\[OK\]** をクリックして変更を保存します。

設定を有効にするには、IMAP4 の接続タイムアウト制限を設定した後、IMAP4 サービスを再起動する必要があります。IMAP4 サービスを再起動する方法の詳細については、「[IMAP4 サービスの開始および停止](start-and-stop-the-imap4-services-exchange-2013-help.md)」を参照してください。

## シェルを使用して IMAP4 の接続タイムアウト制限を設定する

この例では、認証済みのアイドル接続の接続タイムアウト制限を設定します。

    Set -ImapSettings -Identity CAS01 -AuthenticatedConnectionTimeout TimeValue

この例では、認証されていないアイドル接続の接続タイムアウト制限を設定します。

    Set -ImapSettings -Identity CAS01 -PreAuthenticatedConnectionTimeout TimeValue

設定を有効にするには、IMAP4 の接続タイムアウト制限を設定した後、IMAP4 サービスを再起動する必要があります。IMAP4 サービスを再起動する方法の詳細については、「[IMAP4 サービスの開始および停止](start-and-stop-the-imap4-services-exchange-2013-help.md)」を参照してください。

構文およびパラメーターの詳細については、「[Set-ImapSettings](https://technet.microsoft.com/ja-jp/library/aa998252\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

接続制限が正常に設定されたことを確認するには、次の手順のいずれかを実行します。

1.  EAC で **\[サーバー\]\>\[サーバー\]** に移動します。

2.  サーバーの一覧でクライアント アクセス サーバーを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  サーバーのプロパティ ページで、**\[IMAP4\]** をクリックします。

4.  下にスクロールして、**\[その他のオプション\]** をクリックします。

5.  **\[タイムアウト設定\]** で、接続設定が正しいことを確認します。

または

1.  シェルで、次のコマンドを実行します。
    
        Get-ImapSettings | format-list

2.  接続設定が正しいことを確認します。

## 詳細情報

IMAP4 の認証タイムアウト制限を設定した後、必要に応じて次の操作も実行してください。

[Exchange 2016 で IMAP4 を有効にする](enable-imap4-in-exchange-2013-exchange-2013-help.md)

[IMAP4 の接続の制限を設定する](set-connection-limits-for-imap4-exchange-2013-help.md)

