---
title: 'クライアント アクセス サーバーのスタートアップ モードを構成する: Exchange 2013 Help'
TOCTitle: クライアント アクセス サーバーのスタートアップ モードを構成する
ms:assetid: 71cc9061-9e3c-4b4a-8dbe-f590ca5bcee8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ673533(v=EXCHG.150)
ms:contentKeyID: 50555811
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# クライアント アクセス サーバーのスタートアップ モードを構成する

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2013-02-15_

Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービス用のスタートアップ モードは、クライアント アクセス サーバー上で指定できます。既定で、クライアント アクセス サーバーは TCP モードで起動しますが、トランスポート層セキュリティ (TLS) を使用してボイス オーバー IP (VoIP) トラフィックを暗号化している場合、TLS モードまたはデュアル モードを使用するようクライアント アクセス サーバーを構成する必要があります。スタートアップ モードとしてデュアルを使用するようにクライアント アクセス サーバーを構成することをお勧めします。これは、すべてのクライアント アクセス サーバーおよびメールボックス サーバーは、すべての UM ダイヤル プランの着信呼び出しに応答でき、これらのダイヤル プランには別々のセキュリティ設定を適用できるためです。スタートアップ モードを変更した場合、Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスを再起動して変更を有効にする必要があります。


> [!IMPORTANT]
> 既定では、クライアント アクセス サーバーを使用して着信呼び出しに応答できます。UM を Microsoft Office Communications Server 2007 R2 または Microsoft Lync Server と統合する場合を除き、UM 呼び出しを処理するためにクライアント アクセス サーバーを UM ダイヤル プランに追加する必要はありません。



ユニファイド メッセージング サーバーとクライアント アクセス サーバーに関連するその他の管理タスクについては、「[UM サービス手順](um-services-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「クライアント アクセス サーバー (UM 呼び出しルーター サービス)」。

  - クライアント アクセス サーバーが、メールボックス サーバーと同じコンピューターまたは個別のコンピューターのどちらにインストールされているかを確認します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してクライアント アクセス サーバー上のスタートアップ モードを構成する

1.  EAC で **\[サーバー\]** \> **\[サーバー\]** に移動します。

2.  リスト ビューで、変更する Exchange サーバーを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[Exchange Server\]** ページで、**\[ユニファイド メッセージング\]** をクリックします。

4.  **\[UM 呼び出しルーターの設定\]** の **\[UM スタートアップ モード\]** で、ドロップダウン リストから次のいずれかを選択します。
    
      - **\[TCP\]**   mTLS を使用せず、セキュリティで保護されていないダイヤル プランのみを使用する場合は、このオプションを使用します。
    
      - **\[TLS\]**   mTLS を使用して、セキュリティで保護された SIP ダイヤル プランまたはセキュリティで保護されたダイヤル プランのみを使用する場合は、このオプションを使用します。
    
      - **\[デュアル\]**   mTLS を使用して、セキュリティで保護されていないダイヤル プラン、セキュリティで保護された SIP ダイヤル プラン、およびセキュリティで保護されたダイヤル プランを使用する場合は、このオプションを使用します。

5.  UM スタートアップ モードを選択し、**\[保存\]** をクリックします。

## シェルを使用して、クライアント アクセス サーバー上でのスタートアップ モードを構成する

この例では、`UMCallRouter1` という名前のクライアント アクセス サーバーのスタートアップ モードをデュアル モードに設定します。

    Set-UMCallRouterSettings -Server UMCallRouter1 -UMStartUpMode Dual

この例では、`UMCallRouter1` という名前のクライアント アクセス サーバーのスタートアップ モードを TLS モードに設定します。

    Set-UMCallRouterSettings -Server UMCallRouter1 -UMStartUpMode TLS

