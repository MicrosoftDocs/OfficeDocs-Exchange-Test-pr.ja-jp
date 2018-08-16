---
title: 'メールボックスに対して Outlook Web App を有効または無効にする: Exchange Online Help'
TOCTitle: メールボックスに対して Outlook Web App を有効または無効にする
ms:assetid: abc19646-6211-4f18-a060-e347452dcc53
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124124(v=EXCHG.150)
ms:contentKeyID: 50555845
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックスに対して Outlook Web App を有効または無効にする

 

_**適用先:** Exchange Online, Exchange Server 2013_

EAC またはシェルを使用して、ユーザー メールボックスの Outlook Web App を有効または無効にできます。Outlook Web App が有効な場合、ユーザーは Outlook Web App を使用して電子メールを送信および受信できます。Outlook Web App が無効な場合、メールボックスは電子メール メッセージの受信を続行し、ユーザーは MAPI クライアント (Microsoft Outlook など) や POP 電子メール クライアント または IMAP 電子メール クライアントを使用して、メールボックスにアクセスして電子メールを送信および受信できます。ただし、メールボックスにおいて、これらのクライアントによるアクセスのサポートが有効であることを前提とします。


> [!NOTE]
> Outlook Web App および MAPI/POP3/IMAP4 電子メール クライアントのサポートは、ユーザー メールボックスの作成時に既定で有効になります。



メールボックスへの電子メール クライアント アクセスの管理に関連する追加の管理タスクについては、次のトピックを参照してください。

  - [メールボックスの MAPI を有効または無効にする](enable-or-disable-mapi-for-a-mailbox-exchange-online-help.md)

  - [ユーザーの IMAP4 アクセスを有効または無効にする](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

  - [ユーザーの POP3 アクセスを有効または無効にする](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

## 始める前に把握しておくべき情報

  - 予想所要時間 : 2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「クライアント アクセス ユーザー設定」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して Outlook Web App を有効または無効にする

1.  EAC で、<strong>受信者</strong> \> <strong>メールボックス</strong>に移動します。

2.  ユーザー メールボックスの一覧で、Outlook Web App を有効または無効にするメールボックスをクリックし、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  メールボックスのプロパティ ページで、<strong>メールボックスの機能</strong> をクリックします。

4.  <strong>電子メール接続</strong> で、次のいずれかを行います。
    
      - Outlook Web App を無効にするには、<strong>Outlook Web App:有効</strong> で <strong>無効にする</strong> をクリックします。
        
        Outlook Web App を無効にするかどうかを確認する警告が表示されます。<strong>はい</strong> をクリックします。
    
      - Outlook Web App を有効にするには、<strong>Outlook Web App:無効</strong> で <strong>有効にする</strong> をクリックします。

5.  <strong>保存</strong> をクリックして変更を保存します。


> [!NOTE]
> EAC の一括編集機能を使用して、複数のユーザー メールボックスに対して Outlook Web App を有効または無効にできます。これを行う方法の詳細については、「<A href="manage-user-mailboxes-exchange-2013-help.md">ユーザー メールボックスの管理</A>」の「ユーザー メールボックスを一括編集する」を参照してください。



## シェルを使用して Outlook Web App を有効または無効にする

この例では、Yan Li のメールボックスにおける Outlook Web App を無効にします。

    Set-CASMailbox -Identity "Yan Li" -OWAEnabled $false

この例では、Elly Nkya のメールボックスにおける Outlook Web App を有効にします。

    Set-CASMailbox -Identity Ellyn@contoso.com -OWAEnabled $true

構文およびパラメーターの詳細については、「[Set-CASMailbox](https://technet.microsoft.com/ja-jp/library/bb125264\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

ユーザー メールボックスの Outlook Web App が正常に有効化または無効化されたことを確認するには、次のいずれかを実行します。

  - EAC で、<strong>受信者</strong> \> <strong>メールボックス</strong> に移動し、メールボックスをクリックし、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

  - メールボックスのプロパティ ページで、<strong>メールボックスの機能</strong> をクリックします。

  - <strong>電子メール接続</strong> で、Outlook Web App が有効または無効であるかを確認します。

または

  - シェルで、次のコマンドを実行します。
    
        Get-CASMailbox <identity>
    
    Outlook Web App が有効な場合、*OWAEnabled* プロパティの値は `True` になります。Outlook Web App が無効な場合、この値は `False` になります.

