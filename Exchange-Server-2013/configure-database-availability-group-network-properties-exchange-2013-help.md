---
title: 'データベース可用性グループのネットワーク プロパティを構成する: Exchange 2013 Help'
TOCTitle: データベース可用性グループのネットワーク プロパティを構成する
ms:assetid: 41197639-988f-476c-9788-51d5191a7dce
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd297927(v=EXCHG.150)
ms:contentKeyID: 48269412
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# データベース可用性グループのネットワーク プロパティを構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-31_

各データベース可用性グループ (DAG) ネットワークには、DAG ネットワークの名前や、DAG ネットワークの説明フィールド、DAG ネットワークが使用するサブネット一覧、レプリケーションに対して DAG ネットワークが有効であるかどうかなど、構成可能なプロパティがいくつかあります。

DAG に関連する他の管理タスクについては、「[データベース可用性グループの管理](managing-database-availability-groups-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[高可用性とサイト復元のアクセス許可](high-availability-and-site-resilience-permissions-exchange-2013-help.md)」の「データベース可用性グループ」。

  - DAG ネットワークは、DAG の自動ネットワーク構成が無効になっているときのみ構成できます。DAG のネットワーク自動構成を無効にする方法の詳細な手順については、「[データベース可用性グループのプロパティを構成する](configure-database-availability-group-properties-exchange-2013-help.md)」をご覧ください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してデータベース可用性グループ ネットワークのプロパティを構成する

1.  EAC で、<strong>サーバー</strong> \> <strong>データベース可用性グループ</strong> に移動します。

2.  構成する DAG を選択し、\[詳細\] ウィンドウ内の構成する DAG ネットワークの下で、以下を選択します。
    
      - <strong>レプリケーションを無効にする</strong> または <strong>レプリケーションを有効にする</strong>   DAG ネットワークのレプリケーション設定を構成します。
    
      - <strong>削除</strong>   DAG ネットワークを削除します。DAG ネットワークを削除する前に、DAG ネットワークから関連付けられたサブネットをすべて削除する必要があります。
    
      - <strong>詳細の表示</strong>   DAG ネットワークの名前、説明、関連サブネットなど、DAG ネットワークのプロパティを構成します。それらのサブネットに関連付けられたネットワーク インターフェイスを表示したり、DAG ネットワークのレプリケーションを有効または無効にしたりすることもできます。

## シェルを使用してデータベース可用性グループ ネットワークのプロパティを構成する

この例では、10.0.0.0 のサブネットと 255.0.0.0 のサブネット マスクを DAG DAG1 の DAG ネットワーク MapiDagNetwork に追加します。

```powershell
Set-DatabaseAvailabilityGroupNetwork -Subnets 10.0.0.0/8 -Identity DAG1\MapiDagNetwork
```

## 正常な動作を確認する方法

DAG ネットワークが正常に構成されたことを確認するには、次の手順を実行します。

  - シェルで次のコマンドを実行して、DAG ネットワーク構成の設定を表示し、DAG ネットワークが正常に構成されたことを確認します。
    
    ```powershell
Get-DatabaseAvailabilityGroupNetwork <DAGNetworkName> | Format-List
```

## 詳細情報

[Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/ja-jp/library/dd298008\(v=exchg.150\))

[Get-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/ja-jp/library/dd297938\(v=exchg.150\))

[New-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/ja-jp/library/dd335225\(v=exchg.150\))

[Remove-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/ja-jp/library/dd298131\(v=exchg.150\))

