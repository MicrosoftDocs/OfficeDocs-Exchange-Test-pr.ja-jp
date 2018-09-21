---
title: 'すべてのメールボックスを保持に設定する: Exchange Online Help'
TOCTitle: すべてのメールボックスを保持に設定する
ms:assetid: 4c141604-3210-44cc-b98e-f3e0f15613b8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn767952(v=EXCHG.150)
ms:contentKeyID: 62486286
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# すべてのメールボックスを保持に設定する

 

_**適用先:** Exchange Online, Exchange Server 2013_


> [!NOTE]
> Exchange Online (Office 365 および Exchange Online のスタンドアロン計画)　における新しいインプレース ホールドの作成のための 2017 年 7 月 1 日の期限は延期になりました。しかし、今年の終わりか来年の初めには、Exchange Online での新しいインプレース ホールドの作成はできなくなります。インプレース ホールドを使用する代わりに、Office 365 セキュリティ/コンプライアンス センターの<A href="https://go.microsoft.com/fwlink/?linkid=780738">電子情報開示ケース</A>または<A href="https://go.microsoft.com/fwlink/?linkid=827811">アイテム保持ポリシー</A>を使用できます。新しいインプレース ホールドの使用停止後にも、引き続き既存のインプレース ホールドを変更することができます。また、Exchange Server 2013 と Exchange のハイブリッド展開でのインプレース ホールドの新規作成は引き続きサポートされます。また、引き続き訴訟ホールドにメールボックスを配置できます。



組織は、すべてのメールボックス データを特定の期間保持しなければならない場合があります。この要件を満たすには、訴訟ホールドまたはインプレース保持を使用します。メールボックスに訴訟ホールドまたはインプレース保持を設定すると、変更した、または永久に削除したメールボックスのアイテムは、\[回復可能なアイテム\] フォルダーに保持されます。詳細については、「[インプレース保持と訴訟ホールド](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/in-place-and-litigation-holds)」を参照してください。

組織内のすべてのメールボックスに訴訟ホールドまたはインプレース保持を設定する前に、次の点を考慮します。

  - メールボックスを保留にする場合、ユーザーのアーカイブ メールボックス内のコンテンツ (有効の場合) も保留になります。

  - 組織内のすべてのメールボックスを保持に設定すると、メールボックスのサイズに大きく影響します。Exchange Server 2013 展開では、組織の保持要件を満たすのに十分なストレージを計画します。ユーザーのExchange Online, 「[メールボックス格納域の制限](https://go.microsoft.com/fwlink/?linkid=403645)」は、ユーザーのサブスクリプション ライセンスによって異なります。

  - メールボックスのデータを長期間保持すると、ユーザーのプライマリ メールボックスとアーカイブ メールボックスにある \[回復可能なアイテム\] フォルダーのサイズが増大します。\[回復可能なアイテム\] フォルダーには独自の格納域の制限があるため、このフォルダー内のアイテムはメールボックスの格納域の制限にカウントされません。Exchange Server 2013 と Exchange Online では、\[回復可能なアイテム\] フォルダーにおける既定の格納域の制限は 30 GB になっています。
    
      - Exchange Online では、メールボックスを保留にすると、\[回復可能なアイテム\] フォルダーのクォータは自動的に 100 GB に引き上げられます。
    
      - Exchange Server 2013 では、\[回復可能なアイテム\] フォルダーが制限に達していないことを確認するため、フォルダーのサイズを定期的に監視することをお勧めします。詳細については、「[\[回復可能なアイテム\] フォルダー](recoverable-items-folder-exchange-2013-help.md)」を参照してください。

## 訴訟ホールドまたはインプレース保持の選択

以下に、組織内のすべてのメールボックスを保持するために使用する機能を決定する際に考慮すべきいくつかの要素を示します。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>必要な操作</th>
<th>訴訟ホールドを使用する</th>
<th>インプレース保持を使用する</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EAC を使用する</p></td>
<td><p>はい</p>
<p>訴訟ホールドを設定する場合、EAC はいくつかのメールボックスのクイック一時アクションに最適です。シェルを使用して、組織内のすべてのユーザーに対して訴訟ホールドを設定することをお勧めします。</p></td>
<td><p>はい</p>
<p>ただし、EAC では、500 を超えるソース メールボックスを選択することはできません。</p></td>
</tr>
<tr class="even">
<td><p>シェルを使用する</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p>10,000 個を超えるメールボックスを保持する</p></td>
<td><p>はい</p>
<p>訴訟ホールドはメールボックスのプロパティです。<strong>Set-Mailbox</strong> コマンドレットを使用して、組織内のすべてのメールボックスを保持します。</p></td>
<td><p>はい。 複数のインプレース保持を使用します。</p>
<p>配布グループを使用して 1 つのインプレース保持に最大 10,000 個のメールボックスを指定できます。追加のメールボックスを保持するには、追加のインプレース保持を作成する必要があります。これにより、追加の管理オーバーヘッドが発生します。多数のメールボックスを保持する訴訟ホールドを使用する方法の方がより簡単です。</p></td>
</tr>
<tr class="even">
<td><p>異なる期間に多くの異なるメールボックスを保持する</p></td>
<td><p>はい</p>
<p>訴訟ホールドはメールボックスのプロパティです。各メールボックス (またはメールボックスのセット) を異なる期間保持できます。</p>
<p>メールボックスのサブセットを訴訟ホールドの対象にできるようにフィルターで受信者のプロパティを使用する例については、「詳細情報」セクションを参照してください。</p></td>
<td><p>はい</p>
<p>何千ものメールボックスを個別に保持する場合は、訴訟ホールドの使用をお勧めします。複数のユーザーが関わる特定のイベントに保持設定を作成する場合は、ユーザーのグループに 1 つのインプレース保持を使用します。</p>
<p>各メールボックスに別々のインプレース保持を作成することはお勧めしません。多数のインプレース保持のクエリが作成されて、訴訟ホールドより管理が困難になるためです。多数のインプレース保持オブジェクトがあることも、保持オブジェクトの更新、作成、または変更の際、EAC のパフォーマンスの低下につながることがあります。</p></td>
</tr>
<tr class="odd">
<td><p>新しいメールボックスを自動的に保持する</p></td>
<td><p>いいえ</p>
<p>新しいメールボックスを作成した後、訴訟ホールドの対象にする必要があります。同じ効果を実現するには、必要なだけ頻繁に実行するようコマンドまたはスクリプトをスケジュールできます。</p></td>
<td><p>いいえ</p>
<p>インプレース保持を作成したときに配布グループを指定した場合でも、新しいメールボックスをインプレース保持に追加する必要があります。同じ効果を実現するには、必要なだけ頻繁に実行するようコマンドまたはスクリプトをスケジュールすることもできます。スクリプトを使用して、既存のインプレース保持が既に 10,000 個のメールボックスの制限に達しているかどうかを確認し、必要な場合は新しいインプレース保持を作成するようにすることをお勧めします。</p></td>
</tr>
<tr class="even">
<td><p>すべてのパブリック フォルダーを保持の対象にする</p></td>
<td><p>いいえ</p>
<p>Exchange Online では、パブリック フォルダー メールボックスを訴訟ホールドの対象にすることはサポートされていません。インプレース ホールドを使用する必要があります。</p></td>
<td><p>はい</p></td>
</tr>
</tbody>
</table>


## すべてのメールボックスを訴訟ホールドの対象にする

シェルを使用することにより、すべてのメールボックスを無制限に、または指定した期間保持するように素早く簡単に設定できます。このコマンドは、2555 日間 (約 7 年間) すべてのメールボックスを保持します。

    Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | Set-Mailbox -LitigationHoldEnabled $true -LitigationHoldDuration 2555

この例では、[Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\)) コマンドレットと受信者フィルターを使用して、組織内のすべてのユーザー メールボックスを取得します。それから、メールボックスの一覧を [Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\)) コマンドレットにパイプ処理して訴訟ホールドを有効にし、保持期間を指定します。詳細については、「[メールボックスを訴訟ホールドの対象にする](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)」を参照してください。

## すべてのメールボックスにインプレース保持を設定する

EAC を使用すると、最大 500 のメールボックスを選択して保持することができます。詳細については、「[インプレース保持を作成または削除する](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/create-or-remove-in-place-holds)」を参照してください。


> [!TIP]
> 500 人以上のユーザーにインプレース保持を設定するには、シェルを使用します。「<A href="https://technet.microsoft.com/ja-jp/library/dd298064(v=exchg.150)">New-MailboxSearch</A>」を参照してください。



## 詳細情報

  - 組織内のすべてのメールボックスを保持する場合、コマンドの実行時に存在するメールボックスのみが保持の対象とされます。後でメールボックスを新規作成する場合は、再度コマンドを実行して保持します。頻繁にメールボックスを新規作成する場合は、必要なだけ頻繁にスケジュールされたタスクとしてコマンドを実行できます。

  - メールボックスを保留に設定すると、指定した期間より前にデータが削除されるのを防止し、メッセージが変更される前に元のバージョンのメッセージが保存されます。メッセージは指定した期間後に自動的に削除されません。訴訟ホールドまたはインプレース保持とアイテム保持ポリシーを組み合わせることで、指定した期間後にメッセージが自動的に削除されるようにして、組織の電子メール保持要件を満たすこともできます。詳細については、「[保持タグおよびアイテム保持ポリシー](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/messaging-records-management/retention-tags-and-policies)」を参照してください。

  - すべてのメールボックスを訴訟ホールドの対象とするためにこのトピックで使用する PowerShell コマンドでは、すべてのユーザーのメールボックスを返す受信者フィルターが使用されます。特定のメールボックスを訴訟ホールドの対象とするために、その他の受信者プロパティを使用して、**Set-Mailbox** コマンドレットにパイプ処理できるそれらのメールボックスの一覧を返すことができます。
    
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

