---
title: 'メールボックス用電子メール アドレスの追加または削除: Exchange Online Help'
TOCTitle: メールボックス用電子メール アドレスの追加または削除
ms:assetid: 93e2d9a4-7558-4509-8641-8381a7eb674f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb123794(v=EXCHG.150)
ms:contentKeyID: 50555830
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックス用電子メール アドレスの追加または削除

 

_**適用先:**Exchange Online, Exchange Server 2013_

同じメールボックスに複数の電子メール アドレスを構成することができます。追加アドレスは、*プロキシ アドレス*と呼ばれます。プロキシ アドレスを使用すると、ユーザーは異なる電子メール アドレスに送信された電子メールを受信できます。ユーザーのプロキシ アドレスに送信された電子メール メッセージは、プライマリ電子メール アドレス (*プライマリ SMTP アドレス*または*既定の返信アドレス*とも呼ばれる) に配信されます。


> [!IMPORTANT]
> Office 365 for Business を使用している場合は、<A href="https://go.microsoft.com/fwlink/p/?linkid=8347775">Office 365 管理センターでユーザー メールボックスの電子メール アドレスの追加または削除を行う必要があります。Office 365 のユーザーに電子メール エイリアスを追加する</A>



受信者の管理に関連する追加の管理タスクについては、「[受信者](recipients-exchange-2013-help.md)」の「受信者に関するドキュメント」の表を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「受信者プロビジョニングのアクセス許可」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

このトピックの手順では、ユーザー メールボックスの電子メール アドレスを追加または削除する方法を示します。同様の手順を使用して、他の受信者の種類でも電子メール アドレスを追加または削除できます。

## 必要な作業

## ユーザー メールボックスに電子メール アドレスを追加する

## EAC を使用して、電子メール アドレスを追加する

1.  EAC で、**\[受信者\]** \> **\[メールボックス\]**に移動します。

2.  ユーザー メールボックスの一覧で、電子メールを追加するメールボックスをクリックし、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  メールボックスのプロパティ ページで、**\[電子メール アドレス\]** をクリックします。
    

    > [!NOTE]
    > <STRONG>[電子メール アドレス]</STRONG> ページでは、プライマリ SMTP アドレスがアドレス一覧に太字テキストで表示され、大文字の <STRONG>SMTP</STRONG> の値が <STRONG>[種類]</STRONG> 列に表示されます。



4.  このメールボックスに SMTP 電子メール アドレスを追加するには、**\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックし、**\[SMTP\]** をクリックします。
    

    > [!NOTE]
    > [SMTP] は既定の電子メール アドレスの種類です。メールボックスには、Exchange ユニファイド メッセージング (EUM) アドレスまたはカスタム アドレスも追加できます。詳細については、「<A href="manage-user-mailboxes-exchange-2013-help.md">ユーザー メールボックスの管理</A>」のトピックの「Change user mailbox properties (メールボックスのプロパティを変更する)」を参照してください。



5.  **\[電子メール アドレス\]** ボックスに新しい SMTP アドレスを入力し、**\[OK\]** をクリックします。
    
    選択したメールボックスの電子メール アドレスの一覧に、新しいアドレスが表示されます。

6.  **\[保存\]** をクリックして変更を保存します。

## シェルを使用して、電子メール アドレスを追加する

このメールボックスに関連付けられた電子メール アドレスは、メールボックスの *EmailAddresses* プロパティに含まれています。これには複数の電子メール アドレスを含めることができるため、*EmailAddresses* プロパティは*複数値*プロパティと呼ばれます。次の例では、複数値プロパティを変更するさまざまな方法を示します。

この例では、Dan Jump のメールボックスに SMTP アドレスを追加する方法を示します。

    Set-Mailbox "Dan Jump" -EmailAddresses @{add="dan.jump@northamerica.contoso.com"}

この例では、複数の SMTP アドレスをメールボックスに追加する方法を示します。

    Set-Mailbox "Dan Jump" -EmailAddresses @{add="dan.jump@northamerica.contoso.com","danj@tailspintoys.com"}

複数値プロパティの値を追加および削除する方法の詳細については、「[複数値プロパティの変更](modifying-multivalued-properties-exchange-2013-help.md)」を参照してください。

この例では、メールボックスに関連付けられたすべてのアドレスを指定して、メールボックスに電子メール アドレスを追加する方法を示します。この例では、danj@tailspintoys.com が追加する新しい電子メール アドレスです。他の 2 つの電子メール アドレスは既存のアドレスです。大文字/小文字が区別される修飾子 `SMTP` は、プライマリ SMTP アドレスです。このコマンド構文を使用する場合は、メールボックスのすべての電子メール アドレスを含める必要があります。そうしないと、コマンドで指定したアドレスにより既存のアドレスが上書きされます。

    Set-Mailbox "Dan Jump" -EmailAddresses SMTP:dan.jump@contoso.com,dan.jump@northamerica.contoso.com,danj@tailspintoys.com

構文およびパラメーターの詳細については、「[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

電子メール アドレスがメールボックスに正常に追加されたことを確認するには、次のいずれかを実行します。

  - EAC で、**\[受信者\]** \> **\[メールボックス\]** に移動し、メールボックスをクリックし、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

  - メールボックスのプロパティ ページで、**\[電子メール アドレス\]** をクリックします。

  - メールボックスの電子メール アドレスの一覧で、新しい電子メール アドレスが含まれていることを確認します。

または

  - シェルで、次のコマンドを実行します。
    
        Get-Mailbox <identity> | fl EmailAddresses

  - 新しいメール アドレスが結果に含まれていることを確認します。

## ユーザー メールボックスからメール アドレスを削除する

## EAC を使用して、電子メール アドレスを削除する

1.  EAC で、**\[受信者\]** \> **\[メールボックス\]**に移動します。

2.  ユーザー メールボックスの一覧で、電子メールを削除するメールボックスをクリックし、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  メールボックスのプロパティ ページで、**\[電子メール アドレス\]** をクリックします。

4.  電子メール アドレスの一覧で削除するアドレスで選択し、**\[削除\]**![\[削除\] アイコン](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[削除] アイコン") をクリックします。

5.  **\[保存\]** をクリックして変更を保存します。

## シェルを使用して電子メール アドレスを削除する

この例では、Janet Schorr のメールボックスから電子メール アドレスを削除する方法を示します。

    Set-Mailbox "Janet Schorr" -EmailAddresses @{remove="janets@corp.contoso.com"}

この例では、複数のアドレスをメールボックスから削除する方法を示します。

    Set-Mailbox "Janet Schorr" -EmailAddresses @{remove="janet.schorr@corp.contoso.com","janets@tailspintoys.com"}

複数値プロパティの値を追加および削除する方法の詳細については、「[複数値プロパティの変更](modifying-multivalued-properties-exchange-2013-help.md)」を参照してください。

メールボックスの電子メール アドレスを設定するコマンドから電子メール アドレスを省略することにより、電子メール アドレスを削除することもできます。たとえば、Janet Schorr のメールボックスには 3 つの電子メール アドレス (janets@contoso.com (プライマリ SMTP アドレス)、janets@corp.contoso.com、および janets@tailspintoys.com) があるとします。アドレス janets@corp.contoso.com を削除するには、次のコマンドを実行します。

    Set-Mailbox "Janet Schorr" -EmailAddresses SMTP:janets@contoso.com,janets@tailspintoys.com

janets@corp.contoso.com は前述のコマンドで省略されているため、これはメールボックスから削除されます。

構文およびパラメーターの詳細については、「[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

電子メール アドレスがメールボックスから正常に削除されたことを確認するには、次のいずれかを実行します。

  - EAC で、**\[受信者\]** \> **\[メールボックス\]** に移動し、メールボックスをクリックし、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

  - メールボックスのプロパティ ページで、**\[電子メール アドレス\]** をクリックします。

  - メールボックスの電子メール アドレスの一覧で、その電子メール アドレスが含まれていないことを確認します。

または

  - シェルで、次のコマンドを実行します。
    
        Get-Mailbox <identity> | fl EmailAddresses

  - 電子メール アドレスが結果に含まれていないことを確認します。

## シェルを使用して、複数のメールボックスに電子メール アドレスを追加する

シェルおよびコンマ区切り値 (CSV) ファイルを使用して、新しい電子メール アドレスを複数のメールボックスに同時に追加できます。

この例では、次の形式の C:\\Users\\Administrator\\Desktop\\AddEmailAddress.csv からデータをインポートします。

    Mailbox,NewEmailAddress
    Dan Jump,danj@northamerica.contoso.com
    David Pelton,davidp@northamerica.contoso.com
    Kim Akers,kima@northamerica.contoso.com
    Janet Schorr,janets@northamerica.contoso.com
    Jeffrey Zeng,jeffreyz@northamerica.contoso.com
    Spencer Low,spencerl@northamerica.contoso.com
    Toni Poe,tonip@northamerica.contoso.com
    ...

CSV ファイルのデータを使用して CSV ファイルに指定された各メールボックスに電子メール アドレスを追加するには、次のコマンドを実行します。

    Import-CSV "C:\Users\Administrator\Desktop\AddEmailAddress.csv" | ForEach {Set-Mailbox $_.Mailbox -EmailAddresses @{add=$_.NewEmailAddress}}


> [!NOTE]
> この CSV ファイルの 1 行目に記述されている列名 (<CODE>Mailbox,NewEmailAddress</CODE>) は任意のものを使用できます。列名にどのような名前を使用したとしても、必ず同じ列名をシェル コマンドで使用してください。



## 正常な動作を確認する方法

電子メール アドレスが複数のメールボックスに正常に追加されたことを確認するには、次のいずれかを実行します。

  - EAC で、**\[受信者\]** \> **\[メールボックス\]** に移動し、アドレスを追加したメールボックスをクリックし、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

  - メールボックスのプロパティ ページで、**\[電子メール アドレス\]** をクリックします。

  - メールボックスの電子メール アドレスの一覧で、新しい電子メール アドレスが含まれていることを確認します。

または

  - 新しい電子メール アドレスの追加に使用したものと同じ CSV ファイルを使用して、シェルで次のコマンドを実行します。
    
        Import-CSV "C:\Users\Administrator\Desktop\AddEmailAddress.csv" | ForEach {Get-Mailbox $_.Mailbox | fl Name,EmailAddresses}

  - 新しいメール アドレスが各メールボックスの結果に含まれていることを確認します。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.


