---
title: 'メールボックス サーバーで着信呼び出し数を構成する: Exchange 2013 Help'
TOCTitle: メールボックス サーバーで着信呼び出し数を構成する
ms:assetid: 419e1de9-2bf8-48a8-824d-2a536b0a6d90
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997637(v=EXCHG.150)
ms:contentKeyID: 50555765
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックス サーバーで着信呼び出し数を構成する

 

_**適用先:** Exchange Server, Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2013-02-23_

Microsoft Exchange Unified Messaging サービスを実行しているメールボックス サーバーが受け入れる着信同時接続数を構成できます。これには、Outlook Voice Access、通話応答、自動応答、および FAX 呼び出しなどのすべての着信呼び出しが含まれます。メールボックス サーバーでの同時接続数を増やすと、同時呼び出し数を減らした場合よりも多くのシステム リソースが必要になります。低速なコンピューターにユニファイド メッセージングがインストールされている場合は、同時呼び出し数を小さくすることが特に重要です。同時に受け付ける音声呼び出し数の範囲は 0 ～ 200 です。既定の設定は 100 です。

ユニファイド メッセージングとメールボックス サーバーに関連するその他のタスクについては、「[UM サービス手順](um-services-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「メールボックス サーバー (UM サービス)」。

  - クライアント アクセス サーバーおよびメールボックス サーバーが正常にインストールされていることを確認します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してメールボックス サーバー上の着信呼び出しの数を構成する

1.  EAC で <strong>サーバー</strong> \> <strong>サーバー</strong> に移動します。

2.  リスト ビューで、変更する Exchange サーバーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>Exchange Server</strong> ページで、<strong>ユニファイド メッセージング</strong> をクリックします。

4.  <strong>UM サービス設定</strong> の <strong>許可される呼び出しの最大数</strong> で、0 ～ 200 の数字を入力して <strong>保存</strong> をクリックします。

## シェルを使用してメールボックス サーバー上の着信呼び出しの数を構成する

この例では、`MyMailboxServer1` という名前のメールボックス サーバーによって受け付けることができる着信音声、Outlook Voice Access、および FAX 呼び出しの数を 50 に設定します。

```powershell
Set-UMService -Identity MyMailboxServer1 -MaxCallsAllowed 50
```

