---
title: 'エッジ トランスポート サーバー上で添付ファイル フィルターを管理する: Exchange 2013 Help'
TOCTitle: エッジ トランスポート サーバー上で添付ファイル フィルターを管理する
ms:assetid: 2ec91cc6-6ade-48ee-88bb-66153874393d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997139(v=EXCHG.150)
ms:contentKeyID: 60830025
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# エッジ トランスポート サーバー上で添付ファイル フィルターを管理する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-08_

添付ファイル フィルターは、エッジ トランスポート サーバー上でのみ使用可能な添付ファイル フィルター エージェントから提供されます。添付ファイル フィルターは、電子メール メッセージに添付されたファイルを組織に入れないようにするのに役立ちます。添付ファイルをコンテンツ タイプ別またはファイル名別に絞り込むように 1 つ以上の添付ファイル フィルター エントリを構成できます。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:10 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[スパム対策とマルウェア対策のアクセス許可](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)」の「スパム対策機能」および「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「トランスポート エージェント」。

  - エッジ トランスポート サーバー上での添付ファイル フィルターの構成変更は、ローカル コンピューターにのみ反映されます。境界ネットワーク上に複数のエッジ トランスポート サーバーが存在する場合は、エッジ トランスポート サーバーごとに添付ファイル フィルターを構成する必要があります。

  - この手順を実行するには、シェルを使用する必要があります。

  - 添付ファイル フィルターを無効にして、Microsoft Exchange トランスポート サービスを再起動すると、すべての添付ファイル フィルター機能が動作を停止します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用して添付ファイル フィルターを有効または無効にする

添付ファイル フィルター エージェントを有効または無効にした場合は、Microsoft Exchange トランスポート サービスの再起動後に変更が反映されます。エッジ トランスポート サーバー上で Microsoft Exchange トランスポート サービスを再起動すると、サーバー上のメール フローが一時的に中断されます。

添付ファイル フィルターを無効にするには、次のコマンドを実行します。

```powershell
Disable-TransportAgent "Attachment Filtering Agent"
```

添付ファイル フィルターを有効にするには、次のコマンドを実行します。

```powershell
Enable-TransportAgent "Attachment Filtering Agent"
```

添付ファイル フィルターを有効まはた無効にしたら、次のコマンドを実行して、Microsoft Exchange トランスポート サービスを再起動します。

```powershell
Restart-Service MSExchangeTransport
```

## 正常な動作を確認する方法

添付ファイル フィルターが正常に有効化または無効化されたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
    ```powershell
Get-TransportAgent "Attachment Filtering Agent"
```

2.  **Enabled** の値が `True` の場合は、添付ファイル フィルターが有効になっています。この値が `False` の場合は、添付ファイル フィルターが無効になっています。

## シェルを使用して添付ファイル フィルター エントリを表示する

添付ファイル フィルター エントリは、組織に入れないようにするメッセージの添付ファイルを定義します。添付ファイル フィルター エージェントによって使用される添付ファイル フィルター エントリを表示するには、次のコマンドを実行します。

```powershell
Get-AttachmentFilterEntry | Format-Table
```

特定の MIME コンテンツ タイプ エントリを表示するには、次の構文を使用します。

```powershell
Get-AttachmentFilteringEntry ContentType:<MIMEContentType>
```

たとえば、JPEG イメージのコンテンツ タイプ エントリを表示するには、次のコマンドを実行します。

```powershell
Get-AttachmentFilteringEntry ContentType:image/jpeg
```

特定のファイル名またはファイル名拡張子のエントリを表示するには、次の構文を使用します。

```powershell
Get-AttachmentFilteringEntry FileName:<FileName or FileNameExtension>
```

たとえば、JPEG の添付ファイルのファイル名拡張子エントリを表示するには、次のコマンドを実行します。

    Get-AttachmentFilteringEntry FileName:*.jpg

## シェルを使用して添付ファイル フィルター エントリを追加する

MIME コンテンツ タイプで添付ファイルを絞り込む添付ファイル フィルター エントリを追加するには、次の構文を使用します。

```powershell
Add-AttachmentFilterEntry -Name <MIMEContentType> -Type ContentType
```

次の例では、JPEG イメージを絞り込む MIME コンテンツ タイプ エントリを追加します。

```powershell
Add-AttachmentFilterEntry -Name image/jpeg -Type ContentType
```

ファイル名またはファイル名拡張子で添付ファイルを絞り込む添付ファイル フィルター エントリを追加するには、次の構文を使用します。

```powershell
Add-AttachmentFilterEntry -Name <FileName or FileNameExtension> -Type FileName
```

次の例では、ファイル名拡張子が .jpg の添付ファイルを絞り込みます。

    Add-AttachmentFilterEntry -Name *.jpg -Type FileName

## 正常な動作を確認する方法

添付ファイル フィルター エントリが正常に追加されたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行して、フィルター エントリが存在することを確認します。
    
    ```powershell
Get-AttachmentFilterEntry | Format-Table
```

2.  外部のメールボックスから内部の受信者への禁止添付ファイルを含むテスト メッセージを送信して、そのメッセージが拒否、除去、または削除されることを確認します。

## シェルを使用して添付ファイル フィルター エントリを削除する

MIME コンテンツ タイプで添付ファイルを絞り込む添付ファイル フィルター エントリを削除するには、次の構文を使用します。

```powershell
Remove-AttachmentFilterEntry ContentType:<ContentType>
```

次の例では、JPEG 画像用の MIME コンテンツ タイプ エントリを削除します。

```powershell
Remove-AttachmentFilterEntry ContentType:image/jpeg
```

ファイル名またはファイル名拡張子で添付ファイルを絞り込む添付ファイル フィルター エントリを削除するには、次の構文を使用します。

```powershell
Remove-AttachmentFilterEntry FileName:<FileName or FileNameExtension>
```

次の例では, .jpg ファイル名拡張子用のファイル名エントリを削除します。

    Remove-AttachmentFilterEntry FileName:*.jpg

## 正常な動作を確認する方法

添付ファイル フィルター エントリが正常に削除されたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行して、フィルター エントリが削除されていることを確認します。
    
    ```powershell
Get-AttachmentFilterEntry | Format-Table
```

2.  外部のメールボックスから内部の受信者への配信が許可された添付ファイルを含むテスト メッセージを送信して、そのメッセージが添付ファイルと一緒に正常に配信されることを確認します。

## シェルを使用して添付ファイル フィルター アクションを表示する

メッセージ内で禁止添付ファイルが検出されたときに使用される添付ファイル フィルター アクションを表示するには、次のコマンドを実行します。

```powershell
Get-AttachmentFilterListConfig
```

## シェルを使用して添付ファイル フィルター アクションを構成する

メッセージ内で禁止添付ファイルが検出されたときに使用される添付ファイル フィルター アクションを構成するには、次の構文を使用します。

    Set-AttachmentFilterListConfig [-Action <Reject | Strip | SilentDelete>] [-RejectResponse "<Message text>"] [-AdminMessage "<Replacement file text>"] [-ExceptionConnectors <ConnectorGUID>]

この例では、添付ファイル フィルター構成に次のような変更を加えます。

  - 禁止添付ファイルを含むメッセージを拒否 (ブロック) します。

  - 拒否されたメッセージに対するカスタム応答を使用します。

<!-- end list -->

    Set-AttachmentFilterListConfig -Action Reject -RejectResponse "This message contains a prohibited attachment. Your message can't be delivered. Please resend the message without the attachment."

詳細については、「[Set-AttachmentFilterListConfig](https://technet.microsoft.com/ja-jp/library/bb123483\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

添付ファイル フィルター アクションが正常に構成されたことを確認するには、禁止添付ファイルを含むテスト メッセージを外部のメールボックスから内部の受信者に送信して、そのメッセージと添付ファイルが想定どおりに処理されることを確認します。

