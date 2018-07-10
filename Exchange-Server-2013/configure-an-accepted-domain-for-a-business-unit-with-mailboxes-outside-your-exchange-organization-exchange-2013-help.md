---
title: 'Exchange 組織外のメールボックスで部署用に承認済みドメインを構成する: Exchange 2013 Help'
TOCTitle: Exchange 組織外のメールボックスで部署用に承認済みドメインを構成する
ms:assetid: ff46310b-5392-4eac-97bc-d39d397e1ce1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657737(v=EXCHG.150)
ms:contentKeyID: 49896572
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 組織外のメールボックスで部署用に承認済みドメインを構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-08-06_

状況によっては、Exchange 組織内部で承認済みドメインを構成する対象が、ドメインに属する一部またはすべての受信者がメールボックスを持っていないビジネス単位になることがあります。このようなケースは、たとえば、組織が複数の異なる電子メール システム間で同じ SMTP アドレス スペースを共有している場合に発生します。そのような状況では、承認済みドメインを内部の中継ドメインとして構成できます。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「承認済みドメイン」。

  - 境界ネットワークでエッジ トランスポート サーバーを購読している場合は、Exchange 組織内のメールボックス サーバーに承認済みドメインを構成します。承認済みドメインの構成は、EdgeSync 同期の際にエッジ トランスポート サーバーにレプリケートされます。詳細については、「[エッジ サブスクリプション](edge-subscriptions-exchange-2013-help.md)」を参照してください。

  - 承認済みドメインを構成する前に、その SMTP 名前空間のパブリック ドメイン ネーム システム (DNS) の MX リソース レコードが存在すること、およびその MX リソース レコードが Exchange 組織に関連付けられているサーバー名と IP アドレスを参照していることを確認する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## EAC を使用して、承認済みドメインを内部の中継ドメインとして構成する

1.  EAC で、**\[メール フロー\]** \> **\[承認済みドメイン\]** に移動して、構成するドメインを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[名前\]** フィールドに、承認済みドメインの表示名を入力します。組織の各承認済みドメインには一意の表示名が必要です。これは、承認済みドメインとは異なる場合があります。たとえば、ドメイン Contoso.com の表示名が Contoso Local Accepted Domain になることがあります。

3.  **\[内部の中継ドメイン\]** を選択します。

4.  **\[保存\]** をクリックします。

## 正常な動作を確認する方法

承認済みドメインを内部の中継ドメインとして正常に構成したことを確認するには、内部中継ドメインから Exchange 組織内のメールボックスにメッセージを送信して受信を確認します。

