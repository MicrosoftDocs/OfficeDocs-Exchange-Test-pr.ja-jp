---
title: 'メールボックスの割り当てポリシーを変更する: Exchange 2013 Help'
TOCTitle: メールボックスの割り当てポリシーを変更する
ms:assetid: 011690a5-233a-4c03-8842-92276f899a89
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd638076(v=EXCHG.150)
ms:contentKeyID: 49895208
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックスの割り当てポリシーを変更する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-08_

メールボックスに割り当てられている管理役割の割り当てポリシーを変更することができます。メールボックスの割り当てポリシーを変更すると、次回メールボックスにログインしたときやメールボックス オプションを開いたときなど、ユーザーが接続を更新したときに直ちに変更が有効になります。Microsoft Exchange Server 2013 での割り当てポリシーの詳細については、「[管理役割の割り当てポリシーについて](understanding-management-role-assignment-policies-exchange-2013-help.md)」を参照してください。

アクセス許可に関連する他の管理タスクについては、「[アクセス許可](permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「役割グループ」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## EAC を使用してメールボックスの割り当てポリシーを変更する

1.  Exchange 管理センター (EAC) で、<strong>受信者</strong> \> <strong>\[メールボックス\]</strong>に移動します。

2.  割り当てポリシーを変更するユーザーまたはリソース メールボックスを選択してから、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>メールボックスの機能</strong> を選択します。

4.  <strong>役割の割り当てポリシー</strong> リストで、メールボックスに割り当てる割り当てポリシーを選択してから <strong>保存</strong> をクリックします。

## シェルを使用してメールボックスの割り当てポリシーを変更する

メールボックスに割り当てられている割り当てポリシーを変更するには、次の構文を使用します。

```powershell
Set-Mailbox <mailbox alias or name> -RoleAssignmentPolicy <assignment policy>
```

この例では、Brian というメールボックスの割り当てポリシーを "Unified Messaging Users/ユニファイド メッセージング ユーザー" に設定します。

```powershell
Set-Mailbox Brian -RoleAssignmentPolicy "Unified Messaging Users"
```

## シェルを使用して、特定の割り当てポリシーが割り当てられているメールボックスのグループの割り当てポリシーを変更する


> [!NOTE]
> EAC を使用して、複数のメールボックスの割り当てポリシーをすべて一度に変更することはできません。



この手順では、パイプライン処理、**Where** コマンドレット、および *WhatIf* パラメーターを利用します。これらの概念の詳細については、以下のトピックを参照してください。

  - [パイプライン処理](https://technet.microsoft.com/ja-jp/library/aa998260\(v=exchg.150\))

  - [コマンド出力の操作](working-with-command-output-exchange-2013-help.md)

  - [WhatIf、Confirm、および ValidateOnly スイッチ](whatif-confirm-and-validateonly-switches-exchange-2013-help.md)

特定のポリシーが割り当てられているメールボックスのグループの割り当てポリシーを変更する場合、次の構文を使用します。

```powershell
Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "<assignment policy to find>" } | Set-Mailbox -RoleAssignmentPolicy <assignment policy to set>
```

この例では、"Redmond Users - No Voicemail/Redmond ユーザー - ボイスメールなし" の割り当てポリシーに割り当てられているすべてのメールボックスを検索し、割り当てポリシーを "Redmond Users - Voicemail Enabled/Redmond ユーザー - ボイスメール有効" に変更します。

```powershell
Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "Redmond Users - No Voicemail" } | Set-Mailbox -RoleAssignmentPolicy "Redmond Users - Voicemail Enabled"
```

この例では、実際に変更を行わずに変更されるすべてのメールボックスを表示できるように、*WhatIf* パラメーターが含まれています。

```powershell
Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "Redmond Users - No Voicemail" } | Set-Mailbox -RoleAssignmentPolicy "Redmond Users - Voicemail Enabled" -WhatIf
```

構文およびパラメーターの詳細については、「[Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\))」または「[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))」を参照してください。

