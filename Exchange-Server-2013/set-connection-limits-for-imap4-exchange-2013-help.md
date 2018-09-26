---
title: 'IMAP4 の接続の制限を設定する: Exchange 2013 Help'
TOCTitle: IMAP4 の接続の制限を設定する
ms:assetid: 8e3aa366-e77c-4c70-b78d-ddbb178cb521
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb123712(v=EXCHG.150)
ms:contentKeyID: 50555827
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# IMAP4 の接続の制限を設定する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-11-28_

EAC またはシェルを使用して、組織の IMAP4 接続制限を管理できます。

IMAP4 の接続制限を指定するときは、サーバー、IP アドレス、または特定のユーザーに対する接続制限を選択できます。

IMAP4 に関連する詳細情報については、「[Exchange Server 2013 での POP3 と IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「IMAP4 の設定」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してサーバー、IP アドレス、またはユーザーに対する IMAP4 接続制限を設定する

1.  EAC で <strong>サーバー\]\>\[サーバー</strong> に移動します。

2.  サーバーのリストでクライアント アクセス サーバーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  サーバー プロパティ ページで、<strong>IMAP4</strong> をクリックします。

4.  下にスクロールし、<strong>その他のオプション</strong> をクリックします。

5.  <strong>接続制限</strong> で、次の設定を使用します。
    
      - <strong>最大接続数</strong>   指定したサーバーが受け付ける接続の総数を指定します。これには、認証された接続と認証されていない接続が含まれます。既定値は 2,147,483,647 です。指定できる値は 1 ～ 2,147,483,647 です。
    
      - <strong>単一 IP アドレスからの接続の最大数</strong>   サーバーが受け付ける単一の IP アドレスからの接続の数を指定します。既定値は 2,147,483,647 です。指定できる値は 1 ～ 2,147,483,647 です。
    
      - <strong>単一ユーザーからの接続の最大数</strong>   サーバーが受け付ける特定のユーザーからの接続の総数を指定します。既定値は 16 です。指定できる値は 1 ～ 2,147,483,647 です。
    
      - <strong>コマンドの最大サイズ (バイト)</strong>   単一のコマンドの最大サイズを指定します。既定のサイズは 10,240 です。指定できる値は 1,024 ～ 16,384 です。

6.  <strong>適用</strong> をクリックし、<strong>OK</strong> をクリックして変更を保存します。

接続制限を設定した後、IMAP4 サービスを再起動する必要があります。IMAP4 サービスを再起動する方法の詳細については、「[IMAP4 サービスの開始および停止](start-and-stop-the-imap4-services-exchange-2013-help.md)」を参照してください。

## シェルを使用してサーバー、IP アドレス、またはユーザーに対する IMAP4 接続制限を設定する

この例では、サーバーの接続の制限を設定します。

```powershell
Set-ImapSettings -Identity CAS01 -MaxConnections Value
```

この例では、IP アドレスの接続の制限を設定します。

```powershell
Set-ImapSettings -Identity CAS01 -MaxConnectionsFromSingleIP Value
```

この例では、ユーザーの接続の制限を設定します。

```powershell
Set-ImapSettings -MaxConnectionsPerUser Value
```

この例では、コマンドの最大サイズを設定します。

```powershell
Set-ImapSettings -MaxCommandSize Value
```

接続制限を設定した後、IMAP4 サービスを再起動する必要があります。IMAP4 サービスを再起動する方法の詳細については、「[IMAP4 サービスの開始および停止](start-and-stop-the-imap4-services-exchange-2013-help.md)」を参照してください。

構文およびパラメーターの詳細については、「[Set-ImapSettings](https://technet.microsoft.com/ja-jp/library/aa998252\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

接続制限が正常に設定されたことを確認するには、次の手順を実行します。

1.  EAC で <strong>サーバー\]\>\[サーバー</strong> に移動します。

2.  サーバーのリストでクライアント アクセス サーバーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  サーバー プロパティ ページで、<strong>IMAP4</strong> をクリックします。

4.  下にスクロールし、<strong>その他のオプション</strong> をクリックします。

5.  <strong>接続制限</strong> で、接続設定が正しいことを確認します。

または

1.  シェルで、次のコマンドを実行します。
    
    ```powershell
    Get-ImapSettings | format-list
    ```

2.  接続設定が正しいことを確認します。

## 詳細情報

サーバー、IP アドレス、またはユーザーに対する IMAP4 接続制限を設定した後で、次の操作も実行できます。

[Exchange 2016 で IMAP4 を有効にする](enable-imap4-in-exchange-2013-exchange-2013-help.md)

[IMAP4 の接続タイムアウト制限を設定する](set-connection-time-out-limits-for-imap4-exchange-2013-help.md)

