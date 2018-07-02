---
title: 'カスタム属性: Exchange 2013 Help'
TOCTitle: カスタム属性
ms:assetid: 2b043878-0b34-4563-a9c2-28a9efa7447e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee423541(v=EXCHG.150)
ms:contentKeyID: 49895311
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# カスタム属性

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-17_

Microsoft Exchange Server 2013 には 15 個の拡張属性があります。 これらの属性を使用すると、従業員 ID や組織単位 (OU) などの受信者についての情報、または既存の属性が存在しないその他のいくつかのカスタム値を追加できます。 これらのカスタム属性には Active Directory 内で **ms-Exch-Extension-Attribute1** ～ **ms-Exch-Extension-Attribute15** というラベルが付いています。 Exchange 管理シェルでは、対応するパラメーターは *CustomAttribute1* ～ *CustomAttribute15* です。 これらの属性は、Exchange コンポーネントでは使用されません。 これらの属性を使用すると、Active Directory スキーマを拡張する必要なく Active Directory データを格納できます。

Exchange Server 2003 以前では、Active Directory にこの情報を格納する場合は Active Directory スキーマを拡張して属性を作成する必要がありました。 スキーマの拡張では、新しい属性のオブジェクト識別子 (OID) の計画と調達、および運用環境で実装する前のテスト環境での拡張プロセスのテストが必要になります。 Exchange 2013 では、アドレス一覧、メール アドレス ポリシー、動的配布グループが使用する受信者フィルターにスキーマ拡張を使用できません。

**目次**

カスタム属性の利点

カスタム属性の例

ConditionalCustomAttributes パラメーターを使用するカスタム属性の例

ExtensionCustomAttributes パラメーターを使用したカスタム属性の例

## カスタム属性の利点

カスタム属性を使用することの利点は、以下のとおりです。

  - Active Directory スキーマの拡張を回避します。

  - Exchange セットアップによって属性が作成されます。

  - 属性は、Exchange 管理センター (EAC) または Exchange 管理シェルで管理できます。 カスタムのコントロールを作成したり、これらの属性を取得および表示するスクリプトを記述したりする必要がありません。

  - カスタム属性はフィルター可能なプロパティで、**Get-Mailbox** などの受信者コマンドレットと共に *Filter* パラメーターで使用できます。 カスタム属性は、EAC とシェルでメール アドレス ポリシー、アドレス一覧、および動的配布グループのフィルターを作成するときにも使用できます。

## 複数の値を持つカスタム属性

Exchange 2010 Service Pack 2 (SP2) では、複数の値を持つ 5 つのカスタム属性を Exchange に追加しました。これは、従来のカスタム属性ではニーズに対応できない場合に、メール受信者のその他の情報を指定するためです。 *ExtensionCustomAttribute1* パラメーターから *ExtensionCustomAttribute5* パラメーターはそれぞれ、最大 1,300 個の値を指定できます。 複数の値は、コンマ区切りの一覧として指定できます。以下のコマンドレットは、これらの新しいパラメーターをサポートしています。

  - [Set-DistributionGroup](https://technet.microsoft.com/ja-jp/library/bb124955\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/ja-jp/library/bb123796\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/ja-jp/library/aa995950\(v=exchg.150\))

  - [Set-MailPublicFolder](https://technet.microsoft.com/ja-jp/library/bb123707\(v=exchg.150\))

  - [Set-RemoteMailbox](https://technet.microsoft.com/ja-jp/library/ff607302\(v=exchg.150\))

複数の値を持つプロパティの詳細については、「[複数値プロパティの変更](modifying-multivalued-properties-exchange-2013-help.md)」を参照してください。

## カスタム属性の例

多くの Exchange 展開では、OU 内のすべての受信者に対して電子メール アドレス ポリシーを作成することは一般的なシナリオです。 OU は、電子メール アドレス ポリシーやアドレス一覧の *RecipientFilter* パラメーターで使用できる、フィルター可能なプロパティではありません。


> [!NOTE]
> 動的配布グループには、特定の OU またはコンテナー内の受信者に制限するために使用可能な追加のパラメーターがあります。



OU 内の受信者が、部署や場所などのフィルター基準となる共通のプロパティを共有しない場合、次の例で示すようにいずれかのカスタム属性に共通値を設定できます。

    Get-Mailbox -OrganizationalUnit Sales | Set-Mailbox CustomAttribute1 "SalesOU"

この例で示すように、*CustomAttribute1* プロパティを SalesOU に設定したすべての受信者に対して電子メール アドレス ポリシーを作成できました。

    New-EmailAddressPolicy -Name "Sales" -RecipientFilter { CustomAttribute1 -eq "SalesOU"} -EnabledEmailAddressTemplates "SMTP:%s%2g@sales.contoso.com"

## ConditionalCustomAttributes パラメーターを使用するカスタム属性の例

動的配布グループ、メール アドレス ポリシー、またはアドレス一覧を作成する際、*RecipeintFilter* パラメーターでカスタム属性を指定する必要はありません。 代わりに、*ConditionalCustomAttribute1* ～ *ConditionalCustomAttribute15* を使用できます。

この例では、*CustomAttribute1* の設定値が SalesOU の受信者を基準に動的配布グループを作成します。

    New-DynamicDistributionGroup -Name "Sales Users and Contacts" -IncludedRecipients "MailboxUsers,MailContacts" -ConditionalCustomAttribute1 "SalesOU"


> [!NOTE]
> <EM>Conditional</EM> パラメーターを使用する場合は、<EM>IncludedRecipients</EM> パラメーターを使用する必要があります。 また、<EM>Conditional</EM> パラメーターを使用する場合は、<EM>RecipientFilter</EM> パラメーターを使用できません。 動的配布グループ、メール アドレス ポリシー、またはアドレス一覧を作成するために追加フィルターを設定する場合は、<EM>RecipientFilter</EM> パラメーターを使用してください。



## ExtensionCustomAttributes パラメーターを使用したカスタム属性の例

この例では、Kweku のメールボックスで *ExtensionCustomAttribute1* を更新して彼が教育クラス MATH307、ECON202、ENGL300 に登録したことを反映します。

    Set-Mailbox -Identity Kweku -ExtensionCustomAttribute1 MATH307,ECON202,ENGL300

次に、MATH307 に登録した全生徒の動的配布グループを *RecipientFilter* パラメーターで作成します。ここで、*ExtensionCustomAttribute1* は MATH307 です。 *ExtentionCustomAttributes* パラメーターを使用するとき、`-like` 演算子の代わりに `-eq` 演算子を使用できます。

    New-DynamicDistributionGroup -Name Students_MATH307 -RecipientFilter {ExtensionCustomAttribute1 -eq "MATH307"}

この例では、Kweku の *ExtensionCustomAttribute1* 値は更新されて、彼がクラス ENGL210 を追加し、クラス ECON202 を削除したことを反映します。

    Set-Mailbox -Identity Kweku -ExtensionCustomAttribute1 @{Add="ENGL210"; Remove="ECON202"}

