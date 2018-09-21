---
title: 'メールボックスを訴訟ホールドの対象にする: Exchange Online Help'
TOCTitle: メールボックスを訴訟ホールドの対象にする
ms:assetid: adee4621-3626-4aec-aa53-00b35ff0d0b0
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn743673(v=EXCHG.150)
ms:contentKeyID: 62268991
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックスを訴訟ホールドの対象にする

 

_**適用先:** Exchange Online, Exchange Server 2013_

メールボックスを訴訟ホールドの対象にすると、削除済みアイテムと変更されたアイテムの元のバージョンを含む、すべてのメールボックスのコンテンツが保持されます。ユーザーのメールボックスを訴訟ホールドの対象にすると、ユーザーのアーカイブ メールボックス (有効である場合) もホールドの対象になります。削除済みアイテムと変更されたアイテムは、指定した期間またはメールボックスを訴訟ホールドの対象から外すまで、保持されます。[インプレース電子情報開示 (eDiscovery)](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery) 検索で、このようなメールボックスのすべてのアイテムが返されます。


> [!IMPORTANT]
> 訴訟ホールドによって、ユーザーのメールボックスにある [回復可能なアイテム] フォルダー内のアイテムを保持します。削除または変更するアイテムの数およびサイズによっては、メールボックスの [回復可能なアイテム] フォルダーのサイズが急に増加する可能性があります。既定では、[回復可能なアイテム] フォルダーは高いクォータで構成されています。Exchange Online では、メールボックスを訴訟ホールドの対象にすると、このクォータは自動的に引き上げられます。Exchange Server 2013 では、訴訟ホールドの対象のメールボックスが回復可能なアイテムのクォータの制限に達していないことを確認するため、これらのメールボックスを週 1 回監視することをお勧めします。



## 始める前に把握しておくべき情報

  - 予想所要時間: 5 分

  - 訴訟ホールド設定が有効になるまでに、最長で 60 分かかる場合があります。

  - [メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md) トピック内の この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。 の「インプレース保持」エントリ。

  - Exchange Online メールボックスを訴訟ホールドの対象にするには、Exchange Online (プラン 2) ライセンスを割り当てる必要があります。メールボックスに Exchange Online (プラン 1) ライセンスが割り当てられている場合は、別の Exchange Online Archiving ライセンスに割り当て、メールボックスを保持の対象にする必要があります。

  - 前述のように、ユーザーのメールボックスを訴訟ホールドの対象にすると、ユーザーのアーカイブ メールボックスのコンテンツも保持の対象になります。Exchange ハイブリッド展開でオンプレミスのプライマリ メールボックスを訴訟ホールドの対象にすると、クラウド ベースのアーカイブ メールボックス (有効な場合) も保持の対象になります。

  - Exchange Online では、メールボックスを訴訟ホールドの対象にすると、\[回復可能なアイテム\] フォルダーのクォータは自動的に 100 GB に引き上げられます。このフォルダーの既定のサイズは 30 GB です。

  - 訴訟ホールドは、削除済みアイテムを保持し、保留が解除されるまで、変更されたアイテムの元のバージョンを保持します。必要に応じて保持期間を指定することもできます (指定した期間中、メールボックスのアイテムが保持されます)。保持期間を指定する場合は、メッセージが受信された、またはメールボックス アイテムが作成された日付から計算されます。指定した条件に一致するアイテムを保持するには、インプレース保持を使用して、*クエリベース*保持を作成します。詳細については、「[インプレース保持を作成または削除する](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/create-or-remove-in-place-holds)」を参照してください。

  - シェルを使用して Exchange Online メールボックスを保持の対象にするには、Exchange Online PowerShell を使用する必要があります。 詳細については、「[リモート PowerShell による Exchange への接続](https://technet.microsoft.com/ja-jp/library/jj984289\(v=exchg.150\))」を参照してください。

  - パブリック フォルダー メールボックスを訴訟ホールドの対象にすることはサポートされていません。パブリック フォルダーを保持の対象にするには、インプレース ホールドを使用する必要があります。

## EAC を使用してメールボックスを訴訟ホールドの対象にする

1.  <strong>受信者</strong> \> <strong>メールボックス</strong> に移動します。

2.  ユーザーのメールボックスのリストで、訴訟ホールドの対象とするメールボックスを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  メールボックスのプロパティ ページで、<strong>メールボックスの機能</strong> をクリックします。

4.  <strong>訴訟ホールド:無効</strong> で、<strong>有効</strong> をクリックすると、メールボックスが訴訟ホールドの対象になります。

5.  <strong>訴訟ホールド</strong> ページで、以下のオプション情報を入力します。
    
      - **訴訟ホールド期間 (日)**   このボックスを使用して、メールボックスを訴訟ホールドの対象にするときに、メールボックス アイテムを保持する期間を指定します。期間は、メールボックス アイテムが受信または作成された日から計算されます。このボックスが空白の場合は、アイテムは無期限に、またはその保留が解除されるまで保持されます。日数で期間を指定します。
    
      - **注**   このボックスを使用して、メールボックスが訴訟ホールドの対象であることをユーザーに通知します。Outlook 2010 以降を使用している場合、ユーザーのメールボックスにメモが表示されます。
    
      - **URL**   このボックスを使用して、訴訟ホールドに関する詳細については Web サイトを参照するようにユーザーに指示します。Outlook 2010 以降を使用している場合、ユーザーのメールボックスにこの URL が表示されます。

6.  <strong>訴訟ホールド</strong> ページの <strong>保存</strong> をクリックして、メールボックスのプロパティ ページにある <strong>保存</strong> をクリックします。

ページのトップへ

## シェルを使用して無期限にメールボックスを訴訟ホールドの対象にする

この例では、メールボックス bsuneja@contoso.com を訴訟ホールドの対象にします。メールボックス内のアイテムは、無期限にまたは保留が解除されるまで保持されます。

```powershell
Set-Mailbox bsuneja@contoso.com -LitigationHoldEnabled $true
```


> [!NOTE]
> メールボックスを無期限に訴訟ホールドの対象にする (期間を指定しない) 場合、メールボックスの <EM>LitigationHoldDuration</EM> プロパティの値は <CODE>Unlimited</CODE> に設定されます。



## シェルを使用してメールボックスを訴訟ホールドの対象にし、指定した期間アイテムを保持する

この例では、メールボックス bsuneja@contoso.com を訴訟ホールドの対象とし、2555 日間 (約 7 年間) アイテムを保持します。

```powershell
Set-Mailbox bsuneja@contoso.com -LitigationHoldEnabled $true -LitigationHoldDuration 2555
```

## シェルを使用してすべてのメールボックスを指定した期間訴訟ホールドの対象にする

組織では、すべてのメールボックス データを特定の期間保持しなければならない場合があります。組織内のすべてのメールボックスを訴訟ホールドの対象にする前に、以下の点を考慮します。

次の例では、組織内のすべてのユーザー メールボックスを 1 年間 (365 日間) 訴訟ホールドの対象にします。

    Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | Set-Mailbox -LitigationHoldEnabled $true -LitigationHoldDuration 365

この例では、[Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\)) コマンドレットを使用して組織内のすべてのユーザー メールボックスを取得し、受信者フィルターを使用してすべてのユーザーのメールボックスを含めます。それから、メールボックスの一覧を [Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\)) コマンドレットにパイプ処理して訴訟ホールドを有効にし、保持期間を指定します。

すべてのユーザー メールボックスを無期限の保持の対象にするには、上記のコマンドを実行しますが、*LitigationHoldDuration* パラメーターは含めません。

1 つ以上のメールボックスを含めるまたは除外するフィルターで他の受信者のプロパティを使用する例については、「詳細情報」セクションを参照してください。

## シェルを使用してメールボックスを訴訟ホールドから削除する

この例では、メールボックス bsuneja@contoso.com を訴訟ホールドから削除します。

```powershell
Set-Mailbox bsuneja@contoso.com -LitigationHoldEnabled $false
```

ページのトップへ

## 正常な動作を確認する方法

メールボックスが正常に訴訟ホールドの対象となったことを確認するには、次のいずれかを実行します。

  - EAC で以下を実行します。
    
    1.  <strong>受信者</strong> \> <strong>メールボックス</strong> に移動します。
    
    2.  ユーザーのメールボックスのリストで、訴訟ホールドの設定を確認するメールボックスをクリックし、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。
    
    3.  メールボックスのプロパティ ページで、<strong>メールボックスの機能</strong> をクリックします。
    
    4.  <strong>訴訟ホールド</strong> の下でそのホールドが有効であることを確認します。
    
    5.  <strong>詳細表示</strong> をクリックして、いつまただれによってメールボックスが訴訟ホールドの対象とされたかを確認します。オプションの <strong>訴訟ホールド期間 (日)</strong>、<strong>メモ</strong>、および <strong>URL</strong> ボックスの値を確認したり、変更したりすることもできます。

  - シェルで、次のいずれかのコマンドを実行します。
    
        Get-Mailbox <name of mailbox> | FL LitigationHold*
    
    または
    
        Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | FL Name,LitigationHold*
    
    メールボックスが無期限に訴訟ホールドの対象とされた場合、メールボックスの *LitigationHoldDuration* プロパティの値は `Unlimited` に設定されています。

## 詳細情報

  - 組織においてすべてのメールボックス データを特定の期間保持する必要がある場合、組織内のすべてのメールボックスを訴訟ホールドの対象にする前に、以下を考慮します。
    
      - 上記のコマンドを使用して、組織内のすべてのメールボックス (または指定した受信者フィルターに一致するメールボックスのサブセット) を保持の対象にすると、コマンドを実行した時点で存在するメールボックスのみが保持の対象になります。後でメールボックスを新規作成する場合は、再度コマンドを実行して、その新しいメールボックスを保持の対象にする必要があります。頻繁にメールボックスを新規作成する場合は、必要な頻度にスケジュールしたタスクとしてコマンドを実行できます。
    
      - すべてのメールボックスを訴訟ホールドの対象にすると、メールボックスのサイズに大きな影響を与える可能性があります。Exchange Server 2013 組織では、組織の保持要件を満たすのに十分なストレージを計画します。
    
      - \[回復可能なアイテム\] フォルダーには独自の格納域の制限があるため、このフォルダー内のアイテムはメールボックスの格納域の制限にカウントされません。上記の説明のとおり、メールボックスのデータを長期間保持すると、ユーザーのメールボックスとアーカイブにある \[回復可能なアイテム\] フォルダーのサイズが増大します。この Exchange Online の増大に対応するため、メールボックスを訴訟ホールドの対象にすると、\[回復可能なアイテム\] フォルダーのクォータは自動的に 30 GB から 100 GB に増加します。
        
        Exchange Server 2013 でも、\[回復可能なアイテム\] フォルダーの既定の格納域の制限は 30 GB です。\[回復可能なアイテム\] フォルダーが制限に達していないことを確認するため、フォルダーのサイズを定期的に監視することをお勧めします。詳細については、「[\[回復可能なアイテム\] フォルダー](recoverable-items-folder-exchange-2013-help.md)」を参照してください。

  - すべてのメールボックスを保持の対象にする上記のコマンドでは、すべてのユーザーのメールボックスを返す受信者フィルターが使用されます。特定のメールボックスを訴訟ホールドの対象とするために、その他の受信者プロパティを使用して、**Set-Mailbox** コマンドレットにパイプ処理できるそれらのメールボックスの一覧を返すことができます。
    
    以下に、**Get-Mailbox** コマンドレットと **Get-Recipient** コマンドレットを使用して、共通のユーザー属性またはメールボックス属性に基づいてメールボックスのサブセットを返す例を示します。これらの例では、関連するメールボックスのプロパティ (*CustomAttributeN* や *Department* など) が入力されていることを想定しています。
    ```
    Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'CustomAttribute15 -eq "OneYearLitigationHold"'
    ```
    ```
```powershell
Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "HR"'
```
    ```
    ```
    Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'PostalCode -eq "98052"'
    ```
    ```
    Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'StateOrProvince -eq "WA"'
    ```
    ```
```powershell
Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -ne "DiscoveryMailbox"}
```
    ```

    フィルターで他のユーザーのメールボックス プロパティを使用して、メールボックスを含めたり、除外したりすることができます。詳細については、「[-Filter パラメーターのフィルター可能なプロパティ](https://technet.microsoft.com/ja-jp/library/bb738155\(v=exchg.150\))」を参照してください。

ページのトップへ

