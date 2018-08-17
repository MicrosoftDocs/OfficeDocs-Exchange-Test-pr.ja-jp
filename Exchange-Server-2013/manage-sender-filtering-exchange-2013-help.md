---
title: '送信者のフィルターの管理: Exchange 2013 Help'
TOCTitle: 送信者のフィルターの管理
ms:assetid: a7f4b3e1-2970-45ad-911e-a9f46d880d3d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124087(v=EXCHG.150)
ms:contentKeyID: 49896404
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 送信者のフィルターの管理

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-08_

送信者フィルターは送信者フィルター エージェントによって提供されます。送信者フィルター エージェントは、 **MAIL FROM:** に依存しています。RCPT TO: SMTP ヘッダーに基づいて、受信電子メール メッセージに対して行う処理がある場合にどの処理を行うかを判断します。

送信者のフィルター機能が Exchange サーバーで有効になっている場合、送信者のフィルター機能は、そのコンピューターのすべての受信コネクタを介して入ってくるメッセージをすべてフィルター処理します。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[スパム対策とマルウェア対策のアクセス許可](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)」の「スパム対策機能」。

  - この手順を実行するには、シェルを使用する必要があります。

  - 既定では、メールボックス サーバーのトランスポート サービスでスパム対策機能が有効になっていません。一般的には、Exchange 組織が受信メッセージの受信前にスパム対策フィルターを事前に設定しない場合に限り、スパム対策機能を有効にします。詳細については、「[メールボックス サーバーのスパム対策機能を有効にする](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用して送信者フィルターを有効または無効にする

送信者のフィルターを無効にするには、次のコマンドを実行します。

    Set-SenderFilterConfig -Enabled $false

送信者フィルターを有効にするには、次のコマンドを実行します。

    Set-SenderFilterConfig -Enabled $true


> [!NOTE]
> 送信者フィルターを無効にしても、基になる送信フィルター エージェントは有効のままです。送信者フィルター エージェントを無効にするには、次のコマンドを実行します。<CODE>Disable-TransportAgent "Sender Filter Agent"</CODE>



## 正常な動作を確認する方法

送信者フィルターの有効化または無効化が正常に実行されたことを確認するには、次の操作を行います。

1.  次のコマンドを実行します。
    
        Get-SenderFilterConfig | Format-List Enabled

2.  表示された値が構成した値であることを確認します。

## シェルを使用して、受信拒否者および受信拒否ドメインのリストを構成するには

既存の値を置き換えるには、次のコマンドを実行します。

    Set-SenderFilterConfig -BlockedSenders <sender1,sender2...> -BlockedDomains <domain1,domain2...> -BlockedDomainsAndSubdomains <domain1,domain2...>

この例では、kim@contoso.com および john@contoso.com からのメッセージ、fabrikam.com ドメインからのメッセージ、ならびに northwindtraders.com とそのすべてのサブドメインからのメッセージを受信拒否するよう送信者フィルター エージェントが構成されています。

    Set-SenderFilterConfig -BlockedSenders kim@contoso.com,john@contoso.com -BlockedDomains fabrikam.com -BlockedDomainsAndSubdomains northwindtraders.com

既存の値を変更せずにエントリを追加または削除するには、次のコマンドを実行します。

    Set-SenderFilterConfig -BlockedSenders @{Add="<sender1>","<sender2>"...; Remove="<sender1>","<sender2>"...} -BlockedDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...} -BlockedDomainsAndSubdomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

この例では、次の情報を指定して送信者フィルター エージェントを構成します。

  - chris@contoso.com および michelle@contoso.com を既存の受信拒否者リストに追加する。

  - tailspintoys.com を既存の受信拒否ドメインリストから削除する。

  - blueyonderairlines.com を既存の受信拒否ドメインおよびサブドメインリストに追加する。

<!-- end list -->

    Set-SenderFilterConfig -BlockedSenders @{Add="chris@contoso.com","michelle@contoso.com"} -BlockedDomains @{Remove="tailspintoys.com"} -BlockedDomainsAndSubdomains @{Add="blueyonderairlines.com"}

## 正常な動作を確認する方法

受信拒否が正常に設定されたことを確認するには、次の操作を実行します。

1.  次のコマンドを実行します。
    
        Get-SenderFilterConfig | Format-List BlockedSenders,BlockedDomains,BlockedDomainsAndSubdomains

2.  表示された値が構成した値であることを確認します。

## シェルを使用して、送信者が空白のメッセージに対する受信拒否を有効または無効にします。

送信者が空白のメッセージに対する受信拒否を有効または無効にするには、次のコマンドを実行します。

    Set-SenderFilterConfig -BlankSenderBlockingenabled <$true | $false>

この例では、MAIL FROM 欄に送信者が指定されていないメッセージを受信拒否するよう送信者フィルターが構成されています。SMTP コマンド:

    Set-SenderFilterConfig -BlankSenderBlockingEnabled $true

## 正常な動作を確認する方法

送信者が空白のメッセージに対する受信拒否が正常に実行されたことを確認するには、次の操作を行います。

1.  次のコマンドを実行します。
    
        Get-SenderFilterConfig | Format-List BlankSenderBlockingEnabled

2.  表示された値が構成した値であることを確認します。

