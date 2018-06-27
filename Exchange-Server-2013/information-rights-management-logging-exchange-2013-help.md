---
title: 'Information Rights Management のログ: Exchange 2013 Help'
TOCTitle: Information Rights Management のログ
ms:assetid: e06f57f9-a9e2-43a2-b88c-288b324d71f0
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff461940(v=EXCHG.150)
ms:contentKeyID: 49896521
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Information Rights Management のログ

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-03-09_

Microsoft Exchange Server 2013 では、Information Rights Management (IRM) の動作が IRM ログに記録されます。IRM ログを使用することにより、組織内の Exchange 2013 サーバーにある Rights Management Services (RMS) クライアントと Active Directory Rights Management Services (AD RMS) クラスター間のインタラクションを監視してトラブルシューティングできます。

IRM の詳細については、「[Information Rights Management](information-rights-management-exchange-2013-help.md)」を参照してください。

**目次**

IRM ログの構造

ログ プロセス

IRM ログに書き込まれる情報

IRM ログの管理

IRM に関連する管理タスクについては、「[Information Rights Management の手順](information-rights-management-procedures-exchange-2013-help.md)」を参照してください。

## IRM ログの構造

既定では、IRM ログは C:\\Program Files\\Microsoft\\Exchange Server\\V14\\Logging\\IRMLogs に格納されます。

IRM ログ ファイルの命名規則は \<*プロセス*\>\_\<*プロセス ID* または *IIS AppPool ID*\>\_IRMLOG*yyyymmdd*-*nnnn*.log です。

  - \<*プロセス*\>= ログ ファイルを作成するプロセス。たとえば、トランスポート サービスでは、EdgeTransport です。

  - \<*プロセス ID* または *IIS AppPool ID\>* =プロセス ID。

  - *yyyymmdd* は、ログ ファイルを作成した協定世界時 (UTC) の日付です。

  - *nnnn* = インスタンス番号で、毎日 1 から開始します。

IRM ログ ファイル名の例 EdgeTransport\_1056\_IRMLOG20101201-1.log。

次の表は、さまざまなサーバーの役割で生成されるログを示します。

### サーバーの役割のログ

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>サーバーの役割</th>
<th>IRM ログ ファイル名</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Transport サービス</p></td>
<td><p>EdgeTransport_&lt;<em>プロセス ID</em>&gt;_IRMLOG<em>yyyymmdd</em>-<em>nnnn</em>.log</p></td>
<td><p>このログは、トランスポート サービス上でトランスポート パイプラインによって行われた RMS トランザクションすべてを記録するために使用されます (トランスポート保護ルールとジャーナル レポートの暗号化など)。edgetransport.exe プロセスのプロセス ID (PID) がログ ファイル名の生成に使用されます。</p></td>
</tr>
<tr class="even">
<td><p>メールボックス</p></td>
<td><p>msftefd_&lt;<em>プロセス ID</em>&gt;_IRMLOG<em>yyyymmdd</em>-<em>nnnn</em>.log</p></td>
<td><p>このログは、検索とインデックス処理要求中に発生するすべての RMS トランザクションを記録するために使用されます。Exchange 2013 メールボックス サーバーはコンテンツのインデックス処理に msftefd.exe プロセスを使用します。msftefd.exe プロセスの PID がログ ファイル名の生成に使用されます。</p></td>
</tr>
<tr class="odd">
<td><p>クライアント アクセス</p></td>
<td><p>w3wp_MSExchangeOWAAppOol_IRMLOG<em>yyyymmdd</em>-<em>nnnn</em>.log</p></td>
<td><p>このログは、Microsoft OfficeOutlook Web App 内の IRM の全てのトランザクションを記録するのに使用されます。</p></td>
</tr>
<tr class="even">
<td><p>すべての Exchange 2013 サーバーの役割</p></td>
<td><p>w3wp_MSExchangePowerShellAppPool_IRMLOG<em>yyyymmdd</em>-<em>nnnn</em>.log</p></td>
<td><p>このログは、Windows PowerShell から発行されるすべての IRM RMS トランザクションを記録するために使用されます (<strong>Test-IRMConfiguration</strong> コマンドレットを発行する場合など)。</p></td>
</tr>
</tbody>
</table>


IRM ログの構造

## ログ プロセス

情報は、ファイル サイズが指定された最大値に達するまでログ ファイルに書き込まれます。最大サイズに達すると、インスタンス番号が付いたログ ファイルが作成されます。このプロセスを終日繰り返します。循環ログでは、接続ログ ディレクトリが指定された最大サイズに達するか、またはログ ファイルが指定された最大保存期間に達すると、最も古いログ ファイルが削除されます。これらの値は、各サーバーの IRM ログ構成で指定されます。

IRM ログの構造

## IRM ログに書き込まれる情報

IRM ログ ファイルは、データをコンマ区切り (CSV) 形式で格納するテキスト ファイルです。各 IRM ログ ファイルには、以下の情報を含むヘッダーがあります。

  - **\#Software**   IRM ログ ファイルを作成したソフトウェアの名前です。通常、この値は `Microsoft Exchange Server` です。

  - **\#Version**   IRM ログ ファイルを作成したソフトウェアのバージョン番号です。

  - **\#Log-Type**   ログの種類の値で、`Rms Client Manager Log` です。

  - **\#Date**   ログ ファイルが作成された UTC の日時です。UTC の日時は次のような ISO 8601 の日時形式で表されます。*yyyy*-*mm*-*dd*T*hh*:*mm*:*ss.fff*Z
    
      - yyyy = 年
    
      - *mm* = 月
    
      - *dd* = 日
    
      - T = 時刻部分の開始を示す時刻指定子
    
      - *hh* = 時
    
      - *mm* = 分
    
      - *ss* = 秒
    
      - *fff* = 秒の小数部分
    
      - Z = Zulu (UTC の別称)

  - **\#Fields**   IRM ログ ファイルで使用されているフィールド名をコンマで区切ったものです。
    
    IRM ログには、各 RMS トランザクション イベントがコンマ区切りフィールドに整理され、1 行として格納されます。次の表は、IRM 機能が有効なサーバーの役割すべての IRM ログのフィールドを示しています。
    
    ### IRM ログで使用されるフィールド
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>フィールド</th>
    <th>説明</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Date-time</strong></p></td>
    <td><p>UTC タイムスタンプをリストします。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Feature</strong></p></td>
    <td><p>使用される RMS クライアント機能をリストします。有効な値は次のとおりです。</p>
    <ul>
    <li><p><code>RacClc</code></p></li>
    <li><p><code>Template</code></p></li>
    <li><p><code>Prelicense</code></p></li>
    <li><p><code>UseLicense</code></p></li>
    <li><p>署名の検証</p></li>
    <li><p><code>ServerInfo</code></p></li>
    </ul></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Event-Type</strong></p></td>
    <td><p>イベントの種類をリストします。有効な値は次のとおりです。</p>
    <ul>
    <li><p><code>Acquire</code>   RMS ライセンスまたはテンプレートが要求されています。</p></li>
    <li><p><code>Success</code>   RMS ライセンスまたはテンプレートが正常に取得されました。</p></li>
    <li><p><code>Exception</code>   エラーが発生しました。</p></li>
    <li><p><code>Queued</code>   要求は保留中です。</p></li>
    </ul></td>
    </tr>
    <tr class="even">
    <td><p><strong>Tenant-Id</strong></p></td>
    <td><p>マイクロソフトの内部使用のため予約済み。</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Server-url</strong></p></td>
    <td><p>操作中にアクセスされた RMS サーバーの URLをリストします。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Context</strong></p></td>
    <td><p>複数の RMS トランザクションをまとめるため、呼び出しプロセスが使用します。有効な値は次のとおりです。</p>
    <ul>
    <li><p><code>MessageID: &lt;Actual message ID&gt;</code></p></li>
    <li><p><code>MailboxGuid: &lt;Mailbox GUID&gt;</code></p></li>
    <li><p><code>AttachmentFileName: &lt;File name&gt;</code></p></li>
    </ul></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Transaction-id</strong></p></td>
    <td><p>一意のトランザクションを識別します。1つの トランザクション中に発生するすべてのイベントには、同じトランザクション ID が指定されます。</p></td>
    </tr>
    </tbody>
    </table>


IRM ログの構造

## IRM ログの管理

IRM 機能が有効である各サーバーの役割では、既定で IRM ログが有効です。各サーバーの役割では、サーバーの役割の対応する **Set** コマンドレットを使用することにより、次の IRM ログ構成を変更できます。たとえば、メールボックス サーバーの IRM ログを構成するには、**Set-MailboxServer** コマンドレットを使用します。

### IRM ログの構成パラメーター

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
<td><p><em>IrmLogEnabled</em></p></td>
<td><p>IRM トランザクションのログを有効にします。既定で IRM ログが有効です。サーバーの役割で IRM を無効にするには、このパラメーターを <code>$false</code> に設定します。</p></td>
</tr>
<tr class="even">
<td><p><em>IrmLogMaxAge</em></p></td>
<td><p>IRM ログ ファイルの最大保存期間を指定します。指定した期間より古いファイルは削除されます。既定値は <code>30.00:00:00</code> (30 日) です。</p></td>
</tr>
<tr class="odd">
<td><p><em>IrmLogMaxDirectorySize</em></p></td>
<td><p>接続ログ ディレクトリ内のすべての IRM ログの最大サイズを指定します。ディレクトリが最大ファイル サイズに達すると、最も古いログ ファイルが削除されます。既定値は <code>250 MB</code> です。</p></td>
</tr>
<tr class="even">
<td><p><em>IrmLogMaxFileSize</em></p></td>
<td><p>単一ログ ファイルの最大ファイル サイズを指定します。ファイルが指定されたサイズに達すると、ログ ファイルが作成され、インスタンス番号が増加します。既定値は <code>10 MB</code> です。</p></td>
</tr>
<tr class="odd">
<td><p><em>IrmLogPath</em></p></td>
<td><p>IRM ログの場所を指定します。既定のパスは、%ExchangeInstallPath%Logging\IRMLogs です。</p></td>
</tr>
</tbody>
</table>


構文およびパラメーターの詳細については、以下のトピックを参照してください。

  - [Set-MailboxServer](https://technet.microsoft.com/ja-jp/library/aa998651\(v=exchg.150\))

  - [Set-ClientAccessServer](https://technet.microsoft.com/ja-jp/library/bb125157\(v=exchg.150\))

  - [Set-TransportService](https://technet.microsoft.com/ja-jp/library/jj215682\(v=exchg.150\))

IRM ログの構造

