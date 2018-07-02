---
title: '動的配布グループのメンバーを表示する: Exchange Online Help'
TOCTitle: 動的配布グループのメンバーを表示する
ms:assetid: 40b100c6-864e-4c82-9f98-08dd5c83e378
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb232019(v=EXCHG.150)
ms:contentKeyID: 48269408
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 動的配布グループのメンバーを表示する

 

_**適用先:** Exchange Online, Exchange Server 2013_

動的配布グループは、定義済みの受信者セットではなく特定の受信者フィルターに基づいたメンバーシップの配布グループです。MicrosoftExchange には、動的配布グループの受信者フィルターを簡単に作成できるように既定のフィルターが用意されています。*既定のフィルター*は、よく使用されるフィルターです。このフィルターを使用すると、さまざまな受信者フィルター処理の条件を満たすことができます。動的配布グループに含める受信者の種類を指定できます。また、受信者が満たす必要のある条件の一覧を指定することもできます。シェルを使用して、既定のフィルターを使用する動的配布グループの受信者の一覧をプレビューできます。

## 始める前に把握しておくべき情報

  - 予想所要時間:2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「動的配布グループ」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## シェルを使用して動的配布グループのメンバーの一覧をプレビューする

この例では、Full Time Employees という動的配布グループのメンバーの一覧を返します。最初のコマンドは、動的配布グループ オブジェクトを変数 `$FTE` に格納します。2 番目のコマンドは、**Get-Recipient** コマンドレットを使用して、動的配布グループに定義されている条件に一致する受信者を一覧表示します。

    $FTE = Get-DynamicDistributionGroup "Full Time Employees"

    Get-Recipient -RecipientPreviewFilter $FTE.RecipientFilter -OrganizationalUnit $FTE.RecipientContainer

構文およびパラメーターの詳細については、「[Get-DynamicDistributionGroup](https://technet.microsoft.com/ja-jp/library/bb124762\(v=exchg.150\))」と「[Get-Recipient](https://technet.microsoft.com/ja-jp/library/aa996921\(v=exchg.150\))」を参照してください。


> [!NOTE]
> EAC を使用して、動的配布グループのメンバーを表示することはできません。



## 正常な動作を確認する方法

動的配布グループのメンバーが正常に表示されたことを確認するには、以下を実行します。

  - シェルで、前述のコマンドを実行して動的配布グループのメンバーの一覧をプレビューすると、メンバーの一覧が返されます。たとえば、動的配布グループの受信者フィルターに一致するプロパティを持つ新しいユーザー メールボックスを作成した場合、この新しいユーザーはグループ メンバーの一覧に表示される必要があります。

