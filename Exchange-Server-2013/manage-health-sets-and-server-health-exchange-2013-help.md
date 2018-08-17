---
title: '正常性セットおよびサーバーの状態の管理: Exchange 2013 Help'
TOCTitle: 正常性セットおよびサーバーの状態の管理
ms:assetid: a4f84312-6cfa-4f17-9707-676aadab1143
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn482054(v=EXCHG.150)
ms:contentKeyID: 59895173
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 正常性セットおよびサーバーの状態の管理

 

_**適用先:** Exchange Online, Exchange Server 2013 SP1_

_**トピックの最終更新日:** 2013-12-02_

組み込みの正常性をレポートするコマンドレットを使用して、可用性管理に関連した以下のようなさまざまなタスクを実行できます。

  - サーバーまたはサーバーのグループの正常性の表示

  - 正常性セットの一覧の表示

  - 特定の正常性セットに関連付けられているプローブ、モニター、レスポンダーの一覧の表示

  - モニターとその現在の正常性の一覧の表示

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:2 分

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## サーバーの状態の表示

シェルを使用して、Exchange 2013 を実行しているサーバーの正常性の概要を取得できます。

## シェルを使用してサーバーの状態を表示する

次のコマンドのいずれかを実行し、Exchange 2013 を稼働しているサーバーの正常性セットと正常性情報を表示します。

```
Get-HealthReport -Identity <ServerName>
```
```
Get-ServerHealth -Identity <ServerName> | Format-Table Server,CurrentHealthSetState,Name,HealthSetName,AlertValue,HealthGroupName -Auto
```

次のコマンドのいずれかを実行し、Exchange 2013 を稼働しているサーバーまたはデータベース可用性グループの正常性セットを表示します。

```
Get-ExchangeServer | Get-HealthReport -RollupGroup
```
```
Get-ExchangeServer | Get-HealthReport -RollupGroup -HealthSetName <HealthSet>
```
```
(Get-DatabaseAvailabiltyGroup <DAGName>).Servers | Get-HealthReport -RollupGroup
```

## 正常性セットの一覧の表示

正常性セットは、コンポーネントが正常かどうかを決定するコンポーネントのモニター、プローブ、レスポンダーのグループです。シェルを使用して、Exchange 2013 を稼働しているサーバーの正常性セットの一覧を表示できます。

## シェルを使用して正常性セットの一覧を表示する

次のコマンドを実行して、Exchange 2013 を稼働しているサーバーの正常性セットを表示します。

    Get-HealthReport -Server <ServerName>

## 正常性セットのプローブ、モニター、レスポンダーの表示

正常性セットは、コンポーネントが正常かどうかを決定するコンポーネントのモニター、プローブ、レスポンダーのグループです。シェルを使用して、Exchange 2013 を稼働しているサーバーの正常性セットに関連したプローブ、モニター、レスポンダーの一覧を表示できます。

## シェルを使用して、正常性セットのプローブ、モニター、レスポンダーを表示する

以下のコマンドを使用して、Exchange 2013 を稼働しているサーバーの正常性セットに関連したプローブ、モニター、レスポンダーの一覧を表示します。

    Get-MonitoringItemIdentity -Server <ServerName> -Identity <HealthSetName> | Format-Table Identity,ItemType,Name -Auto

## モニターとその現在の正常性の一覧の表示

正常性セットの「最下位の」モニターが、複数のモニターの正常性として報告されます。正常性セットの詳細を表示して、どのモニターが正常で、どのモニターが問題であるかを見ることができます。

## シェルを使用してモニターとその現在の正常性の一覧を表示する

以下のコマンドを実行して、Exchange 2013 を稼働しているサーバーのモニターとその現在の正常性の一覧を表示します。

    Get-ServerHealth -HealthSet <HealthSetName> -Server <ServerName> | Format-Table Name, AlertValue -Auto

