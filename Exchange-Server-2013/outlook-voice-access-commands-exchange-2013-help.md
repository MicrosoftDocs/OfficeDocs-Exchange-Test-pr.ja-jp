---
title: 'Outlook Voice Access コマンド: Exchange Online Help'
TOCTitle: Outlook Voice Access コマンド
ms:assetid: 8fe9247c-695f-47d8-827e-c79d0426854b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn205137(v=EXCHG.150)
ms:contentKeyID: 54651683
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Voice Access コマンド

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

Outlook Voice Access では、ユニファイド メッセージング (UM) の有効なユーザーが、アナログ、デジタル、または携帯電話からメールボックスにアクセスできます。UM が有効なユーザーは、Outlook Voice Access のメニュー システムを使って、電子メールを読む、音声メッセージを聞く、Outlook 予定表を操作する、個人用連絡先にアクセスする、パーソナル オプションを管理する (Outlook Voice Access PIN の構成やボイス メール メッセージの録音など) ことができます。ここでは、Outlook Voice Access コマンドの一覧と、Outlook Voice Access 番号を呼び出してメールボックスにアクセスする場合のコマンドの使用方法を示します。

## Outlook Voice Access のユーザーインターフェイス

Outlook Voice Access は、2 つのユーザー インターフェイスから構成されています。電話のキーパッドを使用する電話ユーザー インターフェイス (TUI) と、音声コマンドを賞する音声ユーザー インターフェイス (VUI) です。Outlook Voice Access は、外部または内部の電話からボイス メール システムにアクセスし、メールボックス内の個人用の電子メール、音声メッセージ、連絡先、および予定表情報にアクセスするために使用できます。

## 電子メールとボイス メールのコマンド リファレンス

Outlook Voice Access ユーザーが Outlook Voice Access 番号に電話をかけると、メールボックスにアクセスして電子メールとボイス メールを管理できるメニュー オプションが示されます。次の表に、電子メールとボイス メールの管理に使用できるコマンドの一覧を示します。

### 電子メールとボイス メールのコマンド

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>音声コマンド</th>
<th>タッチトーン コマンド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&quot;再生&quot;</p></td>
<td><p></p></td>
<td><p>現在の電子メール メッセージまたはボイス メール メッセージを再生します。</p></td>
</tr>
<tr class="even">
<td><p>&quot;次&quot;</p></td>
<td><p>#</p></td>
<td><p>次の電子メール メッセージまたはボイス メール メッセージを読みます。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;次の未読&quot;</p></td>
<td><p>00 の後に ##</p></td>
<td><p>次の未読の電子メール メッセージを読みます。電子メールにのみ、使用できます。</p></td>
</tr>
<tr class="even">
<td><p>&quot;削除&quot;</p></td>
<td><p>7</p></td>
<td><p>現在の電子メール メッセージまたはボイス メール メッセージを削除します。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;返信&quot;</p></td>
<td><p>8</p></td>
<td><p>現在の電子メール メッセージまたはボイス メール メッセージを送信したユーザーに返信します。</p></td>
</tr>
<tr class="even">
<td><p>&quot;全員へ返信&quot;</p></td>
<td><p>00 の後に 88</p></td>
<td><p>現在の電子メール メッセージの全ユーザーに返信します。ボイス メール メッセージで利用できるオプションではありません。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;未読にする&quot;</p></td>
<td><p>9</p></td>
<td><p>電子メール メッセージを未読にします。</p></td>
</tr>
<tr class="even">
<td><p>&quot;終了&quot;</p></td>
<td><p>33</p></td>
<td><p>読むのをやめ、現在の電子メール メッセージまたはボイス メール メッセージの最後に移動します。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;その他のオプション&quot;</p></td>
<td><p>00</p></td>
<td><p>[その他のオプション] メニューを開きます。</p></td>
</tr>
<tr class="even">
<td><p>&quot;前の&quot;</p></td>
<td><p>00 の後に 11</p></td>
<td><p>前の電子メール メッセージまたはボイス メール メッセージを読みます。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;ヘッダーを読む&quot;</p></td>
<td><p></p></td>
<td><p>電子メール メッセージまたはボイス メール メッセージのヘッダーを読みます。</p></td>
</tr>
<tr class="even">
<td><p>&quot;送信者に電話&quot;</p></td>
<td><p>00 の後に 2</p></td>
<td><p>現在の電子メール メッセージまたはボイス メール メッセージを送信したユーザーに電話をかけます。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;転送する&quot;</p></td>
<td><p>00 の後に 6</p></td>
<td><p>現在の電子メール メッセージまたはボイス メール メッセージを、他の電子メール受信者またはグループに転送します。</p></td>
</tr>
<tr class="even">
<td><p>&quot;フラグの設定&quot;</p></td>
<td><p>00 の後に 44</p></td>
<td><p>現在の電子メール メッセージまたはボイス メール メッセージにフラグを設定します。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;名前で検索&quot;</p></td>
<td><p></p></td>
<td><p>ユーザーの名前を使用して、そのユーザーのメールボックスにある電子メール メッセージまたはボイス メール メッセージを検索します。</p></td>
</tr>
<tr class="even">
<td><p>&quot;会話を削除&quot;</p></td>
<td><p>00 の後に 77</p></td>
<td><p>電子メールの会話に関連付けられているすべての電子メール メッセージを削除します。電子メールにのみ、使用できます。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;会話を隠す&quot;</p></td>
<td><p>00 の後に 99</p></td>
<td><p>同じ電子メールの会話内に含まれている追加の電子メール メッセージを隠します。電子メールにのみ、使用できます。</p></td>
</tr>
<tr class="even">
<td><p>&quot;エンベロープ情報&quot;</p></td>
<td><p>00 の後に 5</p></td>
<td><p>電子メール メッセージまたはボイス メール メッセージのエンベロープ情報を読みます。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;言語選択&quot;</p></td>
<td><p>00 の後に 55</p></td>
<td><p>電子メール メッセージまたはボイス メール メッセージを読み上げる言語を選択できます。</p></td>
</tr>
<tr class="even">
<td><p>&quot;巻戻し&quot; または &quot;リピート&quot;</p></td>
<td><p>1</p></td>
<td><p>現在の電子メール メッセージまたはボイス メール メッセージを巻き戻すか、繰り返します。メッセージの再生中のみ使用できます。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;一時停止&quot;</p></td>
<td><p>2</p></td>
<td><p>現在の電子メール メッセージまたはボイス メール メッセージを一時停止します。メッセージの再生中のみ使用できます。</p></td>
</tr>
<tr class="even">
<td><p>&quot;早送り&quot;</p></td>
<td><p>3</p></td>
<td><p>現在の電子メール メッセージまたはボイス メール メッセージを早送りします。メッセージの再生中のみ使用できます。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;スピード ダウン&quot;</p></td>
<td><p>4</p></td>
<td><p>現在の電子メール メッセージを読むスピード、またはボイス メール メッセージを再生するスピードを落とします。メッセージの再生中のみ使用できます。</p></td>
</tr>
<tr class="even">
<td><p>&quot;スピード アップ&quot;</p></td>
<td><p>6</p></td>
<td><p>現在の電子メール メッセージを読むスピード、またはボイス メール メッセージを再生するスピードを速くします。メッセージの再生中のみ使用できます。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;前の&quot;</p></td>
<td><p>11</p></td>
<td><p>前の電子メールを最初から読みます。電子メールにのみ、使用できます。</p></td>
</tr>
<tr class="even">
<td><p>&quot;リプレイ&quot;</p></td>
<td><p>00 の後に 1</p></td>
<td><p>現在の電子メール メッセージまたはボイス メール メッセージをもう一度再生します。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;繰り返し&quot;</p></td>
<td><p>0</p></td>
<td><p>現在のメニュー オプションを繰り返します。</p></td>
</tr>
<tr class="even">
<td><p>&quot;メイン メニュー&quot;</p></td>
<td><p>*</p></td>
<td><p>メイン メニューに戻ります。</p></td>
</tr>
</tbody>
</table>



> [!IMPORTANT]
> Outlook Voice Access を使用して電子メール メッセージを削除した後でそのメッセージにアクセスする必要がある場合は、Outlook Web App または Outlook を使用して、必要な電子メール メッセージを削除済みアイテム フォルダーから適切なフォルダーに戻すことができます。Outlook Voice Access を使用して削除済みアイテム フォルダーにアクセスすることはできません。



## 予定表オプションのコマンド リファレンス

Outlook Voice Access ユーザーが Outlook Voice Access 番号に電話をかけると、メールボックスにアクセスして予定表を管理できるメニュー オプションが示されます。次の表に、予定表の管理に使用できるコマンドの一覧を示します。

### 予定表のコマンド

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>音声コマンド</th>
<th>タッチトーン コマンド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&quot;次&quot;</p></td>
<td><p>#</p></td>
<td><p>予定表にある次の予定を読みます。</p></td>
</tr>
<tr class="even">
<td><p>&quot;翌日&quot;</p></td>
<td><p>##</p></td>
<td><p>予定表にある翌日の予定を開いて読みます。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;繰り返し&quot;</p></td>
<td><p>0</p></td>
<td><p>使用できるメニュー オプションを繰り返します。あるいは、VUI を使用している場合、予定表の予定が再度読み出されます。</p></td>
</tr>
<tr class="even">
<td><p>&quot;その他のオプション&quot;</p></td>
<td><p>00</p></td>
<td><p>予定表オプションのその他のメニューを再生します。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;繰り返し&quot;</p></td>
<td><p>1</p></td>
<td><p>予定表にある予定をもう一度読みます。</p></td>
</tr>
<tr class="even">
<td><p>&quot;前の会議&quot;</p></td>
<td><p>00 の後に 11</p></td>
<td><p>予定されている前の会議を開きます。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;会議場所に電話&quot;</p></td>
<td><p>2</p></td>
<td><p>会議場所の一覧に記載されている電話番号に電話をかけます。</p></td>
</tr>
<tr class="even">
<td><p>&quot;開催者に電話&quot;</p></td>
<td><p>00 の後に 22</p></td>
<td><p>会議の開催者の一覧に記載されている電話番号に電話をかけます。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;遅れます&quot;</p></td>
<td><p>3</p></td>
<td><p>会議の出席者全員に &quot;遅れます&quot; というメッセージを送信します。</p></td>
</tr>
<tr class="even">
<td><p>&quot;承諾&quot; または &quot;仮承諾&quot;</p></td>
<td><p>4</p></td>
<td><p>会議出席依頼を承諾するか、または仮承諾します。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;会議の詳細&quot;</p></td>
<td><p>5</p></td>
<td><p>現在読まれている会議の詳細を読み上げるか、再生します。</p></td>
</tr>
<tr class="even">
<td><p>&quot;出席の詳細&quot;</p></td>
<td><p>00 の後に 55</p></td>
<td><p>予定されている会議の詳細を読み上げるか、再生します。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;転送する&quot;</p></td>
<td><p>00 の後に 6</p></td>
<td><p>会議出席依頼を他のユーザーに転送します。</p></td>
</tr>
<tr class="even">
<td><p>&quot;辞退&quot; または &quot;取り消す&quot;</p></td>
<td><p>7</p></td>
<td><p>会議出席依頼を辞退するか、取り消します。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;予定の消去&quot;</p></td>
<td><p>00 の後に 77</p></td>
<td><p>該当日の特定の時間について、予定表をクリアします。</p></td>
</tr>
<tr class="even">
<td><p>&quot;返信&quot;</p></td>
<td><p>00 の後に 8</p></td>
<td><p>会議開催者に返信します。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;全員へ返信&quot;</p></td>
<td><p>00 の後に 88</p></td>
<td><p>会議の出席者全員に返信します。</p></td>
</tr>
<tr class="even">
<td><p>&quot;メニューのリピート&quot;</p></td>
<td><p>5 の後に 0</p></td>
<td><p>使用できるメニュー オプションを繰り返します。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;巻戻し&quot;</p></td>
<td><p>5 の後に 1</p></td>
<td><p>会議の詳細を巻き戻します。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>5 の後に 11</p></td>
<td><p>会議の詳細の先頭に戻ります。</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>5 の後に 2</p></td>
<td><p>会議の詳細の再生を一時停止し、再開します。</p></td>
</tr>
<tr class="even">
<td><p>&quot;早送り&quot;</p></td>
<td><p>5 の後に 3</p></td>
<td><p>会議の詳細内で先に進みます。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;終了&quot;</p></td>
<td><p>5 の後に 33</p></td>
<td><p>会議の詳細の最後にスキップします。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>5 の後に 4</p></td>
<td><p>会議の詳細を再生するスピードまたは読み上げるスピードを下げます。</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>5 の後に 55</p></td>
<td><p>会議の詳細を読み上げる言語を選択します。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>5 の後に 6</p></td>
<td><p>会議の詳細を再生するスピードまたは読み上げるスピードを上げます。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;メイン メニュー&quot;</p></td>
<td><p>*</p></td>
<td><p>メイン メニューに戻ります。</p></td>
</tr>
</tbody>
</table>


## 連絡先の検索のコマンド リファレンス

Outlook Voice Access ユーザーが Outlook Voice Access 番号に電話をかけると、メールボックスにアクセスしたり、個人オプションを変更したり、連絡先に電話をかけたりメッセージを送信したりするためのメニュー オプションが示されます。自分の音声を使用すること (既定の設定) を選択し、連絡先のメニュー オプションを選択すると、ボイル メール システムから、電話のキーパッドを使って連絡先のオプションを検索するように指示されます。電話のキーパッドを使って、ディレクトリ内のユーザーまたは連絡先を検索することもできます。次の表に、連絡先の管理やユーザーの検索に使用できるコマンドの一覧を示します。

### 連絡先コマンド

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>音声コマンド</th>
<th>タッチトーン コマンド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&quot;ディレクトリ&quot;</p></td>
<td><p>00</p></td>
<td><p>ディレクトリ内でユーザーを検索します。</p></td>
</tr>
<tr class="even">
<td><p>&quot;詳細を再生&quot;</p></td>
<td><p>1</p></td>
<td><p>個人用連絡先としてリストされている電話番号などの、個人用連絡先の詳細を再生します。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;メッセージを送信&quot;</p></td>
<td><p>3</p></td>
<td><p>選択されている個人用連絡先にメッセージを送信します。</p></td>
</tr>
<tr class="even">
<td><p>&quot;別の連絡先を探す&quot;</p></td>
<td><p>4</p></td>
<td><p>別の連絡先を探します。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;携帯に電話&quot;</p></td>
<td><p>2 の後に 1</p></td>
<td><p>個人用連絡先の一覧に記載されている携帯電話番号に電話をかけます。</p></td>
</tr>
<tr class="even">
<td><p>&quot;勤務先に電話&quot;</p></td>
<td><p>2 の後に 2</p></td>
<td><p>個人用連絡先の一覧に記載されている会社やオフィスの番号に電話をかけます。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;自宅に電話&quot;</p></td>
<td><p>2 の後に 3</p></td>
<td><p>個人用連絡先の一覧に記載されている自宅の電話番号に電話をかけます。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>##</p></td>
<td><p>ディレクトリ検索機能を使用している場合は、ディレクトリ内のユーザーの電子メール エイリアスまたは名前を入力します。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;メイン メニュー&quot;</p></td>
<td><p>*</p></td>
<td><p>メイン メニューに戻ります。</p></td>
</tr>
</tbody>
</table>


## 個人オプションのコマンド リファレンス

Outlook Voice Access ユーザーが Outlook Voice Access 番号に電話をかけると、メールボックスにアクセスして、個人オプションを管理できるメニュー オプションが示されます。Outlook Voice Access を使って個人オプションを構成する場合、電話のキーパッドだけを使ってメニューを操作できます。自分の音声を使ったメニューの操作は、個人オプションの構成には使用できません。次の表に、個人オプションの管理に使用できるコマンドの一覧を示します。

### 個人オプションのコマンド

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>音声コマンド</th>
<th>タッチトーン コマンド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>1</p></td>
<td><p>不在時の案内応答のオンとオフを切り替えます。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>2</p></td>
<td><p>個人用のボイス メールまたは不在時のボイス メールによる案内応答を録音します。</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>3</p></td>
<td><p>Outlook Voice Access に使用している PIN を変更します。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>4</p></td>
<td><p>VUI またはタッチトーン インターフェイスを使用して起動します。</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>5</p></td>
<td><p>使用するローカル タイム ゾーンを設定します。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>6</p></td>
<td><p>12 時間制または 24 時間制の時刻形式を選択します。</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>*</p></td>
<td><p>メイン メニューに戻ります。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>0</p></td>
<td><p>使用できるメニュー オプションを繰り返します。</p></td>
</tr>
</tbody>
</table>


## 詳細情報

[Outlook Voice Access の設定](setting-up-outlook-voice-access-exchange-2013-help.md)

[クライアント ボイス メール機能をセットアップする](set-up-client-voice-mail-features-exchange-2013-help.md)

