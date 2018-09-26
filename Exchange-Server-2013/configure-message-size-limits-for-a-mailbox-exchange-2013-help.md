---
title: 'メールボックスのメッセージ サイズ制限を構成する: Exchange 2013 Help'
TOCTitle: メールボックスのメッセージ サイズ制限を構成する
ms:assetid: d1220685-14c0-4c4f-abb2-3920f3046212
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124708(v=EXCHG.150)
ms:contentKeyID: 50555880
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# メールボックスのメッセージ サイズ制限を構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-11-12_

ユーザー メールボックスのメッセージのサイズ制限の構成に、EAC およびシェルを使用できます。これらの制限により、ユーザーが送受信できるメッセージのサイズが規制されます。既定では、メールボックスの作成時には、送受信メッセージのサイズ制限はありません。

Exchange 組織では、メールボックスで送受信できる最大メッセージ サイズを決定する設定は他にもあります (たとえばメールボックス サーバーで構成される最大メッセージ サイズなど)。Exchange でのメッセージ サイズの制限の種類や、範囲、優先順位などの詳細については、「[メッセージ サイズの制限](message-size-limits-exchange-2013-help.md)」を参照してください。

ユーザー メールボックスに関するその他の管理タスクについては、「[ユーザー メールボックスの管理](https://docs.microsoft.com/ja-jp/exchange/recipients-in-exchange-online/manage-user-mailboxes/manage-user-mailboxes)」を参照してください。


> [!NOTE]
> また、メール ユーザーが送受信するメッセージのサイズや共有メールボックスから送信するメッセージのサイズを規制することもできます。



## 始める前に把握しておくべき情報

  - 予想所要時間:2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「受信者プロビジョニングのアクセス許可」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してメッセージのサイズ制限を設定する

1.  EAC で、<strong>受信者</strong> \> <strong>\[メールボックス\]</strong>に移動します。

2.  ユーザー メールボックス リストで、メッセージ サイズを変更するメールボックスをクリックし、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  メールボックスのプロパティ ページで、<strong>メールボックスの機能</strong> をクリックします。

4.  <strong>メッセージのサイズ制限</strong> の下で、<strong>詳細を表示</strong> をクリックして、次のメッセージサイズ制限を表示および変更します。
    
      - <strong>送信済みメッセージ</strong>   送信者が送信するメッセージの最大サイズを指定するには、 <strong>最大メッセージ サイズ (KB)</strong> チェック ボックスを選択し、値を入力します。 メッセージ サイズは 0 ～ 2,097,151 KB の間の値にする必要があります。指定したサイズを超えるメッセージが受信者に送信されると、エラーの内容を表すメッセージと共にメッセージが送信者に返されます。
    
      - <strong>受信したメッセージ</strong>   受信者が受信するメッセージの最大サイズを指定するには、 <strong>最大メッセージ サイズ (KB)</strong> チェック ボックスを選択し、値を入力します。 メッセージ サイズは 0 ～ 2,097,151 KB の間の値にする必要があります。指定したサイズを超えるメッセージをユーザーが受信すると、メッセージはエラーの内容を説明するエラー メッセージと共に送信者に返されます。

5.  <strong>OK</strong> をクリックし、<strong>保存</strong> をクリックして変更を保存します。

## シェルを使用してメッセージ サイズの制限を設定する

この例では、メールボックス Debra Garcia の送信メッセージの最大サイズを 25 MB、受信メッセージの最大サイズを 35 MB に設定しています。

```powershell
Set-Mailbox "Debra Garcia" -MaxSendSize 25mb -MaxReceiveSize 35mb
```

構文およびパラメーターの詳細については、「[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

メールボックスのメッセージサイズ制限が正常に設定されたことを確認するには、次のいずれかを実行します。

1.  EAC で、<strong>受信者</strong> \> <strong>\[メールボックス\]</strong>に移動します。

2.  ユーザー メールボックス リストで、メッセージ サイズ制限を確認するメールボックスをクリックし、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  メールボックスのプロパティ ページで、<strong>メールボックスの機能</strong> をクリックします。

4.  <strong>メッセージのサイズ制限</strong> の下で、<strong>詳細を表示</strong> をクリックして、メールボックスのメッセージ サイズ制限を確認します。

または

シェルで、次のコマンドを実行します。

```powershell
Get-Mailbox <identity> | fl MaxSendSize,MaxReceiveSize
```

