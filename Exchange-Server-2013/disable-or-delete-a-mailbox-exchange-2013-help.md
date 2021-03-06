﻿---
title: 'メールボックスの無効化または削除: Exchange 2013 Help'
TOCTitle: メールボックスの無効化または削除
ms:assetid: 31ad25d6-2942-4fd9-aecb-cdf9654163d2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ863434(v=EXCHG.150)
ms:contentKeyID: 50555751
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックスの無効化または削除

 

_**適用先:** Exchange Server 2013 SP1_

_**トピックの最終更新日:** 2015-03-09_

EAC またはシェルを使用して、Exchange 2013 のメールボックスを無効または削除することができます。メールボックスを無効または削除した場合、Exchange はメールボックス データベースでメールボックスを保持しつつ、メールボックスを無効な状態に切り替えます。無効化および削除したメールボックスは、削除済みメールボックスの保持期間 (既定で 30 日) が経過するまで、メールボックス データベース内に保持されます。保持期間を過ぎると、メールボックスは完全に削除されます。

Exchange Online のメールボックスを削除する必要がある場合は、「[Exchange Online でユーザー メールボックスを削除または復元する](https://technet.microsoft.com/ja-jp/library/dn186233\(v=exchg.150\))」を参照してください。


> [!NOTE]
> 無効化または削除されたメールボックスは、<EM>切断されたメールボックス</EM>と呼ばれます。



メールボックスの削除と無効化の主な違いは、メールボックスを無効にすると、Exchange の属性が対応する Active Directory ユーザー アカウントから削除されますが、ユーザー アカウントは保持されるということです。メールボックスを削除すると、Exchange の属性と Active Directory ユーザー アカウントの両方が削除されます。この違いにより、無効化したメールボックスや削除したメールボックスを再接続または復元する場合のオプションも異なります。

次の表に、無効化および削除できる Exchange メールボックスの種類を示します。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>メールボックスの種類</th>
<th>無効化</th>
<th>削除</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>アーカイブ メールボックス</p></td>
<td><p>○</p></td>
<td><p>X *</p></td>
</tr>
<tr class="even">
<td><p>リンクされたメールボックス</p></td>
<td><p>○</p></td>
<td><p>○</p></td>
</tr>
<tr class="odd">
<td><p>リソース メールボックス (会議室または備品)</p></td>
<td><p>X</p></td>
<td><p>○</p></td>
</tr>
<tr class="even">
<td><p>共有メールボックス</p></td>
<td><p>○</p></td>
<td><p>○</p></td>
</tr>
<tr class="odd">
<td><p>ユーザー メールボックス</p></td>
<td><p>○</p></td>
<td><p>○</p></td>
</tr>
</tbody>
</table>


\* アーカイブ メールボックスが有効である場合、アーカイブ メールボックスはプライマリ メールボックスが削除されたときに削除されます。アーカイブ メールボックスの無効化の詳細については、「[Exchange 2013 でインプレース アーカイブを管理する](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)」を参照してください。

メールボックスのあるユーザー アカウントを管理者が削除した場合、Exchange Information store、メールボックスがユーザー アカウントと接続されていないことを検出して、メールボックスが保留中の場合でも、そのメールボックスに削除のためのマークを付けます。メールボックスを保持する場合は、次の操作を行う必要があります。

1.  ユーザー アカウントを削除するのではなくユーザー アカウントを無効にします。

2.  メールボックスのプロパティを変更して、その使用とメールボックスへのアクセスとを制限します。たとえば、送受信クォータを 1 に設定し、メールボックスにメッセージを送信できるユーザーをブロックし、メールボックスにアクセスできるユーザーを制限します。

3.  すべてのデータが削除されるまで、または保持する必要がなくなるまで、メールボックスを保持します。

切断されたメールボックスに関連する追加の管理タスクについては、次のトピックを参照してください。

  - [未接続のメールボックス](disconnected-mailboxes-exchange-2013-help.md)

  - [無効にされたメールボックスを接続する](connect-a-disabled-mailbox-exchange-2013-help.md)

  - [削除されたメールボックスの接続または復元](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

  - [メールボックスの完全削除](permanently-delete-a-mailbox-exchange-2013-help.md)

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「受信者プロビジョニングのアクセス許可」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## メールボックスを無効にする

前述のように、メールボックスを無効にすると、Exchange の属性は対応する Active Directory ユーザー アカウントから削除されますが、ユーザー アカウントは残ります。

## EAC を使用してメールボックスを無効にする

次の手順では、ユーザー メールボックスを無効にする方法を示します。この手順を使用して、EAC で該当するページに移動した後に他のメールボックスの種類を無効にします。

1.  EAC で、<strong>受信者</strong> \> <strong>\[メールボックス\]</strong>に移動します。

2.  ユーザー メールボックスの一覧で、無効化するメールボックスをクリックします。

3.  <strong>詳細</strong> ![\[その他のオプション\] アイコン](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "[その他のオプション] アイコン") クリックして、<strong>無効にする</strong> をクリックします。

4.  メールボックスを無効にするかどうかを確認する警告が表示されます。<strong>はい</strong> をクリックしてメールボックスを無効にします。

メールボックスはメールボックス一覧から削除されます。

## シェルを使用してメールボックスを無効にする

次のコマンドを使用して、ユーザー メールボックス、リンクされたメールボックス、リソース メールボックス、および共有メールボックスを無効にします。

```powershell
Disable-Mailbox <identity>
```

このコマンドを実行すると、メールボックスを無効にすることを確認するメッセージが表示されます。

次にメールボックスを無効にするコマンドの例を示します。
```powershell
Disable-Mailbox danj
```
```powershell
Disable-Mailbox "Conf Room 31/1234 (12)"
```
```powershell
Disable-Mailbox sharedmbx@contoso.com
```

## 正常な動作を確認する方法

メールボックスが正常に無効化されたことを確認するには、次のいずれかの手順を実行します。

  - EAC で、<strong>受信者</strong> をクリックし、無効にしたメールボックスの種類に対する関連ページに移動して、無効にしたメールボックスが表示されなくなっていることを確認します。

  - Active Directory ユーザーとコンピューターで、メールボックスを無効にしたユーザー アカウントを右クリックし、<strong>プロパティ</strong> をクリックします。<strong>全般</strong> タブで、<strong>電子メール</strong> フィールドが空欄になっていることに注意してください。これにより、メールボックスが無効になっていて、ユーザー アカウントが残っていることを確認します。

  - シェルで、次のコマンドを実行します。
    
    ```powershell
    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisconnectReason,DisconnectDate
    ```
    
    *DisconnectReason* プロパティの値が `Disabled` であることは、メールボックスが無効であることを示します。
    

    > [!NOTE]
    > メールボックスを削除した場合も、<EM>DisconnectReason</EM> プロパティの値は <CODE>Disabled</CODE> になります。ただし、対応する Active Directory ユーザー アカウントが削除されます。



  - シェルで、次のコマンドを実行します。
    
    ```powershell
    Get-User <identity>
    ```
    
    *RecipientType* プロパティの値が `User` で、`UserMailbox` (ユーザーが有効なメールボックスを持つ場合の値) ではないことに注意してください。これにより、メールボックスが無効になっていて、ユーザー アカウントが残っていることを確認します。

## メールボックスの削除

前述のように、メールボックスを削除する場合、Exchange の属性と Active Directory ユーザー アカウントの両方が削除されます。メールボックスの保持期間が経過すると、メールボックス データベースからメールボックス (および、有効な場合はアーカイブ メールボックス) が完全に削除されます。

## EAC を使用してメールボックスを削除する

次の手順では、ユーザー メールボックスを削除する方法を示します。この手順を使用して、EAC で該当するページに移動した後に他のメールボックスの種類を削除します。

1.  EAC で、<strong>受信者</strong> \> <strong>\[メールボックス\]</strong>に移動します。

2.  ユーザー メールボックスの一覧で、削除するメールボックスをクリックし、<strong>削除</strong>![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") をクリックします。

3.  メールボックスを削除するかどうかを確認する警告が表示されます。<strong>はい</strong> をクリックしてメールボックスを削除します。

メールボックスはメールボックス一覧から削除されます。

## シェルを使用してメールボックスを削除する

次のコマンドを使用して、ユーザー メールボックス、リンクされたメールボックス、リソース メールボックス、および共有メールボックスを削除します。

```powershell
Remove-Mailbox <identity>
```

このコマンドを実行すると、メールボックスと対応する Active Directory ユーザー アカウントを削除することを確認するメッセージが表示されます。

次にメールボックスを削除するコマンドの例を示します。
```powershell
Remove-Mailbox pilarp@contoso.com
```
```powershell
Remove-Mailbox "Fleet Van (16)"
```
```powershell
Remove-Mailbox corpprint
```

## 正常な動作を確認する方法

メールボックスが正常に削除されたことを確認するには、次のいずれかの確認手順を実行します。

1.  EAC で、<strong>受信者</strong> をクリックし、削除したメールボックスの種類に対する関連ページに移動して、削除したメールボックスが表示されなくなっていることを確認します。

2.  Active Directory ユーザーとコンピューターで、対応するユーザー アカウントが表示されなくなっていることを確認します。

または

1.  次のコマンドを実行してメールボックスが削除されたことを確認します。
    
    ```powershell
    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisconnectReason,DisconnectDate
    ```
    
    *DisconnectReason* プロパティの値が `Disabled` であることは、メールボックスが削除されたことを示します。
    

    > [!NOTE]
    > メールボックスを無効にした場合も、<EM>DisconnectReason</EM> プロパティの値は <CODE>Disabled</CODE> になります。ただし、対応する Active Directory ユーザー アカウントは残ります。



2.  次のコマンドを実行して、Active Directory ユーザー アカウントが削除されていることを確認します。
    
    ```powershell
    Get-User <identity>
    ```
    
    このコマンドでユーザーが見つからなかったことを示すエラーが返されたら、アカウントは削除されています。

