---
title: 'メールボックスのストレージ クォータを構成する: Exchange 2013 Help'
TOCTitle: メールボックスのストレージ クォータを構成する
ms:assetid: 5f5fe292-c80e-4a0b-b3e6-e193ea5171d0
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998353(v=EXCHG.150)
ms:contentKeyID: 50555789
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックスのストレージ クォータを構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-07-07_

**概要**:EAC またはシェルを使用して、特定のメールボックスのストレージ クォータを設定します。

ストレージ クォータにより、メールボックスのサイズを制御し、メールボックス データベースの増大を管理できます。メールボックスが指定されたストレージ クォータに達するか制限を超えた場合、Exchange はメールボックスの所有者にそのことを示す通知を送信します。


> [!NOTE]
> <CODE>Get-MailboxStatistics</CODE> コマンドレットを実行すると、指定されたメールボックスの <CODE>TotalItemSize</CODE> プロパティで定義されているサイズに対し、ストレージ クォータが適用されます。詳細については、「<A href="https://technet.microsoft.com/ja-jp/library/bb124612(v=exchg.150)">Get-MailboxStatistics</A>」を参照してください。



ストレージ クォータは通常、データベース単位で構成されます。つまり、メールボックス データベースに構成された制限は、そのデータベース内のすべてのメールボックスに適用されます。データベースごとのメールボックスの設定の詳細については、「[Exchange 2013 のメールボックス データベースの管理](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)」を参照してください。

このトピックでは、メールボックス データベースのストレージ設定を使用する代わりに、特定のメールボックスのストレージ設定をカスタマイズする方法を示します。ユーザー メールボックスに関するその他の管理タスクについては、「[ユーザー メールボックスの管理](https://docs.microsoft.com/ja-jp/exchange/recipients-in-exchange-online/manage-user-mailboxes/manage-user-mailboxes)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間:2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「受信者プロビジョニングのアクセス許可」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して、メールボックスの格納域の制限を構成する

1.  EAC で、<strong>受信者</strong> \> <strong>\[メールボックス\]</strong>に移動します。

2.  ユーザー メールボックス リストで、格納域の制限を変更するメールボックスをクリックし、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  メールボックスの \[プロパティ\] ページで、<strong>メールボックスの使用状況</strong> をクリックし、次に <strong>その他のオプション</strong> をクリックします。

4.  <strong>このメールボックスの設定をカスタマイズする</strong> をクリックし、次のボックスを構成します。ストレージ クォータ設定の値の範囲は、0 から 2047 ギガバイト (GB) です。
    
      - <strong>警告を表示する使用量 (GB)</strong>   このボックスには、ユーザーに警告が発行される前のストレージの上限が表示されます。メールボックスのサイズが指定した値に達する、またはその値を超えた場合、Exchange はメールボックス ユーザーに警告メッセージを送信します。
        

        > [!IMPORTANT]
        > <STRONG>[警告を表示する]</STRONG> クォータに関連付けられたメッセージは、この設定の値が <STRONG>[送信禁止]</STRONG> クォータに指定された値の 50% を超えない限り、ユーザーには送信されません。たとえば、<STRONG>[送信禁止]</STRONG> クォータを 8 MB に設定した場合、<STRONG>[警告を表示する]</STRONG> クォータは少なくとも 4 MB に設定する必要があります。そのように設定しない場合、<STRONG>[警告を表示する]</STRONG> クォータ メッセージは送信されません。

    
      - <strong>送信を禁止する使用量 (GB)</strong>   このボックスには、メールボックスの*送信禁止*制限値が表示されます。メールボックスのサイズが指定した値に達する、またはその値を超えた場合、Exchange はユーザーによる新しいメッセージの送信を禁止し、そのことを示すエラー メッセージが表示されます。
    
      - <strong>送受信を禁止する使用量 (GB)</strong>   このボックスには、メールボックスの*送受信禁止*制限値が表示されます。メールボックスのサイズが指定した値に達するか、またはその値を超えた場合、Exchange はメールボックス ユーザーによる新しいメッセージの送信を禁止し、メールボックスには新しいメッセージが配信されなくなります。このメールボックスに送信されたメッセージは、エラーの内容を示すメッセージと共に送信者に返されます。

5.  <strong>保存</strong> をクリックして変更を保存します。

## シェルを使用して、メールボックスの格納域の制限を構成する

この例は、Joe Healy のメールボックスの警告の表示、送信禁止、および送受信禁止の各制限をそれぞれ 24.5 GB、24.75 GB、および 25 GB に設定します。


> [!NOTE]
> メールボックス データベースの既定値の代わりにメールボックスのカスタム設定が使用されるようにするには、<EM>UseDatabaseQuotaDefaults</EM> パラメーターを <CODE>$false</CODE> に設定する必要があります。



```powershell
Set-Mailbox -Identity "Joe Healy" -IssueWarningQuota 24.5gb -ProhibitSendQuota 24.75gb -ProhibitSendReceiveQuota 25gb -UseDatabaseQuotaDefaults $false
```

この例は、Ayla Kol のメールボックスの警告の表示、送信禁止、および送受信禁止の各制限をそれぞれ 900 MB、950 MB、および 1 GB に設定し、カスタム設定を使用するようにメールボックスを構成します。

```powershell
Set-Mailbox -Identity "Ayla Kol" -IssueWarningQuota 900mb -ProhibitSendQuota 950mb -ProhibitSendReceiveQuota 1gb -UseDatabaseQuotaDefaults $false
```

構文およびパラメーターの詳細については、「[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

メールボックスの格納域の制限が正常に設定されたことを確認するには、次のいずれかを実行します。

1.  EAC で、<strong>受信者</strong> \> <strong>\[メールボックス\]</strong>に移動します。

2.  ユーザー メールボックス リストで、格納域の制限を確認するメールボックスをクリックし、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  メールボックスの \[プロパティ\] ページで、<strong>メールボックスの使用状況</strong> をクリックし、次に <strong>その他のオプション</strong> をクリックします。

4.  <strong>このメールボックスの設定をカスタマイズする</strong> が選択されていることを確認します。

5.  格納域の制限の設定を確認します。

または

シェルで、次のコマンドを実行します。

```powershell
Get-Mailbox <identity> | fl IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults
```

