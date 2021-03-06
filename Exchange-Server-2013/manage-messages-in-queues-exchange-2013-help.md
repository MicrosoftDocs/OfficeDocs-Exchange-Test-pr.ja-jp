﻿---
title: 'キュー内のメッセージを管理する: Exchange 2013 Help'
TOCTitle: キュー内のメッセージを管理する
ms:assetid: 83358884-6036-4e91-87a8-35200541874d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb123535(v=EXCHG.150)
ms:contentKeyID: 51407554
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# キュー内のメッセージを管理する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-05-07_

Microsoft Exchange Server 2013 では、Exchange ツールボックスのキュー ビューアーまたは Exchange 管理シェルを使用して、キューに登録されたメッセージを管理できます。Exchange 管理シェルでのメッセージ管理コマンドレットの使用の詳細については、「[Exchange 管理シェルを使用してキューを管理する](use-the-exchange-management-shell-to-manage-queues-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「キュー」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## キューからメッセージを削除する

複数の受信者に送信されるメッセージは、複数のキューに存在する可能性があります。1 回の操作で複数のキューからメッセージを削除するには、フィルターを使用する必要があります。メッセージをキューから削除するときは、配信不能レポート (NDR) を送信するかどうかを選択できます。送信キューからはメッセージを削除できません。

## Exchange ツールボックスのキュー ビューアーを使用してメッセージを削除する

1.  <strong>スタート</strong> \> <strong>すべてのプログラム</strong> \> <strong>Microsoft Exchange 2013</strong> \> <strong>Exchange ツールボックス</strong> の順にクリックします。

2.  <strong>メール フロー ツール</strong> セクションで、<strong>キュー ビューアー</strong> をダブルクリックして、新しいウィンドウにツールを開きます。

3.  キュー ビューアーで、<strong>メッセージ</strong> タブをクリックします。接続先のサーバー上にあるすべてのメッセージの一覧が表示されます。処理対象を単一のキューにするには、<strong>キュー</strong> タブをクリックし、キュー名をダブルクリックします。次に、表示される *\[Server\\Queue\]* タブをクリックします。

4.  一覧で 1 つまたは複数のメッセージを選択し、右クリックして、<strong>メッセージを削除 (NDR を送信)</strong> または <strong>メッセージを削除 (NDR を送信しない)</strong> をクリックします。選択した処理を確認するダイアログ ボックスが表示され、<strong>続行しますか?</strong> というメッセージが表示されます。<strong>はい</strong> をクリックします。

5.  特定のキューにあるメッセージをすべて削除するには、<strong>キュー</strong> タブをクリックします。キューを選択し、右クリックします。次に、<strong>メッセージを削除 (NDR を送信)</strong> または <strong>メッセージを削除 (NDR を送信しない)</strong> をクリックします。選択した処理を確認するダイアログ ボックスが表示され、<strong>続行しますか?</strong> というメッセージが表示されます。<strong>はい</strong> をクリックします。
    

    > [!NOTE]
    > フィルター処理された一覧で作業している場合、表示されたページにはフィルターのすべてのアイテムが含まれていないことがあります。その場合は、次のメッセージが表示されます。<STRONG>[この処理はこのページ上のすべてのアイテムに適用されます。この処理の適用範囲を広げて、このフィルターに含まれるすべてのアイテムを含めるには、以下のチェック ボックスをオンにしてから [OK] をクリックしてください。]</STRONG> というメッセージが表示されます。



## シェルを使用してメッセージを削除する

キューからメッセージを削除するには、次の構文を使用します。

```powershell
Remove-Message <-Identity MessageIdentity | -Filter {MessageFilter}> -WithNDR <$true | $false>
```

この例では、"Win Big" という件名を持つメッセージを、NDR を送信せずにキューから削除します。

```powershell
Remove-Message -Filter {Subject -eq "Win Big"} -WithNDR $false
```

この例では、Mailbox01 というサーバーの到達不能キューからメッセージ ID 3 のメッセージを削除して、NDR を送信します。

```powershell
Remove-Message -Identity Mailbox01\Unreachable\3 -WithNDR $true
```

## 正常な動作を確認する方法

キューからメッセージが正常に削除されたことを確認するには、次のいずれかの手順を実行します。

  - キュー ビューアーで、キューを選択するか、またはフィルターを作成して、メッセージがないことを確認します。

  - *Queue* または *Filter* パラメーターで **Get-Message** コマンドレットを使用して、メッセージがないことを確認します。詳細については、「[Get-Message](https://technet.microsoft.com/ja-jp/library/bb124738\(v=exchg.150\))」を参照してください。

## キュー内のメッセージを再開する

現在の状態が "中断" であるメッセージを再開できます。メッセージを再開することで、メッセージの配信を可能にします。有害なメッセージ キューにあるメッセージを再開すると、そのメッセージは処理のためにカテゴライザーに送信されます。複数の受信者に送信されるメッセージは、複数のキューに存在する可能性があります。1 回の操作で複数のキューにあるメッセージを再開するには、フィルターを使用する必要があります。

## Exchange ツールボックスのキュー ビューアーを使用してメッセージを再開する

1.  <strong>スタート</strong> \> <strong>すべてのプログラム</strong> \> <strong>Microsoft Exchange 2013</strong> \> <strong>Exchange ツールボックス</strong> の順にクリックします。

2.  <strong>メール フロー ツール</strong> セクションで、<strong>キュー ビューアー</strong> をダブルクリックして、新しいウィンドウにツールを開きます。

3.  キュー ビューアーで、<strong>メッセージ</strong> タブをクリックします。接続先のサーバー上にあるすべてのメッセージの一覧が表示されます。処理対象を 1 つのキューにするには、<strong>キュー</strong> タブをクリックし、キュー名をダブルクリックします。次に、表示される *\[Server\\Queue\]* タブをクリックします。

4.  <strong>フィルターの作成</strong> をクリックし、次のようにフィルター式を入力します。
    
    1.  メッセージ プロパティのボックスの一覧から <strong>状態</strong> を選択します。
    
    2.  比較演算子のボックスの一覧から <strong>次の値と等しい</strong> を選択します。
    
    3.  値のボックスの一覧から <strong>中断</strong> を選択します。

5.  <strong>フィルターの適用</strong> をクリックします。状態が "中断" であるすべてのメッセージが表示されます。

6.  一覧から 1 つ以上のメッセージを選択し、右クリックして、<strong>再開</strong> をクリックします。

## シェルを使用してメッセージを再開する

メッセージを再開するには、次の構文を使用します。

```powershell
Resume-Message <-Identity MessageIdentity | -Filter {MessageFilter}>
```

この例では、Contoso.com ドメインの送信者から送信されるすべてのメッセージを再開します。

```powershell
Resume-Message -Filter {FromAddress -eq "*contoso.com"}
```

この例では、サーバー Hub01 上の到達不能キュー内にあるメッセージ ID 3 のメッセージを再開します。

```powershell
Resume-Message -Identity Hub01\Unreachable\3
```

有害メッセージ キューからメッセージを再送信するには、次の手順に従います。

## 正常な動作を確認する方法

キューのメッセージが正常に再開されたことを確認するには、次のいずれかの手順を実行します。

  - キュー ビューアーで、キューを選択するか、またはフィルターを作成して、メッセージが中断されていないことを確認します。

  - *Queue* または *Filter* パラメーターで **Get-Message** コマンドレットを使用して、メッセージが中断されていないことを確認します。詳細については、「[Get-Message](https://technet.microsoft.com/ja-jp/library/bb124738\(v=exchg.150\))」を参照してください。

なお、サーバーのどのキューにもメッセージが見つからない場合、メッセージは次ホップに正常に配信されています。

## キュー内のメッセージを中断する

メッセージを中断すると、メッセージは配信されなくなります。キュー内に現れるが既に配信中のメッセージは中断されません。配信は続行され、メッセージの状態は **PendingSuspend** になります。配信に失敗すると、メッセージは再度キューに置かれた後で中断されます。送信キューまたは有害なメッセージ キューにあるメッセージを中断することはできません。

複数の受信者に送信されるメッセージは、複数のキューに存在する可能性があります。1 回の操作で複数のキューにあるメッセージを中断するには、フィルターを使用する必要があります。

## Exchange ツールボックスのキュー ビューアーを使用してメッセージを中断する

1.  <strong>スタート</strong> \> <strong>すべてのプログラム</strong> \> <strong>Microsoft Exchange 2013</strong> \> <strong>Exchange ツールボックス</strong> の順にクリックします。

2.  <strong>メール フロー ツール</strong> セクションで、<strong>キュー ビューアー</strong> をダブルクリックして、新しいウィンドウにツールを開きます。

3.  キュー ビューアーで、<strong>メッセージ</strong> タブをクリックします。接続先のサーバー上にあるすべてのメッセージの一覧が表示されます。表示を単一のキューに制限するには、<strong>キュー</strong> タブをクリックし、キュー名をダブルクリックします。次に、表示される *\[Server\\Queue\]* タブをクリックします。

4.  1 つ以上のメッセージを選択し、右クリックして、<strong>中断</strong> をクリックします。

## シェルを使用してメッセージを中断する

メッセージを中断するには、次の構文を使用します。

```powershell
Suspend-Message <-Identity MessageIdentity | -Filter {MessageFilter}>
```

この例では、ドメイン contoso.com 内の任意の送信者から送信されたキュー内のすべてのメッセージを中断します。

```powershell
Suspend-Message -Filter {FromAddress -eq "*contoso.com"}
```

この例では、Mailbox01 というサーバー上の到達不能キュー内のメッセージ ID 3 のメッセージを中断します。

```powershell
Suspend-Message -Identity Mailbox01\Unreachable\3
```

## 正常な動作を確認する方法

キューのメッセージが正常に中断されたことを確認するには、次のいずれかの手順を実行します。

  - キュー ビューアーで、キューを選択するか、またはフィルターを作成して、メッセージが中断されていることを確認します。

  - *Queue* または *Filter* パラメーターで **Get-Message** コマンドレットを使用して、メッセージが中断されていることを確認します。詳細については、「[Get-Message](https://technet.microsoft.com/ja-jp/library/bb124738\(v=exchg.150\))」を参照してください。

