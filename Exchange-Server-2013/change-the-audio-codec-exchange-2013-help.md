---
title: 'オーディオ コーデックの変更: Exchange Online Help'
TOCTitle: オーディオ コーデックの変更
ms:assetid: 139b2ccd-28c5-46c0-9050-777f4f59aade
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa996342(v=EXCHG.150)
ms:contentKeyID: 49895260
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# オーディオ コーデックの変更

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージングでは、4 つのコーデックのいずれかを使用してボイス メール メッセージを作成できます。MP3、Windows Media Audio (WMA)、Group System Mobile (GSM) 06.10、および G.711 パルス符号変調 (PCM) リニアのいずれかを使用できます。既定では、ユニファイド メッセージング (UM) ダイヤル プランを作成すると、ボイス メッセージを記録するために MP3 オーディオ コーデックが使用されます。MP3 オーディオ形式は、複数のオペレーティング システム、電子メール クライアント、および MP3 プレーヤーで使用される一般的なオーディオ形式です。UM ダイヤル プランを作成した後で、WMA、GSM 06.10、または G.711 リニア PCM オーディオ コーデックなど他のオーディオ形式のいずれかを使用して、UM ダイヤル プランを構成できます。ボイス メッセージを聞くには、携帯電話またはコンピューターが互換性のあるオーディオ ソフトウェア アプリケーションをインストールしている必要があります。

UM ダイヤル プランに関連するその他のタスクについては、「[UM ダイヤル プラン手順](um-dial-plan-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ダイヤル プラン」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してユニファイド メッセージング ダイヤル プランのオーディオ コーデックを変更する

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。

2.  リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[UM ダイヤル プラン\]** ページで、**\[構成\]** をクリックします。

4.  **\[設定\]** の **\[オーディオ コーデック\]** の下で、ドロップダウン リストを使用して次のいずれかを選択します。
    
      - MP3
    
      - WMA
    
      - GSM
    
      - G711

5.  **\[保存\]** をクリックします。

## シェルを使用して、ユニファイド メッセージング ダイヤル プランのオーディオ コーデックを変更する

この例では、`MyUMDialPlan` という名前の UM ダイヤル プランのオーディオ コーデックを G.711 に設定します。

    Set-UMDialPlan -Identity MyUMDialPlan -AudioCodec G711

この例では、`MyUMDialPlan` という名前の UM ダイヤル プランのオーディオ コーデックを WMA に設定します。

    Set-UMDialPlan -Identity MyUMDialPlan -AudioCodec Wma

