---
title: 'Active Directory サイト間の TLS を無効にする: Exchange 2013 Help'
TOCTitle: Active Directory サイト間の TLS を無効にする
ms:assetid: 1e1a0acf-24e7-4f94-9b33-603a4e0a812c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd876856(v=EXCHG.150)
ms:contentKeyID: 52057801
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Active Directory サイト間の TLS を無効にする

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2013-02-19_

Microsoft Exchange Server 2013 では、SMTP トラフィックを圧縮する WAN 最適化コントローラー (WOC) デバイスが使用されている特定のトポロジのメールボックス サーバー間で SMTP 通信の TLS を無効にすることができます。

このトピックでは、TLS が無効になるように該当のメールボックス サーバーでトランスポート サービスを構成する方法、および Active Directory のルーティング トポロジがメッセージを正しくルーティングするように構成されていることを確認する方法について詳細に説明します。このシナリオの詳細については、「[シナリオ: WAN 最適化コントローラーをサポートするように Exchange を構成する](scenario-configure-exchange-to-support-wan-optimization-controllers-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - このタスクの予想所要時間:60 分。

  - このシナリオの各構成手順は権限が低くても完了できますが、エンドツーエンドのシナリオ タスク全体を完了するには、アカウントが組織管理役割グループのメンバーである必要があります。

  - WOC デバイスを通過する接続上の TLS のみが無効になっていることを確認してください。

  - この手順では、Exchange 2013 が複数の Active Directory サイトで展開されており、少なくとも 1 つのサイトが WAN リンクを介して他のサイトに接続されている必要があります。

  - この手順では、WAN リンク上の SMTP トラフィックを圧縮するために WOC デバイスが展開されている必要があります。

  - この手順では、WOC デバイスを展開している WAN リンク上の Exchange に対して論理メッセージ フロー パスが存在する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## 手順 1:シェルを使用して、ダウングレードされた Exchange サーバー認証を使用するように、メールボックス サーバーのトランスポート サービスを構成する

ダウングレードされた Exchange サーバー認証を使用するように、メールボックス サーバーのトランスポート サービスを構成するには、次のコマンドを実行します。

```powershell
Set-TransportService <ServerIdentity> -UseDowngradedExchangeServerAuth $true
```

この例では、Mailbox01 というサーバーでこの構成変更を行います。

```powershell
Set-TransportService Mailbox01 -UseDowngradedExchangeServerAuth $true
```

## 手順 2:対象の Active Directory サイト用に、メールボックス サーバーで専用の受信コネクタを作成する

## EAC を使用して受信コネクタを作成する

1.  Exchange 管理センター (EAC) で、<strong>メール フロー</strong> \> <strong>受信コネクタ</strong>、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") の順にクリックします。

2.  <strong>受信コネクタの新規作成</strong> ウィザードの最初のページで、次の値を入力します。
    
      - **名前**   わかりやすい値を入力します。
    
      - **種類**   内部
    
    完了したら、<strong>次へ</strong> をクリックします。

3.  <strong>受信コネクタの新規作成</strong> ウィザードの 2 番目のページの <strong>リモート設定</strong> セクションで、対象の Active Directory サイトの IP アドレスまたは IP アドレス範囲を入力します。完了したら、<strong>完了</strong> をクリックします。

## シェルを使用して受信コネクタを作成する

メールボックス サーバー上で受信コネクタを作成するには、次のコマンドを実行します。

  ```powershell
  New-ReceiveConnector -Name <Name> -Server <ServerIdentity> -RemoteIPRanges <IPAddressRange> -Internal
  ```

この例では、次の設定を使用して、WAN という受信コネクタを Mailbox01 というサーバー上に作成します。

  - *RemoteIPRanges* パラメーターは 10.0.2.0/24 に設定されています。この IP アドレスの範囲は、この受信コネクタが暗号化されていない接続を受信するリモート Active Directory サイトに対応しています。リモート サイトに複数の IP サブネットが存在する場合は、各 IP サブネットをコンマで区切って入力してください。

  - 使用法の種類は \[内部\] に設定されます。

<!-- end list -->

```powershell
New-ReceiveConnector -Name WAN -Server Hub01 -RemoteIPRanges 10.0.2.0/24 -Internal
```

## 手順 3:シェルを使用して、専用の受信コネクタで TLS を無効にする

受信コネクタで TLS を無効にするには、次のコマンドを実行します。

```powershell
Set-ReceiveConnector <ReceiveConnectorIdentity> -SuppressXAnonymousTLS $true
```

この例では、Mailbox01 というメールボックス サーバーの、WAN という受信コネクタで TLS を無効にします。

```powershell
Set-ReceiveConnector Mailbox01\WAN -SuppressXAnonymousTLS $true
```

## 手順 4:シェルを使用して Active Directory サイトをハブ サイトとして指定する

Active Directory サイトをハブ サイトとして指定するには、次のコマンドを実行します。

```powershell
Set-AdSite <ADSiteIdentity> -HubSiteEnabled $true
```

暗号化されていないトラフィックにメールボックス サーバーが関与する Active Directory サイトごとに、この手順を 1 回実行する必要があります。

この例では、Central Office Site 1 という Active Directory サイトをハブ サイトとして構成します。

```powershell
Set-AdSite "Central Office Site 1" -HubSiteEnabled $true
```

## 手順 5:シェルを使用して WAN 接続を通過する最小コスト ルーティング パスを構成する

Active Directory での IP サイト リンク コストの構成方法によっては、この手順を実行する必要がない場合もあります。展開されている WOC デバイスとのネットワーク リンクが最小コスト ルーティング パスになっていることを確認する必要があります。Active Directory サイトのリンク コストおよび Exchange 固有のサイト リンク コストを確認するには、次のコマンドを実行します。

```powershell
Get-AdSiteLink
```

展開されている WOC デバイスとのネットワーク リンクが最小コスト ルーティング パスになっていない場合は、特定の IP サイト リンクに Exchange 固有のコストを割り当て、メッセージが正しくルーティングされるようにする必要があります。この問題の詳細については、「[シナリオ: WAN 最適化コントローラーをサポートするように Exchange を構成する](scenario-configure-exchange-to-support-wan-optimization-controllers-exchange-2013-help.md)」の「Exchange 固有の Active Directory サイト リンク コストの構成」セクションを参照してください。

この例では、Branch Office 2-Branch Office 1 という IP サイト リンクで Exchange 固有のコストを 15 に構成します。

```powershell
Set-AdSiteLink "Branch Office 2-Branch Office 1" -ExchangeCost 15
```

