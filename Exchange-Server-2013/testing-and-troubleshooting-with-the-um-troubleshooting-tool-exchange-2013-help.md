---
title: 'UM トラブルシューティング ツールによるテストとトラブルシューティング: Exchange 2013 Help'
TOCTitle: UM トラブルシューティング ツールによるテストとトラブルシューティング
ms:assetid: 1fab2e52-bd2d-4e46-b222-53fee9d34cba
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg621148(v=EXCHG.150)
ms:contentKeyID: 56270039
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM トラブルシューティング ツールによるテストとトラブルシューティング

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2016-12-09_

Microsoft Exchange 2010 UM トラブルシューティング ツールは **Test-ExchangeUMCallFlow** という名前の Exchange 管理シェル コマンドレットです。このコマンドレットを使用して、通話応答シナリオに特有な構成エラーを診断したり、社内および社内外にまたがる Microsoft Exchange Server 2010 Service Pack 1 (SP1) 以降の UM 展開の両方でボイスメールが適切に機能しているかどうかをテストしたりすることができます。このコマンドレットは、Microsoft Office の Microsoft Lync Server 2010 以降を使用した展開、または Vo IP ゲートウェイ、IP PBX、セッション ボーダー コントローラー (SBC) を使用した UM 展開で使用できます。

## 概要

このコマンドレットは呼び出しをエミュレートして、テレフォニー設備の構成エラー、Exchange 2010 SP1 およびその後のユニファイド メッセージングの設定、および社内と社内外の展開にまたがる Exchange 2010 SP1 およびその後のユニファイド メッセージングの間の接続の問題を社内の管理者が識別するのに役立つ一連の診断テストを実行します。

このコマンドレットを実行すると、検出された問題に関してその理由と実行可能な解決方法を示します。ジッターおよび平均パケット損失などの、ネットワーク接続に関連する音質の問題の診断に関して、一般的な音質の測定値についても出力します。**Test-ExchangeUMCallFlow** コマンドレットは、`Secured` の UM コンポーネント、`SIP Secured`、および `Unsecured` 呼び出しのテストをサポートしており、`Gateway` モードか `SIPClient` モードのいずれかで実行できます。

既定では、UM トラブルシューティング ツールを実行している場合、ツールはコンピューターのログオン時に使用される資格情報を使用します。使用される資格情報は、発信側を示すものです。UM トラブルシューティング ツールを `SIPClient` モードで実行する際は、使用する資格情報を設定または指定する必要があります。ただし、UM トラブルシューティング ツールを `Gateway` モードで実行している場合は、資格情報の設定は必要ありません。UM トラブルシューティング ツールを `SIPClient` モードで使用する場合は、それ以外に Office Communications Server 2007 R2 または Lync Server に対する要件および前提条件も満たす必要があります。詳細については、「[チェックリスト:Office Communications Server 2007 R2 および Exchange 2010 ユニファイド メッセージングの展開](https://go.microsoft.com/fwlink/p/?linkid=311961)」または「[チェックリスト: Exchange 2013 UM と Lync Server の統合](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md)」を参照してください。


> [!IMPORTANT]
> <STRONG>Test-ExchangeUMCallFlow</STRONG> コマンドレットは、Exchange 2010 Service Pack 1 (SP1) または Microsoft Exchange 2013 がインストールされている Microsoft Exchange Server 2010 ユニファイド メッセージング サーバーのボイス メール機能をテストする場合にのみ使用する必要があります。



**Test-ExchangeUMCallFlow** コマンドレットは、ローカルの Exchange 2010 ユニファイド メッセージング サーバー、 Exchange 2013 メールボックス サーバー、または次のオペレーティング システムを実行するその他の 64 ビット コンピューターにインストールできます。

  - Windows 7 または Windows 8 オペレーティング システム。

  - Windows Server 2008 または Windows Server 2008 R2 オペレーティング システム

  - Windows Server 2012 または Windows Server 2012 R2 オペレーティング システム。

**Test-ExchangeUMCallFlow** コマンドレットでは、コマンドレットのインストール前に、Windows 7、Windows 8、Windows Server 2008、または Windows Server 2012 の 64 ビット コンピューターに次のコンポーネントをインストールする必要があります。

  - Microsoft .NET Framework 3.5 Service Pack 1 (SP1)。このサービス パックをダウンロードするには、「[Microsoft .NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/?linkid=152380)」を参照してください。

  - Windows Vista または Windows Server 2008 コンピューターでツールを実行する場合、Windows Vista x64 および Windows Server 2008 x64 用の Microsoft .NET Framework 3.5 ファミリの更新プログラムを更新します。更新プログラムをダウンロードするには、「[Windows Vista x64 および Windows Server 2008 x64 用 Microsoft .NET Framework 3.5 ファミリの更新プログラム](https://go.microsoft.com/fwlink/p/?linkid=178998)」を参照してください。

  - Windows Windows リモート管理 (WinRM) 2.0 および Windows PowerShell V2 (Windows6.0-KB968930.msu)。詳細については、Microsoft サポート技術情報の文書番号 968930「[Windows 管理フレームワークのコア パッケージ (Windows PowerShell 2.0 および WinRM 2.0)](http://go.microsoft.com/fwlink/?linkid=3052%26kbid=968930)」を参照してください。

  - Unified Communications Managed AP1 2.0、コア ランタイム (64 ビット)。   UcmaRuntimeWebDownloadX64.msi のプログラム ファイルをダウンロードするには、「[Unified Communications Managed API 2.0、Core ランタイム (64-bit)](https://go.microsoft.com/fwlink/p/?linkid=198175)」を参照してください。

**Test-ExchangeUMCallFlow** コマンドレットは、Exchange 2010 SP1 DVD や Exchange 2010 SP1 のみのダウンロード、または Exchange 2013 インストール メディアには含まれません。ただし、このコマンドレットは「[Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/p/?linkid=182625)」からダウンロードできます。

構文およびパラメーターの詳細については、「[Test-ExchangeUMCallFlow](https://technet.microsoft.com/ja-jp/library/ff630913\(v=exchg.150\))」を参照してください。

