---
title: '添付ファイル ブロックの一般的なシナリオ: Exchange Online Help'
TOCTitle: 添付ファイル ブロックの一般的なシナリオ
ms:assetid: 5c576439-d55b-4c7f-90ed-a7f72cbb16c2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn950026(v=EXCHG.150)
ms:contentKeyID: 65207680
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 添付ファイル ブロックの一般的なシナリオ

 

_**適用先:** Exchange Online, Exchange Online Protection, Exchange Server 2013_

組織では、法的またはコンプライアンス要件を満たすために、または特定のビジネス ニーズを実装するために、特定の種類のメッセージのブロックまたは拒否が必要になることがあります。以下に、すべての添付ファイルをブロックするために、Exchange でトランスポート ルールを使用してセットアップできる一般的なシナリオの例を示します。

  -  例 1: 添付ファイル付きのメッセージをブロックして、送信者に通知する

  -  例 2: 受信メッセージをブロックした場合に目的の受信者に通知する

  -  例 3: 通知の件名を変更する

  -  例 4: 時間制限付きのルールを適用する

特定の添付ファイルをブロックする方法を示す追加の例を調べるには、以下を参照してください。

  - [トランスポート ルールを使用してメッセージの添付を検査する](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md) (Exchange Server 2013)

  - [Office 365 で、メール フロー ルールを使用してメッセージの添付ファイルを検査する](https://technet.microsoft.com/ja-jp/library/jj919236\(v=exchg.150\)) (Exchange Online, Exchange Online Protection)

マルウェア フィルターには、一般的な添付ファイルの種類フィルターが含まれます。Exchange 管理センター (EAC) で <strong>保護</strong> に移動し、次に <strong>新規作成</strong> (![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン")) をクリックしてフィルターを追加します。Exchange Online ポータルで <strong>保護</strong> を参照し、<strong>マルウェア フィルター</strong> を選択します。

特定のメッセージの種類をブロックする以下のいずれかのシナリオの実装を開始するには、次のようにします。

1.  Exchange 管理センター にサインインします。

2.  <strong>メール フロー</strong> \> <strong>ルール</strong> に移動します。

3.  <strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン")</strong> (新規作成) を選択し、<strong>新しいルールを作成する</strong> を選択します。

4.  <strong>名前</strong> ボックスで、ルールの名前を指定して <strong>その他のオプション</strong> をクリックします。

5.  必要な条件とアクションを選択します。

**メモ**:EAC で入力できる添付ファイルの最小サイズは 1 キロバイトです。この値でほとんどの添付ファイルを検出できるはずです。しかし、サイズを問わずすべての添付ファイルを検出しようとしている場合は、EAC でルールを作成した後に、PowerShell を使用して添付ファイルのサイズを 1 バイトに調整する必要があります。オンプレミスの Exchange 組織で Exchange 管理シェル を開く方法については、「[シェルを開く](https://technet.microsoft.com/ja-jp/library/dd638134\(v=exchg.150\))」を参照してください。 Windows PowerShell を使って Exchange Online に接続する方法については、「[Exchange Online PowerShell への接続](https://go.microsoft.com/fwlink/p/?linkid=396554)」を参照してください。 Windows PowerShell を使って Exchange Online Protection に接続する方法については、「[Exchange Online Protection の PowerShell への接続](https://go.microsoft.com/fwlink/p/?linkid=627290)」を参照してください。

*\<Rule Name\>* を既存のルールの名前と交換し、以下のコマンドを実行して添付ファイルのサイズを 1 バイトに設定します。

    Set-TransportRule -Identity "<Rule Name>" -AttachmentSizeOver 1B

添付ファイルのサイズを 1 バイトに調整し終えると、EAC ではルールの値として **0.00 KB** が表示されます。

## 例 1: 添付ファイル付きのメッセージをブロックして、送信者に通知する

組織内のユーザーに添付ファイルの送受信を禁じるには、添付ファイル付きのすべてのメッセージをブロックするトランスポート ルールをセットアップできます。

この例では、組織が送受信する添付ファイル付きのすべてのメッセージがブロックされます。

![すべての添付ファイルをブロックするルール](images/Dn950026.38094183-166f-4ba5-a9cf-242e7d0f4e04(EXCHG.150).png "すべての添付ファイルをブロックするルール")

メッセージをブロックするだけでよければ、このルールに一致した時点でルール処理を停止できます。ルールのダイアログ ボックスを下にスクロールして、<strong>これ以上の処理を中止する</strong> チェック ボックスをオンにします。

## 例 2: 受信メッセージをブロックした場合に目的の受信者に通知する

メッセージを拒否するものの、目的の受信者にそのことを知らせるには、<strong>受信者にメッセージを通知する</strong> アクションを使用できます。

通知メッセージにプレース ホルダーを含めて、元のメッセージに関する情報をそこに含めることができます。プレース ホルダーは 2 つのパーセント記号 (%%) で囲む必要があります。通知メッセージが送信されるとき、プレース ホルダーは元のメッセージの情報に置き換えられます。メッセージの中では、\<br\>、\<b\>、\<i\>、および \<img\> などの基本的な HTML も使用できます。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>情報の種類</strong></p></td>
<td><p><strong>プレースホルダー</strong></p></td>
</tr>
<tr class="even">
<td><p>メッセージの送信者。</p></td>
<td><p>%%From%%</p></td>
</tr>
<tr class="odd">
<td><p>[宛先] 行に列挙された受信者。</p></td>
<td><p>%%To%%</p></td>
</tr>
<tr class="even">
<td><p>[CC] 行に列挙された受信者。</p></td>
<td><p>%%Cc%%</p></td>
</tr>
<tr class="odd">
<td><p>元のメッセージの件名</p></td>
<td><p>%%Subject%%</p></td>
</tr>
<tr class="even">
<td><p>元のメッセージのヘッダー。 これは、元のメッセージに対して生成される配信状態通知 (DSN) 内のヘッダーの一覧に似ています。</p></td>
<td><p>%%Headers%%</p></td>
</tr>
<tr class="odd">
<td><p>元のメッセージが送信された日付。</p></td>
<td><p>%%MessageDate%%</p></td>
</tr>
</tbody>
</table>


この例では、組織内のユーザー宛に送信された添付ファイル付きのメッセージはすべてブロックされ、受信者は通知を受け取ります。

![受信メッセージがブロックされるときに受信者に通知するルール](images/Dn950026.f9a14733-d68a-4528-a736-206325881c47(EXCHG.150).png "受信メッセージがブロックされるときに受信者に通知するルール")

## 例 3: 通知の件名を変更する

受信者に通知が送信されるときの件名は、元のメッセージの件名です。受信者に分かりやすいように件名を変更するには、2 つのトランスポート ルールを使用する必要があります。

  - 最初のルールでは、添付ファイル付きのすべてのメッセージの件名の先頭に「配信不能」という単語を追加します。

  - 2 番目のルールではメッセージをブロックし、元のメッセージの新しい件名を使用して送信者に通知メッセージを送信します。


> [!IMPORTANT]
> 2 つのルールの条件は同一でなければなりません。ルールは順番に処理されます。したがって、最初のルールが「配信不能」という単語を追加し、2 番目のルールがメッセージをブロックして、受信者に通知を行います。



件名に「配信不能」と追加する場合の最初のルールの様子を以下に示します。

![添付ファイル付きメッセージに \[配信不能\] と追加するルール](images/Dn950026.2552b0bd-c69d-48b4-9e69-267fcaf20e70(EXCHG.150).png "添付ファイル付きメッセージに [配信不能] と追加するルール")

2 番目のルールは、ブロックと通知を行います (例 2 と同じルール)。

![受信メッセージがブロックされるときに受信者に通知するルール](images/Dn950026.f9a14733-d68a-4528-a736-206325881c47(EXCHG.150).png "受信メッセージがブロックされるときに受信者に通知するルール")

## 例 4: 時間制限付きのルールを適用する

マルウェアの集団感染が発生した場合は、時間制限付きのルールを適用して、一時的に添付ファイルをブロックできます。たとえば、次のルールには、開始と停止の両方の日時が指定されています。

![制限時間を示すルール](images/Dn950026.bdc8c4d8-72fa-4c5b-97f2-5fe76d50e643(EXCHG.150).png "制限時間を示すルール")

## 関連項目


[Exchange Online のメール フロー ルール (トランスポート ルール)](https://technet.microsoft.com/ja-jp/library/jj919238\(v=exchg.150\))  


[メール フローやトランスポート ルール](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)  
[Exchange Online Protection のメール フロー ルール (トランスポート ルール)](https://technet.microsoft.com/ja-jp/library/dn271424\(v=exchg.150\))

