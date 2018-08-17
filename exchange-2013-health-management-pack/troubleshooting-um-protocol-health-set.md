---
title: UM.Protocol 正常性セットのトラブルシューティング
TOCTitle: UM.Protocol 正常性セットのトラブルシューティング
ms:assetid: 8dd9a16f-77a1-4a8d-aea4-5e96ab922dd4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.scom.um.protocol(v=EXCHG.150)
ms:contentKeyID: 53181835
ms.date: 01/28/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM.Protocol 正常性セットのトラブルシューティング

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

UM.Protocol 正常性セットは、メールボックス サーバー上のユニファイド メッセージング (UM) プロトコルを監視します。

UM.Protocol が正常でないことを示す警告を受け取った場合、それが示すのは、ユーザーが組織内の UM サービスを使用できなくなる可能性がある問題です。UM.Protocol 正常性セットは、次の正常性セットに密接に関連しています。

[UM 正常性セットのトラブルシューティング](troubleshooting-um-health-set.md)

[UM.CallRouter 正常性セットのトラブルシューティング](troubleshooting-um-callrouter-health-set.md)

## 説明

UM.Protocol サービスは、次のプローブとモニターを使用して監視されます。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Probe</th>
<th>正常性セット</th>
<th>依存関係</th>
<th>関連するモニター</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>UMSelfTestProbe</p></td>
<td><p>UM.Protocol</p></td>
<td><p>Active Directory ドメイン サービス (AD DS)</p></td>
<td><p>UMSelfTestMonitor</p></td>
</tr>
</tbody>
</table>


プローブとモニターの詳細については、「[サーバーの状態とパフォーマンス](https://technet.microsoft.com/ja-jp/library/jj150551\(v=exchg.150\))」を参照してください。

## ユーザー操作

サービスは、警告の発行後に回復することがあります。そのため、正常性セットが異常であることを示す警告を受け取ったときは、まず、その問題がまだ存在しているかどうかを確認します。問題が存在する場合は、次のセクションで説明する適切な回復操作を実行します。

## 問題がまだ存在していることを確認する

1.  警告に記載された正常性セット名とサーバー名を確認します。

2.  メッセージの詳細には、警告の正確な原因に関する情報が示されています。ほとんどの場合、根本原因を特定するためのトラブルシューティング情報としては、メッセージの詳細だけで十分です。メッセージの詳細が不明確な場合は、次の操作を行います。
    
    1.  Exchange 管理シェル を開き、次のコマンドを実行して、警告を発行した正常性セットの詳細を取得します。
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        たとえば、server1.contoso.com に関する UM.Protocol 正常性セットの詳細を取得するには、次のコマンドを実行します。
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "UM.Protocol"}
    
    2.  コマンド出力を確認して、エラーを報告したモニターを特定します。警告を発行したモニターの **AlertValue** の値は `Unhealthy` になります。
    
    3.  正常状態にないモニターに関連するプローブを再実行します。関連するプローブについては、「説明」セクションの表を参照してください。このためには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        たとえば、失敗したモニターが **UMSelfTestMonitor** だとします。そのモニターに関連するプローブは **UMSelfTestProbe** です。そのプローブを server1.contoso.com で実行するには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe UM.Protocol\UMSelfTestMonitor -Server server1.contoso.com | Format-List
    
    4.  コマンド出力で、プローブの **Result** の値を確認します。値が **Succeeded** であれば、この問題は一時的なエラーであり、もう存在しません。値がそれ以外の場合は、次のセクションで説明する回復手順を参照してください。

## トラブルシューティングの手順

正常性セットから警告を受け取ったときは、電子メール メッセージに次の情報が含まれています。

  - 警告を送信したサーバーの名前

  - 警告の発生日時

  - 使用された認証メカニズムと資格情報

  - 最後のエラーの完全な例外追跡 (診断データおよび特定の HTTP ヘッダー情報を含む)
    
    **注**   完全な例外の追跡に記載された情報を使用して、問題をトラブルシューティングできます。プローブによって生成された例外には、プローブが失敗した理由を説明する「エラーの理由」が含まれています。

UJM 警告メッセージのトラブルシューティングの詳細については、「[UM 正常性セットのトラブルシューティング](troubleshooting-um-health-set.md)」を参照してください。

## 詳細情報

[Exchange 2013 の新機能](https://technet.microsoft.com/ja-jp/library/jj150540\(v=exchg.150\))

[Exchange 2013 コマンドレット](https://technet.microsoft.com/ja-jp/library/bb124413\(v=exchg.150\))

