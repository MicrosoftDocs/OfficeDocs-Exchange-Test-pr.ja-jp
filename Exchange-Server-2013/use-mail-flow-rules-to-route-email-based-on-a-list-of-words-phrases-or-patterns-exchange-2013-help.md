---
title: '単語、語句、パターンの一覧に基づいてメールをルーティングするメール フロー ルールの使用: Exchange Online Help'
TOCTitle: 単語、語句、パターンの一覧に基づいてメールをルーティングするメール フロー ルールの使用
ms:assetid: 4c5bee1b-58b5-4152-baef-86fa103050ae
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn951131(v=EXCHG.150)
ms:contentKeyID: 65218712
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 単語、語句、パターンの一覧に基づいてメールをルーティングするメール フロー ルールの使用

 

_**適用先:** Exchange Online, Exchange Online Protection, Exchange Server 2013_

ユーザーが組織の電子メール ポリシーに準拠できるよう、Exchange トランスポート ルールを使用して、特定の単語またはパターンが含まれている電子メールのルーティング方法を決定できます。単語や語句のリストが短い場合は、Exchange 管理センター を使用できます。リストがより長い場合は、Exchange モジュールを使用して Windows PowerShell でテキスト ファイルからリストを読み取ることもできます。

  - 例 1: 不適切な単語の短いリストを使用する場合

  - 例 2: 不適切な単語の長いリストを使用する場合

データ損失防止 (DLP) をご使用の組織は、機密情報を含む電子メールの識別とルーティングのための追加のオプションについて、「[データ損失防止](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)」を参照してください。

## 例 1: 不適切な単語の短いリストを使用する場合

単語または語句のリストが短い場合は、Exchange 管理センター を使用してルールを作成できます。たとえば、不適切な単語が含まれていたり、会社名、内部的な頭字語、製品名にスペル ミスがあったりする電子メールを誰も送信できないようにするには、メッセージをブロックして送信者に通知するルールを作成できます。単語、語句、およびパターンが、大文字小文字を区別しないことに注意してください。

次の例では、一般的なタイプミスがあるメッセージをブロックします。

![テキスト パターンに基づくメッセージのブロックを示すルール](images/Dn951131.a8489cbb-be59-4890-ae30-1431703eeb88(EXCHG.150).png "テキスト パターンに基づくメッセージのブロックを示すルール")

## 例 2: 不適切な単語の長いリストを使用する場合

単語、語句、パターンのリストが長い場合は、単語、語句、パターンを 1 行に 1 つずつ記載したテキスト ファイルを使用できます。Exchange モジュールを使用して Windows PowerShell でキーワードのリストを変数に読み込み、トランスポート ルールを作成して、キーワードが入った変数をトランスポート ルールの条件に割り当てます。たとえば、次のスクリプトは misspelled\_companyname.txt という名前のファイルに記されたスペル ミスのリストを使用します。

    $keywords=Import-Content  .\misspelled_companyname.txt
    New-TransportRule -Name "Block messages with unacceptable words" -SubjectOrBodyContainsWords $keywords -SentToScope "NotInOrganization" -RejectMessageReasonText "Do not use internal acronyms, product names, or misspellings in external communications."

## テキスト ファイルにおける語句とパターンの使用

テキスト ファイルにはパターンの正規表現を含めることができます。これらの式では、大文字と小文字は区別されません。一般的な正規表現には、次のものが含まれます。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>式</strong></p></td>
<td><p><strong>一致</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>.</strong></p></td>
<td><p>任意の 1 文字</p></td>
</tr>
<tr class="odd">
<td><p><strong>*</strong></p></td>
<td><p>任意の追加文字</p></td>
</tr>
<tr class="even">
<td><p><strong>\d</strong></p></td>
<td><p>任意の 10 進数字</p></td>
</tr>
<tr class="odd">
<td><p>[<em>文字グループ</em>]</p></td>
<td><p><em>文字グループ</em>に含まれる任意の 1 文字。</p></td>
</tr>
</tbody>
</table>


たとえば、このテキスト ファイルには Microsoft の一般的なスペルミスが含まれています。

    [mn]sft
    [mn]icrosft
    [mn]icro soft
    [mn].crosoft

正規表現を使用してパターンを指定する方法については、「[正規表現言語 - クイック リファレンス](https://go.microsoft.com/fwlink/p/?linkid=532394)」を参照してください。

