---
title: 'Exchange 組織のフェデレーション共有を無効または再度有効にする: Exchange 2013 Help'
TOCTitle: Exchange 組織のフェデレーション共有を無効または再度有効にする
ms:assetid: d36490d8-0268-47b9-a6d4-e56427f1b02e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657497(v=EXCHG.150)
ms:contentKeyID: 49896494
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 組織のフェデレーション共有を無効または再度有効にする

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-02-17_

状況により、組織のフェデレーション共有を一時的に無効にする必要があります。既存のフェデレーション信頼や組織の関係の削除を行い、将来的に必要になる場合があるポリシーを共有する代わりに、単にフェデレーション信頼の組織識別子 (OrgID) を無効にすることができます。


> [!NOTE]
> Office 365 とのハイブリッド展開の場合、社内サーバーのフェデレーション信頼を無効にすると、共有された予定表の空き時間情報、メール ヒント、メッセージ追跡などのハイブリッド機能も無効になります。ただし、社内組織のフェデレーション信頼が無効になっている場合、セキュリティ保護されたメール トランスポートはハイブリッド展開において無効になりません。



フェデレーション信頼の詳細については、「[フェデレーション](federation-exchange-2013-help.md)」を参照してください。フェデレーション共有の詳細については、「[共有](sharing-exchange-2013-help.md)」を参照してください。

フェデレーション共有に関連する追加の管理タスクについては、「[フェデレーションの手順](federation-procedures-exchange-2013-help.md)」を参照してください。


> [!IMPORTANT]
> Exchange Server 2013 のこの機能は、中国で 21Vianet によって運用される Office 365 との完全な互換性を備えておらず、いくつかの機能制限が適用される場合があります。詳細については、「<A href="https://go.microsoft.com/fwlink/?linkid=313640">21Vianet が運用している Office 365 について</A>」を参照してください。



## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。 「[Exchange およびシェル インフラストラクチャのアクセス許可](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)」の「*Federation and certificates* パーミッション」。

  - 他の Exchange フェデレーション組織の既存の組織上の関係および共有ポリシーは変更されず、機能しません。インターネット受信者に予定表情報へのアクセスを提供するよう構成されているポリシーの共有は影響を受けません。

  - Exchange 管理センター (EAC) を使用して、フェデレーション信頼の OrgID を無効または有効にすることはできません。シェルを使用する必要があります。

## シェルを使用してフェデレーション共有を無効化または再度有効化する

この例では OrgID を無効にし、Exchange 組織のフェデレーションおよびフェデレーション共有を無効にします。

```powershell
Set-FederatedOrganizationIdentifier -Enabled $false
```

この例では OrgID を有効にし、Exchange 組織のフェデレーションおよびフェデレーション共有を再度有効にします。

```powershell
Set-FederatedOrganizationIdentifier -Enabled $true
```

構文およびパラメーターの詳細については、「[Set-FederatedOrganizationIdentifier](https://technet.microsoft.com/ja-jp/library/dd351037\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

OrgID が無効または有効になったことは、まず、**Set-OrganizationIdentifier** コマンドレットが正常に完了したことで判断できます。

さらに正常な動作を確認するには、次の シェル コマンドを実行し、*Enabled* パラメーターに返された値を確認します。

```powershell
Get-FederatedOrganizationIdentifier
```


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。


