---
title: 'ユーザーの IMAP4 アクセスを有効または無効にする: Exchange 2013 Help'
TOCTitle: ユーザーの IMAP4 アクセスを有効または無効にする
ms:assetid: a685fae4-b6f1-42fe-8bdc-5f99f9617799
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb676481(v=EXCHG.150)
ms:contentKeyID: 49896397
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ユーザーの IMAP4 アクセスを有効または無効にする

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2013-01-18_

ユーザーの IMAP4 を有効または無効にすることができます。


> [!NOTE]
> ユーザーの IMAP4 を有効または無効にした後で、Microsoft Exchange IMAP4 サービスおよび Microsoft Exchange IMAP4 Backend サービスを再起動する必要があります。IMAP4 サービスを再起動する方法の詳細については、「<A href="start-and-stop-the-imap4-services-exchange-2013-help.md">IMAP4 サービスの開始および停止</A>」を参照してください。



ユーザーのメールボックスの管理に関連した追加情報については、「[ユーザー メールボックスの管理](manage-user-mailboxes-exchange-2013-help.md)」を参照してください。

POP3 および IMAP4 に関連する詳細情報については、「[Exchange Server 2013 での POP3 と IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「受信者プロビジョニングのアクセス許可」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してユーザーの IMAP4 を有効または無効にする

1.  EAC で、**\[受信者\]** \> **\[メールボックス\]** に移動します。

2.  結果ウィンドウで、IMAP4 を有効または無効にするユーザーを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[ユーザー メールボックス\]** ダイアログ ボックスのコンソール ツリーで、**\[メールボックスの機能\]** をクリックします。
    
    結果ウィンドウの **\[電子メール接続\]** で次のいずれかを実行します。
    
      - ユーザーの IMAP4 を無効にするには、**\[IMAP4:有効\]** で **\[無効にする\]** をクリックします。
    
      - ユーザーの IMAP4 を有効にするには、**\[IMAP4:無効\]** で、**\[有効にする\]** をクリックします。

4.  **\[保存\]** をクリックします。

## シェルを使用して、ユーザーの IMAP4 を有効または無効にする

この例では、ユーザー John Smith の IMAP4 を有効にします。

    Set-CASMailbox -Identity "John Smith" -IMAPEnabled $true

この例では、ユーザー John Smith の IMAP4 を無効にします。

    Set-CASMailbox -Identity "John Smith" -IMAPEnabled $false

## 正常な動作を確認する方法

1.  EAC で、**\[受信者\]** \> **\[メールボックス\]** に移動します。

2.  結果ウィンドウで、IMAP4 を有効にするまたは無効にするユーザーを選択して、**\[編集\]** をクリックします。

3.  **\[ユーザー メールボックス\]** ダイアログ ボックスのコンソール ツリーで、**\[メールボックスの機能\]** をクリックします。
    
    結果ウィンドウで、**\[電子メール接続\]** の下を確認します。
    
      - ユーザーの IMAP4 が有効になっている場合は、次が表示されます: **\[IMAP4: 有効にする\]**。
    
      - ユーザーの IMAP4 が有効になっていない場合は、次が表示されます: **\[IMAP4: 無効にする\]**。

4.  **\[保存\]** をクリックします。

