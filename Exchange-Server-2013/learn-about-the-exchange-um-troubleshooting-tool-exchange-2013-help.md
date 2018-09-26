---
title: 'Exchange UM トラブルシューティング ツールの概要: Exchange 2013 Help'
TOCTitle: Exchange UM トラブルシューティング ツールの概要
ms:assetid: cc11bf5e-2c87-4495-b2ad-3e9a6bc81dbc
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg584301(v=EXCHG.150)
ms:contentKeyID: 56270077
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange UM トラブルシューティング ツールの概要

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2016-12-09_

Microsoft Exchange 2010 ユニファイド メッセージング トラブルシューティング ツールは **Test-ExchangeUMCallFlow** という名前の Exchange 管理シェル コマンドレットです。このツールを使用すると、組織内のユニファイド メッセージング (UM) に対して一連の診断テストを実行できます。いずれかのテストが失敗すると、ツールによって、失敗の理由と、問題を解決するために実行可能な解決方法がレポートとして出力されます。UM トラブルシューティング ツールは、Exchange 2010 以降のサーバーでのみ使用できます。

UM トラブルシューティング ツールを使用すると、ボイス メールが社内および社内外にまたがる展開で適切に機能しているかどうかをテストできます。このツールは Microsoft Office Communications Server 2007 R2 または Microsoft Lync Server 2010 以降が含まれる UM 展開、あるいは VoIP ゲートウェイ、IP 構内交換機 (IP PBX)、またはセッション ボーダー コントローラー (SBC) が含まれる UM 展開で使用できます。


> [!NOTE]
> UM トラブルシューティング ツールは、テストおよびトラブルシューティングを行うために使用します。一方、<STRONG>Test-UMConnectivity</STRONG> コマンドレットは監視のために使用する必要があります。<STRONG>Test-UMConnectivity</STRONG> コマンドレットは、System Center Operations Manager (SCOM) 管理パックと併せて使用されます。これは、Exchange 2010 UM サーバーまたはExchange 2013 クライアント アクセスおよびメールボックス サーバーおよびテレフォニー コンポーネントをモニタリングするために使用されるものです。 <STRONG>Test-UMConnectivity</STRONG> コマンドレットは、ローカルの SIP テストとローカルのログオン テストをメールボックスに対して実行します。このコマンドレットは SCOM タスクとして実行できます。



UM トラブルシューティング ツールをダウンロードするには、「[ユニファイド メッセージング トラブルシューティング ツール](https://go.microsoft.com/fwlink/p/?linkid=182625)」を参照してください。

**目次**

概要

UM トラブルシューティング アーキテクチャ

VoIP ゲートウェイおよび IP PBX の展開

Office Communications Server 2007 R2 と Microsoft Lync Server の展開

UM トラブルシューティング ツールのインストール

コマンドレットのパラメーター

## 概要

UM トラブル―シューティング ツールを使用すると、UM 展開内でのテストおよびトラブルシューティングが簡略化されます。UM トラブルシューティング ツールを実行すると、複数のトレース ファイルが自動的に生成されます。これらのファイルは、C:\\Users\\%UserProfile%\\AppData\\Roaming\\Microsoft Exchange 2010 UM Troubleshooting フォルダー内に保存されます。このツールによって次のトレース ファイルが生成されます。

  - **UMTool\_Collaboration**   RTC スタック トレースが含まれます。

  - **UMTool\_DiagnosticLog**   実行するすべてのテストとテストの結果を一覧します。

  - **UMTool\_S4**   S4: 信号スタック トレースが含まれます。

  - **UMTool\_SIPMessageLogs**   作成されるテスト呼び出しのすべての SIP トレースが含まれます。

UM トラブルシューティング ツールは、社内のセッション ボーダー コントローラー (SBC) があればそれに直接接続し、あるいはデータセンター内の SBC に接続して、VoIP ゲートウェイ経由の PBX または IP PBX から受信されたように着信呼び出しをエミュレートします。UM トラブルシューティング ツールを使用すると、以下の項目を診断できます。

  - Office Communications Server 2007 R2 または Microsoft Lync Server が展開された社内または社内外にまたがる UM 展開での間違った設定。

  - VoIP ゲートウェイおよび PBX または IP PBX を備えた社内または社内外にまたがるテレフォニー装置における間違った設定。

  - ドメイン ネーム システム (DNS) の問題。

  - セキュリティで保護されたSIP または キュリティで保護された UM ダイヤル プランを使用している場合の証明書の問題。

  - DTMF (タッチトーンとも呼びます) とオーディオの信号およびメディアの問題。

UM トラブルシューティング ツールによって構成内の誤りが検出されると、エラーの理由と、検出された問題に対して実行可能な解決方法がレポートとして出力されます。UM トラブルシューティング ツールを社内の展開で使用した場合にレポートされる可能性のあるエラーを以下に示します。

  - 最大呼び出し制限に達した。

  - このユーザーはユニファイド メッセージングに対して有効ではない。

  - UM IP ゲートウェイ、UM ダイヤル プラン、UM ハント グループの情報が見つからない。

  - セキュリティの種類が UM ダイヤル プランと一致しない。

  - 呼び出しを処理するために使用できるワーカー プロセスがない。

  - UM サービスまたは UM 呼び出しルーター サービスが停止する。

  - Active Directory フォレストが見つからない。

  - 利用できるディスク容量がない。

  - 要求で使用された SIP ヘッダーが正しくない。

  - Office Communications Server 2007 R2 サーバーまたは Lync Server サーバーに対して呼び出しが行われた。

  - UM IP ゲートウェイが無効である。

  - 呼び出し先のユーザーの URI が正しくない。

UM のトラブルシューティング ツールを社内外にまたがる展開で使用した場合、以下のようなエラーがレポートされる可能性があります。

  - このユーザーはユニファイド メッセージングに対して有効ではない。

  - UM IP ゲートウェイが無効である。

  - ユーザーの URI が正しくない。

  - セキュリティの種類が UM ダイヤル プランと一致しない。

  - 要求で使用された SIP ヘッダーが正しくない。

  - UM IP ゲートウェイ、UM ダイヤル プラン、UM ハント グループの情報が見つからない。

UM トラブルシューティング ツールを実行すると、15 秒間にわたって wav サンプル ファイルが送信されます。オーディオ ファイルと RTP オーディオ ストリームが送信および再生された後、ツールによって、ジッターや平均パケット損失などのネットワーク接続に関連する音質の問題を診断するための一般的な音質の測定値がレポートとして出力されます。これらのレポートには、UM サーバーとの通信におけるメディア ストリーム品質のほか、以下の情報が含まれます。

  - Network 平均オピニオン値 (NMOS)

  - コーデック

  - 遅延時間 (ミリ秒 (ms))

  - ジッター (ミリ秒 (ms))

  - パケット損失の割合 (%)

  - 音質を判断するために使用される NMOS の分類と評価は次のようになります。
    
      - NMOS が 2 未満である = 良くない
    
      - NMOS が 2 以上 3 未満である = 平均
    
      - NMOS が 3 以上 4 未満である = 良い
    
      - NMOS が 4 以上 5 未満である = 非常に良い

UM トラブルシューティング ツールでは、セキュリティで保護されている呼び出し、セキュリティで保護された SIP 呼び出し、およびセキュリティで保護されていない呼び出しを使用する UM ダイヤル プランのテストがサポートされています。\[セキュリティで保護\] または \[セキュリティで保護された SIP\] を選択すると、使用されている証明書の拇印が確認され、証明書が期限切れでないか、およびTLS (トランスポート層セキュリティ) 通信で使用されている証明書の種類が判定されます。証明書は、リモート コンピューターの ID を正しく識別し、保証するために使用されます。セキュリティで保護されたモードまたはセキュリティで保護された SIP モードを選択すると、UM トラブルシューティング ツールによって、以下の項目に該当するかどうかが検証されます。

  - ローカルの証明書がローカル コンピューター ストアに見つかった。

  - 使用されている証明書は信頼されている。

  - 証明書内に指定されているターゲット名は有効である。

  - 証明書の有効期限が切れている。

  - リモート コンピューターは証明書を信頼している。

  - 証明書が失効している。

  - 証明書に必要な拡張キー使用法が指定されていない。

UM トラブルシューティング ツールは、Office Communications Server 2007 R2 または Lync Server のどちらが展開されているかによって、あるいはユニファイド メッセージング サーバーで VoIP ゲートウェイと PBX または IP PBX のどちらが使用されているかによって、Gateway モードまたは SIPClient モードのいずれかで実行できます。Gateway モードまたは SIPClient モードのいずれかを使用すると、 UM トラブルシューティング ツールでは、次の形式を使用した呼び出しがサポートされます。使用される形式は、UM ダイヤル プランの URI タイプによって決まります。

  - 電話の内線番号   425-555-1010

  - E.164 電話番号   +1 (425) 555-1010

  - SIP アドレス   tonysmith@contoso.com

SIPClient モードを使用している場合、UM トラブルシューティング ツールによって音声メモが呼び出されます。これは、電話、または統合コミュニケーション (UC) エンドポイントの呼び出し音を鳴らさない呼び出しです。代わりに、呼び出しがボイス メールに直接送信されます。UM トラブルシューティング ツールを SIPClient モードで実行する場合、以下の項目が判定されます。

  - 呼び出し先のターゲット ユーザー。

  - SIP 呼び出しが正常に確立されたかどうか。

  - SIP 呼び出しが Exchange 2010 ユニファイド メッセージング サーバーまたは Exchange 2013 メールボックス サーバーによって受け入れられたかどうか。

  - 適切な DTMF シーケンスが受信されたかどうか。

  - 診断の .wav ファイルが送信され、Exchange 2010 UM サーバーまたは Exchange 2013 メールボックス サーバーによって受信されたかどうか。

  - メディアまたは音質ストリームの受信時に使用された測定値。

UM トラブルシューティング ツールは、着信呼び出しをエミュレートし、社内の管理者およびテナント管理者が、呼び出し応答用の呼び出しフローのテスト、および構成エラーの特定を行うのに役立つ一連の診断テストを実行します。UM トラブルシューティング ツールは呼び出し応答シナリオで使用できますが、以下の呼び出しの種類のテストには使用できません。

  - Outlook Voice Access 呼び出し。これには、ボイス メールや電子メール、予定表、ディレクトリ、個人用連絡先、個人オプションにアクセスする各種の呼び出しが含まれます。

  - UM 自動応答

  - 電話での再生

  - 通話応答ルール

  - FAX

  - プロンプトの事前設定

概要

## UM トラブルシューティング アーキテクチャ

UM トラブルシューティング ツールは社内外にわたる展開での構成の問題のトラブルシューティング、診断、修正に役立ちますが、このツールを社内のユニファイド メッセージ展開で使用することもできます。社内外にわたる展開では、このツールはオンサイトの SBC 構成も検証します。管理者は、SBC などのユニファイド メッセージングによって使用されるすべてのユニファイド メッセージング コンポーネントをテストできます。

## VoIP ゲートウェイおよび IP PBX の展開

次の例では、Office Communications Server 2007 R2 または Lync Server を含まない環境での呼び出しフローをテストするために、ゲートウェイ モードが使用されています。この例では、VoIP ゲートウェイ、PBX、および IP PBX、さらにユニファイド メッセージング コンポーネントを含むテレフォニー装置をテストします。この例では、ボイス オーバー IP (VoIP) セキュリティ モードを \[セキュリティ保護なし\] に設定し、IP アドレス 10.1.1.1 を次ホップとして使用し、迂回路情報に内線番号を含めます。

```powershell
Test-ExchangeUMCallFlow -Mode Gateway -VoIPSecurity Unsecured -NextHop 10.1.1.1 -Diversion 12345
```

概要

## Office Communications Server 2007 R2 と Microsoft Lync Server の展開

UM トラブルシューティング ツールは、SIPClient モードを設定している場合、Office Communications Server 2007 R2 または Microsoft Lync Server を含めた社内または社内外にまたがる展開で使用できます。この例では、SIPClient モードを使用して、Office Communications Server 2007 R2 または Lync Server サーバーが含まれる環境で、セキュリティで保護された UM ダイヤル プランを使用した呼び出しフローをテストします。既定では、UM トラブルシューティング ツールを実行している場合、ツールはコンピューターに現在ログオンしているユーザーの資格情報を使用します。次の例を実行すると、UM トラブルシューティング ツールを実行する際に使用する資格情報の入力が求められます。詳細については、「[Exchange UM トラブルシューティング ツールで使用する資格情報を設定する](set-the-credentials-to-use-with-the-exchange-um-troubleshooting-tool-exchange-2013-help.md)」を参照してください。

  ```powershell
  Test-ExchangeUMCallFlow -Mode SIPClient -VoIPSecurity Secured -CallingParty tony@contoso.com -CalledParty david@contoso.com -Credential $get
  ```

## UM トラブルシューティング ツールのインストール

UM トラブルシューティング ツールは、ローカルのユニファイド メッセージング サーバー、または以下のいずれかを実行している別の 64 ビット コンピューターにインストールできます。

  - Windows 7 または Windows 8 オペレーティング システム。

  - Windows Server 2008 または Windows Server 2008 R2 オペレーティング システム。

  - Windows Server 2012 または Windows Server 2012 R2 のオペレーティング システム

Windows 7 の 64 ビット版、Windows 8、または Windows Server 2008 の 64 ビット版で UM トラブルシューティング ツールを使用する場合は、UM トラブルシューティング ツールをインストールする前に、以下のコンポーネントをインストールしておく必要があります。

  - Microsoft .NET Framework 3.5 Service Pack 1 (SP1)  「[Microsoft .NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=152380)」を参照してください。
    

    > [!NOTE]
    > Windows Vista または Windows Server 2008 コンピューター上でこのツールを実行する場合は「<A href="https://go.microsoft.com/fwlink/p/?linkid=178998">Windows Vista x64、および Windows Server 2008 x64 のための Microsoft .NET Framework 3.5 ファミリの更新プログラム</A>」を参照してください。



  - Windows リモート管理 (WinRM) 2.0 および Windows PowerShell V2 (Windows6.0-KB968930.msu)   マイクロソフト サポート技術情報の文書番号 968930「[Windows Management Framework Core パッケージ (Windows PowerShell 2.0 および WinRM 2.0)](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930)」を参照してください。

  - Microsoft Unified Communications Managed API 2.0 Core ランタイム (UcmaRuntimeWebDownloadX64.msi)。  「[Unified Communications Managed API 2.0 Core ランタイム (64-bit)](https://go.microsoft.com/fwlink/p/?linkid=198175)」を参照してください。

UM トラブルシューティング ツール (**Test-ExchangeUMCallFlow** コマンドレット) は、Exchange 2010 SP1 DVD、Exchange 2010 のみを含むダウンロード、または Exchange 2013 インストール メディアには含まれません。ただし、UM トラブルシューティング ツールは、「[Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/p/?linkid=182625)」からダウンロードできます。

詳細については、「[Exchange UM トラブルシューティング ツールをインストールする](install-the-exchange-um-troubleshooting-tool-exchange-2013-help.md)」を参照してください。

概要

## コマンドレットのパラメーター

次の表は、**Test-ExchangeUMCallFlow** コマンドレットと共に使用できるパラメーターと、パラメーターの説明を示しています。また、シェル コマンド `Get-help Test-ExchangeUMCallFlow -detailed` を使用すると、**Test-ExchangeUMCallFlow** コマンドレットと共に使用できる各パラメーターの詳細およびその使用例を参照できます。

### パラメーター

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>CalledParty</em></p></td>
<td><p><em>CalledParty</em> パラメーターには、エンタープライズ ボイスのユーザーとして有効になっている Office Communications Server 2007 R2 または Lync Server ユーザーの SIP URI を指定します。これは、<strong>Test-ExchangeUMCallFlow</strong> コマンドレットの音声呼び出しの対象となるユーザーです。<code>-CalledParty tonysmith@contoso.com</code> と指定します。このツールを SIPClient モードで実行中の場合は、このパラメーターを使用します。</p></td>
</tr>
<tr class="even">
<td><p><em>CallingParty</em></p></td>
<td><p><em>CallingParty</em> パラメーターには、エンタープライズ ボイスのユーザーとして有効になっている Office Communications Server 2007 R2 または Lync Server ユーザーの SIP URI を指定します。これは、着信呼び出しを行うユーザーです。たとえば、<code>-CallingParty tonysmith@contoso.com</code> と指定します。このツールを SIPClient モードで実行中の場合は、このパラメーターを使用します。</p></td>
</tr>
<tr class="odd">
<td><p><em>Diversion</em></p></td>
<td><p><em>Diversion</em> パラメーターには、着信呼び出しに対して迂回路情報として送信する文字列を指定します。これは Diversion または History-Info ヘッダーの形式で指定できます。着信呼び出しに含まれる迂回路情報には内線番号を指定できます。また、追加の迂回路情報を含めることもできます。</p>
<p>迂回路情報を History-Info ヘッダーとして指定する場合は、以下を確認してください。</p>
<ul>
<li><p>異なるユーザー部分を含む異なるエントリが少なくとも 2 つ存在すること。</p></li>
<li><p>最後のエントリに、そのユーザーが関連付けられた UM ダイヤル プランのパイロット番号が含まれていること。</p></li>
<li><p>最後から 2 番目のエントリに、UM が有効なユーザーの内線番号が含まれていること。このエントリには、適切な理由テキストも含まれている必要があります。このテキストは、標準の URL パラメーター エスケープ ルールに従って適切にエスケープされている必要があります。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>Mode</em></p></td>
<td><p><em>Mode</em> パラメーターには、VoIP ゲートウェイ、IP PBX、Office Communications Server 2007 R2 または Lync Server モードを使用するかどうかを指定します。UM 展開に VoIP ゲートウェイまたは IP PBX が含まれる場合は ゲートウェイ モード、あるいは UM 展開に Office Communications Server 2007 R2 または Lync Server が含まれる場合は SIPClient モードのいずれかを指定できます。</p></td>
</tr>
<tr class="odd">
<td><p><em>NextHop</em></p></td>
<td><p><em>NextHop</em> パラメーターには、次ホップの IP アドレスまたは完全修飾ドメイン名 (FQDN) を指定し、<strong>Test-ExchangeUMCallFlow</strong> コマンドレットが VoIP ゲートウェイまたは IP PBX をエミュレートしている最中に接続する必要のある次ホップの TCP ポートを含めることもできます。TCP ポートを含める場合、 セキュリティで保護されていないモードにはポート 5060、あるいはセキュリティで保護されたモードまたはセキュリティで保護された SIP モードにはポート 5061 を指定する必要があります。例:<code>gateway.contoso.com:5061</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>CertificateThumbprint</em></p></td>
<td><p><em>CertificateThumbprint</em> パラメーターには、TLS に使用する証明書の拇印を指定します。UM ダイヤル プランにセキュリティで保護された SIP モードまたはセキュリティで保護されたモードのいずれかが構成されている場合、これは必須となります。この証明書の拇印は、VoIP ゲートウェイ、IP PBX、または SBC からエクスポートされた証明書です。また、UM トラブルシューティング ツールがインストールされていて、呼び出しのフローのテストに使用されているコンピューターは、次ホップの証明機関を信頼する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><em>Credential</em></p></td>
<td><p><em>Credential</em> パラメーターは、コマンドレットを実行するために使用する資格情報を指定します。</p></td>
</tr>
<tr class="even">
<td><p><em>HuntGroup</em></p></td>
<td><p><em>HuntGroup</em> パラメーターには、エミュレートされる VoIP ゲートウェイに関連付けられた UM ハント グループを指定します。これは通常、内線番号です。このツールを Gateway モードで実行中の場合は、このパラメーターを使用します。</p></td>
</tr>
<tr class="odd">
<td><p><em>VoIPSecurity</em></p></td>
<td><p><em>VoIPSecurity</em> パラメーターには、コマンドレットを Gateway モードで使用する場合のセキュリティ モードを指定します。次のいずれかの VoIP セキュリティ モードを使用できます。</p>
<ul>
<li><p>セキュリティで保護されたモード (TLS/SRTP)</p></li>
<li><p>セキュリティで保護されないモード (TCP/RTP) (既定値)</p></li>
<li><p>セキュリティで保護された SIP モード (TLS/RTP)</p></li>
</ul></td>
</tr>
</tbody>
</table>


概要

