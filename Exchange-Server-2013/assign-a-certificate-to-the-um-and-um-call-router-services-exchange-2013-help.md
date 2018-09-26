---
title: 'UM および UM 呼び出しルーター サービスへの証明書の割り当て: Exchange 2013 Help'
TOCTitle: UM および UM 呼び出しルーター サービスへの証明書の割り当て
ms:assetid: 8a900e5f-9779-4213-92d7-ec157b15fbc5
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn205140(v=EXCHG.150)
ms:contentKeyID: 54652977
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM および UM 呼び出しルーター サービスへの証明書の割り当て

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2013-04-29_

EAC またはシェルを使って特定の Exchange サービスに対して、自己署名型内部公開キー基盤 (PKI) またはサードパーティーの商用証明書を割り当てることができます。**New-ExchangeCertificate** コマンドレットで *Services* パラメーターを使って Exchange サービスに証明書を割り当てた場合、Exchange サービスに証明書を割り当てるように求められます。EAC を使って証明書を作成した場合、Exchange 証明書の新規作成ウィザードから、Exchange サービスに証明書を割り当てるように求められることはありません。証明書のプロパティを編集し、証明書を割り当てるサービスを選択して証明書を割り当てる必要があります。

サービスが異なれば、証明書の要件も異なります。たとえば、証明書の <strong>サブジェクト名</strong> または <strong>サブジェクトの別名</strong> ボックスにサーバー名だけが含まれていればよいサービスもあれば、完全修飾ドメイン名 (FQDN) が必要なサービスもあります。証明書名が、有効にするサービスに必要な使用法をサポートできることを確認してください。


> [!NOTE]
> ユニファイド メッセージング (UM) と Microsoft Lync Server を統合している場合、自己署名証明書は使えません。



ユニファイド メッセージングの証明書の管理に関するその他の管理タスクについては、「[UM の証明書の展開手順](deploying-certificates-for-um-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[Exchange およびシェル インフラストラクチャのアクセス許可](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)」の「証明書管理」と「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM サービス」。コンピューターのローカルの Administrators グループのメンバーであるアカウントを使用してログオンしていることを確認する必要もあります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使ったユニファイド メッセージングと UM 呼び出しルーター サービスへの証明書の割り当て

1.  EAC で、<strong>サーバー</strong> \> <strong>証明書</strong> の順に移動します。

2.  リスト ビューで、ユニファイド メッセージングと UM 呼び出しルーター サービスに割り当てる証明書を選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  \[*\<証明書名\>*\] ページで <strong>サービス</strong> を選択した後、<strong>UM</strong> と <strong>UM 呼び出しルーター</strong> を選択します。

4.  <strong>保存</strong> をクリックします。

## シェルを使ったユニファイド メッセージングと UM 呼び出しルーター サービスへの証明書の割り当て

この例では、ユニファイド メッセージングと UM 呼び出しルーター サービスへ証明書を割り当てます。

  ```powershell
  Enable-ExchangeCertificate -Thumbprint 5113ae0233a72fccb75b1d0198628675333d010e -Services 'UM, UMCallRouter'
  ```

