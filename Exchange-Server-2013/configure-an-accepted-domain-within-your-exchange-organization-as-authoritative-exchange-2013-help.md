---
title: 'Exchange 組織内の承認済みドメインを権限ありとして構成する: Exchange 2013 Help'
TOCTitle: Exchange 組織内の承認済みドメインを権限ありとして構成する
ms:assetid: e182d54f-e58a-47ba-a5c1-28c0dfa86eed
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657734(v=EXCHG.150)
ms:contentKeyID: 49896524
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 組織内の承認済みドメインを権限ありとして構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-02-17_

組織に属するドメインが、SMTP 名前空間内のすべての受信者のメールボックスをホストする場合、そのドメインには権限があると見なされます。既定では、1 つの承認済みドメインが Exchange 組織の権限のあるドメインとして構成されます。組織に複数の SMTP 名前空間がある場合は、複数の承認済みドメインを権限のあるドメインとして構成できます。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「承認済みドメイン」。

  - 境界ネットワークでエッジ トランスポート サーバーを購読している場合は、Exchange 組織内のメールボックス サーバーに承認済みドメインを構成します。承認済みドメインの構成は、EdgeSync 同期の際にエッジ トランスポート サーバーにレプリケートされます。詳細については、「[エッジ サブスクリプション](edge-subscriptions-exchange-2013-help.md)」を参照してください。

  - 既に構成されているリモート ドメインと同じ名前を持つ承認済みドメインを作成することはできません。たとえば、fabrikam.com をリモート ドメインとして構成している場合、fabrikam.com の承認済みドメインを作成することはできません。

  - 承認済みドメインを構成する前に、その SMTP 名前空間のパブリック ドメイン ネーム システム (DNS) の MX リソース レコードが存在すること、およびその MX リソース レコードが Exchange 組織に関連付けられているサーバー名と IP アドレスを参照していることを確認する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## EAC を使用して承認済みドメインを権限のあるドメインとして構成する

Exchange 組織の承認済みドメインが、ドメインの SMTP 名前空間内の受信者のすべてのメールボックスをホストする場合は、そのドメインを権限のあるドメインとして構成することが必要な場合があります。

1.  EAC で、<strong>メール フロー</strong> \> <strong>承認済みドメイン</strong> に移動し、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  <strong>名前</strong> フィールドに、承認済みドメインの表示名を入力します。組織の各承認済みドメインには一意の表示名が必要です。これは、承認済みドメインとは異なる場合があります。たとえば、ドメイン contoso.com の表示名が Contoso Local Accepted Domain になることがあります。

3.  <strong>承認済みドメイン</strong> フィールドに、承認済みドメインを入力します。組織が電子メール メッセージを受け取る SMTP 名前空間を指定します。(Contoso.com など)。

4.  <strong>権限あり</strong> を選択します。これは、SMTP 名前空間内のすべての受信者のメールボックスをホストする承認済みドメインの Exchange 組織内のサーバーに電子メールが中継される場合のオプションです。

5.  <strong>保存</strong> をクリックします。


> [!TIP]
> 既に作成されている承認済みドメインを構成するには、承認済みドメイン一覧からドメインを選択し、<STRONG>[編集]</STRONG><IMG title=編集アイコン alt=編集アイコン src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif"> をクリックします。複数のドメインを権限のあるドメインとして構成できます。



## 正常な動作を確認する方法

新しい承認済みドメインは、EAC の承認済みドメイン一覧に表示されます。承認済みドメインが権限のあるドメインとして正常に構成されたことを確認するには、そのドメインにメールを送信し、メールが受信されることを確認します。

