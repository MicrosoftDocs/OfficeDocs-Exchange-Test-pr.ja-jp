---
title: 'オフライン アドレス帳のダウンロードのために受信者を準備する: Exchange Online Help'
TOCTitle: オフライン アドレス帳のダウンロードのために受信者を準備する
ms:assetid: 141751ac-16d3-4e3c-b70c-004aeedcb5a0
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa996345(v=EXCHG.150)
ms:contentKeyID: 49895261
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# オフライン アドレス帳のダウンロードのために受信者を準備する

 

_**適用先:**Exchange Online, Exchange Server 2013_

組織内で複数のオフライン アドレス帳 (OAB) を使用している場合、いくつかの方法で、どの受信者がどの OAB をダウンロードするのかを指定します。

  - **メールボックス データベース単位**   EAC またはシェルを使用して、Office Outlook 2007、Outlook 2010、および Outlook 2013 クライアントの既定 OAB にメールボックス データベースをリンクすることによって、OAB ダウンロードの受信者をプロビジョニングすることができます。

  - **受信者単位**   シェルで **Set-Mailbox** コマンドレットを使用して、受信者のメールボックスに OAB を直接リンクすることで、どの OAB をダウンロードするのかを指定できます。

  - **複数受信者単位**   シェルでパイプライン コマンドを使用して、一般的な属性に基づいて、複数の受信者がダウンロードする OAB を指定できます。

  - **アドレス帳ポリシー単位**   メールボックス ユーザーのアカウントにアドレス帳ポリシー (ABP) を割り当てて、OAB が受信者のメールボックスにダウンロードされるよう指定できます。OAB がすでに割り当てられているユーザー アカウントに ABP を割り当てると、そのメールボックスに明示的に割り当てられた OAB が優先されます。詳細については、「[メール ユーザーへのアドレス帳ポリシーの割り当て](assign-an-address-book-policy-to-mail-users-exchange-2013-help.md)」を参照してください。

OAB に関連するその他の管理タスクについては、「[オフライン アドレス帳の手順](offline-address-book-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - Exchange 管理センター (EAC) を使用してこれらの手順を実行することはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## パブリック フォルダー データベース、または既定 OAB に受信者のメールボックス データベースをリンクすることで、シェルを使用して OAB ダウンロードの受信者をプロビジョニングする

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「メールボックス データベース」。

この例では、既定のメールボックス データベース向けに、My OAB の Web ベース配信を設定します。

    Set-MailboxDatabase -Identity "Mailbox Database" -OfflineAddressBook "My OAB"

構文およびパラメーターの詳細については、「[Set-MailboxDatabase](https://technet.microsoft.com/ja-jp/library/bb123971\(v=exchg.150\))」を参照してください。

## シェルを使用して、受信者のメールボックスに OAB を直接リンクすることで、ダウンロードされる OAB を指定する

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「受信者プロビジョニングのアクセス許可」。

受信者のメールボックスに OAB を直接リンクすることでダウンロードされる OAB を指定するには、以下の構文を使用します。

    Set-Mailbox -Identity <MailboxIDParameter> -OfflineAddressBook <OfflineAddressBookIdParameter>


> [!NOTE]
> <EM>Identity</EM> パラメーターはメールボックスを識別し、次の値を受け取ることができます。GUID、ADObjectID、識別名 (DN)、<EM>domain\account</EM>、ユーザー プリンシパル名 (UPN)、LegacyExchangeDN、SmtpAddress、およびエイリアス。



この例では、ユーザー Kim が "My OAB" という OAB をダウンロードすることを指定します。

    Set-Mailbox -Identity Kim -OfflineAddressBook "My OAB"

構文およびパラメーターの詳細については、「[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))」を参照してください。

## シェルを使用して、複数の受信者がダウンロードする OAB を指定する

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「受信者プロビジョニングのアクセス許可」。

この例では、米国の Contoso のすべてのユーザー メールボックスが "Contoso United States" という OAB をダウンロードすることを指定しています。

    Get-User -ResultSize Unlimited -Filter { Company -eq "Contoso" -and RecipientType -eq "UserMailbox" } | Where { $_.CountryOrRegion -eq "United States"} | Set-Mailbox -OfflineAddressBook "Contoso United States"

構文およびパラメーターの詳細については、「[Get-User](https://technet.microsoft.com/ja-jp/library/aa996896\(v=exchg.150\))」と「[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))」を参照してください。

