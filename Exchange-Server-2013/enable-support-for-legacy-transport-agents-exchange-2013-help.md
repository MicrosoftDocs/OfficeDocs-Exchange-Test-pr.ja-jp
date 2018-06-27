---
title: '従来のトランスポート エージェントのサポートを有効にする: Exchange 2013 Help'
TOCTitle: 従来のトランスポート エージェントのサポートを有効にする
ms:assetid: 00617e87-7199-406e-b4a3-94378f657f1f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ591524(v=EXCHG.150)
ms:contentKeyID: 49115877
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 従来のトランスポート エージェントのサポートを有効にする

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-03-09_

Microsoft Exchange Server 2013 では、Microsoft .NET Framework バージョン 4.0 を使用して作成されたトランスポート エージェントが既定でサポートされます。Exchange 2013 は、以前のバージョンの .NET Framework を使用して作成されたトランスポート エージェントをサポートしますが、これらの従来のトランスポート エージェントは既定では有効になっていません。従来のトランスポート エージェントを有効にするには、適切な XML アプリケーション構成ファイルを変更する必要があります。変更する必要があるファイルは、トランスポート エージェントがインストールされている位置によって異なります。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>サーバー</th>
<th>アプリケーション構成ファイル</th>
<th>Microsoft Windows サービス</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>クライアント アクセス サーバー</p></td>
<td><p>%ExchangeInstallPath%Bin\MSExchangeFrontendTransport.exe.config</p></td>
<td><p>Microsoft Exchange フロント エンド トランスポート (MSExchangeFrontendTransport)</p></td>
</tr>
<tr class="even">
<td><p>メールボックス サーバー</p></td>
<td><ul>
<li><p>%ExchangeInstallPath%Bin\EdgeTransport.exe.config</p></li>
<li><p>%ExchangeInstallPath%Bin\MSExchangeTransport.exe.config</p></li>
</ul></td>
<td><p>Microsoft Exchange トランスポート (MSExchangeTransport)</p></td>
</tr>
</tbody>
</table>


従来のトランスポート エージェントのサポートは、アプリケーション構成ファイル内のキーによって制御されます。既定では、必要なキーがアプリケーション構成ファイル内にありません。これらのキーは手動で追加する必要があります。次の表で、それぞれのキーを詳しく説明します。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>キー</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>useLegacyV2RuntimeActivationPolicy</em></p></td>
<td><p>このキーで、従来のトランスポート エージェントのサポートを有効または無効にします。このキーの有効な値は、<code>true</code> または <code>false</code> です。このキーが指定されていない場合、既定値は <code>false</code> です。</p></td>
</tr>
<tr class="even">
<td><p><em>supportedRuntime version</em></p></td>
<td><p>このキーには、エージェントが必要とする Microsoft .NET Framework のバージョンを指定します。このキーで有効な値は以下のとおりです。</p>
<ul>
<li><p><code>v4.0</code> または<code>v4.0.30319</code></p></li>
<li><p><code>v3.5</code> または<code>v3.5.21022</code></p></li>
<li><p><code>v3.0</code> または<code>v3.0.4506</code></p></li>
<li><p><code>v2.0</code> または<code>v2.0.50727</code></p></li>
</ul>
<p><em>supportedRuntime version</em> キーの複数の独立したインスタンスを使用して、複数の値を指定します。</p>
<p><em>useLegacyV2RuntimeActivationPolicy</em> キーを使用して従来のトランスポート エージェントを有効にする場合、従来のトランスポート エージェントが必要とする値とともに、値 <code>v4.0</code> を常に指定する必要があります。</p></td>
</tr>
</tbody>
</table>


## 始める前に把握しておくべき情報

  - 予想所要時間 : 15 分

  - Exchange のアクセス許可は、このトピックの手順には適用されません。これらの手順は、Exchange Server のオペレーティング システムで実行されます。

  - アプリケーション構成ファイルに保存する変更は、対応するサービスを再起動した後に適用されます。

  - アプリケーション構成ファイルに関連付けられたサービスのいずれかを再起動すると、サーバー上のメール フローが一時的に中断されます。

  - Exchange XML アプリケーション構成ファイルで行うカスタマイズ済みのサーバーごとの設定 (クライアント アクセス サーバーの web.config ファイルまたはメールボックス サーバーの EdgeTransport.exe.config ファイルなど) は、Exchange 累積更新プログラム (CU) のインストール時に上書きされます。インストール後にサーバーを簡単に再構成できるよう、必ずこの情報を保存しておいてください。これらの設定は、Exchange 累積更新プログラムのインストール後に構成し直す必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## コマンド プロンプトを使用して、従来のトランスポート エージェントのサポートを構成する

従来のトランスポート エージェントのサポートを有効にするには、次の手順を使用します。

1.  従来のトランスポート エージェント サポートを構成する Exchange 2013 サーバーのコマンド プロンプト ウィンドウで、次のコマンドを実行することによって、適切なアプリケーション構成ファイルをメモ帳で開きます。
    
        Notepad %ExchangeInstallPath%Bin\<AppConfigFile>
    
    たとえば、メールボックス サーバーの EdgeTransport.exe.config ファイルを開くには、次のコマンドを実行します。
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  ファイルの終わりにある *\</configuration\>* キーを探して、次のキーを *\</configuration\>* キーの前に貼り付けます。
    
        <startup useLegacyV2RuntimeActivationPolicy="true">
           <supportedRuntime version="v4.0" />
           <supportedRuntime version="v3.5" />
           <supportedRuntime version="v3.0" />
           <supportedRuntime version="v2.0" />
        </startup>

3.  完了したら、アプリケーション構成ファイルを保存して閉じます。

4.  手順 1 ～ 3 を繰り返して、他のアプリケーション構成ファイルを変更します。

5.  次のコマンドを実行して、関連する Windows サービスを再起動します。
    
        net stop <service> && net start <service>
    
    たとえば、EdgeTransport.exe.config ファイルを変更した場合、次のコマンドを実行して Microsoft Exchange トランスポート サービスを再起動する必要があります。
    
        net stop MSExchangeTransport && net start MSExchangeTransport

6.  手順 5 を繰り返して、他の変更済みアプリケーション構成ファイルに関連付けられたサービスを再起動します。

## 正常な動作を確認する方法

従来のトランスポート エージェントが正常にインストールされたら、この手順が機能したことがわかります。このトピックの手順を実行せずに従来のトランスポート エージェントをインストールしようとすると、次のようなエラーが表示されます。

    Mixed mode assembly is built against version '<version>' of the runtime and cannot be loaded in the 4.0 runtime without additional configuration information.

