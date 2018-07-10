---
title: 'パブリック フォルダーのメールの有効化またはメールの無効化: Exchange Online Help'
TOCTitle: パブリック フォルダーのメールの有効化またはメールの無効化
ms:assetid: 3d69f76d-ff3c-46c1-b962-6a1baa425d8a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997560(v=EXCHG.150)
ms:contentKeyID: 49896213
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# パブリック フォルダーのメールの有効化またはメールの無効化

 

_**適用先:** Exchange Online, Exchange Server 2013_

パブリック フォルダーは、共有アクセスのために設計された、情報を収集、整理してワークグループや組織内の他のユーザーと共有するための容易かつ効果的な方法です。メールが有効なパブリック フォルダーでは、ユーザーがそのフォルダーに電子メール メッセージを送信すると投稿できます。パブリック フォルダーでメールが有効な場合、Exchange 管理センター (EAC) で、パブリック フォルダーに電子メール アドレスやメール クォータなどの追加の設定を行うことができます。シェルでは、パブリック フォルダーでメールを有効にする前に、**Set-PublicFolder** コマンドレットで、そのすべての設定を管理します。パブリック フォルダーでメールが有効になると、**Set-PublicFolder** コマンドレットと **Set-MailPublicFolder** コマンドレットで設定を管理できます。

インターネット上のユーザーがメールが有効なパブリック フォルダーにメールを送信できるようにするには、**Add-PublicFolderClientPermission** コマンドレットを使用して追加のアクセス許可を設定する必要があります。

パブリック フォルダーの管理に関するその他の管理タスクについては、「[パブリック フォルダーの手順](public-folder-procedures-exchange-2013-help.md)」を参照してください。

パブリック フォルダーに関するその他の管理タスクについては、「[Office 365 と Exchange Online のパブリック フォルダーの手順](https://technet.microsoft.com/ja-jp/library/jj966272\(v=exchg.150\))」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分

  - ユーザーが電子メール メッセージをメールが有効なパブリックフォルダーに送信できるようにするには、そのパブリック フォルダーで、匿名アカウントに対し、少なくとも *CreateItems* アクセス権を与える必要があります。その方法について詳しくは、「匿名ユーザーがメールが有効なパブリック フォルダーに電子メールを送信できるようにする」を参照してください。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[共有とコラボレーションのアクセス許可](sharing-and-collaboration-permissions-exchange-2013-help.md)」の「パブリック フォルダー」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EAC を使用してパブリック フォルダーのメールの有効と無効を切り替える

1.  **\[パブリック フォルダー\]** \> **\[パブリック フォルダー\]** に移動します。

2.  リスト ビューで、メールの有効や無効を切り替えるパブリック フォルダーを選択します。

3.  詳細ウィンドウの **\[メールの設定\]** の下で、**\[有効にする\]** または **\[無効にする\]** をクリックします。

4.  そのパブリック フォルダーの電子メールを有効にするか無効にするか、確認を求める警告ボックスが表示されます。**\[はい\]** をクリックして続行します。

外部のユーザーがこのパブリック フォルダーにメールを送信できるようにする場合は、「匿名ユーザーがメールが有効なパブリック フォルダーに電子メールを送信できるようにする」の手順に従ってください。

## シェルを使用してパブリック フォルダーのメールを有効にする

この例では、パブリック フォルダー Help Desk でメールを有効にします。

    Enable-MailPublicFolder -Identity "\Help Desk"

この例では、Marketing パブリック フォルダーの下のパブリック フォルダー Reports でメールを有効にしますが、アドレス一覧にこのフォルダーは表示しません。

    Enable-MailPublicFolder -Identity "\Marketing\Reports" -HiddenFromAddressListsEnabled $True

外部のユーザーがこのパブリック フォルダーにメールを送信できるようにする場合は、「匿名ユーザーがメールが有効なパブリック フォルダーに電子メールを送信できるようにする」の手順に従ってください。

構文およびパラメーターの詳細については、「[Enable-MailPublicFolder](https://technet.microsoft.com/ja-jp/library/aa998824\(v=exchg.150\))」を参照してください。

## シェルを使用してパブリック フォルダーのメールを無効にする

この例では、パブリック フォルダー Marketing\\Reports でメールを無効にします。

    Disable-MailPublicFolder -Identity "\Marketing\Reports"

構文およびパラメーターの詳細については、「[Disable-MailPublicFolder](https://technet.microsoft.com/ja-jp/library/bb123781\(v=exchg.150\))」を参照してください。

## 匿名ユーザーがメールが有効なパブリック フォルダーに電子メールを送信できるようにする

Outlook またはシェルを使用して、パブリック フォルダーの匿名アカウントにアクセス許可を設定できます。EAC を使用して匿名アカウントにアクセス許可を設定することはできません。

**Outlook を使用して匿名アカウントにアクセス許可を設定する**

1.  匿名ユーザーをメール送信先とする電子メールが有効なパブリック フォルダーの所有者アクセス許可が付与されたアカウントを使用して、Outlook を開きます。

2.  **\[パブリック フォルダー - \<ユーザー名\>\]** に移動します。

3.  変更するパブリック フォルダーに移動します。

4.  パブリック フォルダーを右クリックし、**\[プロパティ\]** をクリックして、**\[アクセス許可\]** タブを選択します。

5.  **\[匿名\]** アカウントを選択し、**\[書き込み\]** の下の **\[アイテムの作成\]** を選択して、**\[OK\]** をクリックします。

**シェルを使用して匿名アカウントのアクセス許可を設定する**

この例では、「お客様からのフィードバック」というメールが有効なパブリック フォルダーに対する匿名アカウントの `CreateItems` アクセス許可を設定します。

    Add-PublicFolderClientPermission "\Customer Feedback" -AccessRights CreateItems -User Anonymous

構文およびパラメーターの詳細については、「[Add-PublicFolderClientPermission](https://technet.microsoft.com/ja-jp/library/bb124743\(v=exchg.150\))」を参照してください。

