﻿---
title: 'メールボックスへの電子メールの転送を構成する: Exchange Online Help'
TOCTitle: メールボックスへの電子メールの転送を構成する
ms:assetid: c7a7afaf-577e-49d6-8cee-bb4c4a5d570b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd351134(v=EXCHG.150)
ms:contentKeyID: 50555870
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックスへの電子メールの転送を構成する

 

_**適用先:** Exchange Online, Exchange Server 2013_

電子メール転送では、そのメールボックスに送信された電子メール メッセージを組織の内部または外部の別のユーザーのメールボックスに転送するようにメールボックスをセットアップします。


> [!IMPORTANT]
> Office 365 for Business を使用している場合は、<A href="https://go.microsoft.com/fwlink/p/?linkid=834774">Office 365 管理センターで電子メール転送を構成する必要があります。Office 365 で電子メールの転送を構成する</A>



組織でオンプレミス Exchange またはハイブリッド Exchange 環境を使用する場合は、オンプレミスの Exchange 管理センター (EAC) を使用して、共有メールボックスを作成および管理する必要があります。

## Exchange 管理センター を使用してメールの転送を構成する

Exchange 管理センター (EAC) を使用して、1 人の内部受信者、1 人の外部受信者 (メール連絡先を使用)、複数の受信者 (配布グループを使用) へのメールの転送を設定できます。

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」トピックの「受信者準備のアクセス許可」エントリ。

1.  EAC で、<strong>受信者</strong> \> <strong>メールボックス</strong>に移動します。

2.  ユーザー メールボックスの一覧で、メールの転送を構成するメールボックスをクリックまたはタップし、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックまたはタップします。

3.  メールボックスのプロパティ ページで、<strong>メールボックスの機能</strong> をクリックします。

4.  <strong>メール フロー</strong> で <strong>詳細の表示</strong> を選択し、メール メッセージを転送するための設定を表示または変更します。
    
    このページでは、ユーザーがメッセージを送信できる受信者の最大数を設定できます。社内 Exchange 組織の場合、受信者の制限はありません。Exchange Online 組織の場合、受信者は 500 人までです。

5.  <strong>転送を有効にする</strong> チェック ボックスをオンにしてから、<strong>参照</strong> をクリックまたはタップします。

6.  <strong>受信者の選択</strong> ページで、すべての電子メールを転送するユーザーを選択します。送信された電子メールのコピーを受信者と転送先の電子メール アドレスの両方が受け取る場合は、<strong>メッセージを転送先アドレスとメールボックスの両方に配信する</strong> チェック ボックスをオンにします。<strong>OK</strong> をクリックまたはタップしてから、<strong>保存</strong> をクリックまたはタップします。

また、電子メールを組織外部の電子メール アドレスに転送したり、複数の受信者に転送したりすることも可能です。

  - **外部アドレス**。メール連絡先を作成してから、上記の手順で、<strong>受信者の選択</strong> ページでそのメール連絡先を選択します。メール連絡先を作成する方法については、「[メール連絡先の管理](manage-mail-contacts-exchange-2013-help.md)」を参照してください。

  - **複数の受信者**。配布グループを作成し、それに受信者を追加し、上記の手順で、<strong>受信者の選択</strong> ページでそのメール連絡先を選択します。メール連絡先を作成する方法については、「[配布グループの作成と管理](create-and-manage-distribution-groups-exchange-2013-help.md)」を参照してください。

## 正常な動作を確認する方法

メールの転送が正常に設定されたことを確認するには、次の手順を実行します。

1.  EAC で、<strong>受信者</strong> \> <strong>メールボックス</strong> に移動します。

2.  ユーザー メールボックスの一覧で、電子メール転送を構成したメールボックスをクリックまたはタップしてから、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  メールボックスのプロパティ ページで、<strong>メールボックスの機能</strong> をクリックまたはタップします。

4.  <strong>メール フロー</strong> で <strong>詳細の表示</strong> をクリックまたはタップして、メール転送設定を表示します。

## 追加情報

このトピックは、管理者を対象としています。自分の電子メールを別の受信者に転送したい場合は、次のトピックを参照してください。

  - [電子メールを別の電子メール アカウントに転送する](https://go.microsoft.com/fwlink/p/?linkid=510866)

  - [ルールを使用してメール メッセージを管理する](https://go.microsoft.com/fwlink/p/?linkid=510869)

このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

