---
title: 'エッジ トランスポート サーバーでの受信者フィルターの管理: Exchange 2013 Help'
TOCTitle: エッジ トランスポート サーバーでの受信者フィルターの管理
ms:assetid: f2d0041f-2872-4669-95ec-443233f4956d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb125187(v=EXCHG.150)
ms:contentKeyID: 49896552
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# エッジ トランスポート サーバーでの受信者フィルターの管理

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-08_

受信者フィルターは受信者フィルター エージェントによって提供されます。Exchange サーバーで受信者フィルターを有効にすると、インターネットから入ってくるが認証されていない受信メッセージがフィルター処理されます。これらのメッセージは外部メッセージとして処理されます。


> [!NOTE]
> メールボックス サーバー上で受信者フィルター エージェントを利用することは可能ですが、それは設定しないようにしてください。メールボックス サーバー上の受信者フィルターによってメッセージ中に無効な、またはブロックされている受信者が検出された場合、他の有効な受信者がそのメッセージに含まれていても、メッセージは拒否されます。メールボックス サーバー上にスパム対策エージェントをインストールすると、既定の動作として受信者フィルター エージェントが有効になります。しかし、その時点ではどの受信者も禁止しない構成になっています。詳細については、「<A href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">メールボックス サーバーのスパム対策機能を有効にする</A>」を参照してください。



## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[スパム対策とマルウェア対策のアクセス許可](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)」の「スパム対策機能」。

  - この手順を実行するには、シェルを使用する必要があります。

  - 既定では、メールボックス サーバーのトランスポート サービスでスパム対策機能が有効になっていません。一般的には、Exchange 組織が受信メッセージの受信前にスパム対策フィルターを事前に設定しない場合に限り、スパム対策機能を有効にします。詳細については、「[メールボックス サーバーのスパム対策機能を有効にする](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)」を参照してください。

  - **Set-AcceptedDomain** コマンドレットの *AddressBookEnabled* パラメーターにより、承認済みドメインに所属する受信者の受信者フィルターを有効または無効にすることができます。既定では、受信者フィルターは権限のあるドメインについては有効、内部の中継ドメインおよび外部の中継ドメインについては無効になっています。組織の承認済みドメインの *AddressBookEnabled* パラメーターのステータスを表示するには、次のコマンドを実行します。
    
    ```powershell
Get-AcceptedDomain | Format-List Name,AddressBookEnabled
```

  - このトピックの手順を使用して受信者フィルターを無効にすると、受信者フィルターの機能は無効になりますが、ベースになっている受信者フィルター エージェントは有効な状態を維持します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用して受信者フィルターを有効または無効にする

受信者のフィルターを無効にするには、次のコマンドを実行します。

```powershell
Set-RecipientFilterConfig -Enabled $false
```

受信者のフィルターを有効にするには、次のコマンドを実行します。

```powershell
Set-RecipientFilterConfig -Enabled $true
```


> [!NOTE]
> 受信者フィルターを無効にしても、ベースになっている受信者フィルター エージェントは有効な状態を維持します。受信者フィルター エージェントを無効にするには、次のコマンドを実行します。<CODE>Disable-TransportAgent "Recipient Filter Agent"</CODE>.



## 正常な動作を確認する方法

受信者フィルターを正常に有効または無効にしたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
    ```powershell
Get-RecipientFilterConfig | Format-List Enabled
```

2.  表示された値が構成した値であることを確認します。

## シェルを使用して受信者禁止一覧を有効または無効にする

次のコマンドを実行します。

```powershell
Set-RecipientFilterConfig -BlockListEnabled <$true | $false>
```

この例では、受信者禁止一覧を有効にします。

```powershell
Set-RecipientFilterConfig -BlockListEnabled $true
```

## 正常な動作を確認する方法

受信者禁止一覧を正常に有効または無効にしたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
    ```powershell
Get-RecipientFilterConfig | Format-List BlockListEnabled
```

2.  表示された値が構成した値であることを確認します。

## シェルを使用して受信者IP禁止一覧を構成する

既存の値を置き換えるには、次のコマンドを実行します。

```powershell
Set-RecipientFilterConfig -BlockedRecipients <recipient1,recipient2...>
```

この例では、valuesmark@contoso.com と kim@contoso.com を含む受信者禁止一覧を構成します。

```powershell
Set-RecipientFilterConfig -BlockedRecipients mark@contoso.com,kim@contoso.com
```

既存の値を変更せずにエントリを追加または削除するには、次のコマンドを実行します。

    Set-RecipientFilterConfig -BlockedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...}

この例では、受信者の一覧に chris@contoso.com が追加され、受信者禁止リストの受信者の一覧から michelle@contoso.com が削除されます。

    Set-RecipientFilterConfig -BlockedRecipients @{Add="chris@contoso.com"; Remove="michelle@contoso.com"}

## 正常な動作を確認する方法

受信者禁止一覧を正常に構成したことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
    ```powershell
Get-RecipientFilterConfig | Format-List BlockedRecipients
```

2.  表示された値が構成した値であることを確認します。

## シェルを使用して受信者参照を有効または無効にする

次のコマンドを実行します。

```powershell
Set-RecipientFilterConfig -RecipientValidationEnabled <$true | $false>
```

組織に存在しない受信者に対するメッセージをブロックするには、以下のコマンドを実行します。

```powershell
Set-RecipientFilterConfig -RecipientValidationEnabled $true
```

## 正常な動作を確認する方法

受信者参照を正常に有効または無効にしたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
    ```powershell
Get-RecipientFilterConfig | Format-List RecipientValidationEnabled
```

2.  表示された値が構成した値であることを確認します。

