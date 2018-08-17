﻿---
title: 'TNEF 変換オプション: Exchange 2013 Help'
TOCTitle: TNEF 変換オプション
ms:assetid: 989a62fc-4bc1-448f-90c8-7c7b56fe1084
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb310786(v=EXCHG.150)
ms:contentKeyID: 52057468
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# TNEF 変換オプション

 

_**適用先:** Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

Exchange 組織から外部に送信されるメッセージでは、トランスポート ニュートラル カプセル化形式 (TNEF) を維持するか削除するかを指定できます。TNEF は、Outlook リッチ テキスト形式または Exchange リッチ テキスト形式とも呼ばれ、MAPI メッセージのプロパティをカプセル化する Microsoft 固有の形式です。MicrosoftOutlook のすべてのバージョンは、TNEF を完全に理解できます。Outlook Web App は TNEF を MAPI に変換し、書式設定されたメッセージを表示します。ただし、TNEF を認識できない他の電子メール クライアントでは、通常、TNEF 形式のメッセージは、Winmail.dat または Win.dat という添付ファイルを持つテキスト形式のメッセージとして表示されます。

**目次**

リモート ドメインの TNEF 変換オプション

メール ユーザーおよびメール連絡先の TNEF 変換オプション

Outlook の TNEF 変換オプション

TNEF 変換オプションの優先順位

## リモート ドメインの TNEF 変換オプション

リモート ドメインの TNEF 変換オプションを構成する場合、これらの TNEF 変換オプションが、そのドメインに送信されるすべてのメッセージに適用されます。

  - Exchange Online 専用の場合は、Exchange 管理センター (EAC) を使用してリモート ドメインの TNEF 変換オプションを設定します: <strong>メール フロー</strong> \> <strong>リモート ドメイン</strong> \> <strong>編集</strong> (![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン")) \> <strong>Exchange リッチ テキスト形式を使用する</strong>。

  - Exchange Online および Exchange 2013 の場合は、**Set-RemoteDomain** コマンドレットで *TnefEnabled* パラメーターを使用してリモート ドメインの TNEF 変換オプションを設定します。

組織内のリモート ドメインには、TNEF 変換用の次の構成オプションがあります。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>設定</th>
<th>EAC</th>
<th>シェル</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>リモート ドメインに送信されるすべてのメッセージで TNEF を使用します。</p></td>
<td><p><strong>[常に]</strong></p></td>
<td><p><code>$true</code></p></td>
</tr>
<tr class="even">
<td><p>リモート ドメインに送信されるメッセージでは TNEF を使用しません。</p></td>
<td><p><strong>[使用しない]</strong></p></td>
<td><p><code>$false</code></p></td>
</tr>
<tr class="odd">
<td><p>TNEF メッセージは、リモート ドメインの受信者に対して個別に許可または禁止されません。リモート ドメインの受信者に TNEF メッセージが送信されるかどうかは、メール連絡先またはメール ユーザーに関する特定の設定、または Outlook で送信者が指定した設定によって決まります。これは既定の値です。</p></td>
<td><p><strong>[ユーザーの設定に従う]</strong></p></td>
<td><p><code>$null</code> (空白)</p></td>
</tr>
</tbody>
</table>


リモート ドメインの詳細については、「[リモート ドメイン](remote-domains-exchange-2013-help.md)」または「[Exchange Online のリモート ドメイン](https://technet.microsoft.com/ja-jp/library/jj966211\(v=exchg.150\))」を参照してください。

ページのトップへ

## メール ユーザーおよびメール連絡先の TNEF 変換オプション

メール連絡先またはメール ユーザーの TNEF 変換オプションを構成する場合、これらの TNEF 変換オプションが、その特定の受信者に送信されるすべてのメッセージに適用されます。**Set-MailUser** および **Set-MailContact** コマンドレットの *UseMapiRichTextFormat* パラメーターを使用して、メール ユーザーおよびメール連絡先の TNEF 変換オプションを構成することができます。

組織内のメール ユーザーとメール連絡先には、TNEF 変換用の次の構成オプションがあります。

  - <strong>常に</strong>   受信者に送信されたすべてのメッセージで TNEF が使用されます。*UseMapiRichTextFormat* パラメーターの対応する値は、`Always` です。

  - <strong>使用しない</strong>   受信者に送信されたメッセージには TNEF は使用されません。*UseMapiRichTextFormat* パラメーターの対応する値は、`Never` です。

  - <strong>既定の設定を使用する</strong>   TNEF メッセージは、メール ユーザーまたはメール連絡先に対して個別に許可または禁止されません。受信者に TNEF メッセージが送信されるかどうかは、対応するリモート ドメインに関する特定の設定、または Outlook で送信者が指定した設定によって決まります。*UseMapiRichTextFormat* パラメーターの対応する値は、`UseDefaultSettings` です。これは既定の設定です。

ページのトップへ

## Outlook の TNEF 変換オプション

送信者は、Exchange 組織外のすべての受信者に送信される TNEF メッセージについて、既定の TNEF メッセージ変換オプションを制御できます。これらのオプションは、*インターネット メッセージ形式*オプションと呼ばれます。これらはリモート受信者にのみ適用され、Exchange 組織の受信者には適用されません。


> [!NOTE]
> 次のオプションは、Outlook リッチ テキストを含むメッセージが外部受信者に送信される場合の処理方法を定義します。使用しているメッセージ形式が HTML またはテキストの場合、これらの設定は適用されません。



Outlook には次の TNEF 変換オプションがあります。

  - <strong>HTML 形式に変換</strong>   これが既定のオプションです。リモート受信者に送信されるすべての TNEF メッセージが HTML に変換されます。メッセージの書式設定は元のメッセージとよく似ています。MIME でエンコードされた HTML メッセージは、すべてではありませんが多くの電子メール クライアントによってサポートされています。

  - <strong>テキスト形式に変換</strong>   リモート受信者に送信されるすべての TNEF メッセージがテキスト形式に変換されます。メッセージの書式設定はすべて失われます。

  - <strong>Outlook リッチ テキスト形式で送信</strong>   リモート受信者に送信されるすべての TNEF メッセージが TNEF メッセージとして維持されます。

これらのオプションは Outlook の次の場所で構成できます。

  - **Outlook 2010 または Outlook 2013** <strong>ファイル</strong> \> <strong>オプション</strong> \> <strong>メール</strong> \> <strong>メッセージ形式</strong>。

  - **Outlook 2007** <strong>ツール</strong> \> <strong>オプション</strong> \> <strong>メール形式</strong> \> <strong>インターネット メール形式</strong>。

送信者は、Exchange 組織外の特定の受信者に送信される TNEF メッセージについて、既定の TNEF メッセージ変換オプションも制御できます。これらのオプションは*インターネット受信者メッセージ形式*オプションと呼ばれます。これらは連絡先フォルダーに保存されているリモート受信者にのみ適用され、Exchange 組織の受信者には適用されません。連絡先フォルダー内のリモート受信者に対して次の TNEF 変換オプションがあります。

  - <strong>最適な送信形式を自動的に選択する</strong>   これが既定の設定です。この設定を選択すると、Outlook では既定のインターネット メール形式で指定されている TNEF 変換オプションが使用されます。設定可能な値は、<strong>HTML 形式に変換</strong>、<strong>テキスト形式に変換</strong>、<strong>Outlook リッチ テキスト形式で送信</strong> のいずれかです。したがって、TNEF メッセージは TNEF として保持されることも、HTML に変換されることも、あるいはテキスト形式に変換されることもあります。TNEF メッセージとして保持したい受信者については、必ずこの設定を <strong>最適な送信形式を自動的に選択する</strong> から <strong>Outlook リッチ テキスト形式で送信</strong> に変更してください。

  - <strong>テキスト形式で送信</strong>   受信者に送信されるすべての TNEF メッセージがテキスト形式に変換されます。メッセージの書式設定はすべて失われます。

  - <strong>Outlook リッチ テキスト形式で送信</strong>   リモート受信者に送信されるすべての TNEF メッセージが TNEF メッセージとして維持されます。

これらの連絡先のオプションは Outlook の次の場所で構成できます。

  - **Outlook 2010 または Outlook 2013**   連絡先カードを開いて電子メール アドレスをダブルクリックし、<strong>このユーザーと連絡をとるためのその他のオプションを表示します</strong> アイコンをクリックして <strong>Outlook のプロパティ</strong> を選択します。<strong>電子メールのプロパティ</strong> ダイアログ ボックスで <strong>インターネット メール形式</strong> を選択します。

  - **Outlook 2007**   連絡先カードを開いて <strong>電子メール</strong> フィールドをダブルクリックし、<strong>インターネット メール形式</strong> を選択します。

ページのトップへ

## TNEF 変換オプションの優先順位

Exchange では、Exchange 組織外の受信者への送信メッセージに適用される TNEF 変換オプションは、次に示す優先順位に従って決まります。

1.  リモート ドメイン設定

2.  メール ユーザーまたはメール連絡先の設定

3.  Outlook の設定

このリストでは、優先順位が高い順に上から下へ並べられています。リモート ドメインの TNEF 設定は、メール ユーザー、メール連絡先、または Outlook の TNEF 設定よりも優先されます。たとえば、Outlook でリッチ テキスト メッセージを送信するとします。しかし、受信者のドメインでは、リモート ドメインの個別の設定で TNEF 形式のメッセージが禁止されています。この場合、受信者が受け取るメッセージは TNEF ではなく、テキストか HTML です。

また、Exchange は、STNEF (Summary Transport Neutral Encoding Format) メッセージを外部受信者に送信しません。Exchange 組織外の受信者に送信できるのは、TNEF メッセージだけです。

ページのトップへ

