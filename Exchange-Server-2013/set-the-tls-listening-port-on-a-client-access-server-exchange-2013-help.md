---
title: 'クライアント アクセス サーバーで TLS リスニング ポートを設定する: Exchange 2013 Help'
TOCTitle: クライアント アクセス サーバーで TLS リスニング ポートを設定する
ms:assetid: f4401923-61fa-4dc5-95f8-c0d2f515b2ea
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ673576(v=EXCHG.150)
ms:contentKeyID: 50555900
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# クライアント アクセス サーバーで TLS リスニング ポートを設定する

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2013-02-17_

Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスを実行するクライアント アクセス サーバー上で SIP 要求を待機するために使用されるトランスポート層セキュリティ (TLS) ポートを構成できます。既定では、クライアント アクセス サーバーのインストール時に、SIP TLS リスニング ポート番号が 5061 に設定されます。

次の設定を行うために、TLS リスニング ポートを 5061 に構成する必要がある場合があります。

  - UM ダイヤル プランの VoIP セキュリティ設定をセキュリティ保護された SIP に設定する。

  - UM ダイヤル プランの VoIP セキュリティ設定をセキュリティ保護ありに設定する。

  - MicrosoftOffice Communications Server 2007 R2 または Microsoft Lync Server と統合する。

  - 相互トランスポート層セキュリティ (相互 TLS) を使用して、クライアント アクセス サーバー、Microsoft Exchange ユニファイド メッセージング サービスを実行するメールボックス サーバー、および VoIP ゲートウェイ、セッション開始プロトコル (SIP) が有効な構内交換機 (PBX)、IP PBX、またはセッション ボーダー コントローラー (SBC) 間でネットワーク データを暗号化する。

UM IP ゲートウェイとセキュリティ保護された SIP モードまたはセキュリティ保護されたモードで動作するダイヤル プラン間で相互 TLS を使用する場合は、UM IP ゲートウェイを作成する際に、完全修飾ドメイン名 (FQDN) を使用して構成した後に UM IP ゲートウェイを TLS ポート 5061 で待機するように構成する必要があります。また、VoIP ゲートウェイ、SIP が有効な PBX、IP PBX、または SBC が相互 TLS 要求をポート 5061 で待機するように構成されていることを確認する必要もあります。

クライアント アクセス サーバーの TCP および TLS ポートのみを構成できます。Exchange 2013 メールボックス サーバーのポートを構成することはできません。ただし、**Set-UMService** コマンドレットを使用することで、Exchange 2010 UM サーバーの TCP および TLS のリスニング ポートを構成できます。

ユニファイド メッセージング サーバーおよびクライアント アクセス サーバーに関連する追加のタスクについては、「[UM サービス手順](um-services-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「クライアント アクセス サーバー (UM 呼び出しルーター サービス)」。

  - クライアント アクセス サーバーおよびメールボックス サーバーが正常にインストールされていることを確認します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して、クライアント アクセス サーバーの TLS リスニング ポートを構成する

1.  EAC で <strong>サーバー</strong> \> <strong>サーバー</strong> に移動します。

2.  リスト ビューで、変更する Exchange サーバーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>Exchange Server</strong> ページで、<strong>ユニファイド メッセージング</strong> をクリックします。

4.  <strong>UM サービス設定</strong> の <strong>TLS リスニング ポート</strong> に TLS ポートの番号を入力し、<strong>保存</strong> をクリックします。

## シェルを使用して、クライアント アクセス サーバーの TLS リスニング ポートを構成する

この例では、`MyClientAccessServer` というクライアント アクセス サーバー上の TLS リスニング ポートを 5561 に設定します。

```powershell
Set-UMCallRouterSettings -Server MyClientAccessServer -SipTlsListeningPort 5561
```

