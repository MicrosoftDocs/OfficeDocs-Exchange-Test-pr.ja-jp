---
title: 'コマンド出力の操作: Exchange 2013 Help'
TOCTitle: コマンド出力の操作
ms:assetid: 8320e1a5-d3f5-4615-878d-b23e2aaa6b1e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb123533(v=EXCHG.150)
ms:contentKeyID: 49129564
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# コマンド出力の操作

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

Exchange 管理シェルには、コマンド出力の書式設定に使用できるいくつかの方法が含まれています。このトピックでは、次の内容について説明します。

  - How to format data   表示するデータの書式を制御するには、**Format-List** コマンドレット、**Format-Table** コマンドレット、および **Format-Wide** コマンドレットを使用します。

  - How to output data   シェル コンソール ウィンドウまたはファイルをデータの出力先として指定するには、**Out-Host** コマンドレットと **Out-File** コマンドレットを併用します。このトピックに含まれているスクリプトの例では、データは Microsoft Internet Explorer に出力されます。

  - How to filter data   データを抽出するには、次のいずれかのフィルタリング方法を使用します。
    
      - 特定のコマンドレットで使用できる、サーバー側のフィルタリング。
    
      - コマンドの出力を **Where-Object** コマンドレットにパイプ処理することによって、すべてのコマンドレットで使用できる、クライアント側のフィルタリング。

このトピックで説明する機能を使用するには、次の概念を理解しておく必要があります。

  - [パイプライン処理](https://technet.microsoft.com/ja-jp/library/aa998260\(v=exchg.150\))

  - [シェル変数](https://technet.microsoft.com/ja-jp/library/bb124036\(v=exchg.150\))

  - [比較演算子](https://technet.microsoft.com/ja-jp/library/bb125229\(v=exchg.150\))

## データを書式設定する方法

パイプラインの最後に書式設定コマンドレットを呼び出すと、既定の書式設定を変更して、表示内容と表示方法を制御できます。書式設定コマンドレットは、**Format-List**、**Format-Table**、および **Format-Wide** です。各コマンドレットは、他の書式設定コマンドレットとは異なる、固有の出力方式を持っています。

## Format-List

**Format-List** コマンドレットは、パイプラインから入力を取得し、各オブジェクトの指定されたすべてのプロパティの一覧を縦に並べた列で出力します。*Property* パラメーターを使用して、表示するプロパティを指定できます。パラメーターを指定しないで **Format-List** コマンドレットを呼び出すと、すべてのプロパティが出力されます。**Format-List** コマンドレットでは、行は切り捨てられるのではなく、折り返されます。**Format-List** コマンドレットの最適な使用方法の 1 つは、コマンドレットの既定の出力を変更して、追加情報やより集中した情報を取得できるようにすることです。

たとえば、**Get-Mailbox** コマンドレットを呼び出した場合、表形式で表示される情報量は限られたものです。**Get-Mailbox** コマンドレットの出力を **Format-List** コマンドレットにパイプ処理して、追加情報またはより集中した情報を表示するために必要なパラメーターを追加すると、目的の出力が得られます。

また、プロパティ名の一部にワイルドカード文字 "\*" も指定できます。ワイルドカード文字を使用すると、各プロパティ名を個々に入力しなくても、複数のプロパティに一致させることができます。たとえば、"`Get-Mailbox | Format-List -Property Email* `" と指定すると、"`Email`" で始まるすべてのプロパティが返されます。

次の例は、**Get-Mailbox** コマンドレットによって返される同じデータを異なる方法で表示したものです。

```powershell
Get-Mailbox TestUser1

Name                      Alias                ServerName       ProhibitSendQuo
                                                                ta
----                      -----                ----------       ---------------
TestUser1                 TestUser1            mbx              unlimited
```

最初の例では、**Get-Mailbox** コマンドレットは特定の書式設定を指定されずに呼び出されているので、既定の出力は表形式で、事前に設定されていたプロパティ セットが表示されます。

```powershell
Get-Mailbox TestUser1 | Format-List -Property Name,Alias,EmailAddresses

Name           : TestUser1
Alias          : TestUser1
EmailAddresses : {SMTP:TestUser1@contoso.com}
```

2 番目の例では、**Get-Mailbox** コマンドレットの出力は、特定のプロパティを指定した **Format-List** コマンドレットにパイプ処理されます。ご覧のとおり、出力の形式と内容は大幅に異なります。

```powershell
Get-Mailbox TestUser1 | Format-List -Property Name, Alias, Email*
Name                      : Test User
Alias                     : TestUser1
EmailAddresses            : {SMTP:TestUser1@contoso.com}
EmailAddressPolicyEnabled : True
```

最後の例では、**Get-Mailbox** コマンドレットの出力は 2 番目の例と同じように、**Format-List** コマンドレットにパイプ処理されます。ただし、最後の例では、ワイルドカード文字を使用して、`Email` で始まるすべてのプロパティと一致させています。

**Format-List** コマンドレットに複数のオブジェクトが渡された場合、オブジェクトの指定されたプロパティはすべて、オブジェクトごとに表示され、グループ化されます。表示される順序は、コマンドレットの既定のパラメーターによって決まります。既定のパラメーターは通常、*Name* パラメーターまたは *Identity* パラメーターです。たとえば、**Get-Childitem** コマンドレットが呼び出された場合、既定の表示順序はファイル名のアルファベット順です。この動作を変更するには、*GroupBy* パラメーター、および出力をグループ化する対象のプロパティ値の名前を指定して、**Format-List** コマンドレットを呼び出す必要があります。たとえば、次のコマンドでは、ディレクトリ内のすべてのファイルの一覧が拡張子ごとにグループ化されて表示されます。

```powershell
Get-Childitem | Format-List Name,Length -GroupBy Extension

    Extension: .xml

Name   : Config_01.xml
Length : 5627

Name   : Config_02.xml
Length : 3901


    Extension: .bmp

Name   : Image_01.bmp
Length : 746550

Name   : Image_02.bmp
Length : 746550


    Extension: .txt

Name   : Text_01.txt
Length : 16822

Name   : Text_02.txt
Length : 9835
```

この例では、**Format-List** コマンドレットは、*GroupBy* パラメーターで指定された *Extension* プロパティごとに項目をグループ化します。パイプライン ストリームでは、オブジェクトの有効なプロパティを指定して、*GroupBy* パラメーターを使用できます。

## Format-Table

**Format-Table** コマンドレットでは、ラベル ヘッダーとプロパティ データの列が設定された表形式で項目が表示されます。既定では、**Get-Process** コマンドレットや **Get-Service** コマンドレットなどの多くのコマンドレットが出力に表形式を使用します。**Format-Table** コマンドレットのパラメーターとしては、*Properties* パラメーターや *GroupBy* パラメーターが挙げられます。これらのパラメーターは、**Format-List** コマンドレットの場合とまったく同じように動作します。

また、**Format-Table** コマンドレットは *Wrap* パラメーターも使用します。このパラメーターを使用すると、プロパティ情報が長い行になる場合でも、行末で切り捨てられることなく完全に表示されます。*Wrap* パラメーターを使用して、返された情報がどのように表示されるかを確認するには、次の 2 つの例の **Get-Command** コマンドの出力を比較してください。

最初の例では、**Get-Command** コマンドレットを使用して **Get-Process** コマンドレットに関するコマンド情報が表示された場合、*Definition* プロパティの情報は切り捨てられています。

```powershell
Get-Command Get-Process | Format-Table Name,Definition

Name                                    Definition
----                                    ----------
get-process                             get-process [[-ProcessName] String[]...
```

2 番目の例では、コマンドに *Wrap* パラメーターを追加して、*Definition* プロパティの完全な内容が表示されるように設定しています。

```powershell
Get-Command Get-Process | Format-Table Name,Definition -Wrap

Get-Process                             Get-Process [[-Name] <String[]>] [-Comp
                                    uterName <String[]>] [-Module] [-FileVe
                                    rsionInfo] [-Verbose] [-Debug] [-ErrorA
                                    ction <ActionPreference>] [-WarningActi
                                    on <ActionPreference>] [-ErrorVariable
                                    <String>] [-WarningVariable <String>] [
                                    -OutVariable <String>] [-OutBuffer <Int
                                    32>]
                                    Get-Process -Id <Int32[]> [-ComputerNam
                                    e <String[]>] [-Module] [-FileVersionIn
                                    fo] [-Verbose] [-Debug] [-ErrorAction <
                                    ActionPreference>] [-WarningAction <Act
                                    ionPreference>] [-ErrorVariable <String
                                    >] [-WarningVariable <String>] [-OutVar
                                    iable <String>] [-OutBuffer <Int32>]
                                    Get-Process [-ComputerName <String[]>]
                                    [-Module] [-FileVersionInfo] -InputObje
                                    ct <Process[]> [-Verbose] [-Debug] [-Er
                                    rorAction <ActionPreference>] [-Warning
                                    Action <ActionPreference>] [-ErrorVaria
                                    ble <String>] [-WarningVariable <String
                                    >] [-OutVariable <String>] [-OutBuffer
                                    <Int32>]
```

**Format-List** コマンドレットの場合と同じように、ここでもプロパティ名の一部にワイルドカード文字 "`*`" を使用できます。ワイルドカード文字を使用すると、各プロパティ名を個々に入力しなくても、複数のプロパティに一致させることができます。

## Format-Wide

**Format-Wide** コマンドレットは、他の書式設定コマンドレットよりも、さらに簡単に出力を制御できます。既定では、**Format-Wide** コマンドレットは、出力の行に、できる限り多くのプロパティ値の列を表示しようとします。パラメーターを追加することによって、列の数と出力領域の使用方法を制御できます。

最も基本的な使用方法として、パラメーターを指定しないで **Format-Wide** コマンドレットを呼び出すと、ページに収まる限りの多くの列に出力が表示されます。たとえば、**Get-Childitem** コマンドレットを実行して、その出力を **Format-Wide** コマンドレットにパイプ処理すると、次のような情報が表示されます。

```powershell
Get-ChildItem | Format-Wide

    Directory: FileSystem::C:\WorkingFolder

Config_01.xml                           Config_02.xml
Config_03.xml                           Config_04.xml
Config_05.xml                           Config_06.xml
Config_07.xml                           Config_08.xml
Config_09.xml                           Image_01.bmp
Image_02.bmp                            Image_03.bmp
Image_04.bmp                            Image_05.bmp
Image_06.bmp                            Text_01.txt
Text_02.txt                             Text_03.txt
Text_04.txt                             Text_05.txt
Text_06.txt                             Text_07.txt
Text_08.txt                             Text_09.txt
Text_10.txt                             Text_11.txt
Text_12.txt
```

通常、パラメーターを指定しないで **Get-Childitem** コマンドレットを呼び出すと、プロパティの表にディレクトリ内のすべてのファイル名が表示されます。この例では、**Get-Childitem** コマンドレットの出力を **Format-Wide** コマンドレットにパイプ処理することによって、出力は 2 つの名前の列で表示されました。一度に表示できるプロパティは 1 種類だけで、**Format-Wide** コマンドレットの後ろに続くプロパティ名で指定しています。*Autosize* パラメーターを追加すると、出力される列は 2 列から、画面の幅に収まる限りの多くの列に変更されます。

```powershell
Get-ChildItem | Format-Wide -AutoSize

    Directory: FileSystem::C:\WorkingFolder

Config_01.xml   Config_02.xml   Config_03.xml   Config_04.xml   Config_05.xml
Config_06.xml   Config_07.xml   Config_08.xml   Config_09.xml   Image_01.bmp
Image_02.bmp    Image_03.bmp    Image_04.bmp    Image_05.bmp    Image_06.bmp
Text_01.txt     Text_02.txt     Text_03.txt     Text_04.txt     Text_05.txt
Text_06.txt     Text_07.txt     Text_08.txt     Text_09.txt     Text_10.txt
Text_11.txt     Text_12.txt
```

この例では、表は、2 列ではなく 5 列で表示されています。*Column* パラメーターを使用すると、次のように情報を表示する列の最大数を指定できるので、より細かく制御できます。

```powershell
Get-ChildItem | Format-Wide -Column 4

    Directory: FileSystem::C:\WorkingFolder

Config_01.xml       Config_02.xml       Config_03.xml       Config_04.xml
Config_05.xml       Config_06.xml       Config_07.xml       Config_08.xml
Config_09.xml       Image_01.bmp        Image_02.bmp        Image_03.bmp
Image_04.bmp        Image_05.bmp        Image_06.bmp        Text_01.txt
Text_02.txt         Text_03.txt         Text_04.txt         Text_05.txt
Text_06.txt         Text_07.txt         Text_08.txt         Text_09.txt
Text_10.txt         Text_11.txt         Text_12.txt
```

この例では、*Column* パラメーターを使用して、列の数を 4 に設定しています。

## データを出力する方法

## Out-Host コマンドレットと Out-File コマンドレット

**Out-Host** コマンドレットは、パイプラインの最後にある、非表示の既定コマンドレットです。すべての書式設定が適用された後で、**Out-Host** コマンドレットによって最終出力がコンソール ウィンドウに送信されて、表示されます。**Out-Host** コマンドレットは既定の出力なので、明示的に呼び出す必要はありません。**Out-File** コマンドレットをコマンド内の最後のコマンドレットとして呼び出すことによって、コンソール ウィンドウへの出力の送信を変更できます。**Out-File** コマンドレットは、次の例に示すように、コマンドに指定されたファイルに出力を書き込みます。

```powershell
Get-ChildItem | Format-Wide -Column 4 | Out-File c:\OutputFile.txt
```

この例では、**Out-File** コマンドレットは、**Get-ChildItem | Format-Wide -Column 4** コマンドで出力された情報を `OutputFile.txt` というファイルに書き込みます。また、リダイレクト演算子 (終わり山かっこ (`>`) を使用して、パイプラインの出力をファイルにリダイレクトすることもできます。コマンドのパイプライン出力で既存のファイルを置き換えるのではなく、パイプライン出力を既存のファイルに追加するには、次の例に示すように、終わり二重山かっこ (`>>`) を使用します。

```powershell
Get-ChildItem | Format-Wide -Column 4 >> C:\OutputFile.txt
```

この例では、**Get-Childitem** コマンドレットからの出力は、書式設定のために **Format-Wide** コマンドレットにパイプ処理されてから、`OutputFile.txt` ファイルの最後に書き込まれます。`OutputFile.txt` ファイルが存在しないときに、終わり二重山かっこ (`>>`) を使用すると、ファイルが作成されます。

パイプラインの詳細については、「[パイプライン処理](https://technet.microsoft.com/ja-jp/library/aa998260\(v=exchg.150\))」を参照してください。

上の例で使用されている構文の詳細については、「[構文](https://technet.microsoft.com/ja-jp/library/bb123552\(v=exchg.150\))」を参照してください。

## Internet Explorer でのデータの表示

Exchange 管理シェルは柔軟で、スクリプトを簡単に実行できるので、ほとんど制約なく、コマンドによって返されたデータを取得、書式設定、出力することができます。

次の例は、簡単なスクリプトを使用して、コマンドによって返されたデータを出力して、Internet Explorer に表示する方法を示したものです。このスクリプトは、パイプラインによって渡されたオブジェクトを取得し、Internet Explorer ウィンドウを開き、Internet Explorer にデータを表示します。

```powershell
$Ie = New-Object -Com InternetExplorer.Application
$Ie.Navigate("about:blank")
While ($Ie.Busy) { Sleep 1 }
$Ie.Visible = $True
$Ie.Document.Write("$Input")
# If the previous line doesn't work on your system, uncomment the line below.
# $Ie.Document.IHtmlDocument2_Write(\"$Input\")
$Ie
```

このスクリプトを使用するには、スクリプトを実行するコンピューター上の `C:\Program Files\Microsoft\Exchange Server\V15\Scripts` ディレクトリにこのスクリプトを保存します。ファイルに `Out-Ie.ps1` という名前を付けます。ファイルを保存した後は、通常のコマンドレットとしてこのスクリプトを使用できます。


> [!NOTE]
> Exchange 2013 でスクリプトを実行するには、スクリプトを対象範囲外の管理役割に追加し、管理役割を直接的にまたは管理役割グループを介して自分に割り当てる必要があります。詳細については、「<A href="understanding-management-roles-exchange-2013-help.md">管理の役割について</A>」を参照してください。



`Out-Ie` スクリプトでは、受け取るデータは有効な HTML であることを前提にしています。表示するデータを HTML に変換するには、コマンドの出力を **ConvertTo-Html** コマンドレットにパイプ処理する必要があります。次に、そのコマンドの出力を `Out-Ie` スクリプトにパイプ処理することができます。次の例は、Internet Explorer のウィンドウに一覧表示されるディレクトリの表示方法を示したものです。

```powershell
Get-ChildItem | Select Name,Length | ConvertTo-Html | Out-Ie
```

## データをフィルター処理する方法

シェルを使用して、組織内のサーバー、メールボックス、Active Directory、およびその他のオブジェクトに関する膨大な量の情報にアクセスできます。このような情報にアクセスすることで、自身の環境をより深く理解できますが、情報量が多すぎて有効活用できないことがあります。シェルを使用すると、フィルター処理によってこのような情報を制御し、目的のデータだけを取得できます。次の種類のフィルター処理を使用できます。

  - **サーバー側のフィルタリング**   サーバー側のフィルタリングは、コマンド ラインで指定されたフィルターを取得し、クエリを実行する Exchange サーバーにそのフィルターを送信します。そのサーバーは、クエリを処理して、指定されたフィルターと一致するデータのみを返します。
    
    サーバー側のフィルタリングは、何万、何十万という結果を返すことができるオブジェクトに対してのみ実行されます。したがって、受信者管理コマンドレット (**Get-Mailbox** コマンドレットなど) およびキュー管理コマンドレット (**Get-Queue** コマンドレットなど) のみがサーバー側のフィルタリングをサポートしています。これらのコマンドレットは、*Filter* パラメーターをサポートしています。このパラメーターによって、指定されたフィルター式を取得して、処理のためにサーバーに送信します。

  - **クライアント側のフィルタリング**   クライアント側のフィルタリングは、現在作業中のローカルなコンソール ウィンドウ内のオブジェクトに対して実行されます。クライアント側のフィルタリングを使用した場合、コマンドレットは、ローカルなコンソール ウィンドウで実行中のタスクに一致するすべてのオブジェクトを取得します。シェルは、返された出力をすべて取得し、それらの結果にクライアント側のフィルターを適用し、指定されたフィルターに一致する出力のみを返します。すべてのコマンドレットは、クライアント側のフィルタリングをサポートしています。これは、コマンドの出力を **Where-Object** コマンドレットにパイプ処理することによって呼び出されます。

## サーバー側のフィルタリング

サーバー側のフィルタリングの実装は、サポートされているコマンドレットに固有です。サーバー側のフィルタリングは、返されるオブジェクトの特定のプロパティに対してのみ有効です。詳細については、次のコマンドレットのヘルプを参照してください。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Get-ActiveSyncDevice</p></td>
<td><p>Get-ActiveSyncDeviceClass</p></td>
<td><p>Get-CASMailbox</p></td>
<td><p>Get-Contact</p></td>
<td><p>Get-DistributionGroup</p></td>
</tr>
<tr class="even">
<td><p>Get-DynamicDistributionGroup</p></td>
<td><p>Get-Group</p></td>
<td><p>Get-Mailbox</p></td>
<td><p>Get-MailboxStatistics</p></td>
<td><p>Get-MailContact</p></td>
</tr>
<tr class="odd">
<td><p>Get-MailPublicFolder</p></td>
<td><p>Get-MailUser</p></td>
<td><p>Get-Message</p></td>
<td><p>Get-MobileDevice</p></td>
<td><p>Get-Queue</p></td>
</tr>
<tr class="even">
<td><p>Get-QueueDigest</p></td>
<td><p>Get-Recipient</p></td>
<td><p>Get-RemoteMailbox</p></td>
<td><p>Get-RoleGroup</p></td>
<td><p>Get-SecurityPrincipal</p></td>
</tr>
<tr class="odd">
<td><p>Get-StoreUsageStatistics</p></td>
<td><p>Get-UMMailbox</p></td>
<td><p>Get-User</p></td>
<td><p>Get-UserPhoto</p></td>
<td><p>Remove-Message</p></td>
</tr>
<tr class="even">
<td><p>Resume-Message</p></td>
<td><p>Resume-Queue</p></td>
<td><p>Retry-Queue</p></td>
<td><p>Suspend-Message</p></td>
<td><p>Suspend-Queue</p></td>
</tr>
</tbody>
</table>


## クライアント側のフィルタリング

クライアント側のフィルタリングは、あらゆるコマンドレットで使用できます。この機能に対応したコマンドレットには、サーバー側のフィルタリングをサポートしているものもあります。このトピックで説明したように、クライアント側のフィルタリングは、パイプラインの前のコマンドによって返されるすべてのデータを受け付け、代わりに、指定されたフィルターに一致する出力のみを返します。**Where-Object** コマンドレットは、このフィルタリングを実行します。このコマンドは、**Where** に短縮することもできます。

データがパイプラインを通過すると、**Where** コマンドレットは前のオブジェクトからデータを受け取り、次のオブジェクトに渡す前にそのデータをフィルター処理します。フィルタリングは、**Where** コマンドで定義されたスクリプト ブロックに基づいています。スクリプト ブロックは、オブジェクトのプロパティと値に基づいて、データをフィルター処理します。

**Clear-Host** コマンドレットを使用して、コンソール ウィンドウを消去します。この例では、次のコマンドを使用すると、**Clear-Host** コマンドレットに定義されているすべてのエイリアスを検索できます。

```powershell
Get-Alias | Where {$_.Definition -eq "Clear-Host"}

CommandType     Name                            Definition
-----------     ----                            ----------
Alias           clear                           clear-host
Alias           cls                             clear-host
```

**Get-Alias** コマンドレットと **Where** コマンドは連携動作して、**Clear-Host** コマンドレットに定義されているエイリアスの一覧を返し、それ以外のコマンドレットについては何も返しません。次の表は、例に使用されている **Where** コマンドの各要素の概要説明です。

### Where コマンドの要素

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>{ }</code></p></td>
<td><p>中かっこで、フィルターを定義するスクリプト ブロックを囲みます。</p></td>
</tr>
<tr class="even">
<td><p><code>$_</code></p></td>
<td><p>この特別な変数は自動的に開始され、パイプラインのオブジェクトにバインドされます。</p></td>
</tr>
<tr class="odd">
<td><p><code>Definition</code></p></td>
<td><p><code>Definition</code> プロパティは、エイリアス定義の名前を格納する、現在のパイプライン オブジェクトのプロパティです。<code>$_</code> 変数を指定して <code>Definition</code> を使用すると、プロパティ名の前にピリオドが付きます。</p></td>
</tr>
<tr class="even">
<td><p><code>-eq</code></p></td>
<td><p>&quot;と等しい&quot; を表す比較演算子。式で指定されているプロパティ値に結果が正確に一致する必要のあることを指定するために使用されます。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;<strong>Clear-Host</strong>&quot;</p></td>
<td><p>この例では、&quot;<strong>Clear-Host</strong>&quot; は、コマンドによって解析される値です。</p></td>
</tr>
</tbody>
</table>


この例では、**Get-Alias** コマンドレットによって返されるオブジェクトは、システムに定義されているすべてのエイリアスを表します。コマンド ラインから確認できなくても、エイリアスは収集され、パイプラインによって **Where** コマンドレットに渡されます。**Where** コマンドレットは、スクリプト ブロック内の情報を使用して、エイリアス オブジェクトにフィルターを適用します。

特別な変数 `$`\_ は、渡されているオブジェクトを表します。`$_` 変数はシェルによって自動的に開始され、現在のパイプライン オブジェクトにバインドされます。この特別な変数の詳細については、「[シェル変数](https://technet.microsoft.com/ja-jp/library/bb124036\(v=exchg.150\))」を参照してください。

標準的な "ドット" 表記法 (object.property) を使用して、`Definition` プロパティが追加され、評価のためにオブジェクトの正確なプロパティが定義されます。`-eq` 比較演算子は、次にこのプロパティの値と `"Clear-Host"` を比較します。この基準と一致する `Definition` プロパティを持つオブジェクトのみが、コンソール ウィンドウに渡されて出力されます。比較演算子の詳細については、「[比較演算子](https://technet.microsoft.com/ja-jp/library/bb125229\(v=exchg.150\))」を参照してください。

**Get-Alias** コマンドレットで返されたオブジェクトを **Where** コマンドを介してフィルター処理した後、このフィルター処理済みオブジェクトを別のコマンドにパイプ処理できます。Where コマンドで返されたフィルター処理済みオブジェクトのみが、次のコマンドによって処理されます。

