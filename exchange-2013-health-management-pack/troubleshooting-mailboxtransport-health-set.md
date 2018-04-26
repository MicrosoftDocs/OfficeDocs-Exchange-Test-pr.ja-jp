---
title: MailboxTransport 正常性セットのトラブルシューティング
TOCTitle: MailboxTransport 正常性セットのトラブルシューティング
ms:assetid: 02bfa4cf-6929-437e-bae5-079ea1b92373
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.scom.mailboxtransport(v=EXCHG.150)
ms:contentKeyID: 54651706
ms.date: 01/28/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# MailboxTransport 正常性セットのトラブルシューティング

 

_**適用先:**Exchange Server 2013, Project Server 2013_

_**トピックの最終更新日:**2015-03-09_

**MailboxTransport** 正常性セットは、メールボックス サーバー上のメールボックス トランスポート発信サービスとメールボックス トランスポート配信サービスの全体的な正常性を監視します。これらのサービスは、メールボックス データベースとの間のメールの送受信を担当します。詳細については、「[メール フロー](https://technet.microsoft.com/ja-jp/library/aa996349\(v=exchg.150\))」を参照してください。

**MailboxTransport** 正常性セットが正常でないことを示す警告を受け取った場合、メールボックス データベースとの間のメール送信または受信を妨げる可能性のある問題があることを示しています。

## 説明

**MailboxTransport** サービスは、次のプローブとモニターを使用して監視されます。


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
<td><p>MailboxDeliveryAvailability</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxDeliveryAvailabilityMonitor</p></td>
</tr>
<tr class="even">
<td><p>MailboxDeliveryAvailabilityAggregationProbe</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxDeliveryAvailabilityAggregationMonitor</p></td>
</tr>
<tr class="odd">
<td><p>MailboxDeliveryInstanceAvailabilityProbe</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxDeliveryInstanceAvailabilityMonitor</p></td>
</tr>
<tr class="even">
<td><p>MailboxTransportDeliveryServiceRunning</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxTransportDeliveryServiceRunningMonitor</p></td>
</tr>
<tr class="odd">
<td><p>MailboxTransportSubmissionServiceRunning</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxTransportSubmissionServiceRunningMonitor</p></td>
</tr>
<tr class="even">
<td><p>Mapi.Submit.Probe</p></td>
<td><p>MailboxTransport</p></td>
<td><p>Mapi.Submit.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>[なし] (通知またはチェック)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>CrashEvent.msexchangedelivery</p></td>
</tr>
<tr class="even">
<td><p>[なし] (通知またはチェック)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>CrashEvent.msexchangesubmission</p></td>
</tr>
<tr class="odd">
<td><p>[なし] (通知またはチェック)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>DeliveryBackpressureSustainedTimeMonitor</p></td>
</tr>
<tr class="even">
<td><p>[なし] (通知またはチェック)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>DeliveryInterceptorStoreDriverAgentPctPermFailedMonitor</p></td>
</tr>
<tr class="odd">
<td><p>[なし] (通知またはチェック)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxTransportUserQuarantineMonitor</p></td>
</tr>
<tr class="even">
<td><p>[なし] (通知またはチェック)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MBTSubmissionInterceptorSubmissionAgentMonitor</p></td>
</tr>
<tr class="odd">
<td><p>[なし] (通知またはチェック)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MSExchangeAsstAvgEventProcessingTimeSubmissionMonitor50</p></td>
</tr>
<tr class="even">
<td><p>[なし] (通知またはチェック)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MSExchangeAsstAvgEventProcessingTimeSubmissionMonitor70</p></td>
</tr>
<tr class="odd">
<td><p>[なし] (通知またはチェック)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>PrivateWorkingSetError.msexchangedelivery</p></td>
</tr>
<tr class="even">
<td><p>[なし] (通知またはチェック)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>PrivateWorkingSetError.msexchangesubmission</p></td>
</tr>
<tr class="odd">
<td><p>[なし] (通知またはチェック)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>PrivateWorkingSetWarning.msexchangedelivery</p></td>
</tr>
<tr class="even">
<td><p>[なし] (通知またはチェック)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>PrivateWorkingSetWarning.msexchangesubmission</p></td>
</tr>
<tr class="odd">
<td><p>[なし] (通知またはチェック)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>ProcessProcessorTimeError.msexchangedelivery</p></td>
</tr>
<tr class="even">
<td><p>[なし] (通知またはチェック)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>ProcessProcessorTimeError.msexchangesubmission</p></td>
</tr>
<tr class="odd">
<td><p>[なし] (通知またはチェック)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>ProcessProcessorTimeWarning.msexchangedelivery</p></td>
</tr>
<tr class="even">
<td><p>[なし] (通知またはチェック)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>ProcessProcessorTimeWarning.msexchangesubmission</p></td>
</tr>
<tr class="odd">
<td><p>[なし] (通知またはチェック)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>SubmissionBackpressureSustainedTimeMonitor</p></td>
</tr>
<tr class="even">
<td><p>[なし] (通知またはチェック)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>SubmissionInterceptorSubmissionAgentPctPermFailedMonitor</p></td>
</tr>
<tr class="odd">
<td><p>[なし] (通知またはチェック)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>TransportDeliveryFailuresDeliveryStoreDriver560Monitor</p></td>
</tr>
</tbody>
</table>


プローブとモニターの詳細については、「[サーバーの状態とパフォーマンス](https://technet.microsoft.com/ja-jp/library/jj150551\(v=exchg.150\))」を参照してください。

## ユーザー操作

サービスは、警告の発行後に回復することがあります。そのため、**MailboxTransport** 正常性セットが異常であることを示す警告を受け取ったときは、まず、その問題がまだ存在しているかどうかを確認します。問題が存在する場合は、次のセクションで説明する適切な回復操作を実行します。

## 問題の確認

1.  警告に記載された正常性セット名とサーバー名を確認します。

2.  メッセージの詳細には、警告の正確な原因に関する情報が示されています。ほとんどの場合、根本原因を特定するためのトラブルシューティング情報としては、メッセージの詳細だけで十分です。メッセージの詳細が不明確な場合は、次の操作を行います。
    
    1.  Exchange 管理シェル を開き、次のコマンドを実行して、警告を発行した正常性セットの詳細を取得します。
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        たとえば、mailbox1.contoso.com に関する **MailboxTransport** 正常性セット詳細を取得するには、次のコマンドを実行します。
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealthSetName -eq "MailboxTransport"}
    
    2.  コマンド出力を確認して、エラーを報告したモニターを特定します。警告を発行したモニターの **AlertValue** の値は **Unhealthy** になります。
    
    3.  正常状態にないモニターに関連するプローブを再実行します。関連するプローブについては、「[説明](troubleshooting-activesync-health-set.md)」セクションの表を参照してください。このためには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        たとえば、失敗したモニターが **MailboxDeliveryAvailabilityMonitor** だとします。そのモニターに関連するプローブは **MailboxDeliveryAvailability** です。mailbox1.contoso.com でこのプローブを実行するには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe MailboxTransport\MailboxDeliveryAvailabilityMonitor -Server mailbox1.contoso.com | Format-List
    
    4.  コマンド出力で、プローブの Result セクションを確認します。値が **Succeeded** であれば、この問題は一時的なエラーであり、もう存在しません。

