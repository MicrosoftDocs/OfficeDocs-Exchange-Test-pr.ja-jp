---
title: 'メールボックス サーバーのスタートアップ モードを構成する: Exchange 2013 Help'
TOCTitle: メールボックス サーバーのスタートアップ モードを構成する
ms:assetid: 4457d6a0-52bd-4269-8cb5-d34d7fe9bfc3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee423544(v=EXCHG.150)
ms:contentKeyID: 50555767
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックス サーバーのスタートアップ モードを構成する

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2013-02-15_

Microsoft Exchange Unified Messaging サービス用のスタートアップ モードは、メールボックス サーバー上で指定できます。既定で、メールボックス サーバーは TCP モードで起動しますが、トランスポート層セキュリティ (TLS) を使用してボイス オーバー IP (VoIP) トラフィックを暗号化している場合、TLS またはデュアル モードを使用するようにメールボックス サーバーを構成する必要があります。メールボックス サーバーはスタートアップ モードとしてデュアルを使用するように構成することをお勧めします。こうすることで、すべてのクライアント アクセス サーバーとメールボックス サーバーがすべての UM ダイヤル プランの着信呼び出しに応答でき、それらのダイヤル プランを異なるセキュリティ (セキュリティ保護なし、セキュリティ保護された SIP、またはセキュリティ保護あり) に設定できるためです。スタートアップ モードを変更した場合、Microsoft Exchange ユニファイド メッセージング サービスを再起動して変更を有効にする必要があります。


> [!IMPORTANT]
> 既定では、メールボックス サーバーを着信呼び出しの応答に使用できます。UM と Microsoft Office Communications Server 2007 R2 または Microsoft Lync Server を統合している場合を除いて、UM 呼び出しを処理するためにメールボックス サーバーを UM ダイヤル プランに追加する必要はありません。



ユニファイド メッセージングとメールボックス サーバーに関するその他の管理タスクについては、「[UM サービス手順](um-services-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「メールボックス サーバー (UM サービス)」。

  - メールボックス サーバーがクライアント アクセス サーバーと同じコンピューターにインストールされているか、または別のコンピューターにインストールされているかを確認します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してメールボックス サーバー上のスタートアップ モードを構成する

1.  EAC で <strong>サーバー</strong> \> <strong>サーバー</strong> に移動します。

2.  リスト ビューで、変更する Exchange サーバーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>Exchange Server</strong> ページで、<strong>ユニファイド メッセージング</strong> をクリックします。

4.  <strong>UM サービス設定</strong> の <strong>UM スタートアップ モード</strong> で、ドロップダウン リストから次のいずれかを選択します。
    
      - <strong>TCP</strong>   mTLS を使用せず、セキュリティで保護されていないダイヤル プランのみを使用する場合は、このオプションを使用します。
    
      - <strong>TLS</strong>   mTLS を使用して、セキュリティで保護された SIP ダイヤル プランまたはセキュリティで保護されたダイヤル プランのみを使用する場合は、このオプションを使用します。
    
      - <strong>デュアル</strong>   mTLS を使用して、セキュリティで保護されていないダイヤル プラン、セキュリティで保護された SIP ダイヤル プラン、およびセキュリティで保護されたダイヤル プランを使用する場合は、このオプションを使用します。

5.  UM スタートアップ モードを選択し、<strong>保存</strong> をクリックします。

## シェルを使用してメールボックス サーバー上のスタートアップ モードを構成する

この例では、`MyUMServer1` という名前のメールボックス サーバーのスタートアップ モードをデュアル モードに設定します。
```powershell
    Set-UMService -Identity MyUMServer1 -UMStartUpMode Dual
```

この例では、`MyUMServer1` という名前のメールボックス サーバーのスタートアップ モードを TLS モードに設定します。
```powershell
    Set-UMService -Identity MyUMServer1 -UMStartUpMode TLS
```
