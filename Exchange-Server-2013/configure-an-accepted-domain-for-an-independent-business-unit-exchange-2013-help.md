---
title: '独立した部署の承認済みドメインの構成: Exchange 2013 Help'
TOCTitle: 独立した部署の承認済みドメインの構成
ms:assetid: bc95dbdc-3669-4c06-ab94-90093bc0dbfd
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657491(v=EXCHG.150)
ms:contentKeyID: 49896445
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 独立した部署の承認済みドメインの構成

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-02-17_

場合によっては、Exchange 組織外部の電子メール サーバーを使用して、独立した部署の承認済みドメインを構成する場合もあります。このような場合は、承認済みドメインを外部の中継ドメインとして構成できます。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「承認済みドメイン」。

  - 境界ネットワークでエッジ トランスポート サーバーを購読している場合は、Exchange 組織内のメールボックス サーバーに承認済みドメインを構成します。承認済みドメインの構成は、EdgeSync 同期の際にエッジ トランスポート サーバーにレプリケートされます。詳細については、「[エッジ サブスクリプション](edge-subscriptions-exchange-2013-help.md)」を参照してください。

  - 既に構成されているリモート ドメインと同じ名前を持つ承認済みドメインを作成することはできません。たとえば、fabrikam.com をリモート ドメインとして構成している場合、fabrikam.com の承認済みドメインを作成することはできません。

  - 承認済みドメインを構成する前に、その SMTP 名前空間のパブリック ドメイン ネーム システム (DNS) の MX リソース レコードが存在すること、およびその MX リソース レコードが Exchange 組織に関連付けられているサーバー名と IP アドレスを参照していることを確認する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## EAC を使用して承認済みドメインを外部の中継ドメインとして構成する

Exchange 組織外部の電子メール サーバーを使用して部署の承認済みドメインを構成する場合もあります。

1.  EAC で、<strong>メール フロー</strong> \> <strong>承認済みドメイン</strong> と移動し、構成したいドメインを選択して <strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  <strong>名前</strong> フィールドに、承認済みドメインの表示名を入力します。組織の各承認済みドメインには一意の表示名が必要です。これは、承認済みドメインとは異なる場合があります。たとえば、ドメイン Contoso.com の表示名が Contoso Local Accepted Domain になることがあります。

3.  <strong>外部の中継ドメイン</strong> を選択します。このオプションでは、電子メールが Exchange 外部のサーバーに中継されます。

4.  <strong>保存</strong> をクリックします。

## 正常な動作を確認する方法

承認済みドメインが外部の中継ドメインとして正常に構成されたことを確認するには、外部の中継ドメインとして構成された承認済みドメインからメッセージを送信し、それが受信されることを確認します。

