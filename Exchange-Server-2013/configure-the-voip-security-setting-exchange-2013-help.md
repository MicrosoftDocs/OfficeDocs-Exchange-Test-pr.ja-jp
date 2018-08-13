---
title: 'VoIP セキュリティ設定の構成: Exchange Online Help'
TOCTitle: VoIP セキュリティ設定の構成
ms:assetid: b5335654-c766-4f3f-883c-f31263e1d9c1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb201721(v=EXCHG.150)
ms:contentKeyID: 49896427
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# VoIP セキュリティ設定の構成

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) ダイヤル プランでボイス オーバー IP (VoIP) セキュリティを有効にすることができます。既定では、UM ダイヤル プランを作成すると、セキュリティで保護されていないモードまたは暗号化なしが使用されます。Exchange サーバーは、1 つまたは複数の UM および各種 VoIP セキュリティ設定のダイヤル プランの呼び出しに応答できます。Office 365 と Exchange Online で、セキュリティで保護されたモードは必須であり、無効にすることはできません。

UM ダイヤル プランを、セキュリティで保護されたセッション開始プロトコル (SIP) モードまたはセキュリティ保護モードを使用するように構成する場合、その UM ダイヤル プランの呼び出しに応答する Exchange サーバーは、SIP 信号トラフィック（セキュリティで保護された SIP モードの場合)、またはリアルタイム転送プロトコル (RTP) メディア チャネルと SIP 信号トラフィック (セキュリティで保護されたモードの場合) を暗号化します。


> [!IMPORTANT]
> 社内展開およびハイブリッド展開を行う際に、Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスを実行しているクライアント アクセス サーバー、または Microsoft Exchange ユニファイド メッセージング サービスを実行しているメールボックス サーバー上で SipTCPListeningPort、SipTLSListeningPort、または UMStartUpMode を構成する場合は、SIP および RTP ネットワーク トラフィックを使用できるように、Windows ファイアウォール ルールを正しく構成する必要があります。



UM ダイヤル プランに関連するその他の管理タスクについては、「[UM ダイヤル プラン手順](um-dial-plan-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ダイヤル プラン」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して UM ダイヤル プランで VoIP セキュリティを構成する

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** の順に選択し、VoIP セキュリティを変更する UM ダイヤル プランを選択して **\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページで、**\[構成\]** をクリックします。

3.  **\[全般\]** の **\[VoIP セキュリティ モード\]** で、次のオプションから 1 つを選択します。
    
      - **セキュリティで保護された SIP**
    
      - **\[セキュリティ保護なし\]** (既定)
    
      - **セキュリティで保護**

4.  **\[保存\]** をクリックします。

## シェルを使用して UM ダイヤル プランで VoIP セキュリティを構成する

この例では、SIP と RTP トラフィックの両方が暗号化されるように、`MySecureDialPlan` という UM ダイヤル プランを構成します。

    Set-UMDialPlan -identity MySecureDialPlan -VoIPSecurity Secured

この例では、SIP が暗号化され、RTP トラフィックは暗号化されないように、`MySecureDialPlan` という UM ダイヤル プランを構成します。

    Set-UMDialPlan -identity MySecureDialPlan -VoIPSecurity SIPsecured

この例では、SIP と RTP トラフィックが暗号化されないように、`MySecureDialPlan` という UM ダイヤル プランを構成します。

    Set-UMDialPlan -identity MySecureDialPlan -VoIPSecurity Unsecured

