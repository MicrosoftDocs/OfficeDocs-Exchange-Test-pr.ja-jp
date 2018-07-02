---
title: '管理ロールのスコープ フィルターについて: Exchange 2013 Help'
TOCTitle: 管理ロールのスコープ フィルターについて
ms:assetid: 6acc2922-ee9c-41f1-8a0f-10a541e8c273
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd298043(v=EXCHG.150)
ms:contentKeyID: 49896297
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理ロールのスコープ フィルターについて

 

_**適用先:** Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

管理役割スコープ フィルターを使用すると、容易にカスタマイズできる管理スコープを定義できます。スコープ フィルターを使用すると、受信者、データベース、サーバーを区分して、管理者がアクセスする必要があるオブジェクトのみ管理できるようにするスコープを作成できます。スコープ フィルターは、ほぼすべての受信者、データベース、またはサーバー オブジェクトのプロパティを使用できます。

管理役割スコープ フィルターを使用するには、管理役割スコープを十分に理解しておく必要があります。管理役割スコープの詳細については、「[管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)」を参照してください。

Microsoft Exchange Server 2013 でのフィルター処理カスタム スコープは、**New-ManagementScope** コマンドレットを使用して作成します。受信者と構成という 2 種類のフィルター処理スコープ (サーバーおよびデータベースのスコープから構成) は、通常スコープと排他的スコープに分かれています。次の一覧に、フィルター処理スコープのそれぞれの種類を作成するために使用する **New-ManagementScope** コマンドレットのパラメーターを示します。

  - **受信者正規フィルター処理スコープ**   この種のフィルター処理スコープを作成するには、*RecipientRestrictionFilter* パラメーターを使用します。

  - **受信者排他フィルター処理スコープ**   この種のフィルター処理スコープを作成するには、*RecipientRestrictionFilter* パラメーターと *Exclusive* スイッチを併用します。

  - **サーバーベースの構成正規フィルター処理スコープ**   この種のフィルター処理スコープを作成するには、*ServerRestrictionFilter* パラメーターを使用します。

  - **サーバーベースの構成排他フィルター処理スコープ**   この種のフィルター処理スコープを作成するには、*ServerRestrictionFilter* パラメーターと *Exclusive* スイッチを併用します。

  - **データベースを使用する構成正規フィルター処理スコープ**   この種のフィルター処理スコープを作成するには、*DatabaseRestrictionFilter* パラメーターを使用します。

  - **データベースを使用する構成排他フィルター処理スコープ**   この種のフィルター処理スコープを作成するには、*DatabaseRestrictionFilter* パラメーターと *Exclusive* スイッチを併用します。

フィルター処理カスタム スコープを作成すると、そのスコープは、フィルターを管理役割の暗黙の読み取りスコープ内でアクセス可能なオブジェクトと照合しようとします。オブジェクトが見つかった場合、そのオブジェクトはフィルターによって返される結果に含まれ、カスタム スコープによって管理役割が利用できるようになります。フィルターは、管理役割の暗黙の読み取りスコープ外にある結果を返すことはできません。

*RecipientRestrictionFilter* パラメーターを使用して受信者フィルターを指定する場合、*RecipientRoot* パラメーターを使用し、組織単位 (OU) を指定してフィルターの適用先を制限できます。*RecipientRoot* パラメーターに OU を指定すると、受信者フィルターは、暗黙の読み取りスコープ内全体でなく、その OU のみに存在する受信者との照合を試みます。

このトピックで説明するフィルター可能なプロパティを使用した管理スコープの作成については、「[通常または排他スコープを作成する](create-a-regular-or-exclusive-scope-exchange-2013-help.md)」を参照してください。

## フィルターの構文

受信者フィルターと構成フィルターのどちらも、同じ構文を使用してフィルター クエリを作成します。すべてのフィルター クエリには、少なくとも次の構成要素が必要になります。

  - **左角かっこ**   左中かっこ (") は、フィルター クエリの開始を示します。

  - **検査するプロパティ**   このプロパティはテストするオブジェクトの値です。たとえば、受信者オブジェクトの市区町村や部門であったり、サーバー構成オブジェクトの Active Directory サイト名やサーバー名であったり、または、データベース構成オブジェクトのデータベース名であったりします。

  - **比較演算子**   比較演算子は、指定された値とプロパティに保存されている値との評価方法をクエリに指示します。たとえば、比較演算子には、**Eq** (等しい)、**Ne** (等しくない)、または **Like** (類似している) などを指定できます。Exchange 管理シェルで使用できる演算子の全一覧については、「[比較演算子](https://technet.microsoft.com/ja-jp/library/bb125229\(v=exchg.150\))」を参照してください。

  - **比較する値**   フィルター クエリに指定した値は、指定したプロパティに保存されている値と比較されます。指定した値は、二重引用符 (' ') で囲む必要があります。部分文字列を指定する場合、指定する文字列をワイルドカード文字 (\*) で囲み、**Like** などのワイルドカード文字をサポートしている比較演算子を使用できます。部分文字列を含む任意の文字列は、フィルター クエリと一致します。

  - **右角かっこ**   右中かっこ (}) は、フィルター クエリの末尾を示します。

次の構成要素はオプションで、より複雑なフィルター クエリを作成できます。

  - **かっこ**   数学と同様に、フィルター クエリにかっこ ( ) を指定すると、演算を行う順序を強制できます。フィルター クエリでは、一番内側のかっこが最初に評価され、順次一番外側のかっこまで評価されます。

  - **論理演算子**   論理演算子は 1 つ以上の比較演算子を連結したもので、フィルター クエリではそのステートメント全体を評価する必要があります。たとえば、論理演算子には、**And**、**Or**、**Not** などがあります。

まとめると、単純なクエリは `{ City -Eq "Vancouver" }` のようになります。このフィルターは、**City** プロパティの値が文字列 "Vancouver" に等しい受信者と一致します。

別のより複雑なクエリは `{ ((City -Eq "Vancouver") -And (Department -Eq "Sales")) -Or (Title -Like "*Manager*") }` のようになります。このフィルター クエリは、次の順序で評価されます。

1.  **City** プロパティと **Department** プロパティが評価されます。それぞれは、各プロパティに保存されている値に従って `True` または `False` に設定されます。

2.  次に、**City** および **Department** の各ステートメントの結果が評価されます。両方が `True` の場合、**And** ステートメント全体が `True` になります。一方または両方が `False` の場合は、**And** ステートメント全体が `False` になります。次の事項が適用されます。
    
      - **And** ステートメントが `True` と評価される場合、フィルター クエリ全体が `True` になります。**Or** 演算子が、クエリの一方または他方の側が `True` でなければならないと示しているためです。オブジェクトは役割割り当てに公開されます。
    
      - **And** ステートメントが `False` の場合、フィルター クエリは引き続き **Title** プロパティの評価を実行します。

3.  次に、**Title** プロパティが評価されます。これは、**Title** プロパティに保存されている値に従って、`True` または `False` に設定されます。次の事項が適用されます。
    
      - **Title** プロパティが `True` と評価される場合、フィルター クエリ全体が `True` になります。**Or** 演算子が、クエリの一方または他方の側が `True` でなければならないと示しているためです。オブジェクトは役割割り当てに公開されます。
    
      - **Title** プロパティが `False` と評価される場合、フィルター クエリ全体が `False` と評価され、オブジェクトは役割割り当てに公開されません。

次の表に、複雑なクエリが `True` と評価される場合、および `False` と評価される場合の値の例を示します。

### 複雑なクエリ

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>都市</th>
<th>部署</th>
<th>役職</th>
<th>結果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Vancouver (True)</p></td>
<td><p>Sales (True)</p></td>
<td><p>CEO (False)</p></td>
<td><p>True (<strong>City</strong> および <strong>Department</strong> の両方が True と評価されたため)。<strong>Title</strong> は、フィルター クエリ条件が既に満たされているため、評価されません。</p></td>
</tr>
<tr class="even">
<td><p>Seattle (False)</p></td>
<td><p>Sales (True)</p></td>
<td><p>IT Manager (True)</p></td>
<td><p>True (<strong>Title</strong> が True と評価されたため)。<strong>City</strong> と <strong>Department</strong> の比較の結果は、破棄されます。<strong>Title</strong> が True と評価され、フィルター クエリ条件が満たされたためです。</p>

> [!NOTE]
> IT Manager は、フィルター クエリに一致します。その理由は、<STRONG>Like</STRONG> 比較演算子が使用されていて、フィルター クエリにワイルドカード文字 (*) が使用されているため、部分文字列に一致するからです。


</td>
</tr>
<tr class="odd">
<td><p>Vancouver (True)</p></td>
<td><p>Marketing (False)</p></td>
<td><p>Writer (False)</p></td>
<td><p>False (<strong>City</strong> と <strong>Department</strong> の両方が True と評価されず、かつ <strong>Title</strong> も True と評価されていないため)。</p></td>
</tr>
</tbody>
</table>


## フィルター処理可能な受信者プロパティ

受信者フィルターを作成する場合、受信者オブジェクト上のほとんどすべてのプロパティを使用できます。フィルター処理可能な受信者プロパティの一覧については、「[-RecipientFilter パラメーターのフィルター可能なプロパティ](https://technet.microsoft.com/ja-jp/library/bb738157\(v=exchg.150\))」を参照してください。ここでは、他のコマンドレットの *RecipientFilter* パラメーターと併用できるプロパティについて説明していますが、これらのプロパティのほとんどは、**New-ManagementScope** コマンドレットの *RecipientRestrictionFilter* パラメーターでも機能します。

## フィルター処理可能なサーバー プロパティ

*ServerRestrictionFilter* パラメーターを使用して管理スコープを作成する場合、次のサーバー プロパティを使用できます。

  - **CurrentServerRole**

  - **CustomerFeedbackEnabled**

  - **DataPath**

  - **DistinguishedName**

  - **ExchangeLegacyDN**

  - **ExchangeLegacyServerRole**

  - **ExchangeVersion**

  - **Fqdn**

  - **Guid**

  - **InternetWebProxy**

  - **Name**

  - **NetworkAddress**

  - **ObjectCategory**

  - **ObjectClass**

  - **ProductID**

  - **ServerRole**

  - **ServerSite**

  - **WhenChanged**

  - **WhenChangedUTC**

  - **WhenCreated**

  - **WhenCreatedUTC**

## フィルター処理可能なデータベース プロパティ

*DatabaseRestrictionFilter* パラメーターを使用して管理スコープを作成する場合、次のデータベース プロパティを使用できます。

  - **AdminDisplayName**

  - **AllowFileRestore**

  - **BackgroundDatabaseMaintenance**

  - **CircularLoggingEnabled**

  - **DatabaseCreated**

  - **DeletedItemRetention**

  - **Description**

  - **DistinguishedName**

  - **EdbFilePath**

  - **EventHistoryRetentionPeriod**

  - **ExchangeLegacyDN**

  - **ExchangeVersion**

  - **Guid**

  - **IssueWarningQuota**

  - **LogFilePrefix**

  - **LogFileSize**

  - **LogFolderPath**

  - **MasterServerOrAvailabilityGroup**

  - **MountAtStartup**

  - **Name**

  - **ObjectCategory**

  - **ObjectClass**

  - **RetainDeletedItemsUntilBackup**

  - **Server**

  - **WhenChanged**

  - **WhenChangedUTC**

  - **WhenCreated**

  - **WhenCreatedUTC**

