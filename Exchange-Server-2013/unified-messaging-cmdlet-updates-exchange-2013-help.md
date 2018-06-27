---
title: 'ユニファイド メッセージングのコマンドレットの更新: Exchange 2013 Help'
TOCTitle: ユニファイド メッセージングのコマンドレットの更新
ms:assetid: a42c6643-67ed-4003-854a-ac1d66efb965
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ150557(v=EXCHG.150)
ms:contentKeyID: 48269891
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ユニファイド メッセージングのコマンドレットの更新

 

_**適用先:**Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:**2015-03-09_

Exchange Server 2010 に存在したユニファイド メッセージング (UM) コマンドレットの多くは Exchange Server 2013 に持ち込まれていますが、これらのコマンドレットの一部が変更されています。さらに、Exchange 2013 には新しいコマンドレットも追加されました。

## 更新されたパラメーターと新しい UM コマンドレット

以下は、Exchange 2013 で更新されたパラメーターおよび新しいコマンドレットの一覧です。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>コマンドレット</th>
<th>パラメーター</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>New-UMIPGateway</p></td>
<td><p><code>[-IPAddressFamily &lt;IPv4Only | IPv6Only | Any&gt;]</code></p></td>
</tr>
<tr class="even">
<td><p>Set-UMIPGateway</p></td>
<td><p><code>[-IPAddressFamily &lt;IPv4Only | IPv6Only | Any&gt;]</code></p></td>
</tr>
<tr class="odd">
<td><p>Get-UMMailbox</p></td>
<td><p><code>[-AccountPartition &lt;AccountPartitionIdParameter&gt;]</code></p></td>
</tr>
<tr class="even">
<td><p>Set-UMMailbox</p></td>
<td><p><code>[-ImListMigrationCompleted &lt;$true | $false&gt; -VoiceMailAnalysisEnabled &lt;$true | $false&gt;]</code></p></td>
</tr>
<tr class="odd">
<td><p>Test-Connectivity</p></td>
<td><p><code>[-CallRouter &lt;SwitchParameter&gt;]</code></p></td>
</tr>
<tr class="even">
<td><p>New-UMCallAnsweringRule</p></td>
<td><p><code>[-Name &lt;String&gt; [-CallerIds &lt;MultiValuedProperty&gt;] [-CallersCanInterruptGreeting &lt;$true | $false&gt;] [-CheckAutomaticReplies &lt;$true | $false&gt;] [-Confirm [&lt;SwitchParameter&gt;]] [-DomainController &lt;Fqdn&gt;] [-ExtensionsDialed &lt;MultiValuedProperty&gt;] [-KeyMappings &lt;MultiValuedProperty&gt;] [-Mailbox &lt;MailboxIdParameter&gt;] [-Organization &lt;OrganizationIdParameter&gt;] [-Priority &lt;Int32&gt;] [-ScheduleStatus &lt;Int32&gt;] [-TimeOfDay &lt;TimeOfDay&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p></td>
</tr>
<tr class="odd">
<td><p>Remove-UMCallAnsweringRule</p></td>
<td><p><code>[-Identity &lt;UMCallAnsweringRuleIdParameter&gt; [-Confirm [&lt;SwitchParameter&gt;]] [-DomainController &lt;Fqdn&gt;] [-Mailbox &lt;MailboxIdParameter&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p></td>
</tr>
<tr class="even">
<td><p>Get-UMCallAnsweringRule</p></td>
<td><p><code>[-Identity &lt;UMCallAnsweringRuleIdParameter&gt;] [-DomainController &lt;Fqdn&gt;] [-Mailbox &lt;MailboxIdParameter&gt;]</code></p></td>
</tr>
<tr class="odd">
<td><p>Set-UMCallAnsweringRule</p></td>
<td><p><code>[-Identity &lt;UMCallAnsweringRuleIdParameter&gt; [-CallerIds &lt;MultiValuedProperty&gt;] [-CallersCanInterruptGreeting &lt;$true | $false&gt;] [-CheckAutomaticReplies &lt;$true | $false&gt;] [-Confirm [&lt;SwitchParameter&gt;]] [-DomainController &lt;Fqdn&gt;] [-ExtensionsDialed &lt;MultiValuedProperty&gt;] [-KeyMappings &lt;MultiValuedProperty&gt;] [-Mailbox &lt;MailboxIdParameter&gt;] [-Name &lt;String&gt;] [-Priority &lt;Int32&gt;] [-ScheduleStatus &lt;Int32&gt;] [-TimeOfDay &lt;TimeOfDay&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p></td>
</tr>
<tr class="even">
<td><p>Enable-UMCallAnsweringRule</p></td>
<td><p><code>[-Identity &lt;UMCallAnsweringRuleIdParameter&gt; [-Confirm [&lt;SwitchParameter&gt;]] [-DomainController &lt;Fqdn&gt;] [-Mailbox &lt;MailboxIdParameter&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p></td>
</tr>
<tr class="odd">
<td><p>Disable-UMCallAnsweringRule</p></td>
<td><p><code>[-Identity &lt;UMCallAnsweringRuleIdParameter&gt; [-Confirm [&lt;SwitchParameter&gt;]] [-DomainController &lt;Fqdn&gt;] [-Mailbox &lt;MailboxIdParameter&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p></td>
</tr>
<tr class="even">
<td><p>Get-UMCallRouterSettings</p></td>
<td><p><code>[-DomainController &lt;Fqdn&gt;] [-Server &lt;ServerIdParameter&gt;]</code></p></td>
</tr>
<tr class="odd">
<td><p>Set-UMCallRouterSettings</p></td>
<td><p><code>Set-UMCallRouterSettings [-Confirm [&lt;SwitchParameter&gt;]] [-DialPlans &lt;MultiValuedProperty&gt;] [-DomainController &lt;Fqdn&gt;] [-IPAddressFamily &lt;IPv4Only | IPv6Only | Any&gt;] [-IPAddressFamilyConfigurable &lt;$true | $false&gt;] [-Server &lt;ServerIdParameter&gt;] [-SipTcpListeningPort &lt;Int32&gt;] [-SipTlsListeningPort &lt;Int32&gt;] [-UMPodRedirectTemplate &lt;String&gt;] [-UMStartupMode &lt;TCP | TLS | Dual&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p></td>
</tr>
<tr class="even">
<td><p>Disable-UMService</p></td>
<td><p><code>-Identity &lt;UMServerIdParameter&gt; [-Confirm [&lt;SwitchParameter&gt;]] [-DomainController &lt;Fqdn&gt;] [-Immediate &lt;$true | $false&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p>

> [!NOTE]
> このコマンドレットは Exchange 2007 サーバーおよび Exchange 2010 UM サーバーでのみ動作します。


</td>
</tr>
<tr class="odd">
<td><p>Enable-UMService</p></td>
<td><p><code>-Identity &lt;UMServerIdParameter&gt; [-Confirm [&lt;SwitchParameter&gt;]] [-DomainController &lt;Fqdn&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p>

> [!NOTE]
> このコマンドレットは Exchange 2007 サーバーおよび Exchange 2010 UM サーバーでのみ動作します。


</td>
</tr>
<tr class="even">
<td><p>Get-UMService</p></td>
<td><p><code>[-Identity &lt;UMServerIdParameter&gt;] [-DomainController &lt;Fqdn&gt;]</code></p></td>
</tr>
<tr class="odd">
<td><p>Set-UMService</p></td>
<td><p><code>Set-UMService -Identity &lt;UMServerIdParameter&gt; [-Confirm [&lt;SwitchParameter&gt;]] [-DialPlans &lt;MultiValuedProperty&gt;] [-DomainController &lt;Fqdn&gt;] [-GrammarGenerationSchedule &lt;ScheduleInterval[]&gt;] [-IPAddressFamily &lt;IPv4Only | IPv6Only | Any&gt;] [-IPAddressFamilyConfigurable &lt;$true | $false&gt;] [-IrmLogEnabled &lt;$true | $false&gt;] [-IrmLogMaxAge &lt;EnhancedTimeSpan&gt;] [-IrmLogMaxDirectorySize &lt;Unlimited&gt;] [-IrmLogMaxFileSize &lt;ByteQuantifiedSize&gt;] [-IrmLogPath &lt;LocalLongFullPath&gt;] [-MaxCallsAllowed &lt;Int32&gt;] [-SIPAccessService &lt;ProtocolConnectionSettings&gt;] [-UMStartupMode &lt;TCP | TLS | Dual&gt;] [-WhatIf [&lt;SwitchParameter&gt;]]</code></p></td>
</tr>
</tbody>
</table>


すべての UM コマンドレットの詳細については、「[ユニファイド メッセージングのコマンドレット](https://technet.microsoft.com/ja-jp/library/aa997665\(v=exchg.150\))」を参照してください。

