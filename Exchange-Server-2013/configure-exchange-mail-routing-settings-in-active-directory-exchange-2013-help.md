---
title: 'Exchange のメール ルーティング設定を Active Directory で構成する: Exchange 2013 Help'
TOCTitle: Exchange のメール ルーティング設定を Active Directory で構成する
ms:assetid: d01f8545-c201-4a96-be39-ed4c7008afcf
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ674705(v=EXCHG.150)
ms:contentKeyID: 49896485
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange のメール ルーティング設定を Active Directory で構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-08_

既定では、Microsoft Exchange Server 2013 は Active Directory の IP サイト リンク オブジェクトを参照することにより、最小コストのルーティング パスを決定できます。ただし、Active Directory IP サイト リンクのコストおよびトラフィック フロー パターンが、Exchange でのメールのルーティングに最適ではないと判断される場合は、Exchange によってのみ使用される Active Directory の設定を構成して、メール フローを最適化できます。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「Active Directory サイトおよびサイト リンク管理」。

  - この手順を実行するには、シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用して、Active Directory IP サイト リンクに Exchange 固有のコストを設定する

Exchange のコストを設定する Active Directory IP サイト リンクの名前を特定します。低いコスト値は、より優先されるルートであることを示します。ルーティング テーブル ログの内容を調べ、**ADTopologyPath ID** セクション内のデータを表示することによって、2 つの Active Directory サイト間で計算された最小コストのルーティング パスの詳細を確認できます。

Active Directory サイト リンクに Exchange 固有のコストを設定するには、次のコマンドを実行します。

``` 
 Set-AdSiteLink <ADSiteLinkIdentity> -ExchangeCost <Integer | $null>
```

この例では、Exchange 固有のコスト 10 を IPSiteLinkAB という名前の IP サイト リンクに設定します。

    Set-AdSiteLink IPSiteLinkAB -ExchangeCost 10

この例では、IPSiteLinkAB という名前の IP サイト リンクから Exchange のコストをクリアします。

    Set-AdSiteLink IPSiteLinkAB -ExchangeCost $null

## 正常な動作を確認する方法

Active Directory サイト リンクに Exchange コストが正常に設定されたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
        Get-AdSiteLink | Format-List Name,ExchangeCost

2.  Active Directory サイト リンクに Exchange コストが構成されていることを確認します。

## シェルを使用して Active Directory サイトをハブ サイトとして構成

メッセージの最小コストのルーティング パス上にハブ サイトが存在する場合は、そのハブ サイトを介してメッセージをルーティングする必要があります。ルーティング テーブル ログの内容を調べて **ADTopologyPath ID** セクションのデータを参照し、選択したサイトが 2 つの Active Directory サイト間で最小コストのルーティング パスに存在するかどうかを確認します。これに該当しない場合は、Exchange 固有のコストを IP サイト リンクに割り当て、選択した 2 つのサイト間を結ぶ最も安価なルーティング パスを作成する必要があります。

Active Directory サイトをハブ サイトとして構成するには、次のコマンドを実行します。

    Set-AdSite <ADSiteIdentity> -HubSiteEnabled $true

この例では、Site A という名前の Active Directory サイトをハブ サイトとして構成します。

    Set-AdSite "Site A" -HubSiteEnabled $true

この例では、Site B という名前の Active Directory サイトからハブ サイト属性を削除します。

    Set-AdSite "Site B" -HubSiteEnabled $false

## 正常な動作を確認する方法

Active Directory サイトがハブ サイトとして正常に構成されたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
        Get-AdSite | Format-List Name,HubSiteEnabled

2.  Active Directory サイトの *HubSiteEnabled* の値が `True` であることを確認します。

