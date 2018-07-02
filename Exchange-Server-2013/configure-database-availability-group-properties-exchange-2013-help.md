---
title: 'データベース可用性グループのプロパティを構成する: Exchange 2013 Help'
TOCTitle: データベース可用性グループのプロパティを構成する
ms:assetid: 50daeac5-a16f-4362-a325-19e0fe25d59d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd297985(v=EXCHG.150)
ms:contentKeyID: 48269485
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# データベース可用性グループのプロパティを構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-06-24_

EAC またはシェルを使用して、データベース可用性グループ (DAG) のプロパティ (DAG IP アドレス構成、DAG が使用する監視サーバーと監視ディレクトリなど) を構成します。シェルを使用すると、EAC からでは構成できない DAG プロパティ (代替監視サーバーと代替監視ディレクトリの情報、レプリケーションに使用する TCP ポート、データセンター アクティブ化調整 (DAC) モードなど) を構成できます。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[高可用性とサイト復元のアクセス許可](high-availability-and-site-resilience-permissions-exchange-2013-help.md)」の「データベース可用性グループ」。

  - DAG プロパティ値は、Active Directory とクラスター データベースの両方に保存されます。ただし、一部のプロパティは、クラスター データベースにのみ保存されます。そのため、DAG の基になるクラスターが稼動している必要があります。また、以下のプロパティを設定するためにクォーラムが必要です。
    
      - ReplicationPort
    
      - NetworkCompression
    
      - NetworkEncryption
    
      - DiscoverNetworks

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用したデータベース可用性グループ プロパティの構成

1.  EAC で、**\[サーバー\]** \> **\[データベース可用性グループ\]** に移動します。

2.  構成する DAG を選択して ![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  
    
    **\[全般\]** ページを使用して DAG メンバーシップおよび稼動状態を表示し、DAG 監視サーバー、監視ディレクトリ、およびネットワーク自動構成を構成します。
    
      - **\[監視サーバー\]**   DAG 用の監視サーバーのホスト名または完全修飾ドメイン名 (FQDN)。これはすべての DAG に必須のプロパティですが、DAG メンバーの偶数メンバーが存在してクラスターによって使用されるクォーラム モデルがノードおよびファイル共有マジョリティである場合は監視サーバーが使用されます。
    
      - **\[監視ディレクトリ\]**   監視サーバー上にある witness.log ファイルの格納に使用されるディレクトリの完全なパス。これはすべての DAG に必要なプロパティですが、DAG の監視サーバーが使用中の場合に限り、監視ディレクトリが使用されます。
    
      - **\[運用サーバー\]**   DAG メンバーの一覧とその現在の稼働状態を表示する読み取り専用のフィールド。
    
      - **\[データベース可用性グループ ネットワークを手動で構成する\]**   すべての DAG ネットワークを手動で構成する場合にオンにするチェック ボックス。このチェック ボックスをオフのままにしておくと、DAG ネットワークは、ネットワーク インターフェイス構成を基にして、システムにより自動的に構成されます。チェック ボックスがオフの場合、**Set-DatabaseAvailabilityGroupNetwork** および **New-DatabaseAvailabilityGroupNetwork** コマンドレットを DAG に対する管理用としては使用できません。

4.  
    
    DAG に割り当てられた IP アドレスを表示し変更するには、**\[IP アドレス\]** ページを使用します。
    
      - 既存の IP アドレスを選択し、![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックして変更します。
    
      - 既存の IP アドレスを選択し、マイナスのアイコン (削除) をクリックして削除します。
    
      - IP アドレスを入力し、![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックして DAG に追加します。

5.  
    
    **\[保存\]** をクリックし、変更を保存します。

## シェルを使用したデータベース可用性グループ プロパティの構成

この例では、DAG1 という DAG の監視ディレクトリを C:\\DAG1DIR に設定します。

    Set-DatabaseAvailabilityGroup -Identity DAG1 -WitnessDirectory C:\DAG1DIR

この例では、DAG1 という DAG に対して、代替ミラーリング監視サーバーを CAS3 に、代替監視ディレクトリを C:\\DAGFileShareWitnesses\\DAG1.contoso.com に事前に構成します。

    Set-DatabaseAvailabilityGroup -Identity DAG1 -AlternateWitnessDirectory C:\DAGFileShareWitnesses\DAG1.contoso.com -AlternateWitnessServer CAS3

この例では、動的ホスト構成プロトコル (DHCP) を使用して IP アドレスを取得するように、DAG1 という DAG を構成します。

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 0.0.0.0

この例では、静的な IP アドレス 10.0.0.8 を使用するように、DAG1 という DAG を構成します。

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8

この例では、DAG1 という複数サブネットの DAG に複数の静的 IP アドレスを構成します。

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8,10.0.1.8

この例では、DAG1 という DAG を DAC モード用に構成します。

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatacenterActivationMode DagOnly

この例では、DAG DAG1 のレプリケーション ポートを 63132 に構成します。

    Set-DatabaseAvailabilityGroup -Identity DAG1 -ReplicationPort 63132


> [!NOTE]
> DAG の既定のレプリケーション ポートを変更した後、DAG の各メンバーの Windows ファイアウォール例外を手動で変更して、指定されたポートを介して通信が行えるようにする必要があります。



## 正常な動作を確認する方法

DAG が正常に構成されたことを確認するには、次の手順を実行します。

  - シェルで次のコマンドを実行して、DAG の構成設定を表示し、DAG が正常に構成されたことを確認します。
    
        Get-DatabaseAvailabilityGroup <DAGName> | Format-List

## 詳細情報

[データベース可用性グループを作成する](create-a-database-availability-group-exchange-2013-help.md)

[データベース可用性グループを削除する](remove-a-database-availability-group-exchange-2013-help.md)

[データベース可用性グループのネットワークを作成する](create-a-database-availability-group-network-exchange-2013-help.md)

[データベース可用性グループのメンバーシップを管理する](manage-database-availability-group-membership-exchange-2013-help.md)

[Get-DatabaseAvailabilityGroup](https://technet.microsoft.com/ja-jp/library/dd351226\(v=exchg.150\))

[Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/ja-jp/library/dd297934\(v=exchg.150\))

