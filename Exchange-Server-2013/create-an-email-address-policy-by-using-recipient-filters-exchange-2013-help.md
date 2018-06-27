---
title: '受信者フィルターを使用した電子メール アドレス ポリシーの作成: Exchange 2013 Help'
TOCTitle: 受信者フィルターを使用した電子メール アドレス ポリシーの作成
ms:assetid: e3f446bd-1511-479c-8d87-2dfce5547c90
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb232194(v=EXCHG.150)
ms:contentKeyID: 49896529
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 受信者フィルターを使用した電子メール アドレス ポリシーの作成

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2012-10-16_

シェルを使用すると、受信者フィルターを使用して電子メール アドレス ポリシーを作成できます。 電子メール アドレス ポリシーの詳細については、「[電子メール アドレス ポリシー](email-address-policies-exchange-2013-help.md)」を参照してください。

電子メール アドレス ポリシーに関連する追加の管理タスクについては、「[電子メール アドレス ポリシーの手順](email-address-policy-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - *RecipientFilter* パラメーターを使用してカスタム フィルターを作成するには、フィルターの文字列を指定する必要があります。 シェルでは、フィルター構文に OPath を使用します。 OPath は、オブジェクト データ ソースをクエリするために設計されたクエリ言語です。
    

    > [!IMPORTANT]
    > 受信者フィルターを使用して電子メール アドレス ポリシーを作成または編集する場合、電子メール アドレス ポリシーの編集に Exchange 管理コンソール (EAC) を使用することはできません。シェルを使用する必要があります。 構文およびパラメーターの詳細については、「<A href="https://technet.microsoft.com/ja-jp/library/bb124517(v=exchg.150)">Set-EmailAddressPolicy</A>」を参照してください。



  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[電子メール アドレスとアドレス帳](email-addresses-and-address-books-exchange-2013-help.md)」の「電子メール アドレス ポリシー」。

  - 電子メール アドレス ポリシーで SMTP アドレス ドメインを使用する前に、承認済みドメインを構成する必要があります。詳細については、「[承認済みドメイン](accepted-domains-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!WARNING]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用し、受信者フィルターを使用して電子メール アドレス ポリシーを作成する

受信者フィルターを使用して電子メール アドレス ポリシーを作成するには、次の構文を使用します。

    New-EmailAddressPolicy -Name <String> -RecipientFilter <String>

この例では、すべての上級管理者に適用する電子メール アドレス ポリシーを作成し、電子メール アドレスのローカル部分を名の最初の 2 文字と姓の全体で構成します。

    New-EmailAddressPolicy -Name 'Execs' -EnabledEmailAddressTemplates 'SMTP:%2g%s@contoso.com' -RecipientFilter {((RecipientType -eq 'UserMailbox') -and (Title -like 'executive'))}

構文およびパラメーターの詳細については、「[New-EmailAddressPolicy](https://technet.microsoft.com/ja-jp/library/aa996800\(v=exchg.150\))」を参照してください。

