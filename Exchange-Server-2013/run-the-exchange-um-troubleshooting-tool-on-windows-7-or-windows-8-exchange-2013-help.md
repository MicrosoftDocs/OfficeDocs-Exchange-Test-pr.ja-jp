---
title: 'Windows 7 または Windows 8 で Exchange UM トラブルシューティング ツールを実行する: Exchange 2013 Help'
TOCTitle: Windows 7 または Windows 8 で Exchange UM トラブルシューティング ツールを実行する
ms:assetid: 98d6869d-ee4a-4088-849d-ef75b0f5d932
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff851872(v=EXCHG.150)
ms:contentKeyID: 56270074
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Windows 7 または Windows 8 で Exchange UM トラブルシューティング ツールを実行する

 

_**適用先:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2016-12-09_

Microsoft Exchange 2010 UM トラブルシューティング ツールは **Test-ExchangeUMCallFlow** という名前の Exchange 管理シェル コマンドレットです。このコマンドレットを使用して、通話応答シナリオに特有な構成エラーを診断したり、社内および社内外にまたがる Microsoft Exchange Server 2010 Service Pack 1 (SP1) 以降の UM 展開の両方でボイスメールが適切に機能しているかどうかをテストしたりすることができます。このコマンドレットは、Microsoft Office の Microsoft Lync Server 2010 以降を使用した展開、または Vo IP ゲートウェイ、IP PBX、セッション ボーダー コントローラー (SBC) を使用した UM 展開で使用できます。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 3 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」トピックの「UM サーバー」または「UM サービス」エントリ。

  - Exchange 2010 または Exchange 2013 組織が次の要件を満たしているかを確認します。
    
      - UM ダイヤル プランが作成されている。詳細な手順については、「[UM ダイヤル プランを作成する](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)」を参照してください。
    
      - UM メールボックス ポリシーが作成されている。詳細な手順については、「[UM メールボックス ポリシーの作成](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/set-up-voice-mail/create-um-mailbox-policy)」を参照してください。
    
      - UM IP ゲートウェイが作成されている。詳細な手順については、「[UM IP ゲートウェイを作成する](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-ip-gateway)」を参照してください。
    
      - Exchange 2010 UM サーバーが UM ダイヤル プランに追加されました。Exchange 2013 と Lync Server を使用している場合は、SIP URI ダイヤル プランに、すべてのクライアント アクセスおよびメールボックス サーバーを追加します。詳細な手順については、「[ダイヤル プランに UM サーバーを追加](https://go.microsoft.com/fwlink/p/?linkid=313051)」または「[メールボックス サーバーとクライアント アクセス サーバーを SIP URI ダイヤル プランに追加する](add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md)」を参照してください。

  - Exchange 2013 メールボックス サーバーで Exchange 2010 SP1 以降を使用して、ローカル UM サーバーで UM トラブルシューティング ツールを実行している場合は、以下に示されている前提条件の一部のインストールが不要になります。それらは、UM サーバーの役割と共に既にインストールされている可能性があります。ただし、UM サーバーの役割を実行しているサーバー以外の 64 ビット コンピューターに UM トラブルシューティング ツールをインストールしている場合は、以下のコンポーネントをインストールする必要があります。
    
      - Microsoft .NET Framework 3.5 Service Pack 1 (SP1)  「[Microsoft .NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=152380)」を参照してください。
    
      - ツールが Windows Vista または Windows Server 2008 コンピューターで実行される場合は、「[Windows Vista x64 および Windows Server 2008 x64 用 Microsoft .NET Framework 3.5 ファミリの更新プログラム](https://go.microsoft.com/fwlink/?linkid=178998)」を参照してください。
    
      - Windows リモート管理 (WinRM) 2.0 および Windows PowerShell V2 (Windows6.0-KB968930.msu)   マイクロソフト サポート技術情報の文書番号 968930「[Windows Management Framework Core パッケージ (Windows PowerShell 2.0 および WinRM 2.0)](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930)」を参照してください。
    
      - Microsoft Unified Communications Managed API 2.0 Core ランタイム (UcmaRuntimeWebDownloadX64.msi)。  「[Unified Communications Managed API 2.0 Core ランタイム (64-bit)](https://go.microsoft.com/fwlink/p/?linkid=198175)」を参照してください。

  - UM トラブルシューティング ツールをダウンロードして、インストールします。
    
      - Microsoft ダウンロード センターから[ユニファイド メッセージング トラブルシューティング ツール](https://go.microsoft.com/fwlink/p/?linkid=182625)をダウンロードします。
    
      - このツールをインストールします。詳細については、「[Exchange UM トラブルシューティング ツールをインストールする](install-the-exchange-um-troubleshooting-tool-exchange-2013-help.md)」を参照してください。
        

        > [!IMPORTANT]
        > UM トラブルシューティング ツールを <CODE>SIPClient</CODE> モードで使用する場合は、それ以外に Office Communications Server 2007 R2 または Microsoft Lync Server に対する要件および前提条件も満たす必要があります。詳細については、「<A href="https://go.microsoft.com/fwlink/p/?linkid=311961">チェックリスト:Office Communications Server 2007 R2 および Exchange 2010 ユニファイド メッセージングの展開</A>」を参照してください。



  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## Windows Vista、Windows 7、または Windows 8 で UM トラブルシューティング ツールを実行する

1.  <strong>スタート</strong> \> <strong>すべてのプログラム</strong> \> <strong>アクセサリ</strong> \> <strong>Windows PowerShell</strong> をクリックします。

2.  <strong>Windows PowerShell</strong> を右クリックし、ポップアップ メニューから <strong>管理者として実行</strong> を選択します。

3.  Windows PowerShell コマンド プロンプトで、UM トラブルシューティング ツールがインストールされたフォルダーに移動し、以下を実行します。
    
    ```powershell
    C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -psconsolefile .\Microsoft.Exchange.UM.TroubleshootingToolsnapin.psc1 -noexit -command ". '.\Microsoft.Exchange.UM.TroubleshootingTool.ps1' "
    ```

4.  Windows Vista、Windows 7、または Windows 8 で UM トラブルシューティング ツールを実行している場合は、Windows PowerShell コマンド プロンプトで、以下を実行します。
    
    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

5.  \[**スタート**\] メニューから、\[**Microsoft Exchange 2010 UM トラブルシューティング ツール**\] を開きます。

6.  <strong>Microsoft Exchange 2010 UM トラブルシューティング ツール</strong> ウィンドウのプロンプトで、次を入力し、Enter キーを押します。
    
    ```powershell
    $cred=Get-Credential
    ```

7.  <strong>Windows PowerShell 資格情報の要求</strong> ウィンドウに、ドメイン\\ユーザー名およびパスワードを入力して <strong>OK</strong> をクリックします。

8.  <strong>Microsoft Exchange 2010 UM トラブルシューティング ツール</strong> ウィンドウで、呼び出しのフローのテストに必要なコマンドレットのパラメーターを指定します。次に例を示します。
    
    ```powershell
    Test-ExchangeUMCallFlow -Mode SIPClient -CallingParty tonysmith@contoso.com - CalledParty jamiestark@contoso.com NextHop ocsfe.contoso.com -Credential $cred
    ```

