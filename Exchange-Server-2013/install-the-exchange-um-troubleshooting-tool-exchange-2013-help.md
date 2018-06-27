---
title: 'Exchange UM トラブルシューティング ツールをインストールする: Exchange 2013 Help'
TOCTitle: Exchange UM トラブルシューティング ツールをインストールする
ms:assetid: 84223af0-a717-49ee-add6-86313bb30d17
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff844714(v=EXCHG.150)
ms:contentKeyID: 56270073
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange UM トラブルシューティング ツールをインストールする

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:**2016-12-09_

Microsoft Exchange 2010 UM トラブルシューティング ツールは **Test-ExchangeUMCallFlow** という名前の Exchange 管理シェル コマンドレットです。このコマンドレットを使用して、通話応答シナリオに特有な構成エラーを診断したり、社内および社内外にまたがる Microsoft Exchange Server 2010 Service Pack 1 (SP1) 以降の UM 展開の両方でボイスメールが適切に機能しているかどうかをテストしたりすることができます。このコマンドレットは、Microsoft Office の Microsoft Lync Server 2010 以降を使用した展開、または Vo IP ゲートウェイ、IP PBX、セッション ボーダー コントローラー (SBC) を使用した UM 展開で使用できます。

UM トラブルシューティング ツールは、ローカルのユニファイド メッセージング サーバー、Exchange 2013 メールボックス サーバー、または別の 64 ビット コンピューターにインストールできます。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 3 分

  - UM トラブルシューティング ツールを使用するには、事前に Windows Vista、Windows 7、Windows 8、64 ビット版の Windows Server 2008、または Windows Server 2012 以降を実行しているコンピューター上に次のコンポーネントをインストールする必要があります。
    
      - Microsoft .NET Framework 3.5 Service Pack 1 (SP1)  「[Microsoft .NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=152380)」を参照してください。
    
      - Windows Vista または Windows Server 2008 コンピューター上でこのツールを実行する場合は「[Windows Vista x64、および Windows Server 2008 x64 のための Microsoft .NET Framework 3.5 ファミリの更新プログラム](https://go.microsoft.com/fwlink/p/?linkid=178998)」を参照してください。
    
      - Windows リモート管理 (WinRM) 2.0 および Windows PowerShell V2 (Windows6.0-KB968930.msu)   マイクロソフト サポート技術情報の文書番号 968930「[Windows Management Framework Core パッケージ (Windows PowerShell 2.0 および WinRM 2.0)](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=968930)」を参照してください。
    
      - Microsoft Unified Communications Managed API 2.0 Core ランタイム (UcmaRuntimeWebDownloadX64.msi)。  「[Unified Communications Managed API 2.0 Core ランタイム (64-bit)](https://go.microsoft.com/fwlink/p/?linkid=198175)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## UM トラブルシューティング ツールをインストールする

1.  「[Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/p/?linkid=182625)」からユニファイド メッセージング トラブルシューティング ツールをダウンロードし、MicrosoftExchange2010UMTroubleshootingTool.msi インストール フォルダーをダブルクリックします。

2.  **\[Microsoft Exchange 2010 UM トラブルシューティング ツール セットアップ ウィザードへようこそ\]** ページで、**\[次へ\]** をクリックします。

3.  **\[エンドユーザー使用許諾契約書\]** ページで、ソフトウェア ライセンス条項を確認し、同意する場合は、**\[使用許諾契約書に同意します\]** をクリックし、**\[次へ\]** をクリックします。

4.  **\[インストール先フォルダーの選択\]** ページで、インストール フォルダーへのパスを確認し、**\[次へ\]** をクリックします。

5.  **\[インストールの確認\]** ページで **\[次へ\]** をクリックすると、インストールが開始されます。

6.  **\[インストールの完了\]** ページで **\[閉じる\]** をクリックします。

