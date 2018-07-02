---
title: '配布グループ名前付けポリシーの上書き: Exchange Online Help'
TOCTitle: 配布グループ名前付けポリシーの上書き
ms:assetid: 9eb23fc9-3f59-4d09-9077-85c89a051ee0
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ218685(v=EXCHG.150)
ms:contentKeyID: 49115819
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配布グループ名前付けポリシーの上書き

 

_**適用先:** Exchange Online, Exchange Server 2013_

配布グループのグループの名前付けポリシーが適用されるのは、ユーザーが作成したグループだけです。 管理者が Exchange 管理センター (EAC) を使用して配布グループを作成した場合は、グループの名前付けポリシーは無視されます。そのグループの名前には、ポリシーは適用されません。

ただし、Exchange 管理シェルを使用して配布グループの作成または名前の変更を行う場合は、*IgnoreNamingPolicy* パラメーターを使用してグループの名前付けポリシーを上書きしない限り、管理者によって作成されたグループにグループの名前付けポリシーが適用されます。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「配布グループ」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## 新しいグループを作成するときに、シェルを使用してグループの名前付けポリシーを上書きする

グループの名前付けポリシーをオーバーライドするには、次のコマンドを実行します。

    New-DistributionGroup -Name <Group Name> -IgnoreNamingPolicy

たとえば、組織のグループの名前付けポリシーが **DG\_\<Group Name\>\_Users** である場合に、**All Administrators** という名前のグループを作成するには、次のコマンドを実行します。

    New-DistributionGroup -Name "All Administrators" -IgnoreNamingPolicy

Microsoft Exchange でこのグループが作成されると、*Name* パラメーターと *DisplayName* パラメーターには **All Administrators** が使用されます。

## グループ名を変更するときに、シェルを使用してグループの名前付けポリシーを上書きする

シェルで既存のグループの名前を変更するときにグループの名前付けポリシーを上書きするには、次のコマンドを実行します。

    Set-DistributionGroup -Identity <Old Group Name> -Name <New Group Name> -DisplayName <New Group Name> -IgnoreNamingPolicy

たとえば、ある深夜にグループの名前付けポリシーを作成し、翌朝にプレフィックスのテキスト文字列のスペルが間違っていることに気付いたとしましょう。この翌朝、スペルが間違っているプレフィックスを使用して新しいグループが既に作成されていることを確認したとします。 グループの名前付けポリシーは EAC で修正できますが、名前のスペルが間違っているグループの名前を変更するにはシェルを使用する必要があります。次のコマンドを実行します。

    Set-DistributionGroup -Identity "Goverment_Contracts_NWRegion" -Name "Government_ContractEstimates_NWRegion" -DisplayName "Government_ContractEstimates_NWRegion" -IgnoreNamingPolicy


> [!IMPORTANT]
> グループの名前を変更するときは、<EM>DisplayName</EM> パラメーターを必ず指定してください。 指定しない場合、共有アドレス帳、および電子メール メッセージの "宛先:"、"CC:"、"差出人:" の各行には、古い名前が引き続き表示されます。



## 正常な動作を確認する方法

グループの名前付けポリシーを無視する配布グループを正常に作成、または名前変更したことを確認するには、以下のコマンドを実行します。

    Get-DistributionGroup <Name> | FL DisplayName

    Get-OrganizationConfig | FL DistributionGroupNamingPolicy

グループの表示名の形式が組織のグループの名前付けポリシーで強制されるものと異なる場合、正常に完了しています。

