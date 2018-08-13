---
title: 'データベース可用性グループを削除する: Exchange 2013 Help'
TOCTitle: データベース可用性グループを削除する
ms:assetid: 071296e9-31b0-40f4-9a02-177d97486ebd
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd335069(v=EXCHG.150)
ms:contentKeyID: 48269137
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# データベース可用性グループを削除する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-11-16_

データベース可用性グループ (DAG) の削除は、簡単な作業です。DAG を削除するには、EAC またはシェルを使用できます。

DAG に関連する他の管理タスクについては、「[データベース可用性グループの管理](managing-database-availability-groups-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[高可用性とサイト復元のアクセス許可](high-availability-and-site-resilience-permissions-exchange-2013-help.md)」の「データベース可用性グループ」。

  - DAG を削除する前に、DAG を空にする必要があります。削除する DAG に任意のメールボックス サーバーが含まれている場合は、最初にそのサーバーを DAG から削除する必要があります。メールボックス サーバーを DAG から削除する方法の詳細については、「[データベース可用性グループのメンバーシップを管理する](manage-database-availability-group-membership-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してデータベース可用性グループを削除する

1.  **\[サーバー\]** \> **\[データベース可用性グループ\]** に移動します。

2.  削除する DAG を選択して、**\[削除\]**![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") をクリックします。

3.  警告を確認して DAG を削除するには、**\[はい\]** をクリックします。

## シェルを使用してデータベース可用性グループを削除する

この例では、DAG DAG1 が削除されます。

    Remove-DatabaseAvailabilityGroup -Identity DAG1

## 正常な動作を確認する方法

DAG が正常に削除されたことを確認するには、次のいずれかを実行します。

  - EAC で、**\[サーバー\]** \> **\[データベース可用性グループ\]** に移動して、DAG がまだ表示されるかどうかを確認します。

  - シェルで、次のコマンドを実行して、DAG がまだ存在するかどうかを確認します。
    
        Get-DatabaseAvailabilityGroup <DAGName>
    
    DAG が正常に削除された場合、前述コマンドにより、オブジェクトが見つからなかったことを示すエラー メッセージが表示されます。

