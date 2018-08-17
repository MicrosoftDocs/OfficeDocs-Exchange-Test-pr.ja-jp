---
title: '組織上の関係のメール ヒントの管理: Exchange Online Help'
TOCTitle: 組織上の関係のメール ヒントの管理
ms:assetid: 6e6b48ef-c41c-47ad-8063-66901765c2a5
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ649324(v=EXCHG.150)
ms:contentKeyID: 49896305
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 組織上の関係のメール ヒントの管理

 

_**適用先:** Exchange Online, Exchange Server 2013_

Exchange 管理シェルを使用して、さまざまな組織間のメール ヒントのカスタム設定を構成できます。

組織の関係を構築すると、空き時間情報データの共有、セキュリティで保護されたメッセージの流れの構成、およびメッセージの追跡の有効化などによって、両方の組織でユーザーの操作性を向上させることができます。組織の関係の詳細については、「[組織の関係にまたがるメール ヒント](mailtips-over-organization-relationships-exchange-2013-help.md)」を参照してください。

組織の関係を構築した 2 つの組織間でメール ヒントを使用する方法について、さまざまな設定を使用して制御できます。ここで説明する手順では、これらのさまざまな制御について図示します。すべての例において、社内の組織は contoso.com、リモート組織は online.contoso.com、そして組織の関係は Contoso Online という名前です。

**Set-OrganizationRelationship** コマンドレットを使用して、これらの設定を構成します。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「メール ヒント」。

  - この手順を実行するには、シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用して 2 つの組織間のメール ヒントを有効または無効にする

この例では、組織の受信者に対してメッセージを作成すると、リモート組織でメール ヒントが送信者に返されるように組織の関係を構成します。

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessEnabled $true

この例では、組織の受信者に対してメッセージを作成する場合に、リモート組織でメール ヒントが送信者に返されないように組織の関係を構成します。

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessEnabled $false

構文およびパラメーターの詳細については、「[Set-OrganizationRelationship](https://technet.microsoft.com/ja-jp/library/ee332326\(v=exchg.150\))」を参照してください。

## シェルを使用して、リモート組織に返されるメール ヒントを構成する

それぞれの組織の関係について、他の組織の送信者に返されるメール ヒントのセットを決定することができます。この例では組織の関係を構成して、すべてのメール ヒントが返されるようにします。

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel All

この例では、自動応答、最大サイズを超えるメッセージ、制限された受信者、およびメールボックスがいっぱいのメール ヒントだけが返されるように組織の関係を構成します。

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel Limited

この例では、メール ヒントが返されないように組織の関係を構成します。


> [!NOTE]
> この関係のメール ヒントを無効にするのに、このメソッドは使用しないでください。メール ヒントを無効にするには、<EM>MailTipsAccessEnabled</EM> パラメーターを <CODE>$false</CODE> に設定します。



    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel None

構文およびパラメーターの詳細については、「[Set-OrganizationRelationship](https://technet.microsoft.com/ja-jp/library/ee332326\(v=exchg.150\))」を参照してください。

## シェルを使用して、受信者に固有のメール ヒントが返されるユーザーの特定のグループを構成する

受信者に固有のメール ヒントが特定のユーザーのグループに返されるように制限できます。既定では、組織の関係用にメール ヒントを有効にすると、以下の受信者固有のメール ヒントがすべてのユーザーに返されます。:

  - 自動応答

  - メールボックスがいっぱい

  - カスタムのメール ヒント

組織の関係で、メール ヒントのアクセス グループを指定できます。グループを指定した後は、受信者固有のメール ヒントは、そのグループのメンバーのメールボックス、メールの連絡先、およびメール ユーザーにのみ返されます。この例では、ShareMailTips@contoso.com グループのメンバーにのみ、受信者固有のメール ヒントが返されるように組織の関係を構成します。

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessScope ShareMailTips@contoso.com

構文およびパラメーターの詳細については、「[Set-OrganizationRelationship](https://technet.microsoft.com/ja-jp/library/ee332326\(v=exchg.150\))」を参照してください。

