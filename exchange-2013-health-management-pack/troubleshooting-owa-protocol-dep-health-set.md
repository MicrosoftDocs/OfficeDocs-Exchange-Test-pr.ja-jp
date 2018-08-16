---
title: OWA.Protocol.Dep 正常性セットのトラブルシューティング
TOCTitle: OWA.Protocol.Dep 正常性セットのトラブルシューティング
ms:assetid: f39c63d5-f161-4eee-9415-05f3355e7cc7
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.scom.owa.protocol.dep(v=EXCHG.150)
ms:contentKeyID: 54651744
ms.date: 01/28/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# OWA.Protocol.Dep 正常性セットのトラブルシューティング

 

_**適用先:** Exchange Server 2013, Project Server 2013_

_**トピックの最終更新日:** 2015-11-10_

**OWA.Protocol.DEP** 正常性セットは、Lync 2013 と Exchange 2013 の間で統合された、Outlook Web App でのインスタント メッセージング (IM) の全体的な正常性を監視します。Outlook Web App でインスタント メッセージングを有効にする方法について詳しくは、「[Microsoft Lync Server 2013 および Microsoft Outlook Web App 2013 の統合](http://go.microsoft.com/fwlink/p/?linkid=280418)」を参照してください。

**OWA.Protocol.DEP** 正常性セットが異常であることを示す警告を受け取った場合、それはインスタント メッセージングが Outlook Web App で正しく機能しなくなる可能性のある問題が生じたことを示しています。

## 説明

**OWA.Protocol.DEP** サービスは、次のプローブとモニターを使用して監視されます。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>プローブ</th>
<th>正常性セット</th>
<th>関連するモニター</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>なし (通知またはチェック)</p></td>
<td><p>OWA.Protocol.DEP</p></td>
<td><p>OwaIMInitializationFailedMonitor</p></td>
</tr>
<tr class="even">
<td><p>なし (通知またはチェック)</p></td>
<td><p>OWA.Protocol.DEP</p></td>
<td><p>WacDiscoveryFailureEventMonitor</p></td>
</tr>
</tbody>
</table>


プローブとモニターの詳細については、「[サーバーの状態とパフォーマンス](https://technet.microsoft.com/ja-jp/library/jj150551\(v=exchg.150\))」を参照してください。

## ユーザー操作

サービスは、警告の発行後に回復することがあります。そのため、**OWA.Protocol.DEP** 正常性セットが異常であることを示す警告を受け取ったときは、まず、その問題がまだ存在しているかどうかを確認します。問題が存在する場合は、次のセクションで説明する適切な回復操作を実行します。

## 次のエラーに対する回復処理:「InstantMessageOCSProvider.InitializeEndpointManager。IM プロバイダーのレジストリ設定はありません。」

このエラーは、必須のレジストリ キーがメールボックス サーバー上に存在しないを示しています。このレジストリ キーは、Microsoft Unified Communications Managed API (UCMA) 4.0 がサーバーにインストールされたときに構成されている必要があります。次のレジストリ キーが存在しません:

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\MSExchange OWA\InstantMessaging

このキーには、`Microsoft.Rtc.Internal.Ucweb` DLL を示す **ImplementationDLLPath** 文字列が含まれている必要があります。既定の場所は `C:\Program Files\Microsoft UCMA 4.0\Runtime\SSP\Microsoft.Rtc.Internal.Ucweb.dll` です。

この問題を修正するには、UCMA 4.0 を再インストールするか、またはレジストリ キーを手動で作成します。次の場所から UCMA 4.0 をダウンロードできます。[Unified Communications Managed API 4.0 ランタイム](http://go.microsoft.com/fwlink/p/?linkid=260990)

## 次のエラーに対する回復処理:「InstantMessageOCSProvider.InitializeEndpointManager。IM プロバイダーが見つかりません。」

このエラーは、`Microsoft.Rtc.Internal.Ucweb` DLL ファイルがメールボックス サーバー上に存在しないことを示しています。このファイルは、サーバーに UCMA 4.0 がインストールされたときにインストールされている必要があります。既定の場所は `C:\Program Files\Microsoft UCMA 4.0\Runtime\SSP` です。

この問題を修正するには、UCMA 4.0 を再インストールします。詳しくは、「[Unified Communications Managed API 4.0 ランタイム](http://go.microsoft.com/fwlink/p/?linkid=260990)」を参照してください。

## 次のエラーに対する回復処理:「web.config で、インスタント メッセージング サーバーの名前が NULL に設定されているか、または空になっています。」

このエラーは、メールボックス サーバー上の Outlook Web App アプリケーション構成 (web.config) ファイルに、Lync 2013 サーバーが定義されていないことを示しています。この `web.config` ファイルは `%ExchangeInstallPath%ClientAccess\Owa` にあり、Lync 2013 サーバーの FQDN を指定する **IMServerName** という名前のキーを含んでいる必要があります。この問題を修正するには、次の手順に従います。

1.  コマンド プロンプト ウィンドウで、次のコマンドを実行して Outlook Web App web.config ファイルをメモ帳で開きます。
    
        Notepad %ExchangeInstallPath%ClientAccess\Owa\web.config

2.  **IMServerName** という名前のキーを検索します。それが見つかった場合、Lync 2013 サーバーの FQDN を検証します。キーが見つからない場合は、以下の手順を実行してそれを追加します。
    
    1.  **\<appSettings\>** という名前のタグを見つけます。
    
    2.  **\<appSettings\>** ノードで、以下の行を追加します。
        
            <add key="IMServerName" value="Lync Server FQDN" />
        
        たとえば、次のように入力します。
        
            <add key="IMServerName" value="lync01.contoso.com" />
    
    3.  変更を Outlook Web App に適用するには、次のコマンドを実行します。
        
            %windir%\system32\inetsrv\appcmd.exe recycle apppool /apppool.name:"MSExchangeOWAAppPool"

## 次のエラーに対する回復処理:「web.config で、インスタント メッセージング証明書の拇印が NULL または空になっています。」

このエラーは、Lync 2013 と Outlook Web App の統合に使用される証明書が、メールボックス サーバー上の Outlook Web App アプリケーション構成 (web.config) ファイルに定義されていないことを示しています。この `web.config` ファイルは `%ExchangeInstallPath%ClientAccess\Owa` にあり、証明書の拇印 (ハッシュ) を指定する **IMCertificateThumbprint** という名前のキーを含んでいる必要があります。

**Get-ExchangeCertificate** コマンドレットを使用して、または、Exchange 管理センター (EAC) で <strong>サーバー</strong> \> <strong>証明書</strong> を選択して、証明書の拇印の値を取得できます。

この問題を修正するには、次の手順に従います。

1.  コマンド プロンプト ウィンドウで、次のコマンドを実行して Outlook Web App web.config ファイルをメモ帳で開きます。
    
        Notepad %ExchangeInstallPath%ClientAccess\Owa\web.config

2.  **IMCertificateThumbprint** という名前のキーを検索します。それが見つかった場合は、拇印の値が正しいことを確認します。キーが見つからない場合は、以下の手順を実行してそれを追加します。
    
    1.  **\<appSection\>** という名前のタグを見つけます。
    
    2.  **\<appSection\>** ノードで、以下の行を追加します。
        
            <add key="IMCertificateThumbprint" value="thumbprint"/>
        
        たとえば、次のように入力します。
        
            <add key="IMCertificateThumbprint" value="35CB4C441D55506C88E59B7946B567A4F45B3B5C" />
    
    3.  変更を Outlook Web App に適用するには、次のコマンドを実行します。
        
            %windir%\system32\inetsrv\appcmd.exe recycle apppool /apppool.name:"MSExchangeOWAAppPool"

## 次のエラーに対する回復処理:「拇印 \<値\> を含む IM 証明書が見つかりませんでした。」

このエラーは、Lync 2013 と Outlook Web App の統合に使用される証明書が、メールボックス サーバー上に見つからないことを示しています。この証明書は、メールボックス サーバーと Lync 2013サーバーにインストールされていて、両方のサーバーによって信頼されている必要があります。証明書の要件について詳しくは、「[Microsoft Lync Server 2013 および Microsoft Outlook Web App 2013 の統合](http://go.microsoft.com/fwlink/p/?linkid=280418)」の『Outlook Web App でインスタント メッセージングを有効にする』セクションを参照してください。

**Get-ExchangeCertificate** コマンドレットを使用して、または Exchange 管理センター (EAC) で <strong>サーバー</strong> \> <strong>証明書</strong> を選択して、エラーの拇印値を証明書に一致させることができます。

## 次のエラーに対する回復処理:「IM 証明書が期限切れです。」

このエラーは、Lync 2013 と Outlook Web App の統合に使用される証明書が期限切れであることを示しています。このエラーを解決するには、証明書を更新する必要があります。

**Get-ExchangeCertificate** コマンドレットを使用して、または Exchange 管理センター (EAC) で <strong>サーバー</strong> \> <strong>証明書</strong> を選択して、エラーの拇印値を証明書に一致させることができます。

## 次のエラーに対する回復処理:「IM 証明書がまだ有効になっていません。」

このエラーは、Lync 2013 と Outlook Web App の統合に使用される証明書の日付が無効であることを示しています。このエラーを解決するには、新しい証明書を構成する必要があり、`%ExchangeInstallPath%ClientAccess\Owa\web.config` の **IMCertificateThumbprint** キーに新しい拇印値を追加する必要があります。証明書の要件について詳しくは、「[Microsoft Lync Server 2013 および Microsoft Outlook Web App 2013 の統合](http://go.microsoft.com/fwlink/p/?linkid=280418)」の『Outlook Web App でインスタント メッセージングを有効にする』セクションを参照してください。

## 次のエラーに対する回復処理:「IM 証明書に秘密キーがありません。」

このエラーは、Lync 2013 と Outlook Web App の統合に使用される証明書に秘密キーがないことを示しています。このエラーを解決するには、秘密キーのある新しい証明書を構成する必要があり、`%ExchangeInstallPath%ClientAccess\Owa\web.config` の **IMCertificateThumbprint** キーに新しい拇印値を追加する必要があります。証明書の要件について詳しくは、「[Microsoft Lync Server 2013 および Microsoft Outlook Web App 2013 の統合](http://go.microsoft.com/fwlink/p/?linkid=280418)」の『Outlook Web App でインスタント メッセージングを有効にする』セクションを参照してください。

