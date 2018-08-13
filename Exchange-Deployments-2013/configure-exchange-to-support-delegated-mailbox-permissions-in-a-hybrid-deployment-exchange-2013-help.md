---
title: 'ハイブリッド展開で委任されたメールボックスへのアクセス許可をサポートするように Exchange を構成する: Exchange 2013 Help'
TOCTitle: ハイブリッド展開で委任されたメールボックスへのアクセス許可をサポートするように Exchange を構成する
ms:assetid: a2a10cb3-4557-4ff5-8191-c653522f4512
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Mt784505(v=EXCHG.150)
ms:contentKeyID: 74447330
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# ハイブリッド展開で委任されたメールボックスへのアクセス許可をサポートするように Exchange を構成する

 

_<strong>トピックの最終更新日:</strong>2018-01-30_

委任されたメールボックスへのアクセス許可があると、他のユーザーのメールボックスの一部を管理することができます。重役職のメールボックスおよびカレンダーの管理を行う管理アシスタントが一般的な例になります。オンプレミスの Exchange 組織と Office 365 との間のハイブリッド展開では、**フル アクセス**と、アクセス許可のある委任されたメールボックスからの**代理での送信**をサポートしています。ただし、オンプレミスの組織にインストールした Exchange のバージョンによっては、ハイブリッド展開の際に委任されたメールボックスへのアクセス許可を使用するために、追加の構成を行う必要があります。ハイブリッド展開する際の委任されたメールボックスへのアクセス許可をサポートする Exchange のバージョンと、そのバージョンに追加の構成が必要かどうかを次に示します。

  - **Exchange 2016:**  それ以上の構成は必要ありません。

  - **Exchange 2013:**  サポートされている Exchange 2013 の累積的な更新プログラム (CU) と追加の構成が必要です。

  - **Exchange 2010:**  サポートされている Exchange 2010 の更新プログラムのロールアップ (RU) と追加の構成が必要です。

ハイブリッド展開する際の委任されたメールボックスへのアクセス許可をサポートする特定の要件の詳細については、「[Exchange ハイブリッド展開のアクセス許可](permissions-in-exchange-hybrid-deployments-exchange-2013-help.md)」を参照してください。

以下のセクションでは、委任されたメールボックスへのアクセス許可をサポートするための、Exchange 2013 および Exchange 2010 のオンプレミスの展開の構成の手順を示します。これらの手順を実行する前に、最新の Exchange 2013 CU または Exchange SP3 RU を使用していることを確認する必要があります。詳細については、「[ハイブリッド展開の前提条件](hybrid-deployment-prerequisites-exchange-2013-help.md)」を参照してください。

## Exchange 2013

委任されたメールボックスへのアクセス許可のサポートを有効にするために何が必要かは、いくつかの要因によって異なります。メールボックスを Office 365 に移動した場合:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>以下がインストールされました...</th>
<th>そして、組織にある ACLable オブジェクトの同期は...</th>
<th>そのため、必要なことは...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013 CU9 以前</p></td>
<td><p>この機能は、Exchange 2013 CU9 以前では使用できません。</p></td>
<td><p>ACL をサポートするように各メールボックスを手動で構成する</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 CU10 以降</p></td>
<td><p>無効</p></td>
<td><ol>
<li><p>組織レベルで ACLable オブジェクトの同期を有効にする</p></li>
<li><p>組織レベルでの ACLable オブジェクトの同期を有効にする前に、Office 365 に移動した各メールボックスの ACL を手動で有効にします。</p></li>
</ol>
<p>組織レベルでの ACLable オブジェクトの同期を有効にした後は、Office 365 に移動したメールボックスへの追加の構成を行う必要はありません。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 2013 CU10 以降</p></td>
<td><p>有効</p></td>
<td><p>それ以上の構成は必要ありません。</p></td>
</tr>
</tbody>
</table>


## ACLable オブジェクトの同期を有効にする

組織レベルで ACLable オブジェクトの同期を有効にするには、以下を実行します。

1.  すべての AAD Connect サーバーに Azure Active Directory Connect (AAD Connect) の最新バージョンをインストールします。これは、AAD Connect がハイブリッド展開する際のアクセス許可のサポートに不可欠な属性を同期させるために必要です。AAD Connect は、[Microsoft Azure Active Directory Connect](http://go.microsoft.com/fwlink/p/?linkid=510956) からダウンロードすることができます。

2.  最新の Exchange 2013 CU または直前のバージョンの CU を実行しているサーバーで、Exchange 管理シェルを開きます。

3.  次のコマンドを実行します。
    
        Set-OrganizationConfig -ACLableSyncedObjectEnabled $True

これを実行すると、Office 365 に移動するすべてのメールボックスは、委任されたメールボックスへのアクセス許可をサポートするように正しく構成されます。これらの手順を完了する前にメールボックスを Office 365 に移動した場合は、「リモート メールボックスの ACL を有効にする」の手順を従って、これらのメールボックスの ACL を手動で有効にする必要があります。


> [!IMPORTANT]
> Acl は、Office 365 で作成されたリモートのメールボックスで有効になっていません。Office 365 では、リモート メールボックスを作成する場合は、そのリモート メールボックスの Acl を有効にするリモート メールボックス セクションでの Acl を有効にする手順を実行する必要があります。この余分な手順を避けるためには、オンプレミスの Exchange サーバー上にメールボックスを作成し、Office 365 にメールボックスを移動するお勧めします。



## リモート メールボックスの ACL を有効にする

組織レベルでの ACLable オブジェクトの同期を有効にする前に、Office 365 に移動したメールボックスの ACL を有効にするには、以下を実行します。

1.  最新の Exchange 2013 CU または直前のバージョンの CU を実行しているサーバーで、Exchange 管理シェルを開きます。

2.  単一メールボックスの ACL を有効にするには、次のコマンドを実行します。
    
        Get-AdUser <Identity> | Set-AdObject -Replace @{msExchRecipientDisplayType=-1073741818}

3.  Office 365 に移動したすべてのメールボックスの ACL を有効にするには、次のコマンドを実行します。
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid | Set-ADObject -Replace @{msExchRecipientDisplayType=-1073741818}}

4.  メールボックスが正常に更新されたことを確認するには、次のコマンドを実行します。
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid -Properties msExchRecipientDisplayType | Format-Table -AutoSize DistinguishedName, msExchRecipientDisplayType}

## Exchange 2010

Exchange 2010 SP3 サーバーは、リモート メールボックスの ACL の構成をサポートしていますが、この構成は各メールボックスで手動で設定する必要があります。新しいバージョンの Exchange とは異なり、Exchange 2010 では組織レベルでこの機能を設定することができません。以前 Office 365 に移動したメールボックスと、今後 Exchange 2010 SP3 サーバーから Office 365 に移動するすべてのメールボックスについては、以下の手順を実行する必要があります。

## リモート メールボックスの ACL を有効にする

Office 365 に移動したメールボックスの ACL を有効にするには、以下を実行します。

1.  最新の Exchange 2010 SP3 RU または直前のバージョンの RU を実行しているサーバーで、Exchange 管理シェルを開きます。

2.  単一メールボックスの ACL を有効にするには、次のコマンドを実行します。
    
        Get-AdUser <Identity> | Set-AdObject -Replace @{msExchRecipientDisplayType=-1073741818}

3.  Office 365 に移動したすべてのメールボックスの ACL を有効にするには、次のコマンドを実行します。
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid | Set-ADObject -Replace @{msExchRecipientDisplayType=-1073741818}}

4.  メールボックスが正常に更新されたことを確認するには、次のコマンドを実行します。
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid -Properties msExchRecipientDisplayType | Format-Table -AutoSize DistinguishedName, msExchRecipientDisplayType}

