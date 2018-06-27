---
title: 'コンテンツ フィルターの管理: Exchange 2013 Help'
TOCTitle: コンテンツ フィルターの管理
ms:assetid: 05bd9d39-81dc-4514-8b75-7be386d5bcad
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa995953(v=EXCHG.150)
ms:contentKeyID: 49895223
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# コンテンツ フィルターの管理

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-04-08_

コンテンツ フィルターは、コンテンツ フィルター エージェントによって提供されます。コンテンツ フィルター エージェントは、Exchange サーバー上のすべての受信コネクタを通過するすべてのメッセージをフィルター処理します。認証されていないソースから届いたメッセージだけがフィルター処理されます。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:10 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[スパム対策とマルウェア対策のアクセス許可](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)」の「スパム対策機能」。

  - この手順を実行するには、シェルを使用する必要があります。

  - 既定では、メールボックス サーバーのトランスポート サービスでスパム対策機能が有効になっていません。一般的には、Exchange 組織が受信メッセージの受信前にスパム対策フィルターを事前に設定しない場合に限り、スパム対策機能を有効にします。詳細については、「[メールボックス サーバーのスパム対策機能を有効にする](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用してコンテンツ フィルターを有効または無効にする

コンテンツ フィルターを無効にするには、次のコマンドを実行します。

    Set-ContentFilterConfig -Enabled $false

コンテンツ フィルターを有効にするには、次のコマンドを実行します。

    Set-ContentFilterConfig -Enabled $true


> [!NOTE]
> コンテンツ フィルターを無効にしても、基になるコンテンツ フィルター エージェントがまだ有効です。コンテンツ フィルター エージェントを無効にするには、次のコマンドを実行します。<CODE>Disable-TransportAgent "Content Filter Agent"</CODE>.



## 正常な動作を確認する方法

コンテンツ フィルターが正常に有効または無効にされたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
        Get-ContentFilterConfig | Format-List Enabled

2.  表示される *Enabled* プロパティの値を確認します。

## シェルを使用して外部メッセージのコンテンツ フィルターを有効または無効にする

既定では、コンテンツ フィルター機能は外部メッセージに対して有効になっています。

外部メッセージに対してコンテンツ フィルターを無効にするには、次のコマンドを実行します。

    Set-ContentFilterConfig -ExternalMailEnabled $false

外部メッセージに対してコンテンツ フィルターを有効にするには、次のコマンドを実行します。

    Set-ContentFilterConfig -ExternalMailEnabled $true

## 正常な動作を確認する方法

外部メッセージに対してコンテンツ フィルターが正常に有効または無効にされたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
        Get-ContentFilterConfig | Format-List ExternalMailEnabled

2.  表示される *ExternalMailEnabled* プロパティの値を確認します。

## シェルを使用して内部メッセージのコンテンツ フィルターを有効または無効にする

信頼のおけるパートナーや組織内からのメッセージをフィルター処理しないようにお勧めします。スパム対策フィルターを実行する際には、正当なメッセージを誤ってフィルター処理する可能性が常に存在します。正当な電子メール メッセージを誤ってフィルター処理する可能性を減らすには、信頼されていないソースや未知のソースから送信された可能性のあるメッセージに対してのみ、スパム対策エージェントが機能するように設定する必要があります。

内部メッセージに対してコンテンツ フィルターを有効にするには、次のコマンドを実行します。

    Set-ContentFilterConfig -InternalMailEnabled $true

内部メッセージに対してコンテンツ フィルターを無効にするには、次のコマンドを実行します。

    Set-ContentFilterConfig -InternalMailEnabled $false

## 正常な動作を確認する方法

内部メッセージに対してコンテンツ フィルターが正常に有効または無効にされたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
        Get-ContentFilterConfig | Format-List InternalMailEnabled

2.  表示される *InternalMailEnabled* プロパティの値を確認します。

## シェルを使用して受信者と送信者の例外を構成する

既存の値を置き換えるには、次のコマンドを実行します。

    Set-ContentFilterConfig -BypassedRecipients <recipient1,recipient2...> -BypassedSenders <sender1,sender2...> -BypassedSenderDomains <domain1,domain2...>

この例は、コンテンツ フィルターで次の例外を構成します。

  - 受信者の laura@contoso.com と julia@contoso.com は、コンテンツ フィルターによってチェックされません。

  - 送信者の steve@fabrikam.com と cindy@fabrikam.com は、コンテンツ フィルターによってチェックされません。

  - ドメイン nwtraders.com のすべての送信者とすべてのサブドメインは、コンテンツ フィルターによってチェックされません。

<!-- end list -->

    Set-ContentFilterConfig -BypassedRecipients laura@contoso.com,julia@contoso.com -BypassedSenders steve@fabrikam.com,cindy@fabrikam.com -BypassedSenderDomains *.nwtraders.com

既存の値を変更せずにエントリを追加または削除するには、次のコマンドを実行します。

    Set-ContentFilterConfig -BypassedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...} -BypassedSenders @{Add="<sender1>","<sender2>"...; Remove="<sender1>","<sender2>"...} -BypassedSenderDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

この例は、コンテンツ フィルターで次の例外を構成します。

  - tiffany@contoso.com と chris@contoso.com をコンテンツ フィルターによってチェックされない既存の受信者リストに追加します。

  - joe@fabrikam.com と michelle@fabrikam.com をコンテンツ フィルターによってチェックされない既存の送信者リストに追加します。

  - blueyonderairlines.com をコンテンツ フィルターによって送信者がチェックされない既存のドメインのリストに追加します。

  - ドメイン woodgrovebank.com とすべてのサブドメインをコンテンツ フィルターによって送信者がチェックされない既存のドメインのリストから削除します。

<!-- end list -->

    Set-ContentFilterConfig -BypassedRecipients @{Add="tiffany@contoso.com","chris@contoso.com"} -BypassedSenders @{Add="joe@fabrikam.com","michelle@fabrikam.com"} -BypassedSenderDomains @{Add="blueyonderairlines.com"; Remove="*.woodgrovebank.com"}

## 正常な動作を確認する方法

受信者および送信者の例外が正常に構成されたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
        Get-ContentFilterConfig | Format-List Bypassed*

2.  表示される値が指定した設定と一致することを確認します。

## シェルを使用して許可または禁止する語句を構成する

許可およびブロックされる単語と語句を追加するには、次のコマンドを実行します。

    Add-ContentFilterPhrase -Influence GoodWord -Phrase <Phrase> -Influence BadWord -Phrase <Phrase>

この例では、語句 "customer feedback" を含むすべてのメッセージを許可します。

    Add-ContentFilterPhrase -Influence GoodWord -Phrase "customer feedback"

この例では、語句 "stock tip" を含むすべてのメッセージをブロックします。

    Add-ContentFilterPhrase -Influence BadWord -Phrase "stock tip"

許可またはブロックされた語句を削除するには、次のコマンドを実行します。

    Remove-ContentFilterPhrase -Phrase <Phrase>

この例では、語句 "stock tip" を削除します。

    Remove-ContentFilterPhrase -Phrase "stock tip"

## 正常な動作を確認する方法

許可およびブロックされた語句が正常に構成されたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
        Get-ContentFilterPhrase | Format-List Influence,Phrase

2.  表示される値が指定した設定と一致することを確認します。

## シェルを使用して SCL のしきい値を構成する

Spam Confidence Level (SCL) のしきい値およびアクションを構成するには、次のコマンドを実行します。

    Set-ContentFilterConfig -SCLDeleteEnabled <$true | $false> -SCLDeleteThreshold <Value> -SCLRejectEnabled <$true | $false> -SCLRejectThreshold <Value> -SCLQuarantineEnabled <$true | $false> -SCLQuarantineThreshold <Value>


> [!NOTE]
> 削除アクションの方が拒否アクションより優先され、拒否アクションの方が検疫アクションより優先されます。したがって、SCL による削除アクションのしきい値は、SCL による拒否アクションのしきい値よりも大きい値である必要があります。同じく、拒否アクションのしきい値は、SCL による検疫アクションのしきい値よりも大きい値である必要があります。拒否アクションのみが既定で有効であり、SCL しきい値は 7 です。



この例では、SCL しきい値に次の各値を構成します。

  - 削除アクションが有効にされ、対応する SCL しきい値が 9 に設定されます。

  - 拒否アクションが有効にされ、対応する SCL しきい値が 8 に設定されます。

  - 検疫アクションが有効にされ、対応する SCL しきい値が 7 に設定されます。

<!-- end list -->

    Set-ContentFilterConfig -SCLDeleteEnabled $true -SCLDeleteThreshold 9 -SCLRejectEnabled $true -SCLRejectThreshold 8 -SCLQuarantineEnabled $true -SCLQuarantineThreshold 7

## 正常な動作を確認する方法

SCL しきい値が正常に構成されたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
        Get-ContentFilterConfig | Format-List SCL*

2.  表示される値が指定した設定と一致することを確認します。

## シェルを使用して拒否応答を構成する

拒否アクションが有効になっている場合、メッセージ送信者に送信される拒否応答をカスタマイズできます。拒否応答には 240 文字まで入力できます。

カスタム拒否応答を構成するには、次のコマンドを実行します。

    Set-ContentFilterConfig -RejectionResponse "<Custom Text>"

この例では、カスタマイズした拒否応答を送信するよう、コンテンツ フィルター エージェントを構成します。

    Set-ContentFilterConfig -RejectionResponse "Your message was rejected because it appears to be SPAM."

## 正常な動作を確認する方法

拒否応答が正常に構成されたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
        Get-ContentFilterConfig | Format-List *Reject*

2.  表示される値が指定した設定と一致することを確認します。

## シェルを使用して Outlook 電子メールの消印を有効または無効にする

*\[Outlook 電子メールの消印\]* の検証は、受信者のメッセージング システムが正当な電子メールと迷惑メールを区別するために、Microsoft Outlook が送信メッセージに適用するコンピューターによる証拠です。消印は、Outlook 2007 以降で使用可能です。消印を使用することで、誤検知を減らすことができます。Outlook 電子メールの消印は既定で有効です。

Outlook 電子メールの消印を無効にするには、次のコマンドを実行します。

    Set-ContentFilterConfig -OutlookEmailPostmarkValidationEnabled $false

Outlook 電子メールの消印を有効にするには、次のコマンドを実行します。

    Set-ContentFilterConfig -OutlookEmailPostmarkValidationEnabled $true

## 正常な動作を確認する方法

Outlook 電子メールの消印が正常に構成されたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
        Get-ContentFilterConfig | Format-List OutlookEmailPostmarkValidationEnabled

2.  表示される値が指定した設定と一致することを確認します。

