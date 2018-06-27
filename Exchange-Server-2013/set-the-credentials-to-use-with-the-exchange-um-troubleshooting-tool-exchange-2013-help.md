---
title: 'Exchange UM トラブルシューティング ツールで使用する資格情報を設定する: Exchange 2013 Help'
TOCTitle: Exchange UM トラブルシューティング ツールで使用する資格情報を設定する
ms:assetid: 542b7718-9345-40cc-bcb2-e307e70a1fa2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff630916(v=EXCHG.150)
ms:contentKeyID: 56270041
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange UM トラブルシューティング ツールで使用する資格情報を設定する

 

_**適用先:**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:**2016-12-09_

Microsoft Exchange 2010 UM トラブルシューティング ツールは **Test-ExchangeUMCallFlow** という名前の Exchange 管理シェル コマンドレットです。このコマンドレットを使用して、通話応答シナリオに特有な構成エラーを診断したり、社内および社内外にまたがる Microsoft Exchange Server 2010 Service Pack 1 (SP1) 以降の UM 展開の両方でボイスメールが適切に機能しているかどうかをテストしたりすることができます。このコマンドレットは、Microsoft Office の Microsoft Lync Server 2010 以降を使用した展開、または Vo IP ゲートウェイ、IP PBX、セッション ボーダー コントローラー (SBC) を使用した UM 展開で使用できます。

既定では、UM トラブルシューティング ツールを実行している場合、ツールはコンピューターのログオン時に使用される資格情報を使用します。使用される資格情報は、呼び出し元に対して指定されるものです。UM トラブルシューティング ツールを `SIPClient` モードで実行している時に使用される資格情報を設定または指定する必要があります。ただし、UM トラブルシューティング ツールを `Gateway` モードで実行している場合は、資格情報の設定は必要ありません。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 3 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」トピックの「UM サーバー」または「UM サービス」エントリ。

  - Exchange 2010 または Exchange 2013 組織が次の要件を満たしているかを確認します。
    
      - UM ダイヤル プランが作成されている。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。
    
      - UM メールボックス ポリシーが作成されている。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。
    
      - UM IP ゲートウェイが作成されている。詳細な手順については、「[UM IP ゲートウェイを作成する](create-a-um-ip-gateway-exchange-2013-help.md)」を参照してください。
    
      - Exchange 2010 UM サーバーが UM ダイヤル プランに追加されました。Exchange 2013 と Lync Server を使用している場合は、SIP URI ダイヤル プランに、すべてのクライアント アクセスおよびメールボックス サーバーを追加します。詳細な手順については、「[ダイヤル プランに UM サーバーを追加](https://go.microsoft.com/fwlink/p/?linkid=313051)」または「[メールボックス サーバーとクライアント アクセス サーバーを SIP URI ダイヤル プランに追加する](add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md)」を参照してください。

  - UM トラブルシューティング ツールをインストールします。詳細な手順については、「[Exchange UM トラブルシューティング ツールをインストールする](install-the-exchange-um-troubleshooting-tool-exchange-2013-help.md)」を参照してください。
    

    > [!IMPORTANT]
    > UM トラブルシューティング ツールを <CODE>SIPClient</CODE> モードで使用する場合、この他に Office Communications Server 2007 R2 または Microsoft&nbsp;Lync&nbsp;Server&nbsp;に関する要件と前提条件があります。詳細については、「<A href="https://go.microsoft.com/fwlink/p/?linkid=311961">チェックリスト:Office Communications Server 2007 R2 および Exchange 2010 ユニファイド メッセージングの展開</A>」または「<A href="checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md">チェックリスト: Exchange 2013 UM と Lync Server の統合</A>」を参照してください。



  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## UM トラブルシューティング ツールで使用する資格情報を設定する

1.  \[**スタート**\] メニューから、\[**Microsoft Exchange 2010 UM トラブルシューティング ツール**\] を開きます。

2.  **\[Microsoft Exchange 2010 UM トラブルシューティング ツール\]** ウィンドウのプロンプトで、次を入力し、Enter キーを押します。
    
        $cred=Get-Credential

3.  **\[Windows PowerShell 資格情報の要求\]** ウィンドウに、ドメイン\\ユーザー名およびパスワードを入力して **\[OK\]** をクリックします。

4.  **\[Microsoft Exchange 2010 UM トラブルシューティング ツール\]** ウィンドウで、呼び出しのフローのテストに必要なコマンドレットのパラメーターを指定します。次に例を示します。
    
        Test-ExchangeUMCallFlow -Mode SIPClient -CallingParty tonysmith@contoso.com - CalledParty jamiestark@contoso.com NextHop ocsfe.contoso.com -Credential $cred

