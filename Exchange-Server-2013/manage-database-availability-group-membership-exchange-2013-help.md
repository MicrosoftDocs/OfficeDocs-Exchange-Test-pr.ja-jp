---
title: 'データベース可用性グループのメンバーシップを管理する: Exchange 2013 Help'
TOCTitle: データベース可用性グループのメンバーシップを管理する
ms:assetid: fb2ea15e-96d5-4045-b75b-b0aa5fc60479
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd351278(v=EXCHG.150)
ms:contentKeyID: 48270273
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# データベース可用性グループのメンバーシップを管理する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-08-13_

サーバーをデータベース可用性グループ (DAG) に追加すると、そのサーバーは DAG 内の他のサーバーと連動して、データベース障害、サーバー障害、またはネットワーク障害からのデータベース レベルの自動回復を提供します。サーバーを DAG から削除すると、そのサーバーは障害から自動的には保護されなくなります。

DAG に関連する他の管理タスクについては、「[データベース可用性グループの管理](managing-database-availability-groups-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : サーバーごとに 5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[高可用性とサイト復元のアクセス許可](high-availability-and-site-resilience-permissions-exchange-2013-help.md)」の「データベース可用性グループ」。

  - DAG では、Windows フェールオーバー クラスタリング (WFC) テクノロジを使用します。DAG のメンバーである各メールボックス サーバーは、DAG によって使用される基になるクラスター内のノードでもあります。その結果、メールボックス サーバーは任意の時点で 1 つの DAG のみのメンバーになります。DAG では WFC テクノロジが使用されるため、DAG に追加するすべてのサーバーは、次に示す同じオペレーティング システムを実行している必要があります。Windows Server 2008 R2 の Enterprise Edition または Datacenter Edition、Windows Server 2012 または Windows Server 2012 R2 の Standard Edition または Datacenter Edition。

  - Windows Server 2012 を実行するメールボックス サーバーを追加している場合は、DAG 用のクラスター名オブジェクト (CNO) を事前に設定する必要があります。Windows Server 2012 R2 を実行するメールボックス サーバーを追加していて、DAG に管理アクセス ポイントない場合、CNO を事前に設定する必要はありません。管理アクセス ポイントがない DAG には CNO がないからです。詳細な手順については、「[データベース可用性グループのクラスター名オブジェクトを事前設定する](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md)」を参照してください。

  - DAG にメンバーを追加する場合は、事前に、DAG を作成する必要があります。詳細な手順については、「[データベース可用性グループを作成する](create-a-database-availability-group-exchange-2013-help.md)」を参照してください。

  - DAG から削除する前に、サーバーからレプリケートされたすべてのデータベース コピーを削除する必要がある。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してデータベース可用性グループのメンバーシップを管理する

1.  EAC で、**\[サーバー\]** \> **\[データベース可用性グループ\]** に移動します。

2.  構成する DAG を選択して、![DAG メンバーの管理](images/Dd351278.d567ae56-d6cd-4edb-ab67-ad8f7c58f337(EXCHG.150).gif "DAG メンバーの管理") をクリックします。
    
      - 1 つ以上のメールボックス サーバーを DAG に追加するには、![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックし、一覧からサーバーを選択し、**\[追加\]** クリックし、さらに **\[OK\]** をクリックします。
    
      - 1 つ以上のメールボックス サーバーを DAG から削除するには、サーバーを選択して、マイナス \[-\] アイコンをクリックします。

3.  **\[保存\]** をクリックして変更を保存します。

4.  タスクが正常に完了したら、**\[閉じる\]** をクリックします。

## シェルを使用してデータベース可用性グループのメンバーシップを管理する

この例では、メールボックス サーバー MBX1 を DAG1 という名前の DAG に追加します。

    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1

この例では、メールボックス サーバー MBX1 を DAG1 という名前の DAG から削除します。このコマンドを実行する前に、メールボックス サーバ－にレプリケートされたデータベースが存在しないことを確認します。

    Remove-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1

この例では、メールボックス サーバー MBX4 の構成設定を DAG2 という名前の DAG から削除します。MBX4 は長期間オフラインになると想定されるので、残りのオンライン DAG メンバーとクォーラムを確立するために、MBX4 がオフラインである間はその構成が DAG から削除されます。

    Remove-DatabaseAvailabilityGroupServer -Identity DAG2 -MailboxServer MBX4 -ConfigurationOnly

## 正常な動作を確認する方法

DAG メンバーシップが正常に管理されていることを確認するには、次のいずれかの手順を実行します。

  - EAC で、**\[サーバー\]** \> **\[データベース可用性グループ\]** に移動します。**\[メンバー サーバー\]** 列に、現在の DAG メンバーシップが表示されます。

  - シェルで次のコマンドを実行して、DAG メンバーシップ情報を表示します。
    
        Get-DatabaseAvailabilityGroup <DAGName> | Format-List Servers

## 詳細情報

[Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/ja-jp/library/dd298049\(v=exchg.150\))

[Remove-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/ja-jp/library/dd297956\(v=exchg.150\))

