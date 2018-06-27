---
title: 'リモート ドメインを管理する: Exchange 2013 Help'
TOCTitle: リモート ドメインを管理する
ms:assetid: 41a86907-bd9e-40d0-94d3-6deb95a0bffa
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997639(v=EXCHG.150)
ms:contentKeyID: 52057409
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.NewRemoteDomainWizardForm.NewRemoteDomainWizardPage
ms.translationtype: HT
---

# リモート ドメインを管理する

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-04-13_

リモート ドメインとは、Microsoft Exchange 組織の外部にある SMTP ドメインのことです。リモート ドメイン エントリを作成して、Exchange 組織と特定の外部ドメイン間で転送されるメッセージの設定を定義できます。特定の外部ドメイン用のリモート ドメイン エントリの設定は、通常すべての外部受信者に適用される、既定のリモート ドメインの設定より優先されます。リモート ドメイン設定は、Exchange 組織に対してグローバルに適用されます。

リモート ドメイン エントリを削除した場合、メッセージ転送の設定はリモート ドメインに送信されるメッセージには適用されなくなります。リモート ドメイン エントリを削除しても、リモート ドメインへのメール フローは無効になりません。リモート ドメイン エントリが削除された後、既定のリモート ドメインの構成設定が、そのドメインに送信される新しいメッセージに適用されます。既定のリモート ドメインは削除できません。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:10 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「リモート ドメイン」。

  - この手順を実行するには、シェルを使用する必要があります。

  - 組織の承認済みドメインとして構成されたアドレス スペース用のリモート ドメインは作成できません。たとえば、組織が fabrikam.com のメールを受け入れている場合、fabrikam.com のリモート ドメインを作成できません。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 実行内容

## シェルを使用してリモート ドメインを作成する

新しいリモート ドメイン エントリを作成するには、次の構文を使用します。

    New-RemoteDomain -Name <Descriptive Name> -DomainName <SMTP address space>

この例では、contoso.com ドメインに送信されるメッセージのリモート ドメイン エントリを作成します。

    New-RemoteDomain -Name Contoso -DomainName contoso.com

この例では、fabrikam.com ドメインとすべてのサブドメインに送信されるメッセージのリモート ドメイン エントリを作成します。

    New-RemoteDomain -Name Fabrikam -DomainName *.fabrikam.com

## 正常な動作を確認する方法

リモート ドメインが正常に作成されたことを確認するには、次の手順を実行します。

1.  **Get-RemoteDomain** コマンドを実行して、リモート ドメインが一覧表示されていることを確認します。

2.  `Get-RemoteDomain <Remote Domain Name> | Format-List` コマンドを実行して、新しいリモート ドメインの設定を確認します。新しいリモート ドメイン エントリで指定されたアドレス スペース内の受信者にテスト メッセージを送信し、そのメッセージ設定が新しいリモート ドメイン エントリで指定された設定と一致するかどうかを確認します。

## シェルを使用してリモート ドメインを構成する

リモート ドメイン エントリの設定を構成するには、**Set-RemoteDomain** コマンドレットを使用します。自動返信、メッセージの形式とエンコード、およびその他のメッセージ設定に関連する多数の異なる設定があります。詳細については、「[Set-RemoteDomain](https://technet.microsoft.com/ja-jp/library/aa997857\(v=exchg.150\))」を参照してください。

特定のシナリオに対応するリモート ドメインを構成するには、次のトピックを参照してください。

  - [リモート ドメインの不在時の応答の構成](configure-remote-domain-out-of-office-replies-exchange-2013-help.md)

  - [リモート ドメインの自動応答の構成](configure-remote-domain-automatic-replies-exchange-2013-help.md)

  - [リモート ドメインのメッセージ レポート作成の構成](configure-remote-domain-message-reporting-exchange-2013-help.md)

## シェルを使用してリモート ドメインを削除する

リモート ドメイン エントリを削除するには、次の構文を使用します。

    Remove-RemoteDomain <RemoteDomainName>

この例では、Contoso という名前のリモート ドメイン エントリを削除します。

    Remove-RemoteDomain Contoso

## 正常な動作を確認する方法

リモート ドメインが正常に削除されたことを確認するには、次の手順を実行します。

1.  **Get-RemoteDomain** コマンドを実行して、リモート ドメインが一覧表示されていないことを確認します。

2.  `Get-RemoteDomain Default | Format-List` コマンドを実行して、既定のリモート ドメインの設定を確認します。削除したリモート ドメインで指定されたアドレス スペース内の受信者にテスト メッセージを送信し、そのメッセージ設定が既定のリモート ドメインで指定された設定と一致するかどうかを確認します。

