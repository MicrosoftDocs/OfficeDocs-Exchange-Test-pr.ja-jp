---
title: '無効にされたメールボックスを接続する: Exchange 2013 Help'
TOCTitle: 無効にされたメールボックスを接続する
ms:assetid: a8abd399-75fd-4ee2-b2e4-634b55e4f79f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ863439(v=EXCHG.150)
ms:contentKeyID: 50555844
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 無効にされたメールボックスを接続する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-11-13_

EAC またはシェルを使用して、無効にされたメールボックスを Active Directory ユーザー アカウントに接続できます。メールボックスを無効にすると、Exchange はそのメールボックスをメールボックス データベースに保持し、メールボックスを無効な状態に切り替えます。対応する Active Directory ユーザー アカウントからは Exchange 属性も削除されますが、ユーザー アカウントは保持されます。メールボックスは削除済みメールボックスの保存期間 (既定では 30 日) が経過するまで保持され、その後に、メールボックス データベースから完全に削除 (つまり*消去*) されます。

無効にされたメールボックスが Exchange メールボックス データベースから完全に削除されるまでは、EAC またはシェルを使用して、無効にされたメールボックスを元の Active Directory ユーザー アカウントに再接続できます。

切断されたメールボックスおよびその他の関連する管理タスクの実行方法の詳細については、次のトピックを参照してください。

  - [未接続のメールボックス](disconnected-mailboxes-exchange-2013-help.md)

  - [メールボックスの無効化または削除](disable-or-delete-a-mailbox-exchange-2013-help.md)

  - [削除されたメールボックスの接続または復元](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

  - [メールボックスの完全削除](permanently-delete-a-mailbox-exchange-2013-help.md)

## 始める前に把握しておくべき情報

  - 予想所要時間 : 2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「受信者プロビジョニングのアクセス許可」。

  - または、シェルで **Get-User** コマンドレットを実行して、無効にされたメールボックスを接続する Active Directory ユーザー アカウントが存在し、かつ別のメールボックスにまだ関連付けられていないことを確認します。無効にされたメールボックスをユーザー アカウントに接続するには、アカウントが存在している必要があり、かつ *RecipientType* プロパティの値が、アカウントのメールボックスがまだ有効ではないことを示す `User` である必要があります。
    
    社内 Exchange 組織の場合は、この情報を \[Active Directory ユーザーとコンピューター\] で確認することもできます。

  - 次のコマンドを実行して、ユーザー アカウントを接続する無効にされたメールボックスがメールボックス データベースに存在し、回復可能な削除によって削除されたメールボックスではないことを確認します。
    
    ```powershell
    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,Database,DisconnectReason
    ```
    
    無効にされたメールボックスを接続するには、メールボックスがメールボックス データベースに存在し、*DisconnectReason* プロパティの値が `Disabled` である必要があります。メールボックスがデータベースから消去されている場合、コマンドは結果を返しません。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して無効にされたメールボックスを接続する

次の手順では、無効にされたユーザー メールボックスを接続する方法を示します。無効にされたリンク済みのメールボックスおよび無効にされた共有メールボックスを、対応するユーザー アカウントに再接続することもできます。

1.  EAC で、<strong>受信者</strong> \> <strong>\[メールボックス\]</strong>に移動します。

2.  <strong>その他</strong> ![\[その他のオプション\] アイコン](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "[その他のオプション] アイコン") をクリックし、<strong>メールボックスの接続</strong> をクリックします。
    
    Exchange 組織内の選択した Exchange サーバー上にある、切断されたメールボックスの一覧が表示されます。
    

    > [!NOTE]
    > この切断されたメールボックスの一覧には、無効にされたメールボックス、削除されたメールボックス、および回復可能な削除によって削除されたメールボックスが含まれます。



3.  再接続する無効にされたメールボックスをクリックし、<strong>接続</strong> をクリックします。

4.  そのメールボックスを再接続するかどうかを確認するウィンドウで、<strong>はい</strong> をクリックします。
    
    Exchange により、無効にされたメールボックスが対応するユーザー アカウントに再接続されます。

## シェルを使用して無効にされたメールボックスを接続する

シェルで **Connect-Mailbox** コマンドレットを使用して、無効にされたメールボックスにユーザー アカウントを接続します。接続するメールボックスの種類を指定する必要があります。次の例では、ユーザー メールボックス、リンクされたメールボックス、および共有メールボックスを再接続するための構文を示します。

この例では、ユーザー メールボックスを接続しています。*Identity* パラメーターでは、Exchange データベースの切断されたメールボックスを指定します。*User* パラメーターでは、メールボックスを再接続する Active Directory ユーザー アカウントを指定します。

```powershell
Connect-Mailbox -Identity "Jeffrey Zeng" -Database MBXDB01 -User "Jeffrey Zeng"
```

この例では、リンクされたメールボックスを接続しています。*Identity* パラメーターでは、Exchange データベースの切断されたメールボックスを指定します。*LinkedMasterAccount* パラメーターでは、メールボックスを再接続するアカウント フォレスト内の Active Directory ユーザー アカウントを指定します。*Alias* パラメーターではエイリアスを指定します。これは、再接続されたメールボックスでの、電子メール アドレスの @ 記号の左に表示される部分です。

```powershell
Connect-Mailbox -Identity "Kai Axford" -Database MBXDB02 -LinkedDomainController FabrikamDC01 -LinkedMasterAccount kai.axford@fabrikam.com -Alias kaia
```

この例では、共有メールボックスを接続しています。

```powershell
Connect-Mailbox -Identity "Corporate Shared Mailbox" -Database "Mailbox Database 03" -User "Corporate Shared Mailbox" -Alias corpshared -Shared
```


> [!NOTE]
> <STRONG>Connect-Mailbox</STRONG> コマンドレットを実行するときに <EM>Alias</EM> パラメーターを含めない場合は、<EM>User</EM> パラメーターまたは <EM>LinkedMasterAccount</EM> パラメーターで指定した値を使用して、再接続したメールボックスの電子メール アドレスのエイリアスが作成されます。



構文およびパラメーターの詳細については、「[Connect-Mailbox](https://technet.microsoft.com/ja-jp/library/aa997878\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

無効にされたメールボックスがユーザー アカウントに正常に接続されたことを確認するには、次のいずれかを実行します。

  - EAC で、<strong>受信者</strong> をクリックし、再接続したメールボックスの種類の適切なページに移動し、<strong>最新の情報に更新</strong>![\[最新の情報に更新\] アイコン](images/Dn624163.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "[最新の情報に更新] アイコン") をクリックし、メールボックスが一覧に表示されていることを確認します。

  - \[Active Directory ユーザーとコンピューター\] で、メールボックスが無効なユーザー アカウントを右クリックし、<strong>プロパティ</strong> をクリックします。<strong>全般</strong> タブで、再接続したメールボックスの電子メール アドレスが <strong>電子メール</strong> ボックスに読み込まれていることに注意してください。

  - シェルで、次のコマンドを実行します。
    
    ```powershell
    Get-User <identity>
    ```
    
    *RecipientType* プロパティの **UserMailbox** 値は、ユーザー アカウントとメールボックスが接続されていることを示します。**Get-Mailbox** コマンドレットを実行して、メールボックスの存在を確認することもできます。

