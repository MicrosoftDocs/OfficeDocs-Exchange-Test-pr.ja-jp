---
title: 'メールボックスのメールボックス監査ログを有効または無効にする: Exchange 2013 Help'
TOCTitle: メールボックスのメールボックス監査ログを有効または無効にする
ms:assetid: c4bbfd52-6196-49c7-8c31-777fbbee11f2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff461937(v=EXCHG.150)
ms:contentKeyID: 49896465
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックスのメールボックス監査ログを有効または無効にする

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-09-30_

メールボックス監査ログを使用すると、メールボックスへのログオンと、ログオン時のユーザーの操作を追跡できます。 メールボックスのメールボックス監査ログを有効にすると、管理者と代理人が実行した操作が既定で記録されます。 メールボックスの所有者が実行した操作は記録されません。メールボックス監査ログの詳細については、「[メールボックスの監査ログの出力](mailbox-audit-logging-exchange-2013-help.md)」を参照してください。


> [!NOTE]
> メールボックス所有者の操作を監査すると、大量のメールボックス監査ログ エントリが生成される可能性があるため、既定では無効となっています。 業務上またはセキュリティ上必要な、特定の所有者の操作の監査のみを有効にしておくことをお勧めします。



メールボックス監査ログに関連する追加のタスクについては、[メールボックス監査ログの手順](mailbox-audit-logging-procedures-exchange-2013-help.md) を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」トピックの「メールボックス監査ログ」エントリ。

  - Exchange 管理センター (EAC) を使用してメールボックス監査ログを有効または無効にすることはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用してメールボックス監査ログを有効または無効にする

シェルを使用してメールボックスのメールボックス監査ログを有効または無効にすることができます。 これにより、管理者、代理人、およびメールボックスの所有者に指定されたすべての操作のログを有効または無効にできます。

次の例では、Ben Smith のメールボックスのメールボックス監査ログを有効にします。

```powershell
Set-Mailbox -Identity "Ben Smith" -AuditEnabled $true
```

次の例では、Ben Smith のメールボックスのメールボックス監査ログを無効にします。

```powershell
Set-Mailbox -Identity "Ben Smith" -AuditEnabled $false
```

構文およびパラメーターの詳細については、「[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))」を参照してください。

## シェルを使用して、管理者、代理人、および所有者のアクセスのメールボックス監査ログ設定を構成する

メールボックスのメールボックス監査ログが有効の場合、そのメールボックスの監査ログ構成に指定された管理者、代理人、および所有者のアクションのみが記録されます。

この例では、代理ユーザーが実行した `SendAs` および `SendOnBehalf` の操作が Ben Smith のメールボックスに記録されるよう指定します。

```powershell
Set-Mailbox -Identity "Ben Smith" -AuditDelegate SendAs,SendOnBehalf -AuditEnabled $true
```

この例では、管理者が実行した `MessageBind` および `FolderBind` の操作が Ben Smith のメールボックスに記録されるよう指定します。

```powershell
Set-Mailbox -Identity "Ben Smith" -AuditAdmin MessageBind,FolderBind -AuditEnabled $true
```

この例では、メールボックス所有者が実行した `HardDelete` の操作が Ben Smith のメールボックスに記録されるよう指定します。

```powershell
Set-Mailbox -Identity "Ben Smith" -AuditOwner HardDelete -AuditEnabled $true
```

構文およびパラメーターの詳細については、「[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

メールボックスのメールボックス監査ログが正常に有効化され、管理者、代理人、および所有者のアクセスのログ設定が正確に指定されたことを確認するには、[Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\)) コマンドレットを使用してそのメールボックスのメールボックス監査ログ設定を取得します。

この例では、Ben Smith のメールボックス設定を取得して、指定された監査設定（監査ログ保管期限を含む）を **Format-List** コマンドレットにパイプ処理します。

    Get-Mailbox "Ben Smith" | Format-List *audit*

