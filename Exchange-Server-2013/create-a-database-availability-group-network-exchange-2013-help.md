---
title: 'データベース可用性グループのネットワークを作成する: Exchange 2013 Help'
TOCTitle: データベース可用性グループのネットワークを作成する
ms:assetid: 6caec7be-788a-4058-87a7-f31c575b870c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd298051(v=EXCHG.150)
ms:contentKeyID: 48269621
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# データベース可用性グループのネットワークを作成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-11-02_

必要に応じて、データベース可用性グループ (DAG) で使用する追加のネットワークを作成できます。DAG ネットワークを作成するには、EAC またはシェルを使用できます。

DAG に関連する他の管理タスクについては、「[データベース可用性グループの管理](managing-database-availability-groups-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[高可用性とサイト復元のアクセス許可](high-availability-and-site-resilience-permissions-exchange-2013-help.md)」の「データベース可用性グループ」。

  - DAG ネットワークは、DAG のネットワーク自動構成が無効にされたときにのみ作成できます。DAG のネットワーク自動構成を無効にする方法の詳細な手順については、「[データベース可用性グループのプロパティを構成する](configure-database-availability-group-properties-exchange-2013-help.md)」をご覧ください。

  - DAG ネットワークを作成する際には、別の DAG ネットワークに使用されていない、一意のサブネットを割り当てる必要があります。既存の DAG ネットワークに割り当てられたサブネットを使用すると、その DAG ネットワークからサブネットが削除され、新しく作成した DAG ネットワークに追加されます。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してデータベース可用性グループ ネットワークを作成する

1.  EAC で、<strong>サーバー</strong> \> <strong>データベース可用性グループ</strong> に移動します。

2.  構成する DAG を選択して、![DAG ネットワークの追加](images/Dd298051.befcdc4e-7f7a-451d-a0a8-608c79f5d186(EXCHG.150).gif "DAG ネットワークの追加") をクリックします。

3.      
    <strong>データベース可用性グループ ネットワークの新規作成</strong> ページで、以下の情報を入力します。
    
      - <strong>データベース可用性グループ ネットワークの名前</strong>   このフィールドには、DAG 内の一意のネットワークの名前を入力します。
    
      - <strong>説明</strong>   このフィールドには、DAG ネットワークのテキスト説明を入力します。
    
      - <strong>サブネット</strong>   このフィールドは、DAG ネットワークに 1 つ以上のサブネットを関連付けるために使用します。サブネットを追加するには ![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") を、サブネットを編集するには ![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") を、サブネットを削除するにはマイナス (-) をクリックします。

4.  <strong>保存</strong> をクリックして DAG ネットワークを作成します。

## シェルを使用してデータベース可用性グループ ネットワークを作成する

この例では、DAG DAG1 内に、サブネットが 10.0.0.0 でビットマスクが 8 のネットワーク ReplicationDagNetwork02 を作成します。ネットワークでレプリケーションを有効にし、ネットワークのオプションの説明も入力します。

  ```powershell
  New-DatabaseAvailabilityGroupNetwork -DatabaseAvailabilityGroup DAG1 -Name ReplicationDagNetwork02 -Description "Replication network 2" -Subnets 10.0.0.0/8 -ReplicationEnabled:$True
  ```

## 正常な動作を確認する方法

DAG ネットワークが正常に作成されたことを確認するには、次のいずれかを実行します。

  - EAC で、<strong>サーバー</strong> \> <strong>データベース可用性グループ</strong> に移動します。適切な DAG を選択すると、新しく作成した DAG ネットワークが \[詳細\] ウィンドウに表示されます。

  - シェルで次のコマンドを実行して、DAG ネットワークが作成されたことを確認し、DAG ネットワークの構成情報を表示します。
    
    ```powershell
    Get-DatabaseAvailabilityGroupNetwork <DAGNetworkName> | Format-List
    ```

## 詳細情報

[Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/ja-jp/library/dd298008\(v=exchg.150\))

[Get-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/ja-jp/library/dd297938\(v=exchg.150\))

[New-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/ja-jp/library/dd335225\(v=exchg.150\))

[Remove-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/ja-jp/library/dd298131\(v=exchg.150\))

