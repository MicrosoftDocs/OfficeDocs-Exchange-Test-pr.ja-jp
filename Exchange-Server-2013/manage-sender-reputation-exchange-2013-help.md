---
title: '送信者評価の管理: Exchange 2013 Help'
TOCTitle: 送信者評価の管理
ms:assetid: f2716bd9-e3ac-46d9-9264-4e3dabfa0f38
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb125186(v=EXCHG.150)
ms:contentKeyID: 49896550
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 送信者評価の管理

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-08_

送信者評価は、プロトコル分析エージェントによって提供されます。送信者評価は、送信者のさまざまな特徴に従ってメッセージをブロックします。送信者評価では、送信者に関して保持されたデータを使用して、受信メッセージに対して行う処理を決定します。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[スパム対策とマルウェア対策のアクセス許可](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)」の「スパム対策機能」。

  - この手順を実行するには、シェルを使用する必要があります。

  - 既定では、メールボックス サーバーのトランスポート サービスでスパム対策機能が有効になっていません。一般的には、Exchange 組織が受信メッセージの受信前にスパム対策フィルターを事前に設定しない場合に限り、スパム対策機能を有効にします。詳細については、「[メールボックス サーバーのスパム対策機能を有効にする](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)」を参照してください。

  - プロトコル分析エージェントは、送信者評価機能の基礎となるエージェントです。送信者評価を無効にしても、プロトコル分析エージェントは依然有効です。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用して送信者評価を有効または無効にする

この例では送信者評価を無効にします。

    Set-SenderReputationConfig -Enabled $false

この例では送信者評価を有効にします。

    Set-SenderReputationConfig -Enabled $true

## 正常な動作を確認する方法

送信者評価を正常に有効または無効にしたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行して、プロトコル分析エージェントがインストールされ有効になっていることを確認します。
    
        Get-TransportAgent

2.  次のコマンドを実行して、構成した送信者評価の値を確認します。
    
        Get-SenderReputationConfig | Format-List Enabled,*MailEnabled

## シェルを使用して、内部メッセージまたは外部メッセージの送信者評価を有効または無効にする

既定では、送信者評価は外部メッセージの場合は有効で、内部メッセージの場合は無効です。Exchange 組織から見て外部に当たる認証のない接続から受信したメッセージは、外部メッセージとみなされます。認証のない接続から受信したメッセージでも、送信者のドメインが Exchange 組織内部で権限のあるドメインとして構成されている場合は、内部メッセージとみなされます。

外部メッセージの送信者評価を無効にするには、次のコマンドを実行します。

    Set-SenderReputationConfig -ExternalMailEnabled $false

外部メッセージの送信者評価を有効にするには、次のコマンドを実行します。

    Set-SenderReputationConfig -ExternalMailEnabled $true

内部メッセージの送信者評価を無効にするには、次のコマンドを実行します。

    Set-SenderReputationConfig -InternalMailEnabled $false

内部メッセージの送信者評価を有効にするには、次のコマンドを実行します。

    Set-SenderReputationConfig -InternalMailEnabled $true

## 正常な動作を確認する方法

内部および外部メッセージの送信者評価を正常に有効または無効にしたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
        Get-SenderReputationConfig | Format-List Enabled,*MailEnabled

2.  表示される値が設定値と一致することを確認します。

## シェルを使用して送信者評価のプロパティを構成する

送信者評価プロパティを構成するには、次のコマンドを実行します。

    Set-SenderReputationConfig -SrlBlockThreshold <Value> -SenderBlockingPeriod <Hours>

この例では、送信者評価レベル (SRL) 禁止しきい値を 6 に設定し、違反送信者を IP 禁止一覧に 36 時間追加するように送信者評価を構成します。

    Set-SenderReputationConfig -SrlBlockThreshold 6 -SenderBlockingPeriod 36

## 正常な動作を確認する方法

送信者評価プロパティを正常に構成にしたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
        Get-SenderReputationConfig

2.  表示される値が設定値と一致することを確認します。

## シェルを使用してオープン プロキシ サーバーを検出するための送信アクセスを構成する

インターネットとプロトコル分析エージェントを実行する Exchange サーバー間での送信者評価のファイアウォール通過を許可するために、追加ステップを実行しなければならない場合があります。次の表に、送信者評価のために必要な送信用ポートの一覧を示します。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロトコル</th>
<th>ポート</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SOCKS4、SOCKS5</p></td>
<td><p>1081, 1080</p></td>
</tr>
<tr class="even">
<td><p>Wingate、Telnet、Cisco</p></td>
<td><p>23</p></td>
</tr>
<tr class="odd">
<td><p>HTTP CONNECT、HTTP POST</p></td>
<td><p>6588, 3128, 80</p></td>
</tr>
</tbody>
</table>


オープン プロキシ サーバーを検出するための送信アクセスを構成するには、次のコマンドを実行します。

    Set-SenderReputationConfig -ProxyServerName <String> -ProxyServerPort <Port> -ProxyServerType <String>

この例では、HTTP 接続プロトコルをポート 80 で使用する SERVER01 という名前のオープン プロキシ サーバーを使用するように送信者評価を構成します。

    Set-SenderReputationConfig - ProxyServerName SERVER01 -ProxyServerPort 80 -ProxyServerType HttpConnect

## 正常な動作を確認する方法

オープン プロキシ サーバーの検出のために送信アクセスを正常に構成にしたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
        Get-SenderReputationConfig | Format-List ProxyServer*

2.  表示された値が構成した値であることを確認します。

