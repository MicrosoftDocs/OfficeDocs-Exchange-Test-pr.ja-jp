---
title: 'Exchange の電子情報開示のアクセス許可を割り当てる: Exchange Online Help'
TOCTitle: Exchange の電子情報開示のアクセス許可を割り当てる
ms:assetid: 729e09d8-614b-431f-ae04-ae41fb4c628e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd298059(v=EXCHG.150)
ms:contentKeyID: 48269644
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange の電子情報開示のアクセス許可を割り当てる

 

_**適用先:**Exchange Online, Exchange Server 2013_

ユーザーに Microsoft Exchange Server 2013 のインプレース電子情報開示を使用させる場合は、最初にそのユーザーを "Discovery Management/探索管理" 役割グループに追加して権限を付与する必要があります。Discovery Management 役割グループのメンバーは、Exchange セットアップで作成された探索メールボックスに対してフル アクセスのメールボックス アクセス許可を持っています。


> [!NOTE]
> "Discovery Management/探索管理" 役割グループのメンバーは、機密メッセージ コンテンツにアクセスすることができます。特にこれらのメンバーは、<A href="in-place-ediscovery-exchange-2013-help.md">インプレース電子情報開示 (eDiscovery)</A> を使用して、Exchange 組織内のすべてのメールボックスの検索、メッセージ (およびその他のメールボックス アイテム) のプレビュー、それらの探索メールボックスへのコピー、コピーされたメッセージの .pst ファイルへのエクスポートを行うことができます。ほとんどの組織では、このアクセス許可は法務担当者、コンプライアンス担当者または人事管理担当者に付与されます。<BR>



"Discovery Management/探索管理" 役割グループの詳細については、「[検出の管理](discovery-management-exchange-2013-help.md)」を参照してください。役割ベースのアクセス制御 (RBAC) の詳細については、「[役割ベースのアクセス制御について](understanding-role-based-access-control-exchange-2013-help.md)」を参照してください。

この手順を使用しているシナリオに興味はありますか?次のトピックを参照してください。

  - [インプレース電子情報開示検索を作成する](create-an-in-place-ediscovery-search-exchange-2013-help.md)

  - [インプレース保持を作成または削除する](create-or-remove-an-in-place-hold-exchange-2013-help.md)

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「役割グループ」。

  - 既定では、Discovery Management 役割グループにはメンバーが含まれません。組織の管理 役割を持つ管理者も、Discovery Management 役割グループに追加されていないと、探索検索を作成または管理できません。

  - Exchange 2013 では、組織の管理 役割グループのメンバーは、[インプレース保持と訴訟ホールド](in-place-hold-and-litigation-hold-exchange-2013-help.md) を作成して、すべてのメールボックスのコンテンツを保持できます。ただし、クエリベースのインプレース保持を作成するには、ユーザーは "Discovery Management/探索管理" 役割グループのメンバーであるか、"Mailbox Search/メールボックス検索" の役割が割り当てられている必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

## EAC を使用してユーザーを "Discovery Management/探索管理" 役割グループに追加する

1.  **\[アクセス許可\]** \> **\[管理者の役割\]** に移動します。

2.  リスト ビューで、**\[探索管理\]** を選択して **\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[役割グループ\]** の **\[メンバー\]** で、**\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

4.  **\[メンバーの選択\]** で、1 人または複数のユーザーを選択し、**\[追加\]**、**\[OK\]** の順にクリックします。

5.  **\[役割グループ\]** で、**\[保存\]** をクリックします。

## シェルを使用してユーザーを "Discovery Management/探索管理" 役割グループに追加する

この例では、ユーザー Bsuneja を "Discovery Management/探索管理" 役割グループに追加します。

    Add-RoleGroupMember -Identity "Discovery Management" -Member Bsuneja

構文およびパラメーターの詳細については、「[Add-RoleGroupMember](https://technet.microsoft.com/ja-jp/library/dd638207\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

ユーザーが "Discovery Management/探索管理" 役割グループに追加されたことを検証するには、次の操作を実行します。

1.  EAC で **\[アクセス許可\]** \> **\[管理者の役割\]** に移動します。

2.  リスト ビューで、**\[探索管理\]** を選択します。

3.  詳細ウィンドウで、ユーザーが **\[メンバー\]** の一覧に表示されていることを確認します。

このコマンドを実行しても、"Discovery Management/探索管理" 役割グループのメンバーの一覧を表示できます。

    Get-RoleGroupMember -Identity "Discovery Management"


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。


