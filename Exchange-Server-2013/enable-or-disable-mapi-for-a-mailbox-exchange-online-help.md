---
title: 'メールボックスの MAPI を有効または無効にする: Exchange Online Help'
TOCTitle: メールボックスの MAPI を有効または無効にする
ms:assetid: c2c6718c-a2c0-4ed2-b4ed-364c3cb1f592
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124497(v=EXCHG.150)
ms:contentKeyID: 50555867
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックスの MAPI を有効または無効にする

 

_**適用先:** Exchange Online, Exchange Server 2013_

Exchange 管理センター または Exchange 管理シェル を使用して、ユーザー メールボックスの MAPI を有効または無効にできます。MAPI を有効にすると、Outlook や他の MAPI 電子メール クライアントによるユーザーのメールボックスへのアクセスが可能になります。MAPI を無効にすると、Outlook や他の MAPI クライアントによるアクセスは行えません。ただし、メールボックスは電子メール メッセージの受信を続行します。また、これらのクライアントによるアクセスのサポートがメールボックスで有効になっている場合、ユーザーは Outlook Web App、POP 電子メール クライアント、IMAP クライアントを使用してメールボックスにアクセスし、電子メールを送信および受信できます。


> [!NOTE]
> Outlook Web App および MAPI/POP3/IMAP4 電子メール クライアントのサポートは、ユーザー メールボックスの作成時に既定で有効になります。



メールボックスへの電子メール クライアント アクセスの管理に関連する追加の管理タスクについては、次のトピックを参照してください。

  - [メールボックスに対して Outlook Web App を有効または無効にする](enable-or-disable-outlook-web-app-for-a-mailbox-exchange-2013-help.md)

  - [ユーザーの IMAP4 アクセスを有効または無効にする](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

  - [ユーザーの POP3 アクセスを有効または無効にする](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

## 始める前に把握しておくべき情報

  - 予想所要時間:2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「クライアント アクセス ユーザー設定」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EAC を使用して MAPI を有効または無効にする

1.  EAC で、**\[受信者\]** \> **\[メールボックス\]**に移動します。

2.  ユーザー メールボックスの一覧で、MAPI を有効または無効にするメールボックスをクリックし、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  メールボックスのプロパティ ページで、**\[メールボックスの機能\]** をクリックします。

4.  **\[電子メール接続\]** で、次のいずれかを行います。
    
      - MAPI を無効にするには、**\[MAPI: 有効\]** で **\[無効にする\]** をクリックします。
        
        MAPI を無効にするかどうかを確認する警告が表示されます。**\[はい\]** をクリックします。
    
      - MAPI を有効にするには、**\[MAPI: 無効\]** で **\[有効にする\]** をクリックします。

5.  **\[保存\]** をクリックして変更を保存します。

## Exchange 管理シェルを使用して MAPI を有効または無効にする

この例では、Ken Sanchez のメールボックスの MAPI を無効にします。

    Set-CASMailbox -Identity "Ken Sanchez" -MAPIEnabled $false

この例では、Esther Valle のメールボックスの MAPI を有効にします。

    Set-CASMailbox -Identity "Esther Valle" -MAPIEnabled $true

構文およびパラメーターの詳細については、「[Set-CASMailbox](https://technet.microsoft.com/ja-jp/library/bb125264\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

ユーザー メールボックスの MAPI が正常に有効化または無効化されたことを確認するには、次のいずれかを実行します。

  - EAC で、**\[受信者\]** \> **\[メールボックス\]** に移動し、メールボックスをクリックし、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

  - メールボックスのプロパティ ページで、**\[メールボックスの機能\]** をクリックします。

  - **\[電子メール接続\]** で、MAPI が有効または無効であるかを確認します。

または

  - Exchange 管理シェル で、次のコマンドを実行します。
    
        Get-CASMailbox <identity>
    
    MAPI が有効な場合、*MapiEnabled* プロパティの値は `True` になります。MAPI が無効な場合、この値は `False` になります。

