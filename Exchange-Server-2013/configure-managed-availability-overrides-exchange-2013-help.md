---
title: '可用性管理のオーバーライドを構成する: Exchange 2013 Help'
TOCTitle: 可用性管理のオーバーライドを構成する
ms:assetid: c8f315b3-1d5e-4ad9-8bea-9c3a4a13ebfc
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn482055(v=EXCHG.150)
ms:contentKeyID: 59895171
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 可用性管理のオーバーライドを構成する

 

_**適用先:**Exchange Online, Exchange Server 2013 SP1_

_**トピックの最終更新日:**2015-11-30_

可用性管理は、継続的にプローブを実行して Exchange コンポーネントやその依存関係で起こり得る問題を検知し、回復操作を実行して、これらのコンポーネントに関連する問題によってエンド ユーザー エクスペリエンスに影響が出ないようにします。しかし、お使いの環境によっては、標準設定が最適とはならない場合もあります。オーバーライドを作成すると、可用性管理のプローブ、モニター、レスポンダーをカスタマイズできます。

オーバーライドには、ローカルとグローバルの 2 種類があります。その名前が示すように、ローカル オーバーライドは作成元のサーバーでのみ使用でき、グローバル オーバーライドは複数のサーバーにオーバーライドを適用できます。どちらの種類でも、特定の期間または特定のバージョンの Exchange を対象にしたオーバーライドを作成できます (ただし、両方を同時に使用することはできません)。


> [!NOTE]
> オーバーライドを作成しても、すぐには有効になりません。Microsoft Exchange Health Management サービスが 10 分ごとに構成の変更をチェックし、検出された構成の変更を読み込みます。すぐに有効にする場合は、サービスを再起動します。



可用性管理に関連する追加の管理タスクについては、「[正常性セットおよびサーバーの状態の管理](manage-health-sets-and-server-health-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行するには、シェルを使用する必要があります。オンプレミスの Exchange 組織で Exchange 管理シェル を開く方法については、「[シェルを開く](https://technet.microsoft.com/ja-jp/library/dd638134\(v=exchg.150\))」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## Exchange 管理シェル を使用してローカル オーバーライドを作成する

特定の期間のローカル オーバーライドを作成するには、次の構文を使用します。

    Add-ServerMonitoringOverride -Server <ServerName> -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertyName> -PropertyValue <Value> -Duration <dd.hh:mm:ss>

Exchange の特定のバージョンのローカル オーバーライドを作成するには、次の構文を使用します。

    Add-ServerMonitoringOverride -Server <ServerName> -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertyName> -PropertyValue <Value> -Version <15.01.xxxx.xxx>


> [!NOTE]
> オーバーライドを作成する際に <EM>Identity</EM> パラメーターで使用される値は、大文字小文字を区別します。



この例は、EXCH03 という名前のサーバー上の応答側 `ActiveDirectoryConnectivityConfigDCServerReboot` を 20 日間無効にするローカルのオーバーライドを追加します。

    Add-ServerMonitoringOverride -Server EXCH03 -Identity "AD\ActiveDirectoryConnectivityConfigDCServerReboot" -ItemType Responder -PropertyName Enabled -PropertyValue 0 -Duration 20.00:00:00

## 正常な動作を確認する方法

ローカル オーバーライドが正常に作成されたことを確認するには、**Get-ServerMonitoringOverride** コマンドレットを使ってローカル オーバーライドの一覧を表示します。

    Get-ServerMonitoringOverride  -Server <ServerIdentity> | Format-List

作成したオーバーライドが一覧に表示されます。

## Exchange 管理シェル を使用してローカル オーバーライドを削除する

ローカル オーバーライドを削除するには、次の構文を使用します。

    Remove-ServerMonitoringOverride -Server <ServerName> -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <ExistingItemTypeValue> -PropertyName <PropertytoRemove>

この例は、サーバー EXCH01 からの Exchange 正常性セットの `ActiveDirectoryConnectivityConfigDCServerReboot` 応答側の既存ローカル オーバーライドを削除します。

    Remove-ServerMonitoringOverride -Server EXCH01 -Identity Exchange\ActiveDirectoryConnectivityConfigDCServerReboot -ItemType Responder -PropertyName Enabled

## 正常な動作を確認する方法

ローカル オーバーライドが正常に削除されたことを確認するには、**Get-ServerMonitoringOverride** コマンドレットを使ってローカル オーバーライドの一覧を表示します。

    Get-ServerMonitoringOverride  -Server <ServerIdentity> | Format-List

削除されたオーバーライドは、一覧には表示されません。

## Exchange 管理シェル を使用してグローバル オーバーライドを作成する

特定の期間のグローバル オーバーライドを作成するには、次の構文を使用します。

    Add-GlobalMonitoringOverride -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertytoOverride> -PropertyValue <NewPropertyValue> -Duration <dd.hh:mm:ss>

Exchange の特定のバージョンのグローバル オーバーライドを作成するには、次の構文を使用します。

    Add-GlobalMonitoringOverride -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertytoOverride> -PropertyValue <NewPropertyValue> -ApplyVersion <15.01.xxxx.xxx>


> [!NOTE]
> オーバーライドを作成する際に <EM>Identity</EM> パラメーターで使用される値は、大文字小文字を区別します。



この例は、`OnPremisesInboundProxy` プローブを 30 日間無効にするグローバル オーバーライドを追加します。

    Add-GlobalMonitoringOverride -Identity "FrontendTransport\OnPremisesInboundProxy" -ItemType Probe -PropertyName Enabled -PropertyValue 0 -Duration 30.00:00:00

この例は、Exchange バージョン 15.01.0225.042 を実行する全サーバー上の `StorageLogicalDriveSpaceEscalate` 応答側を無効にするグローバル オーバーライドを追加します。

    Add-GlobalMonitoringOverride -Identity "MailboxSpace\StorageLogicalDriveSpaceEscalate" -PropertyName Enabled -PropertyValue 0 -ItemType Responder -ApplyVersion "15.01.0225.042"

## 正常な動作を確認する方法

グローバル オーバーライドが正常に作成されたことを確認するには、**Get-GlobalMonitoringOverride** コマンドレットを使ってグローバル オーバーライドの一覧を表示します。

    Get-GlobalMonitoringOverride

作成したオーバーライドが一覧に表示されます。

## Exchange 管理シェル を使用してグローバル オーバーライドを削除する

グローバル オーバーライドを削除するには、次の構文を使用します。

    Remove-GlobalMonitoringOverride -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <ExistingItemTypeValue> -PropertyName <OverriddenProperty>

この例は、`FrontEndTransport` 正常性セットの `OnPremisesInboundProxy` プローブの `ExtensionAttributes` プロパティの既存のグローバル オーバーライドを削除します。

    Remove-GlobalMonitoringOverride -Identity FrontEndTransport\OnPremisesInboundProxy -ItemType Probe -PropertyName ExtensionAttributes

## 正常な動作を確認する方法

グローバル オーバーライドが正常に削除されたことを確認するには、**Get-GlobalMonitoringOverride** コマンドレットを使ってグローバル オーバーライドの一覧を表示します。

    Get-GlobalMonitoringOverride

削除されたオーバーライドは、一覧には表示されません。

