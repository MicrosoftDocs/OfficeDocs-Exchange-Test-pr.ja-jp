---
title: HubTransport 正常性セットのトラブルシューティング
TOCTitle: HubTransport 正常性セットのトラブルシューティング
ms:assetid: e3932ce3-836c-4230-9f64-63af1b704d79
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.scom.hubtransport(v=EXCHG.150)
ms:contentKeyID: 54651739
ms.date: 01/28/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# HubTransport 正常性セットのトラブルシューティング

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

**HubTransport** 正常性セットは、組織内のメールのルーティングを担当するメールボックス サーバー上で、トランスポート パイプラインの全体的な正常性を監視します。詳細については、「[メール フロー](https://technet.microsoft.com/ja-jp/library/aa996349\(v=exchg.150\))」を参照してください。

**HubTransport** 正常性セットの異常を示す警告を受け取った場合、メールのルーティングや配信が妨げられる可能性のある問題が発生しています。

## 説明

**HubTransport** サービスは、次のプローブとモニターを使用して監視されます。


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
<td><p>ActiveQueueDrainFailureProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>ActiveQueueDrainFailureMonitor</p></td>
</tr>
<tr class="even">
<td><p>DiagnosticsAggregationLocalSnapshotProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>DiagnosticsAggregationLocalSnapshotMonitor</p></td>
</tr>
<tr class="odd">
<td><p>DiagnosticsAggregationWebServiceProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>DiagnosticsAggregationWebServiceMonitor</p></td>
</tr>
<tr class="even">
<td><p>HubAvailabilityProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>HubAvailabilityMonitor</p></td>
</tr>
<tr class="odd">
<td><p>HubTransportServiceRunning</p></td>
<td><p>HubTransport</p></td>
<td><p>HubTransportServiceRunningMonitor</p></td>
</tr>
<tr class="even">
<td><p>ShadowQueueDiscardDrainFailureProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>ShadowQueueDiscardDrainFailureMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ThrottlingServiceRunning</p></td>
<td><p>HubTransport</p></td>
<td><p>ThrottlingServiceRunningMonitor</p></td>
</tr>
<tr class="even">
<td><p>TransportEdgeSync.Service.Probe</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportEdgeSync.Service.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>TransportLogSearchRunningProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportLogSearchRunningMonitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>BootloaderOutstandingItemsTriggerMonitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>CrashEvent.edgetransport</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>CrashEvent.msexchangethrottling</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>CrashEvent.msexchangetransport</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>CrashEvent.msexchangetransportlogsearch</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>EdgeTransportBackpressureSustainedTimeMonitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>FederatedDecryptionAgentFailedToXDecryptMonitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>HubTransport.ServiceInconsistentState.Monitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>IsMemberOfResolverExpandedGroupsCacheSizeMonitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>IsMemberOfResolverResolvedGroupsCacheSizeMonitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Messages.failed.to.be.made.redundant.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>MessagesDeferredDuringCategorizationMonitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>MessageTrackingLogsDirQuotaMonitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetError.edgetransport</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetError.msexchahangetransportlogsearch</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetError.msexchangethrottling</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetError.msexchangetransport</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetWarning.edgetransport</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetWarning.msexchangethrottling</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetWarning.msexchangetransport</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetWarning.msexchangetransportlogsearch</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeError.edgetransport</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeError.msexchangethrottling</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeError.msexchangetransport</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeError.msexchangetransportlogsearch</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeWarning.edgetransport</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeWarning.msexchangethrottling</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeWarning.msexchangetransport</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeWarning.msexchangetransportlogsearch</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueExternalAggregateMonitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueInternalAggregateMonitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueInternalAggregateNormalPriorityMonitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueInternalHubRetryMonitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueInternalHubRetryNormalPriorityMonitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueMailboxRetryMonitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueNonSMTPRetryMonitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleEvaluationFailureEventLogMonitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleEvaluationIgnoredFailureEventLogMonitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleEvaluationIgnoredFipsFailureEventLogMonitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleEvaluationSmallScaleFailureEventLogMonitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleEvaluationSmallScaleFipsFailureEventLogMonitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleExcessiveForkingEventLogMonitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleLoadFailureEventLogMonitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleLoadSmallScaleFailureEventLogMonitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>SmtpProxyEhloOptionsDoNotMatchContinueProxyingMonitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>SubmissionQueueMonitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>TlsDomainClientCertificateSubjectMismatchMonitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Total.Shadow.Queue.Length.Above.Threshold.Monitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>TotalE2ELatencyHighForMSExchangeTransportMonitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>TotalE2ELatencyLowForMSExchangeTransportMonitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>TotalE2ELatencyNormalForMSExchangeTransportMonitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.CatExpiry.Monitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.Critical.Storage.Recovery.Failed.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.DatabaseMoved.Monitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.DomainSecureCert.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.DomainSecureCertAuth.Monitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.DomainSecureServerCertFailed.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.DomainSecureServerDomainCertFailed.Monitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.FailedToCreatePickupDirectory.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.InvalidAcceptedDomain.Monitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.LowDiskSpace.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.Messages.Completing.Categorization.Monitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.NDRForUnrestrictedLargeDL.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.PickupDelete.Monitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.PickupIsBadmailingFile.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.SendConn.AuthKerb.Monitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.SendConnAuth.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.SendConnTLS.Monitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.ServerCertExpireSoon.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.ServerCertMismatch.Monitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.ServiceStartError.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.SmtpSendDirectTrustFailed.Monitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.TemplateDoesNotExist.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.TLSValidate.Monitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.UnknownTemplateInPublishingLicense.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportCategorizerJobAvailabilityMonitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportDatabaseCorruptMonitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportDeliveryFailures544Monitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportDeliveryFailuresDeliveryStoreDriver520Monitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportLogGenerationCheckpointDepthMonitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportLogSearchLogPathInvalidMonitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportMaxLocalLoopCountMonitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportPickupReadMonitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportPoisonMessageMonitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportRejectingMessageSubmissionsMonitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportServerCertPersonalStoreMonitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>UnreachableQueueMonitor</p></td>
</tr>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>HubTransport</p></td>
<td><p>XProxyToTransientInvalidArgumentsMonitor</p></td>
</tr>
</tbody>
</table>


プローブとモニターの詳細については、「[サーバーの状態とパフォーマンス](https://technet.microsoft.com/ja-jp/library/jj150551\(v=exchg.150\))」を参照してください。

## ユーザー操作

サービスは、警告の発行後に回復することがあります。そのため、**HubTransport** 正常性セットが異常であることを示す警告を受け取ったときは、まず、その問題がまだ存在しているかどうかを確認します。問題が存在する場合は、次のセクションで説明する適切な回復操作を実行します。

## 問題の確認

1.  警告に記載された正常性セット名とサーバー名を確認します。

2.  メッセージの詳細には、警告の正確な原因に関する情報が示されています。ほとんどの場合、根本原因を特定するためのトラブルシューティング情報としては、メッセージの詳細だけで十分です。メッセージの詳細が不明確な場合は、次の操作を行います。
    
    1.  Exchange 管理シェル を開き、次のコマンドを実行して、警告を発行した正常性セットの詳細を取得します。
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        たとえば、mailbox1.contoso.com に関する **HubTransport** 正常性セットの詳細を取得するには、以下のコマンドを実行します。
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealthSetName -eq "HubTransport"}
    
    2.  コマンド出力を確認して、エラーを報告したモニターを特定します。警告を発行したモニターの **AlertValue** の値は **Unhealthy** になります。
    
    3.  正常状態にないモニターに関連するプローブを再実行します。関連するプローブについては、「[説明](troubleshooting-activesync-health-set.md)」セクションの表を参照してください。このためには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        たとえば、失敗したモニターが **ActiveQueueDrainFailureMonitor** だとします。そのモニターに関連するプローブは **ActiveQueueDrainFailureProbe** です。mailbox1.contoso.com でこのプローブを実行するには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe HubTransport\ActiveQueueDrainFailureProbe -Server mailbox1.contoso.com | Format-List
    
    4.  コマンド出力で、プローブの Result セクションを確認します。値が **Succeeded** であれば、この問題は一時的なエラーであり、もう存在しません。

