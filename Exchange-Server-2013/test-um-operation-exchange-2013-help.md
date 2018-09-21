---
title: 'UM 動作のテスト: Exchange 2013 Help'
TOCTitle: UM 動作のテスト
ms:assetid: 06c9ab4e-8272-47b1-a217-e366f7e9dbaa
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa995957(v=EXCHG.150)
ms:contentKeyID: 56270037
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM 動作のテスト

 

_**適用先:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2013-06-25_

ここではシェルを使用して、ボイス メール システムの動作をテストする方法について説明します。次の手順を実行すると、Microsoft Exchange のユニファイド メッセージング サービスが動作するメールボックス サーバーが、診断セッション開始プロトコル (SIP) の診断呼び出しを開始し、UM サーバーの稼働状態の変数を返します。

この診断テストはローカルのメールボックス サーバーでのみ実行できます。EAC を使用するメールボックス サーバーの動作をテストすることはできません。

クライアント アクセス サーバーとメールボックス サーバーに関連する追加の管理タスクについては、「[UM サービス手順](um-services-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 3 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」トピックの \[メールボックス サーバー (UM サービス)\] および 「クライアント アクセス サーバー (UM 呼び出しルーター サービス)」エントリ。

  - 以下の手順を実行するには、ローカル Administrators グループのメンバーであるアカウントを使用してメールボックス サーバーにログオンする必要があります。

  - メールボックス サーバーが、クライアント アクセス サーバーと同じコンピューターまたは個別のコンピューターのどちらにインストールされているかを確認します。

  - クライアント アクセス サーバーが、メールボックス サーバーと同じコンピューターまたは個別のコンピューターのどちらにインストールされているかを確認します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## シェルを使用してユニファイド メッセージング サービスの動作をテストする

この例では、ローカルのメールボックス サーバーで接続テストと動作テストを実行し、次にボイス オーバー IP (VoIP) 接続情報を表示します。

```powershell
Test-UMConnectivity
```

この例では、ローカル クライアント アクセス サーバーが TCP ポート 5060 上で、暗号化されていない着信 SIP 要求を待機できるかどうかをテストします。

```powershell
Test-UMConnectivity -ListenPort 5060
```

この例では、ローカル クライアント アクセス サーバーが TCP ポート 5061 上で、暗号化されている着信 SIP 要求を待機できるかどうかをテストします。

```powershell
Test-UMConnectivity -ListenPort 5061
```


> [!NOTE]
> <CODE>-UMIPGateway</CODE> パラメーターが指定されていない場合は、モード 1 を使用します。




> [!NOTE]
> <CODE>-Timeout</CODE> パラメーターには、5 秒未満の値を設定することができます。ただし、このパラメーターは常に 5 秒以上の値で構成することをお勧めします。


