---
title: '電子メール アドレス ポリシーの編集: Exchange 2013 Help'
TOCTitle: 電子メール アドレス ポリシーの編集
ms:assetid: cc8b36a0-95f4-43e9-bc64-87646d2e14e4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124580(v=EXCHG.150)
ms:contentKeyID: 49896479
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.EditEmailAddressPolicyWizardForm.EmailAddressPolicyIntroductionPage
ms.translationtype: HT
---

# 電子メール アドレス ポリシーの編集

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-12-10_

電子メール アドレス ポリシーは、受信者が電子メールの送受信を行えるように、受信者 (ユーザー、連絡先、およびグループを含む) のプライマリ電子メール アドレスおよびセカンダリ電子メール アドレスを生成します。

電子メール アドレス ポリシーに関連する追加の管理タスクについては、「[電子メール アドレス ポリシーの手順](email-address-policy-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - シェルでポリシーを作成した場合は、Exchange 管理センター (EAC) を使用して電子メール アドレス ポリシーを編集することはできません。

  - 受信者フィルターで電子メール アドレス ポリシーを作成した場合は、シェルを使用して電子メール アドレス ポリシーを編集する必要があります。詳細については、「[受信者フィルターを使用した電子メール アドレス ポリシーの作成](create-an-email-address-policy-by-using-recipient-filters-exchange-2013-help.md)」を参照してください。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[電子メール アドレスとアドレス帳](email-addresses-and-address-books-exchange-2013-help.md)」の「電子メール アドレス ポリシー」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!WARNING]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EAC を使用してポリシーが適用される対象の受信者を変更するには

1.  <strong>メール フロー</strong> \> <strong>Email address policies (電子メール アドレス ポリシー)</strong> に移動します。

2.  リスト ビューで、変更する電子メール アドレス ポリシーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>電子メール アドレス ポリシー</strong> で <strong>適用対象</strong> をクリックし、設定を変更します。

## EAC を使用して電子メール アドレス ポリシーの優先度を変更するには

ユーザーは、同じ電子メール アカウントに対して複数のプロキシ電子メール アドレスを持つことができます（たとえば、ayla@exchange.mail.contoso.com、ayla@contoso.com など）。これらの電子メール アドレスは、優先度ごとに適用できます。たとえば、このようなシナリオを考えてみてください。2 つの電子メール アドレス ポリシーがあり、これらに優先度 1 および優先度 2 を割り当てるとします。別のポリシーを作成した場合、これには優先度 3 が自動的に割り当てられます。ただし、2 つのポリシーがある場合に、これらの 1 つを優先度 1 として指定し、もう一方のポリシーには作成時に既定の優先度 2 が割り当てられたとします。この場合、作成する次のポリシーは、既定で優先度 2 のポリシーになります。前の優先度 2 のポリシーには、優先度 3 が割り当てられます。

1.  <strong>メール フロー</strong> \> <strong>Email address policies (電子メール アドレス ポリシー)</strong> に移動します。

2.  優先度を変更する電子メール アドレス ポリシーを選択し、<strong>優先度を上げる</strong>![上矢印アイコン](images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif "上矢印アイコン") または <strong>優先度を下げる</strong>![下矢印アイコン](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "下矢印アイコン") をクリックします。

## シェルを使用して電子メール アドレス ポリシーを編集する

この例では、現在 Georgia、Alabama、および Louisiana の受信者が含まれている電子メール アドレス ポリシー South East Offices を編集して、Texas の受信者も含めます。

```powershell
Set-EmailAddressPolicy -Identity "South East Offices" -ConditionalStateorProvince "Georgia","Alabama","Louisiana","Texas"
```


> [!NOTE]
> この電子メール アドレス ポリシーは既に Georgia、Alabama、および Louisiana の受信者に適用されていますが、パラメーターによって値が上書きされるため、パラメーターにはこれらの受信者も含める必要があります。値は既存の値に追加されません。



構文およびパラメーターの詳細については、「[Set-EmailAddressPolicy](https://technet.microsoft.com/ja-jp/library/bb124517\(v=exchg.150\))」を参照してください。

