---
title: '役割グループの変更または管理者監査ログを検索する: Exchange Online Help'
TOCTitle: 役割グループの変更または管理者監査ログを検索する
ms:assetid: c7188d53-e672-492b-b57d-cd711379ddb3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff459262(v=EXCHG.150)
ms:contentKeyID: 50553906
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 役割グループの変更または管理者監査ログを検索する

 

_**適用先:** Exchange Online, Exchange Server 2013_

管理者監査ログを検索して、組織、サーバー、および受信者構成の変更者を検出できます。これは、予期しない動作の原因を追跡したり、悪意のある管理者を識別したり、または準拠の要件に適合していることを確認する際に便利です。管理者監査ログの詳細については、「[管理者監査ログ](administrator-audit-logging-exchange-2013-help.md)」を参照してください。

メールボックス監査ログを検索する場合は、「[メールボックスの監査ログの出力](mailbox-audit-logging-exchange-2013-help.md)」を参照してください。


> [!TIP]
> Exchange Online では、EAC を使用して管理者監査ログのエントリを表示できます。詳しくは、「<A href="view-the-administrator-audit-log-exchange-2013-help.md">管理者監査ログを表示する</A>」をご覧ください。



## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分未満

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[Exchange およびシェル インフラストラクチャのアクセス許可](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)」の「表示専用の管理者監査ログ」。

  - 既定では、管理者監査ログ出力は有効になっています。管理者監査ログ出力が有効になっていることを確認するために、次のコマンドを実行します。
    
        Get-AdminAuditLogConfig | FL AdminAuditLogEnabled
    
    値が `True` の場合、管理者監査ログ出力は有効になっています。値が `False` の場合は無効になっています。社内 Exchange 組織の管理者監査ログ出力を有効にする必要がある場合は、次のコマンドを実行します。
    
        Set-AdminAuditLogConfig -AdminAuditLogEnabled $true
    

    > [!NOTE]
    > <STRONG>Set-AdminAuditLogConfig</STRONG> コマンドレットは、Exchange Online では使用できません。

    
    詳しくは、「[管理者監査ログの管理](manage-administrator-audit-logging-exchange-2013-help.md)」をご覧ください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EAC を使用して管理役割グループ変更レポートを実行するには

組織の役割グループでの、管理役割グループのメンバーシップに関する変更を確認する場合は、Exchange 管理センター (EAC) の管理者の役割グループ レポートを使用できます。管理者の役割グループ レポートを使用すると、指定した日付の範囲内に変更された役割グループの一覧を表示できます。また、変更を表示する特定の役割グループを選択することもできます。

1.  EAC で、**\[コンプライアンス管理\]** \> **\[監査\]** を選択し、**\[管理者の役割グループ レポートの実行\]** をクリックします。

2.  **\[開始日\]** および **\[終了日\]** フィールドを使用して、日付範囲を選択します。

3.  **\[役割グループの選択\]** をクリックし、変更を表示する役割グループを選択するか、またはこのフィールドを空白にして、すべての役割グループにおける変更を検索します。

4.  **\[検索\]** をクリックします。

指定した条件で変更が見つかった場合は、結果ウィンドウに変更の一覧が表示されます。役割グループをクリックすると、その役割グループへの変更が詳細ウィンドウに表示されます。

## EAP を使用して管理者監査ログをエクスポートする

組織の変更が含まれる XML ファイルを作成する場合は、EAC の管理者監査ログのエクスポート レポートを使用できます。管理者監査ログのエクスポート レポートを使用して、指定したユーザーによる変更が含まれる監査ログ エントリを検索するための日付範囲を指定できます。次に、XML ファイルが電子メールの添付ファイルとして受信者に送信されます。XML ファイルの最大サイズは 10 MB です。


> [!NOTE]
> Outlook Web App では、既定では XML の添付ファイルを開くことができません。Outlook Web App を使用して XML 添付ファイルを表示できるように Exchange を構成するか、Microsoft Outlook など別のメール クライアントを使用して添付ファイルを表示することができます。XML 添付ファイルを表示できるように Outlook Web App を構成する方法については、「<A href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">Outlook Web App 仮想ディレクトリの表示や構成</A>」をご覧ください。



1.  EAC で、**\[コンプライアンス管理\]** \> **\[監査\]** を選択し、**\[管理者監査ログのエクスポート\]** をクリックします。

2.  **\[開始日\]** および **\[終了日\]** フィールドを使用して、日付範囲を選択します。

3.  EAC で、**\[監査レポートの送信先\]** フィールドで **\[ユーザーの選択\]** を選択し、レポートを送信する受信者を選択します。

4.  **\[エクスポート\]** をクリックします。

指定した条件に合うログ エントリが見つかった場合は、XML ファイルが作成され、指定した受信者に電子メールの添付ファイルとして送信されます。

## シェルを使用して監査ログ エントリを検索する

シェルを使用して、指定した条件に合う監査ログ エントリを検索することができます。検索条件の一覧については、「[管理者監査ログ](administrator-audit-logging-exchange-2013-help.md)」を参照してください。この手順では、**Search-AdminAuditLog** コマンドレットを使用してシェルに検索結果を表示します。このコマンドレットは、**New-AdminAuditLogSearch** コマンドレットまたは EAC 監査レポートのレポートで定義されている制限値を超える結果セットを返す必要がある場合に使用できます。

監査ログの検索結果を電子メールの添付ファイルで受信者に送信する場合は、このトピックの後半の「シェルを使用して監査ログ エントリを検索し、結果を受信者に送信する」を参照してください。

指定した条件で監査ログを検索するには、次の構文を使用します。

    Search-AdminAuditLog - Cmdlets <cmdlet 1, cmdlet 2, ...> -Parameters <parameter 1, parameter 2, ...> -StartDate <start date> -EndDate <end date> -UserIds <user IDs> -ObjectIds <object IDs> -IsSuccess <$True | $False >


> [!NOTE]
> <STRONG>Search-AdminAuditLog</STRONG> コマンドレットを実行すると、既定で最大 1,000 個のログ エントリが返されます。返されるログ エントリ数を指定 (最大 250,000 個) するには、<EM>ResultSize</EM> パラメーターを使用します。また、すべてのエントリを返すには、値として <CODE>Unlimited</CODE> を使用します。



この例では、次の条件を使用してすべての監査ログ エントリで検索を実行します。

  - **開始日**   08/04/2012

  - **終了日**   10/03/2012

  - **ユーザー ID**   davids、chrisd、kima

  - **コマンドレット** **Set-Mailbox**

  - **パラメーター** *ProhibitSendQuota*、*ProhibitSendReceiveQuota*、*IssueWarningQuota*、*MaxSendSize*、*MaxReceiveSize*

<!-- end list -->

    Search-AdminAuditLog -Cmdlets Set-Mailbox -Parameters ProhibitSendQuota, ProhibitSendReceiveQuota, IssueWarningQuota, MaxSendSize, MaxReceiveSize -StartDate 08/04/2012 -EndDate 10/03/2012 -UserIds davids, chrisd, kima

この例では、特定のメールボックスの変更を検索します。これは、トラブルシューティングを実行している場合や、調査のために情報を入手する必要がある場合に便利です。次の条件を使用します。

  - **開始日**   05/01/2012

  - **終了日**   10/03/2012

  - **オブジェクト ID**   contoso.com/Users/DavidS

<!-- end list -->

    Search-AdminAuditLog -StartDate 05/01/2012 -EndDate 10/03/2012 -ObjectID contoso.com/Users/DavidS

検索の結果返されるログ エントリが多い場合は、後の「シェルを使用して監査ログ エントリを検索し、結果を受信者に送信する」で説明する手順を使用することをお勧めします。その手順を実行すると、指定した受信者に XML ファイルが電子メールの添付ファイルとして送信されるため、目的のデータをより簡単に抽出することができます。

構文およびパラメーターの詳細については、「[Search-AdminAuditLog](https://technet.microsoft.com/ja-jp/library/ff459250\(v=exchg.150\))」を参照してください。

## 監査ログ エントリの詳細を表示する

**Search-AdminAuditLog** コマンドレットを実行すると、「[管理者監査ログ](administrator-audit-logging-exchange-2013-help.md)」の「監査ログの内容」で説明されているフィールドが返されます。コマンドレットによって返されるフィールドのうち、**CmdletParameters** と **ModifiedProperties** の 2 つのフィールドには、既定では表示できない追加情報が含まれます。

**CmdletParameters** フィールドと **ModifiedProperties** フィールドの内容を表示するには、次の手順を実行します。または、後の「シェルを使用して監査ログ エントリを検索し、結果を受信者に送信する」にある手順を使用して XML ファイルを作成できます。

この手順では、次の概念を使用します。

  - [配列](https://technet.microsoft.com/ja-jp/library/aa998267\(v=exchg.150\))

  - [ユーザー定義変数](https://technet.microsoft.com/ja-jp/library/bb123690\(v=exchg.150\))

<!-- end list -->

1.  検索条件を決定して **Search-AdminAuditLog** コマンドレットを実行し、次のコマンドを使用してその結果を変数に格納します。
    
        $Results = Search-AdminAuditLog <search criteria>

2.  各監査ログ エントリは、変数 `$Results` に配列要素として格納されます。配列要素のインデックスを指定することで、配列要素を選択できます。配列要素のインデックスは、最初の配列要素のゼロ (0) から始まります。たとえば、5 番目の配列要素 (インデックスは 4) を取得するには、次のコマンドを使用します。
    
        $Results[4]

3.  上記のコマンドを実行すると、配列要素 4 に格納されているログ エントリが返されます。このログ エントリの **CmdletParameters** フィールドと **ModifiedProperties** フィールドの内容を表示するには、次のコマンドを使用します。
    
        $Results[4].CmdletParameters
        $Results[4].ModifiedProperties

4.  **CmdletParameters** フィールドや **ModifiedParameters** フィールドの内容を別のログ エントリに表示するには、配列要素のインデックスを変更します。

## シェルを使用して監査ログ エントリを検索し、結果を受信者に送信する

シェルを使用して、指定した条件に合う監査ログ エントリを検索し、その結果を XML 添付ファイルとして指定した受信者に送信できます。結果は 15 分以内に受信者に送信されます。検索条件の一覧については、「[管理者監査ログ](administrator-audit-logging-exchange-2013-help.md)」を参照してください。


> [!NOTE]
> Outlook Web App では、既定では XML の添付ファイルを開くことができません。Outlook Web App を使用して XML 添付ファイルを表示できるように Exchange を構成するか、Microsoft Outlook など別のメール クライアントを使用して添付ファイルを表示することができます。XML 添付ファイルを表示できるように Outlook Web App を構成する方法については、「<A href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">Outlook Web App 仮想ディレクトリの表示や構成</A>」をご覧ください。



指定した条件で監査ログを検索するには、次の構文を使用します。

    New-AdminAuditLogSearch -Cmdlets <cmdlet 1, cmdlet 2, ...> -Parameters <parameter 1, parameter 2, ...> -StartDate <start date> -EndDate <end date> -UserIds <user IDs> -ObjectIds <object IDs> -IsSuccess <$True | $False > -StatusMailRecipients <recipient 1, recipient 2, ...> -Name <string to include in subject>

この例では、次の条件を使用してすべての監査ログ エントリで検索を実行します。

  - **開始日**   08/04/2012

  - **終了日**   10/03/2012

  - **ユーザー ID**   davids、chrisd、kima

  - **コマンドレットSet-Mailbox**

  - **パラメーター***ProhibitSendQuota*、*ProhibitSendReceiveQuota*、*IssueWarningQuota*、*MaxSendSize*、*MaxReceiveSize*

コマンドを実行すると、その結果が SMTP アドレス davids@contoso.com に送信されます。この際、メッセージの件名の行に "Mailbox limit changes/メールボックス制限の変更" という文字列が含まれます。

    New-AdminAuditLogSearch -Cmdlets Set-Mailbox -Parameters ProhibitSendQuota, ProhibitSendReceiveQuota, IssueWarningQuota, MaxSendSize, MaxReceiveSize -StartDate 08/04/2012 -EndDate 10/03/2012 -UserIds davids, chrisd, kima -StatusMailRecipients davids@contoso.com -Name "Mailbox limit changes"


> [!NOTE]
> <STRONG>New-AdminAuditLogSearch</STRONG> コマンドレットで生成されるレポートの最大サイズは 10 MB です。検索を実行した結果、10 MB より大きいレポートが返される場合は、指定する検索条件を変更してください。たとえば、日付範囲を短縮して複数のレポートを実行します。この際、各レポートに元の日付範囲の一部が含まれるようにします。



XML ファイルの形式の詳細については、「[管理者監査ログの構造](administrator-audit-log-structure-exchange-2013-help.md)」を参照してください。

構文およびパラメーターの詳細については、「[New-AdminAuditLogSearch](https://technet.microsoft.com/ja-jp/library/ff459243\(v=exchg.150\))」を参照してください。

