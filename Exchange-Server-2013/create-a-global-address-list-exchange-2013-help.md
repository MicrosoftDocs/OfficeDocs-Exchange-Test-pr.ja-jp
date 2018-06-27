---
title: 'グローバル アドレス一覧の作成: Exchange Online Help'
TOCTitle: グローバル アドレス一覧の作成
ms:assetid: 59e4955a-8999-4d17-be9f-23a41a23b929
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb232063(v=EXCHG.150)
ms:contentKeyID: 49896261
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# グローバル アドレス一覧の作成

 

_**適用先:**Exchange Online, Exchange Server 2013_

グローバル アドレス一覧 (GAL) は、MicrosoftExchange が実装されている組織内のすべてのグループ、ユーザー、連絡先のエントリが含まれているディレクトリです。組織でアドレス帳ポリシーを使用する場合、追加の GAL を作成できます。詳しくは、「[アドレス帳ポリシー](address-book-policies-exchange-2013-help.md)」をご覧ください。

アドレス一覧に関連する追加の管理タスクについては、「[アドレス一覧の手順](address-list-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[電子メール アドレスおよびアドレス帳のアクセス許可](email-address-and-address-book-permissions-exchange-2013-help.md)」の「アドレス一覧」。

  - Exchange Online の既定では、アドレス一覧の役割はどの役割グループにも割り当てられません。アドレス一覧の役割を必要とするコマンドレットを使用するには、その役割を役割グループに追加してください。詳細については、トピック「[役割グループの管理](manage-role-groups-exchange-2013-help.md)」の「役割グループに役割を追加する」を参照してください。

  - Exchange 管理センター (EAC) を使用してこの手順を実行することはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用した条件付きフィルター プロパティを使用する GAL の作成

この例では、メールボックス ユーザーかつ彼らの会社が Contoso と一覧表示されている受信者に対して、GAL\_Contoso という名前の GAL を作成します。

    New-GlobalAddressList -Name "GAL_Contoso" -IncludedRecipients MailboxUsers -ConditionalCompany Contoso


> [!NOTE]
> 既定の条件付きフィルター プロパティを使用している場合、<EM>IncludedRecipients</EM> パラメーターを空白にすることはできません。



構文およびパラメーターの詳細については、「[New-GlobalAddressList](https://technet.microsoft.com/ja-jp/library/bb123785\(v=exchg.150\))」を参照してください。

## シェルを使用した受信者フィルターを使用する GAL の作成

この例では、*CustomAttribute15* パラメーターの値が `AgencyA` である受信者に対して、GAL\_AgencyA という名前の GAL を作成します。

    New-GlobalAddressList -Name "GAL_AgencyA" -RecipientFilter {CustomAttribute15 -like "AgencyA"}

構文およびパラメーターの詳細については、「[New-GlobalAddressList](https://technet.microsoft.com/ja-jp/library/bb123785\(v=exchg.150\))」を参照してください。

