---
title: '複数値プロパティの変更: Exchange 2013 Help'
TOCTitle: 複数値プロパティの変更
ms:assetid: dc2c1062-ad79-404b-8da3-5b5798dbb73b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb684908(v=EXCHG.150)
ms:contentKeyID: 49129833
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 複数値プロパティの変更

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

複数値プロパティとは、複数の値を含むことのできるプロパティです。たとえば、**RecipientFilterConfig** オブジェクトの **BlockedRecipients** プロパティには、次の例のように複数の受信者のアドレスを使用することができます。

  - john@contoso.com

  - kim@northwindtraders.com

  - david@adatum.com

**BlockedRecipients** プロパティには、複数の値を使用することができるため、複数値プロパティと呼ばれています。ここでは、Exchange 管理シェルを使用して、オブジェクトの複数値プロパティに値を追加したり削除したりする方法について説明します。

オブジェクトの詳細については、「[構造化データ](https://technet.microsoft.com/ja-jp/library/aa996386\(v=exchg.150\))」を参照してください。シェルの詳細については、「[Exchange 2013 で Powershell を使用する (Exchange 管理シェル)](https://technet.microsoft.com/ja-jp/library/bb123778\(v=exchg.150\))」を参照してください。

## 複数値プロパティの変更および単一の値のみを使用するプロパティの変更

複数値プロパティの変更方法は、単一の値しか使用できないプロパティの変更方法とは少し異なります。単一の値しか使用できないプロパティを変更する場合は、次のコマンドのように直接値を割り当てることができます。

```powershell
Set-TransportConfig -MaxSendSize 12MB
```

このコマンドを使用して **MaxSendSize** プロパティに新しい値を指定すると、保存されている値が上書きされます。単一の値しか使用できないプロパティの場合は、これで問題ありませんが、複数値プロパティの場合は問題になります。たとえば、**RecipientFilterConfig** オブジェクトの **BlockedRecipients** プロパティが、前のセクションに記載されている 3 つの値を持つように構成されていると仮定します。コマンド `Get-RecipientFilterConfig | Format-List BlockedRecipients` を実行すると、次のように表示されます。

```powershell
BlockedRecipients : {david@adatum.com, kim@northwindtraders.com, john@contoso.com}
```

ここで、ブロックされた受信者の一覧に新しい SMTP アドレスを追加する要求を受信したと仮定します。次のコマンドを実行して、新しい SMTP アドレスを追加します。

```powershell
Set-RecipientFilterConfig -BlockedRecipients chris@contoso.com
```

`Get-RecipientFilterConfig | Format-List BlockedRecipients` コマンドを再度実行すると、次のように表示されます。

```powershell
BlockedRecipients : {chris@contoso.com}
```

これは期待した内容ではありません。ブロックされた受信者の既存の一覧に新しい SMTP アドレスを追加しようとしたにもかかわらず、ブロックされた受信者の既存の一覧が新しい SMTP アドレスで上書きされています。この意図しない結果は、複数値プロパティの変更方法と、単一の値しか使用できないプロパティの変更方法とが異なることを例示しています。複数値プロパティを変更する場合は、値の一覧全体を上書きするのではなく、値を追加または削除することを確認する必要があります。次のセクションでは、この正確な方法を示します。

## 複数値プロパティの変更

複数値プロパティの変更は、単一値プロパティの変更に似ています。プロパティに保存された値をすべて置き換えるのではなく、複数値プロパティに対して値を追加または削除するようにシェルに指示する構文をいくつか追加するだけで済みます。コマンドレットを実行する際、プロパティに対して追加または削除する値とともに構文がパラメーター値として含まれます。次の表は、複数値プロパティを変更するために、コマンドレットのパラメーターに追加する必要のある構文を示しています。

### 複数値プロパティの構文

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Action</th>
<th>構文</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1 つ以上の値を複数値プロパティに追加します。</p></td>
<td><pre><code>@{Add=&quot;&lt;value1&gt;&quot;, &quot;&lt;value2&gt;&quot;, &quot;&lt;value3&gt;&quot;}</code></pre></td>
</tr>
<tr class="even">
<td><p>1 つ以上の値を複数値プロパティから削除します。</p></td>
<td><pre><code>@{Remove=&quot;&lt;value1&gt;&quot;, &quot;&lt;value2&gt;&quot;, &quot;&lt;value3&gt;&quot;}</code></pre></td>
</tr>
</tbody>
</table>


複数値プロパティの構文の表から選択した構文は、コマンドレット上ではパラメーター値として指定されます。たとえば、次のコマンドは複数の値を複数値プロパティに追加します。

```powershell
Set-ExampleCmdlet -Parameter @{Add="Red", "Blue", "Green"}
```

この構文を使用すると、指定した値がすでにプロパティに存在する値のリストに対して追加または削除されます。このトピックで以前取り上げた **BlockedRecipients** の例で説明すると、次のコマンドを使用して、他の値を上書きすることなくこのプロパティに chris@contoso.com を追加できます。

```powershell
Set-RecipientFilterConfig -BlockedRecipients @{Add="chris@contoso.com"}
```

david@adatum.com を値のリストから削除したい場合は、次のコマンドを使用します。

```powershell
Set-RecipientFilterConfig -BlockedRecipients @{Remove="david@adatum.com"}
```

プロパティに対して同時に値を追加したり削除したりするような、より複雑な組み合わせも使用できます。そのためには、セミコロン (`;` ) を `Add` と `Remove` のアクションの間に挿入します。次に例を示します。

```powershell
Set-RecipientFilterConfig -BlockedRecipients @{Add="carter@contoso.com", "sam@northwindtraders.com", "brian@adatum.com"; Remove="john@contoso.com"}
```  

`Get-RecipientFilterConfig | Format-List BlockedRecipients` コマンドを再度使用すると、Carter、Sam、および Brian の電子メール アドレスが追加された一方で、John のアドレスが削除されたことが分かります。

```powershell
BlockedRecipients : {brian@adatum.com, sam@northwindtraders.com, carter@contoso.com, chris@contoso.com, kim@northwindtraders.com}
```  
