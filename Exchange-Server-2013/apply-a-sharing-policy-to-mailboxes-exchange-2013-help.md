---
title: 'メールボックスに共有ポリシーを適用する: Exchange 2013 Help'
TOCTitle: メールボックスに共有ポリシーを適用する
ms:assetid: dd4cc765-8469-4176-bb6e-d5b0f5235927
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657501(v=EXCHG.150)
ms:contentKeyID: 49896514
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックスに共有ポリシーを適用する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-02-15_

ポリシーの共有はフェデレーション共有の一部であり、これにより、さまざまな種類の外部ユーザーとユーザーによって指定されたユーザー間の予定表情報共有を行うことができます。管理者がユーザーのメールボックスに適用する共有ポリシーによって、ユーザーが共有できるアクセス権限のレベル、およびどのユーザーと共有できるかが決まります。何も変更しないと、既定の共有ポリシーがすべてのユーザーに適用されます。新しい共有ポリシーを作成する場合、そのポリシーはメールボックスに適用された後に有効になります。共有ポリシーは、1 つのユーザー メールボックスに適用するか、または複数のユーザー メールボックスに同時に適用できます。管理者は、ユーザーの共有ポリシーを無効にして、カレンダーに対する外部アクセスを防止することもできます。

フェデレーション共有の詳細については、「[共有](sharing-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。 「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「*Recipient Provisioning Permissions*」。

  - 共有ポリシーが存在している必要があります。詳細については、「[共有ポリシーの作成](create-a-sharing-policy-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

## 必要な作業

## EAC を使用して 1 つのメールボックスに共有ポリシーを適用する

1.  <strong>受信者</strong> \> <strong>メールボックス</strong> に移動します。

2.  リスト ビューで、目的のメールボックスを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>ユーザー メールボックス</strong> で、<strong>メールボックスの機能</strong> をクリックします。

4.  <strong>共有ポリシー</strong> の一覧で、このメールボックスに適用する共有ポリシーを選択します。

5.  <strong>保存</strong> をクリックして、共有ポリシーを適用します。

## EAC を使用して複数のメールボックスに共有ポリシーを適用する

1.  <strong>受信者</strong> \> <strong>メールボックス</strong> に移動します。

2.  リスト ビューで、Ctrl キーを押しながら複数のメールボックスを選択します。

3.  詳細ウィンドウでは、メールボックスのプロパティが構成されて一括編集されます。<strong>その他のオプション</strong> をクリックします。

4.  <strong>共有ポリシー</strong> で、<strong>更新</strong> をクリックします。

5.  <strong>共有ポリシーの一括割り当て</strong> で、<strong>共有ポリシーを選択します</strong> リストを使用してメールボックスに割り当てる共有ポリシーを選択します。

6.  <strong>保存</strong> をクリックして、選択したメールボックスに共有ポリシーを適用します。

## シェルを使用して 1 つ以上のメールボックスに共有ポリシーを適用する

この例では、ユーザー Barbara の 1 つのメールボックスに共有ポリシー Contoso を適用します。

```powershell
Set-Mailbox -Identity Barbara -SharingPolicy "Contoso"
```

この例では、マーケティング部門のすべてのユーザー メールボックスが共有ポリシー Contoso Marketing を使用するように指定します。

```powershell
Get-Mailbox -Filter {Department -eq "Marketing"} | Set-Mailbox -SharingPolicy "Contoso Marketing"
```

この例では、共有ポリシー Contoso が適用されたすべてのメールボックスを返します。ユーザーをエイリアスと電子メール アドレスのみを表示する表に並べ替えます。

  ```powershell
  Get-Mailbox -ResultSize unlimited | Where {$_.SharingPolicy -eq "Contoso" } | format-table Alias, EmailAddresses
  ```

構文およびパラメーターの詳細については、「[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))」と「[Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

共有ポリシーがユーザー メールボックスに正常に適用されたことを確認するには、次のいずれかを実行します。

  - EAC で、<strong>受信者</strong> \> <strong>メールボックス</strong> に移動し、共有ポリシーを適用したメールボックスを選択します。<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックし <strong>メールボックスの機能</strong> をクリックしてから、<strong>共有ポリシー</strong> の一覧に正しい共有ポリシーが表示されることを確認します。

  - 次のシェル コマンドを実行して、ユーザー メールボックスに共有ポリシーが割り当てられたことを確認します。*SharingPolicy* パラメーターに、正しい共有ポリシーが表示されていることを確認します。
    
    ```powershell
    Get-Mailbox <user name> | format-list
    ```


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。


