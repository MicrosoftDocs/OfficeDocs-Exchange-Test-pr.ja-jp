---
title: 'DSN メッセージの管理: Exchange 2013 Help'
TOCTitle: DSN メッセージの管理
ms:assetid: 23c9d844-6fc7-44c9-a308-587338281611
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa996803(v=EXCHG.150)
ms:contentKeyID: 49895294
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- 拒否メッセージの変更
- NDR メッセージの変更
- システム メッセージの変更
- クォータ メッセージの変更
ms.translationtype: HT
---

# DSN メッセージの管理

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2013-02-20_

Microsoft Exchange Server 2013 は、メッセージ送信者に配信不能レポート (NDR) やその他の状態メッセージを、配信状態通知 (DSN) で届けます。この場合、組み込み DSN を使用できるほか、所属組織のニーズに合わせてカスタム DSN メッセージを作成することもできます。

## 始める前に把握しておくべき情報

  - 予想所要時間: 15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「DSN」。

  - Exchange に付属の組み込み DSN メッセージは削除できません。組み込み DSN メッセージを変更するには、カスタマイズする DSN コード用のカスタム DSN メッセージを作成する必要があります。カスタマイズした DSN メッセージを削除すると、そのメッセージに関連付けられていた DSN コードは、Exchange に付属の組み込み DSN メッセージに戻ります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用して組み込み DSN メッセージとカスタム DSN メッセージを表示する

Exchange 2013 に付属のすべての組み込み DSN メッセージの要約一覧を表示するには、以下のコマンドを実行します。

```powershell
Get-SystemMessage -Original
```

組織内のすべての組み込み DSN メッセージの要約一覧を表示するには、以下のコマンドを実行します。

```powershell
Get-SystemMessage
```

内部送信者に英語で送信する DSN コード 5.1.2 のカスタム DSN メッセージの詳細情報を表示するには、以下のコマンドを実行します。

```powershell
Get-SystemMessage En\Internal\5.1.2 | Format-List
```

## シェルを使用してカスタム DSN メッセージを作成する

次のコマンドを実行します。

    New-SystemMessage -Internal <$true | $false> -Language <Locale> -DSNCode <x.y.z> -Text "<DSN text>"

この例では、内部送信者に英語で送信する DSN コード 5.1.2 のカスタム プレーン テキスト DSN メッセージを作成します。

    New-SystemMessage -Internal $true -Language En -DSNCode 5.1.2 -Text "You tried to send a message to a disabled mailbox that's no longer accepting messages. Please contact the Help Desk at extension 123 for assistance."

この例では、外部送信者に英語で送信する DSN コード 5.1.2 のカスタム プレーン テキスト DSN メッセージを作成します。

    New-SystemMessage -Internal $false -Language En -DSNCode 5.1.2 -Text "You tried to send a message to a disabled mailbox that's no longer accepting messages. Please contact your System Administrator for more information."

この例では、内部送信者に英語で送信する DSN コード 5.1.2 のカスタム HTML DSN メッセージを作成します。

    New-SystemMessage -DSNCode 5.1.2 -Internal $true -Language En -Text 'You tried to send a message to a <B>disabled</B> mailbox. Please visit <A HREF="http://it.contoso.com">Internal Support</A> or contact &quot;InfoSec&quot; for more information.'

## 正常な動作を確認する方法

カスタム DSN メッセージが正しく作成できたかどうかを確認するには、以下の手順を実行します。

1.  次のコマンドを実行します。
    
    ```powershell
Get-SystemMessge -DSNCode <x.y.z> | Format-List Name,Internal,Text,Language
```

2.  表示された値が構成した値であることを確認します。

3.  構成したカスタム DSN を生成するテスト メッセージを送信します。

## シェルを使用してカスタム DSN メッセージのテキストを変更する

カスタム DSN メッセージのテキストを変更するには、以下のコマンドを実行します。

    Set-SystemMessage <Locale>\<Internal | External>\<DSNcode> -Text "<DSN text>"

この例では、内部送信者に英語で送信する DSN コード 5.1.2 のカスタム DSN メッセージに割り当てたテキストを変更します。

    Set-SystemMessage En\Internal\5.1.2 -Text "The mailbox you tried to send an e-mail message to is disabled and is no longer accepting messages. Please contact the Help Desk at extension 123 for assistance."

## 正常な動作を確認する方法

カスタム DNS メッセージのテキストが正しく変更されたかどうかを確認するには、以下の手順を実行します。

1.  次のコマンドを実行します。`Get-SystemMessage`.
    
    ```powershell
Set-SystemMessage <Locale>\<Internal | External>\<DSNcode> | Format-List -Text
```

2.  表示された値が構成した値であることを確認します。

## シェルを使用してカスタム DSN メッセージを削除する

次のコマンドを実行します。

```powershell
Remove-SystemMessage <Local>\<Internal | External>\<DSNcode>
```

この例では、内部送信者に英語で送信する DSN コード 5.1.2 のカスタム DSN メッセージを削除します。

```powershell
Remove-SystemMessage En\Internal\5.1.2
```

## 正常な動作を確認する方法

カスタム DNS メッセージが正しく削除できたかどうかを確認するには、以下の手順を実行します。

1.  以下のコマンドを実行します。`Get-SystemMessage`.

2.  ロケールの DSN、内部または外部の受信者、そして削除した DSN コードが一覧にないことを確認します。

## DSN メッセージのコピーを Exchange 受信者のメールボックスに転送する

DSN メッセージを Exchange 受信者のメールボックスにコピーすれば監視する DSN コードの一覧を指定できます。ただし、Exchange 受信者には既定ではメールボックスが割り当てられないため、Exchange 受信者に送信されるメッセージはすべて破棄されます。Exchange 受信者のメールボックスに DSN メッセージのコピーを送信するには、その Exchange 受信者にメールボックスを割り当て、監視する DSN コードを指定します。既定では、以下の DSN コードが監視されます。`5.4.8`、`5.4.6`、`5.4.4`、`5.2.4`、`5.2.0`、および `5.1.4` です。

## 手順 1:シェルを使用してメールボックスを Exchange 受信者に割り当てる

メールボックスを Exchange 受信者に割り当てるには、以下の手順を実行します。

1.  受信電子メールが大量に保存される可能性があるので、Exchange 受信者には専用のメールボックスと Active Directory ユーザー アカウントを作成することを考えておいてください。詳細については、「[ユーザー メールボックスを作成する](create-user-mailboxes-exchange-2013-help.md)」を参照してください。あるいは、目的の Exchange 受信者に関連付ける既存のメールボックスを指定します。

2.  次のコマンドを実行します。
    
    ```powershell
Set-OrganizationConfig -MicrosoftExchangeRecipientReplyRecipient <MailboxIdentity>
```
    
    たとえば、"Contoso System Mailbox" という名前の既存のメールボックスを Exchange 受信者に割り当てるには、以下のコマンドを実行します。
    
    ```powershell
Set-OrganizationConfig -MicrosoftExchangeRecipientReplyRecipient "Contoso System Mailbox"
```

## 手順 2:監視する DSN コードを指定する

## EAC で DSN コードを指定する

1.  EAC で、<strong>メール フロー</strong> \> <strong>受信コネクタ</strong> \> <strong>その他のオプション</strong>![\[その他のオプション\] アイコン](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "[その他のオプション] アイコン") \> <strong>組織のトランスポート設定</strong> \> <strong>配信</strong> に移動します。

2.  <strong>DNS コード</strong> セクションで、監視する DSN コードを *\<x.y.z\>* 形式で入力し、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン")をクリックします。既存のエントリを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン")をクリックして変更するか、<strong>削除</strong>![\[削除\] アイコン](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[削除] アイコン")をクリックして削除します。完了したら、<strong>保存</strong> をクリックします。

## シェルを使用して、DSN コードを指定する

既存の値を置き換えるには、次のコマンドを実行します。

```powershell
Set-TransportConfig -GenerateCopyOfDSNFor <x.y.z>,<x.y.z>...
```

この例では、DSN コード 5.7.1、5.7.2、5.7.3 があるすべての DSN メッセージを Exchange 受信者に転送するように Exchange 組織を構成します。

```powershell
Set-TransportConfig -GenerateCopyOfDSNFor 5.7.1,5.7.2,5.7.3
```

既存の値を変更せずにエントリを追加または削除するには、次のコマンドを実行します。

    Set-TransportConfig -GenerateCopyOfDSNFor @{Add="<x.y.z>","<x.y.z>"...; Remove="<x.y.z>","<x.y.z>"...}

この例では、Exchange 受信者に転送する DSN メッセージの既存の一覧に対して DSN コード 5.7.5 を追加し、DSN コード 5.7.1 を削除します。

```powershell
Set-TransportConfig -GenerateCopyOfDSNFor @{Add="5.7.5"; Remove="5.7.1"}
```

## 正常な動作を確認する方法

Exchange 受信者のメールボックスに送信する DSN メッセージのコピーが正しく構成されたかどうかを確認するには、Exchange 受信者に関連付けられたメールボックスを監視し、指定した DSN コードが DSN メッセージにあることを確認します。

