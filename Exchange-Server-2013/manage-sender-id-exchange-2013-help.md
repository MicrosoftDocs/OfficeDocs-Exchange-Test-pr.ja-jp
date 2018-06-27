---
title: '送信者 ID の管理: Exchange 2013 Help'
TOCTitle: 送信者 ID の管理
ms:assetid: 2e7b646a-8a66-4be7-a7c1-0bd43bb79a5b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997136(v=EXCHG.150)
ms:contentKeyID: 49896193
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 送信者 ID の管理

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-04-08_

Sender ID 機能は、Sender ID エージェントの機能です。Sender ID は、送信者の IP アドレスを、送信者ドメインの所有者とされる名前と照合して、電子メール メッセージの発信元を確認します。Sender ID のフィルター処理の対象は、発信元がインターネットで、認証されていない受信メッセージです。これらのメッセージは外部メッセージとして処理されます。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[スパム対策とマルウェア対策のアクセス許可](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)」の「スパム対策機能」。

  - この手順を実行するには、シェルを使用する必要があります。

  - 既定では、メールボックス サーバーのトランスポート サービスでスパム対策機能が有効になっていません。一般的には、Exchange 組織が受信メッセージの受信前にスパム対策フィルターを事前に設定しない場合に限り、スパム対策機能を有効にします。詳細については、「[メールボックス サーバーのスパム対策機能を有効にする](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用して Sender ID を有効または無効にする

Sender ID を無効にするには、次のコマンドを実行します。

    Set-SenderIDConfig -Enabled $false

Sender ID を有効にするには、次のコマンドを実行します。

    Set-SenderIDConfig -Enabled $true


> [!NOTE]
> Sender ID を無効にしても、基になる Sender ID エージェントは引き続き有効です。Sender ID エージェントを無効にするには、<CODE>Disable-TransportAgent "Sender ID Agent"</CODE> コマンドを実行します。



## 正常な動作を確認する方法

Sender ID を正常に、有効または無効にできたことを確認するには、以下の手順を実行します。

1.  次のコマンドを実行します。
    
        Get-SenderIDConfig | Format-List Enabled

2.  表示された値が構成した値であることを確認します。

## シェルを使用してスプーフィングされたメッセージに対する Sender ID アクションを構成する

スプーフィングされたメッセージに対する Sender ID アクションを構成するには、以下のコマンドを実行します。

    Set-SenderIDConfig -SpoofedDomainAction <StampStatus | Reject | Delete>

この例では、送信サーバーの IP アドレスが、送信ドメインの DNS Sender Policy Framework (SPF) レコードに、権限のある SMTP 送信サーバーとして一覧に掲載されていない場合、すべてのメッセージを拒否するように Sender ID エージェントを構成します。

    Set-SenderIDConfig -SpoofedDomainAction Reject

## 正常な動作を確認する方法

スプーフィングされたメッセージに対して Sender ID アクションが正しく構成されたことを確認するには、以下の手順を実行します。

1.  次のコマンドを実行します。
    
        Get-SenderIDConfig | Format-List SpoofedDomainAction

2.  表示された値が構成した値であることを確認します。

## シェルを使用して一時的なエラーに対する Sender ID アクションを構成する

一時的なエラーに対する Sender ID アクションを構成するには、以下のコマンドを実行します。

    Set-SenderIDConfig -TempErrorAction <StampStatus | Reject | Delete>

この例では、一時的な DNS サーバー エラーで Sender ID 状態を判定できないメッセージにスタンプを設定するように Sender ID エージェントを構成します。メッセージは他のスパム対策エージェントによって処理されて、コンテンツ フィルター エージェントはメッセージの SCL 値を特定する際にこのマークを使用します。

    Set-SenderIDConfig -TempErrorAction StampStatus

`StampStatus` は、*TempErrorAction* パラメーターの既定値です。

## 正常な動作を確認する方法

一時的なエラーに対して Sender ID アクションが正しく構成されたことを確認するには、以下の手順を実行します。

1.  次のコマンドを実行します。
    
        Get-SenderIDConfig | Format-List TempErrorAction

2.  表示された値が構成した値であることを確認します。

## シェルを使用して受信者ドメインおよび送信者ドメインの例外を構成する

既存の値を置き換えるには、次のコマンドを実行します。

    Set-SenderIDConfig -BypassedRecipients <recipient1,recipient2...> -BypassedSenderDomains <domain1,domain2...>

この例では、kim@contoso.com と john@contoso.com 宛ての送信メッセージと、fabrikam.com domain 発の受信メッセージで、Sender ID チェックをバイパスするように Sender ID エージェントを構成します。

    Set-SenderIDConfig -BypassedRecipients kim@contoso.com,john@contoso.com -BypassedSenderDomains fabrikam.com

既存の値を変更せずにエントリを追加または削除するには、次のコマンドを実行します。

    Set-SenderIDConfig -BypassedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...} -BypassedSenderDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

この例では、以下の情報で Sender ID エージェントを構成します。

  - Sender ID チェックをバイパスする既存の受信者一覧に chris@contoso.com と michelle@contoso.com を追加します。

  - Sender ID チェックをバイパスする既存の受信者一覧から tailspintoys.com を削除します。

<!-- end list -->

    Set-SenderIDConfig -BypassedRecipients @{Add="chris@contoso.com","michelle@contoso.com"} -BypassedSenderDomains @{Remove="tailspintoys.com"}

## 正常な動作を確認する方法

受信者と送信者のドメイン除外を正常に構成できたことを確認するには、以下の手順を実行します。

1.  次のコマンドを実行します。
    
        Get-SenderIDConfig | Format-List BypassedRecipients,BypassedSenderDomains

2.  表示された値が構成した値であることを確認します。

