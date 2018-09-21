---
title: '社内の移動の管理: Exchange 2013 Help'
TOCTitle: 社内の移動の管理
ms:assetid: 1691b658-f5af-49c6-9170-5c3cb66c7306
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ150487(v=EXCHG.150)
ms:contentKeyID: 48269206
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 社内の移動の管理

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2013-02-25_

移動要求は、メールボックスをあるメールボックス データベースから別のデータベースに移動する処理です。ローカル移動要求は、単一フォレスト内で発生するメールボックスの移動です。Microsoft Exchange Server 2013 では、メールボックスと個人用アーカイブ メールボックスは別々のデータベース上に配置できます。移動要求機能を使用すると、プライマリ メールボックスおよびそれに関連付けられたアーカイブを、同じデータベースや別のデータベースに移動できます。このトピックの手順は、社内メールボックスの移動に役立ちます。

以下の手順を使用して社内組織のメールボックスを移動してください。これらの手順では、Exchange 管理シェルと Exchange センター (EAC) を使用します。

移動要求を使用してメールボックスを移動すると、移動要求は次の 2 つのサービスによって処理されます。

  - Microsoft Exchange メールボックス レプリケーション サービス

  - Microsoft Exchange メールボックス レプリケーション プロキシ

メールボックス レプリケーション サーバーとプロキシの詳細については、「[MRS プロキシの詳細情報](https://technet.microsoft.com/ja-jp/library/jj156451\(v=exchg.150\))」を参照してください。

メールボックスの移動の詳細については、「[Exchange 2013 でのメールボックスの移動](mailbox-moves-in-exchange-2013-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:20 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「メールボックスの移動および移行のアクセス許可」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## 移動準備ができているかどうかをテストする

この例では、*WhatIf* スイッチを使用して Tony Smith のメールボックスを新しいデータベース DB01 に移動する準備ができているかと、コマンドにエラーがないかをテストします。*WhatIf* スイッチを使用すると、システムによってメールボックスのチェックが実行されます。メールボックスの移動準備ができていない場合は、エラーが表示されます。

```powershell
New-MoveRequest -Identity 'tony@alpineskihouse.com' -TargetDatabase DB01 -WhatIf
```

構文およびパラメーターの詳細については、「[New-MigrationBatch](https://technet.microsoft.com/ja-jp/library/jj219166\(v=exchg.150\))」と「[New-MoveRequest](https://technet.microsoft.com/ja-jp/library/dd351123\(v=exchg.150\))」を参照してください。

## ローカル移動要求を作成する

## EAC を使用してローカル移動要求を作成する

ローカル移動要求を作成するには、EAC にログ インして以下の手順を実行します。

1.  EAC で、<strong>受信者</strong> \> <strong>移行</strong> の順に選択し、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  **ローカル メールボックスの移動の新規作成**ウィザードで、移動するユーザーを選択し、<strong>OK</strong> をクリックし、<strong>次へ</strong> をクリックします。

3.  <strong>移動の構成</strong> ページで、新しいバッチの名前を指定します。アーカイブ メールボックス、メールボックス データベースの場所に関するオプションを選択し、\[**新規**\] をクリックします。

## シェルを使用してローカル移動要求を作成する

ローカル移動要求の作成方法の例については、「[New-MoveRequest](https://technet.microsoft.com/ja-jp/library/dd351123\(v=exchg.150\))」の例 2 を参照してください。

## 正常な動作を確認する方法

移行が正常に完了したことを確認するには、次の手順を実行します。

  - EAC で、<strong>受信者</strong> \> <strong>移行</strong> に移動します。

  - EAC で <strong>すべてのバッチの状態</strong> をクリックして、移行が正常に完了したことを確認します。

  - シェルから次のコマンドを実行して、メールボックスの移行情報を取得します。
    
    ```powershell
Get-MigrationUserStatistics -Identity BatchName -Status | Format-List
```

詳細については、「[Get-MigrationUserStatistics](https://technet.microsoft.com/ja-jp/library/jj218695\(v=exchg.150\))」を参照してください。

## バッチ移動要求の作成

## EAC を使用してバッチ移動要求を作成する

EAC にログ インし、以下の手順を実行します。

1.  EAC で、<strong>受信者</strong> \> <strong>移行</strong> の順に選択し、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  **ローカル メールボックスの移動の新規作成**ウィザードで、移動するユーザーを選択し、<strong>OK</strong> をクリックして、<strong>次へ</strong> をクリックします。

3.  <strong>移動の構成</strong> ページで、新しいバッチの名前を指定します。アーカイブ メールボックス、メールボックス データベースの場所に関するオプションを選択し、\[**新規**\] をクリックします。


> [!WARNING]
> [無効なアイテムの制限値] を 50 アイテム以上に設定していないことを確認してください。そのように設定した場合、移動が失敗する可能性があります。[無効なアイテムの制限値] を 50 アイテム以上に設定する場合は、Exchange 管理シェルを使用して –<EM>AcceptLargeDataLoss</EM> パラメーターを True に設定する必要があります。



## シェルを使用してバッチ移動要求を作成する

この例では、ローカル移動の移行バッチを作成します。ここでは、指定した .csv ファイル内のメールボックスが、別のメールボックス データベースに移動されます。この .csv ファイルには、移動するメールボックスの電子メール アドレスが 1 列に格納されています。この列のヘッダーは、**EmailAddress** という名前にする必要があります。この例の移行バッチは、**Start-MigrationBatch** コマンドレットまたは Exchange 管理センター (EAC) を使用して手動で開始する必要があります。または、*AutoStart* パラメーターを使用して移行バッチを自動で開始することもできます。
```
New-MigrationBatch -Local -Name LocalMove1 -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\LocalMove1.csv")) -TargetDatabases MBXDB2 -TimeZone "Pacific Standard Time"
```
```
Start-MigrationBatch -Identity LocalMove1
```

構文およびパラメーターの詳細については、「[New-MigrationBatch](https://technet.microsoft.com/ja-jp/library/jj219166\(v=exchg.150\))」と「[Start-MigrationBatch](https://technet.microsoft.com/ja-jp/library/jj219165\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

移行が正常に完了したことを確認するには、次の手順を実行します。

  - EAC で <strong>すべてのバッチの状態</strong> をクリックして、移行が正常に完了したことを確認します。

  - シェルから次のコマンドを実行して、メールボックスの移行情報を取得します。
    
    ```powershell
Get-MigrationUserStatistics -Identity BatchName -Status | Format-List
```

詳細については、「[Get-MigrationUserStatistics](https://technet.microsoft.com/ja-jp/library/jj218695\(v=exchg.150\))」を参照してください。

## 移行バッチを表示する

シェルで移行バッチを表示する方法の例については、「[Get-MigrationBatch](https://technet.microsoft.com/ja-jp/library/jj219164\(v=exchg.150\))」の例 2 を参照してください。

## ユーザーのプライマリ メールボックスのみを移動する

## EAC を使用してユーザーのプライマリ メールボックスのみを移動する

1.  EAC で、<strong>受信者</strong> \> <strong>移行</strong> の順に選択し、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  **ローカル メールボックスの移動の新規作成**ウィザードで、プライマリ メールボックスを移動するユーザーを選択し、<strong>OK</strong> をクリックし、<strong>次へ</strong> をクリックします。

3.  <strong>移動の構成</strong> ページで、新しいバッチの名前を指定します。<strong>プライマリ メールボックスだけを移動する</strong> を選択し、メールボックス データベースの場所のオプションを選択し、<strong>次へ</strong> をクリックします。

## シェルを使用してユーザーのプライマリ メールボックスのみを移動する

この例では、Tony Smith のプライマリ メールボックスのみ DB01 に移動します。アーカイブは移動されません。

```powershell
New-MoveRequest -Identity 'tony@alpineskihouse.com' -PrimaryOnly -TargetDatabase "DB01"
```

構文およびパラメーターの詳細については、「[New-MoveRequest](https://technet.microsoft.com/ja-jp/library/dd351123\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

移行が正常に完了したことを確認するには、次の手順を実行します。

  - EAC で、<strong>すべてのバッチの状態</strong> をクリックします。

  - シェルから次のコマンドを実行して、メールボックスの移行情報を取得します。
    
    ```powershell
Get-MigrationUserStatistics -Identity BatchName -Status | Format-List
```

詳細については、「[Get-MigrationUserStatistics](https://technet.microsoft.com/ja-jp/library/jj218695\(v=exchg.150\))」を参照してください。

## .csv バッチ ファイルを使用してフォレスト間の移動を作成する

この例では、移行エンドポイントを構成し, .csv ファイルを使用してソース フォレストからターゲット フォレストまでのフォレスト間バッチ移動を作成します。

    New-MigrationEndpoint -Name Fabrikam -ExchangeRemote -Autodiscover -EmailAddress tonysmith@fabrikam.com -Credentials (Get-Credential fabrikam\tonysmith) 
    
    $csvData=[System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\batch.csv")
    New-MigrationBatch -CSVData $csvData -Timezone "Pacific Standard Time" -Name FabrikamMerger -SourceEndpoint Fabrikam -TargetDeliveryDomain "mail.contoso.com"

フォレスト間移動のフォレストの準備方法の詳細については、以下のトピックを参照してください。

  - [メールボックスでフォレスト間の移動要求の準備を行う](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)

  - [サンプル コードを使用してフォレスト間のメールボックス移動を準備する](prepare-mailboxes-for-cross-forest-moves-using-sample-code-exchange-2013-help.md)

  - [シェルの Prepare-MoveRequest.ps1 スクリプトを使用して、フォレスト間のメールボックスの移動を準備する](prepare-mailboxes-for-cross-forest-moves-using-the-prepare-moverequest-ps1-script-in-the-shell-exchange-2013-help.md)

構文およびパラメーターの詳細については、「[New-MigrationBatch](https://technet.microsoft.com/ja-jp/library/jj219166\(v=exchg.150\))」と「[New-MoveRequest](https://technet.microsoft.com/ja-jp/library/dd351123\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

移行が正常に完了したことを確認するには、次の手順を実行します。

  - シェルから次のコマンドを実行して、メールボックスの移行情報を取得します。
    
    ```powershell
Get-MigrationUserStatistics -Identity BatchName -Status | Format-List
```

詳細については、「[Get-MigrationUserStatistics](https://technet.microsoft.com/ja-jp/library/jj218695\(v=exchg.150\))」を参照してください。

## アーカイブ メールボックスのみを移動する

## EAC を使用してアーカイブ メールボックスのみを移動する

1.  EAC で、<strong>受信者</strong> \> <strong>移行</strong> の順に選択し、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  **ローカル メールボックスの移動の新規作成**ウィザードで、アーカイブ メールボックスを移動するユーザーを選択し、<strong>OK</strong> をクリックし、<strong>次へ</strong> をクリックします。

3.  <strong>移動の構成</strong> ページで、新しいバッチの名前を指定します。<strong>アーカイブ メールボックスだけを移動する</strong> を選択し、メールボックス データベースの場所のオプションを選択し、<strong>次へ</strong> をクリックします。

## シェルを使用してアーカイブ メールボックスのみを移動する

この例では、Tony Smith のアーカイブ メールボックスだけ DB03 に移動します。プライマリ メールボックスは移動されません。

```powershell
New-MoveRequest -Identity 'tony@alpineskihouse.com' -ArchiveOnly -ArchiveTargetDatabase "DB03"
```

構文およびパラメーターの詳細については、「[New-MigrationBatch](https://technet.microsoft.com/ja-jp/library/jj219166\(v=exchg.150\))」と「[New-MoveRequest](https://technet.microsoft.com/ja-jp/library/dd351123\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

移行が正常に完了したことを確認するには、次の手順を実行します。

  - シェルから次のコマンドを実行して、メールボックスの移行情報を取得します。
    
    ```powershell
Get-MigrationUserStatistics -Identity BatchName -Status | Format-List
```

詳細については、「[Get-MigrationUserStatistics](https://technet.microsoft.com/ja-jp/library/jj218695\(v=exchg.150\))」を参照してください。

## ユーザーのプライマリ メールボックスとアーカイブ メールボックスを別々のデータベースに移動する

この例では、Ayla のプライマリ メールボックスとアーカイブ メールボックスを別々のデータベースに移動します。プライマリ データベースは DB01 に移動され、アーカイブは DB03 に移動されます。

    New-MoveRequest -Identity 'ayla@humongousinsurance.com' -TargetDatabase DB01 -ArchiveTargetDatabase -DB03

構文およびパラメーターの詳細については、「[New-MigrationBatch](https://technet.microsoft.com/ja-jp/library/jj219166\(v=exchg.150\))」と「[New-MoveRequest](https://technet.microsoft.com/ja-jp/library/dd351123\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

移行が正常に完了したことを確認するには、次の手順を実行します。

  - シェルから次のコマンドを実行して、メールボックスの移行情報を取得します。
    
    ```powershell
Get-MigrationUserStatistics -Identity BatchName -Status | Format-List
```

詳細については、「[Get-MigrationUserStatistics](https://technet.microsoft.com/ja-jp/library/jj218695\(v=exchg.150\))」を参照してください。

## ユーザーのプライマリ メールボックスを移動し、無効なアイテムの制限値に大きな値を設定する

## EAC を使用してユーザーのプライマリ メールボックスを移動し、無効なアイテムの制限値に大きな値を設定する

1.  EAC で、<strong>受信者</strong> \> <strong>移行</strong> の順に選択し、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  **ローカル メールボックスの移動の新規作成**ウィザードで、プライマリ メールボックスを移動するユーザーを選択し、<strong>OK</strong> をクリックし、<strong>次へ</strong> をクリックします。

3.  <strong>移動の構成</strong> ページで、新しいバッチの名前を指定します。<strong>プライマリ メールボックスだけを移動する</strong> を選択し、メールボックス データベースの場所のオプションを選択します。

4.  <strong>その他のオプション</strong> ![\[その他のオプション\] アイコン](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "[その他のオプション] アイコン")をクリックし、無効なアイテムの制限値を入力し、<strong>OK</strong> をクリックします。

## シェルを使用してユーザーのプライマリ メールボックスを移動し、無効なアイテムの制限値に大きな値を設定する

この例では、Lisa のプライマリ メールボックスをメールボックス データベース DB01 へ移動し、無効なアイテムの制限値を `100` に設定します。このように無効なアイテムの制限値に大きな値を設定するには、*AcceptLargeDataLoss* パラメーターを使用する必要があります。

    New-MoveRequest -Identity 'Lisa' -PrimaryOnly -TargetDatabase "DB01" -BadItemLimit 100 -AcceptLargeDataLoss

構文およびパラメーターの詳細については、「[New-MigrationBatch](https://technet.microsoft.com/ja-jp/library/jj219166\(v=exchg.150\))」と「[New-MoveRequest](https://technet.microsoft.com/ja-jp/library/dd351123\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

移行が正常に完了したことを確認するには、次の手順を実行します。

  - シェルから次のコマンドを実行して、メールボックスの移行情報を取得します。
    
    ```powershell
Get-MigrationUserStatistics -Identity BatchName -Status | Format-List
```

詳細については、「[Get-MigrationUserStatistics](https://technet.microsoft.com/ja-jp/library/jj218695\(v=exchg.150\))」を参照してください。

