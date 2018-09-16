﻿---
title: '共有メールボックスを作成する: Exchange Online Help'
TOCTitle: 共有メールボックスを作成する
ms:assetid: d34bc827-1e83-4a7f-a219-8ba9c19fe24b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ150570(v=EXCHG.150)
ms:contentKeyID: 48270090
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 共有メールボックスを作成する

 

_**適用先:** Exchange Online, Exchange Server 2013, Office 365 Enterprise_

**予想所要時間:5 分**

共有メールボックスを使用すると、特定グループのユーザーが、共通アカウント (info@contoso.com、contact@contoso.com など) から電子メールを簡単に監視および送信できるようになります。グループ内のユーザーが共有メールボックス宛に送られたメッセージに返信すると、その電子メールはユーザー個人からではなく、共有メールボックスから送信された電子メールとして表示されます。


> [!IMPORTANT]
> Office 365 for Business を使用している場合は、Office 365 管理センターで共有メールボックスを作成する必要があります。 
> <UL>
> <LI>
> <P><A href="https://go.microsoft.com/fwlink/p/?linkid=834766">一般企業向け Outlook on the web で共有メールボックスを開いて使用する</A></P></LI></UL>



組織でハイブリッド Exchange 環境を使用する場合は、オンプレミスの Exchange 管理センター (EAC) を使用して、共有メールボックスを作成して管理する必要があります。共有メールボックスの詳細については、「[共有メールボックス](shared-mailboxes-exchange-2013-help.md)」を参照してください。

## EAC を使用して共有メールボックスを作成する

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「ユーザー メールボックス」。

1.  <strong>受信者</strong> \> <strong>共有</strong> \> <strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン")に移動します。

2.  必須フィールドの入力。
    
      - **表示名**
    
      - **電子メール アドレス**

3.  「フル アクセス」または「差出人を指定して送信する」のアクセス許可を付与するには、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックし、アクセス許可を付与するユーザーを選択します。**CTRL** キーを使用して、複数のユーザーを選択できます。使用するアクセス許可がわからない場合このトピックの後半の「どのアクセス許可を使用するか。」を参照してください。
    

    > [!NOTE]
    > フル アクセスのアクセス許可を使用すれば、ユーザーはメールボックスを開き、その中でアイテムを作成/変更することができます。「差出人を指定して送信する」アクセス許可を使用すれば、メールボックスの所有者以外のユーザーでも、この共有メールボックスから電子メールを送信することができます。共有メールボックスを正常に操作するには、両方のアクセス許可が必要です。



4.  <strong>保存</strong> をクリックして変更を保存し、共有メールボックスを作成します。

## EAC を使用して共有メールボックスを編集するには

1.  <strong>受信者</strong> \> <strong>共有</strong> \> <strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン")に移動します。

2.  <strong>メールボックスの委任</strong> をクリックします。

3.  「フル アクセス」または「差出人を指定して送信する」のアクセス許可を付与または削除するには、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") または <strong>削除</strong>![\[削除\] アイコン](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[削除] アイコン") をクリックしてから、アクセス許可を付与 (削除) するユーザーを選択します。
    

    > [!NOTE]
    > フル アクセスのアクセス許可を使用すれば、ユーザーはメールボックスを開き、その中でアイテムを作成/変更することができます。「差出人を指定して送信する」アクセス許可を使用すれば、メールボックスの所有者以外のユーザーでも、この共有メールボックスから電子メールを送信することができます。共有メールボックスを正常に操作するには、両方のアクセス許可が必要です。



4.  <strong>保存</strong> をクリックして変更を保存します。

## 共有メールボックスを使用する

ユーザーが共有メールボックスにアクセスして使用する方法の詳細については、以下をご覧ください。

  - [Outlook 2016 および Outlook 2013 で共有メールボックスを開いて使用する](https://go.microsoft.com/fwlink/p/?linkid=834764)

  - [一般企業向け Outlook on the web で共有メールボックスを開いて使用する](https://go.microsoft.com/fwlink/p/?linkid=834766)

## シェルを使用して共有メールボックスを作成する

この例では、共有メールボックス Sales Department を作成し、"フル アクセス"および"代理人として送信する"アクセス許可をセキュリティ グループ MarketingSG に付与します。セキュリティ グループのメンバーには、メールボックスへのアクセス許可が付与されます。


> [!NOTE]
> この例では、セキュリティ グループの MarketingSG を既に作成していて、そのセキュリティ グループはメールが有効と想定します。「<A href="https://docs.microsoft.com/ja-jp/exchange/recipients-in-exchange-online/manage-mail-enabled-security-groups">メールが有効なセキュリティ グループの管理</A>」を参照してください。



    New-Mailbox -Shared -Name "Sales Department" -DisplayName "Sales Department" -Alias Sales | Set-Mailbox -GrantSendOnBehalfTo MarketingSG | Add-MailboxPermission -User MarketingSG -AccessRights FullAccess -InheritanceType All

構文およびパラメーターの詳細については、「[New-Mailbox](https://technet.microsoft.com/ja-jp/library/aa997663\(v=exchg.150\))」を参照してください。

## どのアクセス許可を使用するか。

共有メールボックスと一緒に以下のアクセス許可が使用できます。

  - <strong>フル アクセス</strong>   \[フル アクセス\] アクセス許可を使用すれば、共有メールボックスを開いて、そのメールボックスの所有者として作業できます。共有メールボックスにアクセスした後、ユーザーは予定表アイテムを作成したり、電子メール メッセージの読み取り、表示、削除、変更を行ったり、タスクと予定表の連絡先を作成することができます。ただし、\[フル アクセス\] アクセス許可を持っているユーザーは、\[メールボックス所有者として送信する\] または \[代理人として送信する\] アクセス許可も持っている場合に限り、共有メールボックスから電子メールを送信できます。

  - <strong>メールボックス所有者として送信する</strong>   \[メールボックス所有者として送信する\] アクセス許可を使用すれば、メールの送信時に共有メールボックスを代理で処理できます。たとえば、Kweku が共有メールボックス Marketing Department にログインして電子メールを送信すると、Marketing Department が電子メールを送信したかのように見えます。

  - <strong>代理人として送信する</strong>   \[代理人として送信する\] アクセス許可を使用すれば、共有メールボックスの代わりに電子メールを送信できます。たとえば、John が共有メールボックス Reception Building 32 にログインして電子メールを送信すると、メールが「Reception Building 32 の代わりに John」によって送信されたように見えます。EAC では \[代理人として送信する\] アクセス許可を付与できないため、[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\)) コマンドレットを *GrantSendonBehalf* パラメーターと一緒に使用する必要があります。

## 詳細情報

このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。


