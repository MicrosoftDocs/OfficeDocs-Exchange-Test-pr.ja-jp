---
title: '外部ポストマスターのアドレスを構成する: Exchange 2013 Help'
TOCTitle: 外部ポストマスターのアドレスを構成する
ms:assetid: 6b0c8675-3238-462d-8973-b52305fb90d2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb430765(v=EXCHG.150)
ms:contentKeyID: 52057836
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 外部ポストマスターのアドレスを構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

外部ポストマスター アドレスは、システムによって生成されたメッセージおよび通知が、Microsoft Exchange Server 2013 組織外に存在するメッセージ送信者に対して送信される場合に、送信者として使用されます。外部の送信者とは、組織内の承認済みドメインとして構成されていないドメインにメール アドレスを持つ送信者のことです。

既定では、外部ポストマスターのアドレスの設定値は空白になっています。この既定値により、Exchange 組織では次のような処理が行われます。

  - すべてのメールボックス サーバーおよびサブスクライブされているエッジ トランスポート サーバーでは、外部ポスト マスター アドレスは postmaster@\<*既定の承認済みドメイン*\> になる。

  - すべてのサブスクライブされていないエッジ トランスポート サーバーでは、外部ポスト マスター アドレスは postmaster@\<*Edge Transport server FQDN*\> になる。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「トランスポート構成」。

  - カスタムの外部ポストマスター アドレスを構成する場合、その値は Exchange 組織内のすべての Exchange 2013 メールボックス サーバーと Exchange 2010 ハブ トランスポート サーバーに適用されます。ただし、その値は、エッジ トランスポート サーバーにはレプリケートされません。外部ポストマスター アドレスにカスタム値を指定する場合は、エッジ トランスポート サーバーで外部ポストマスターのアドレス値を手動で構成する必要があります。

  - 組織内に Exchange 2007 ハブ トランスポート サーバーまたはエッジ トランスポート サーバーが存在する場合、**Set-TransportServer** コマンドレットを使用してそれらの各サーバーにカスタムの外部ポストマスター アドレスを構成する必要があります。詳しくは、「[外部ポストマスタのアドレスの管理](https://go.microsoft.com/fwlink/?linkid=279922)」をご覧ください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

## 必要な作業

## EAC を使用して外部ポストマスター アドレスを構成する

1.  EAC で、<strong>メール フロー</strong> \> <strong>受信コネクタ</strong> \> <strong>その他のオプション</strong>![\[その他のオプション\] アイコン](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "[その他のオプション] アイコン") \> <strong>組織のトランスポート設定</strong> \> <strong>配信</strong> の順に移動します。

2.  <strong>外部ポストマスター アドレス</strong> フィールドに、SMTP メール アドレス (たとえば、`postmaster@contoso.com`) を入力します。既定値に外部ポストマスター アドレスを返す場合は、このフィールドが空白になるように既存の値をすべて削除します。

3.  完了したら、<strong>保存</strong> をクリックします。

## シェルを使用して外部ポストマスターのアドレスを構成する

外部ポストマスターのアドレスを構成するには、次の構文を使用します。

    Set-TransportConfig -ExternalPostmasterAddress <postmaster address>

たとえば、外部ポストマスター アドレスの値を `postmaster@contoso.com` に設定するには、次のコマンドを実行します

    Set-TransportConfig -ExternalPostmasterAddress postmaster@contoso.com

外部ポストマスターのアドレスを既定値に戻すには、次のコマンドを実行します。

    Set-TransportConfig -ExternalPostmasterAddress $null

## 正常な動作を確認する方法

外部ポストマスターのアドレスが正常に構成されたことを確認するには、次の操作を行います。

1.  メールボックス サーバーで次のコマンドを実行し、外部ポストマスター アドレス値を確認します。
    
        Get-TransportConfig | Format-List ExternalPostmasterAddress

2.  外部メール アカウントから Exchange 組織にメッセージを送信します。これにより Exchange 組織は配信状態通知 (DSN) を生成します。たとえば、トランスポート ルールを構成して、特定のキーワードを含む送信者からのメッセージに対して、配信不能レポート (NDR) を送信することができます。DSN にある送信者のメール アドレスと、指定した値が一致することを確認します。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

