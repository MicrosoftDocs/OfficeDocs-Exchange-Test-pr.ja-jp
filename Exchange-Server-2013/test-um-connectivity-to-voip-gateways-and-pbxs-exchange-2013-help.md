---
title: 'VoIP ゲートウェイと PBX への UM 接続をテストする: Exchange 2013 Help'
TOCTitle: VoIP ゲートウェイと PBX への UM 接続をテストする
ms:assetid: 2aca8631-a99a-4e29-aff0-e462385f03b2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa996906(v=EXCHG.150)
ms:contentKeyID: 56270038
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# VoIP ゲートウェイと PBX への UM 接続をテストする

 

_**適用先:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2014-09-17_

ユニファイド メッセージング (UM) と関連する接続されたテレフォニー装置の動作をテストできます。次の手順を実行すると、クライアント アクセス サーバーおよびメールボックス サーバーはボイス メール システムのエンド ツー エンドの全動作をテストします。これには、VoIP ゲートウェイ、構内交換機 (PBX)、IP PBX、およびケーブル接続などを含む、クライアント アクセス サーバーおよびメールボックス サーバーに接続されたテレフォニー コンポーネントが含まれます。

UM のトラブルシューティングに関連する他の管理タスクについては、「[UM サービス手順](um-services-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 3 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」トピックの \[メールボックス サーバー (UM サービス)\] および 「クライアント アクセス サーバー (UM 呼び出しルーター サービス)」エントリ。

  - 以下の手順を実行するには、ローカル Administrators グループのメンバーであるアカウントを使用してメールボックス サーバーにログオンする必要があります。

  - メールボックス サーバーが、クライアント アクセス サーバーと同じコンピューターまたは個別のコンピューターのどちらにインストールされているかを確認します。

  - クライアント アクセス サーバーが、メールボックス サーバーと同じコンピューターまたは個別のコンピューターのどちらにインストールされているかを確認します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## シェルを使用してユニファイド メッセージングとテレフォニー コンポーネントの動作をテストする

この例では、TCP ポート 5060 で受信 SIP 要求待ちを行うための UM IP ゲートウェイの機能をテストします。

```powershell
Test-UMConnectivity -ListenPort 5060 -UMIPGateway MyIPGateway
```

この例は、ローカルのメールボックス サーバーが、セキュリティで保護された相互 TLS 接続ではなくセキュリティで保護されていない TCP 接続を使用して、電話番号 56780 を用いて `MyUMIPGateway` という名前の UM IP ゲートウェイ経由で電話をかけることができるかどうかをテストします。

```powershell
Test-UMConnectivity -UMIPGateway MyUMIPGateway -Phone 56780 -Secured $false
```

この例は、SIP URI を使用してダイヤル プランの Outlook Voice Access 番号をテストします。ここでの例は Lync Server を含む環境で使用できます。

```powershell
Test-UMConnectivity -UMIPGateway OCSGateway1 -Phone "sip:SIPdialplan.contoso.com@contoso.com"
```


> [!NOTE]
> <CODE>-Timeout</CODE> パラメーターには、5 秒未満の値を設定することができます。ただし、このパラメーターは常に 5 秒以上の値で構成することをお勧めします。コマンド ラインの構文で <CODE>&shy;UMIPGateway</CODE> パラメーターが指定されている場合は、モード 2 を使用します。


