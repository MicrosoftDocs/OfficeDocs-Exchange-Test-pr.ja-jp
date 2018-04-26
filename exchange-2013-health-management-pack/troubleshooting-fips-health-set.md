---
title: FIPS 正常性セットのトラブルシューティング
TOCTitle: FIPS 正常性セットのトラブルシューティング
ms:assetid: 96e1b096-9cb5-426f-a84e-50d5599e4bbb
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.scom.fips(v=EXCHG.150)
ms:contentKeyID: 54651730
ms.date: 01/28/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# FIPS 正常性セットのトラブルシューティング

 

_**適用先:**Exchange Server 2013, Project Server 2013_

_**トピックの最終更新日:**2015-03-09_

**FIPS** 正常性セットは、Exchange サーバーにおける米国連邦情報処理規格 (FIPS) 設定の全体的な状態を監視します。FIPS 140 の詳細については、「[FIPS 140 検証](http://go.microsoft.com/fwlink/p/?linkid=521913)」を参照してください。

**FIPS** 正常性セットが正常でないことを示す警告を受け取った場合、この警告は Exchange サーバーが FIPS 140 に準拠したコンポーネントおよびプロセスを使用できない問題があることを示します。

## 説明

**FIPS** サービスは、次のプローブとモニターを使用して監視されます。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>プローブ</th>
<th>正常性セット</th>
<th>関連するモニター</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>FIPS</p></td>
<td><p>CrashEvent.scanningprocess</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>FIPS</p></td>
<td><p>MaintenanceFailureMonitor.FIPS</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>FIPS</p></td>
<td><p>MaintenanceTimeoutMonitor.FIPS</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>FIPS</p></td>
<td><p>PrivateWorkingSetWarning.scanningprocess</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>FIPS</p></td>
<td><p>PrivateWorkingSetError.scanningprocess</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>FIPS</p></td>
<td><p>ProcessProcessorTimeWarning.scanningprocess</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>FIPS</p></td>
<td><p>ProcessProcessorTimeError.scanningprocess</p></td>
</tr>
</tbody>
</table>


プローブとモニターの詳細については、「[サーバーの状態とパフォーマンス](https://technet.microsoft.com/ja-jp/library/jj150551\(v=exchg.150\))」を参照してください。

## ユーザー操作

サービスは、警告の発行後に回復することがあります。そのため、**FIPS** 正常性セットが異常であることを示す警告を受け取ったときは、まず、その問題がまだ存在しているかどうかを確認します。問題が存在する場合は、次のセクションで説明する適切な回復操作を実行します。

## 問題の確認

1.  警告に記載された正常性セット名とサーバー名を確認します。

2.  メッセージの詳細には、警告の正確な原因に関する情報が示されています。ほとんどの場合、根本原因を特定するためのトラブルシューティング情報としては、メッセージの詳細だけで十分です。メッセージの詳細が不明確な場合は、次の操作を行います。
    
    1.  Exchange 管理シェル を開き、次のコマンドを実行して、警告を発行した正常性セットの詳細を取得します。
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        たとえば、server1.contoso.com に関する **FIPS** 正常性セットの詳細を取得するには、次のコマンドを実行します。
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "FIPS"}
    
    2.  コマンド出力を確認して、エラーを報告したモニターを特定します。警告を発行したモニターの **AlertValue** の値は **Unhealthy** になります。

