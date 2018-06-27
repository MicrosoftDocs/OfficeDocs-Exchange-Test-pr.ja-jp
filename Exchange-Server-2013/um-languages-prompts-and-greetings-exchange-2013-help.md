---
title: 'UM 言語、プロンプト、および案内応答: Exchange 2013 Help'
TOCTitle: UM 言語、プロンプト、および案内応答
ms:assetid: d48df962-9669-420b-838f-44bfe1012e2f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124728(v=EXCHG.150)
ms:contentKeyID: 49896496
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM 言語、プロンプト、および案内応答

 

_**適用先:**Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:**2016-12-09_

言語パックをインストールして構成し、ユニファイド メッセージング (UM) 環境で複数の言語をサポートできます。

UM 言語パックを使用すると、発信者と Outlook Voice Access ユーザーは複数の言語でボイス メール システムを操作できます。また、追加の言語をメールボックス サーバーにインストールすると、発信者と Outlook Voice Access ユーザーはその言語で電子メール メッセージを聞いたり、ボイス メール システムを操作したりすることができます。

UM 言語パックに依存する複数の重要なコンポーネントがあります。これらのコンポーネントを使用して、ユーザーと発信者は複数の言語でユニファイド メッセージングを効果的に操作できます。各 UM 言語パックには、音声合成 (TTS) エンジン、録音済みのプロンプト、および特定の言語の自動音声認識 (ASR) およびボイス メール プレビューのサポートが含まれます。ここでは、UM 言語パックや UM 言語パックを使用する UM コンポーネントについて、また UM 言語パックをインストールした後、その言語パックを使用して UM ダイヤル プランと UM 自動応答を構成し、他の言語を使用する方法について説明します。

Exchange ユニファイド メッセージング言語パックは、バージョン、およびプラットフォームに固有です。Exchange Server 2007 以降、UM 言語パックは Exchange 2007 の RTM バージョン、Exchange 2007 SP1、SP2、および SP3、Exchange Server 2010 の RTM バージョン、Exchange 2010 SP1 および SP2、Exchange 2013 と、複数リリースされてきました。これらのバージョンの一部では、32 ビット版と 64 ビット版のダウンロードが存在します。また、他のリリースでは、64 ビット版のダウンロードのみが存在します。

メールボックス サーバーに、正しいバージョンと正しいプラットフォームの UM 言語パックをインストールすることが非常に重要です。Exchange の旧バージョンを実行するメールボックス サーバー、または 32 ビット プラットフォーム用に設計されたメールボックス サーバーに UM 言語パックをインストールしないでください。

**目次**

UM 言語パックの概要

UM 言語コンポーネントと機能

ボイス メールのプレビュー

ユニファイド メッセージング言語

ユニファイド メッセージング言語パック

UM ダイヤル プラン言語

UM 自動応答言語

クライアント言語選択プロセス

## UM 言語パックの概要

ユニファイド メッセージング言語パックにより、メールボックス サーバーは発信者に対して他の言語で話すことができ、発信者が ASR を使用している場合、または音声メッセージが書き換えられるときに、他の言語を認識することができます。UM 言語パックには、以下が含まれています。

  - UM 言語パックの言語による録音済みのプロンプト。たとえば、「トーンの後、メッセージを録音してください。録音が終わったら、電話を切るか、さらにオプションが必要な場合は \# を押してください。」

  - UM 言語パックの言語による文章校正ファイル。ディレクトリ内で特定のユーザーの名前を検索する場合に、メールボックス サーバーによって使用されます。

  - 音声合成 (TTS) 翻訳。発信者はコンテンツ (電子メール、予定表、連絡先情報など) を UM 言語パックの言語で読むことができるようになります。

  - 自動音声認識のサポート。発信者は UM 言語パックの言語で音声ユーザー インターフェイス (VUI) を使用して、やり取りすることができます。

  - ボイス メール プレビューのサポート。ユーザーが、Outlook や Outlook Web App などのサポート対象の電子メール クライアント内から、特定の言語でボイス メール メッセージのトランスクリプトを読むことが可能になります。

UM 言語パックには、録音済みのプロンプト、特定の言語の TTS 変換サポート、場合によっては、ASR のサポートが含まれています。一部の発信者は、異なる言語での応答を希望していたり、複数の言語で電子メールを受信しているため、多言語環境では追加の UM 言語パックをインストールしなければならない場合があります。複数の言語が使用されている電子メール メッセージをメールボックス サーバーで読み上げる機能をサポートするには、読み上げるメッセージの本文に応じて選択する言語を TTS 変換システムに対して指定する必要があるため、複数の UM 言語パックをインストールする必要があります。ユニファイド メッセージング言語パックがインストールされていないと、ユーザーに電子メール メッセージを読み上げるときに、意味不明に聞こえます。適切な言語パックをインストールすると、TTS エンジンは正しい言語を使用して電子メールや予定表アイテムを Outlook Voice Access ユーザーに対して読み上げます。また、ユニファイド メッセージングの言語固有の録音済みプロンプトもユーザーに応答します。場合によっては、ASR もサポートされます。


> [!NOTE]
> TTS エンジンはテキストを音声に変換しますが、音声からテキストへの変換は行いません。UM が有効なユーザーは、音声ファイルが添付された電子メール メッセージを別のユーザーに送信できます。ただし、テキスト ベースの電子メール メッセージを作成し、別のユーザーに送信することはできません。



言語パックをインストールすると、インストール プログラムにより次の操作が実行されます。

1.  UM ダイヤル プランと自動応答の構成に使用される言語プロンプトをコピーする。

2.  Outlook Voice Access ユーザーが自分の受信トレイにアクセスしたときに TTS エンジンを使用して、メッセージを読み上げる。

3.  インストールされた言語について、音声認識が有効な UM ダイヤル プランと自動応答用に ASR を有効にする。

4.  クライアントに対してボイス メール プレビューを他の言語で有効にする。

UM 言語パックを「[Exchange Server 2013 UM Language Packs - 日本語](https://go.microsoft.com/fwlink/p/?linkid=266542)」からダウンロードした後で、**Setup.exe** コマンドを使用するか、*\<UMLanguagePack\>*.exe インストール プログラムを実行して、UM 言語パックを追加することができます。ただし、UM 言語パックを削除するには、Setup.exe コマンドを使用する必要があります。Exchange 管理シェル コマンドレットを実行して、メールボックス サーバーに言語パックを追加したり、削除したりすることはできません。UM 言語パックをインストールする方法の詳細については、「[UM 言語パックをインストールする](install-a-um-language-pack-exchange-2013-help.md)」を参照してください。UM 言語パックを削除する方法の詳細については、「[UM 言語パックの削除](remove-a-um-language-pack-exchange-2013-help.md)」を参照してください。


> [!NOTE]
> 既定では、メールボックス サーバーをインストールすると、U.S. 英語 (en-US) 言語パックがインストールされます。メールボックス サーバーをコンピューターから削除しないと、削除できません。



ページのトップへ

次の表に、現在利用できるユニファイド メッセージング言語パックの一覧を示します。また、各 UM 言語パックのインストール ファイルの名前と UM 言語のカルチャー ID の一覧も示します。

### UM 言語パックのインストール ファイル名およびカルチャー ID

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>言語</th>
<th>国/地域名</th>
<th>カルチャー ID</th>
<th>インストール ファイル名</th>
<th>利用の可否</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>カタルニア語</p></td>
<td><p>スペイン</p></td>
<td><p>ca-ES</p></td>
<td><p>UMLanguagePack. ca-ES</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
<tr class="even">
<td><p>中国語 (香港)</p></td>
<td><p>中国</p></td>
<td><p>zh-HK</p></td>
<td><p>UMLanguagePack. zh-HK</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
<tr class="odd">
<td><p>簡体字中国語</p></td>
<td><p>中国</p></td>
<td><p>zh-CHS</p></td>
<td><p>UMLanguagePack.zh-CN</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
<tr class="even">
<td><p>繁体字中国語</p></td>
<td><p>台湾</p></td>
<td><p>zh-TW</p></td>
<td><p>UMLanguagePack.zh-TW</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
<tr class="odd">
<td><p>デンマーク語</p></td>
<td><p>デンマーク</p></td>
<td><p>da-DK</p></td>
<td><p>UMLanguagePack.da-DK</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
<tr class="even">
<td><p>オランダ語</p></td>
<td><p>オランダ</p></td>
<td><p>nl-NL</p></td>
<td><p>UMLanguagePack.nl-NL</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
<tr class="odd">
<td><p>英語</p></td>
<td><p>オーストラリア</p></td>
<td><p>en-AU</p></td>
<td><p>UMLanguagePack.en-AU</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
<tr class="even">
<td><p>英語</p></td>
<td><p>カナダ</p></td>
<td><p>en-CA</p></td>
<td><p>UMLanguagePack. en-CA</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
<tr class="odd">
<td><p>英語</p></td>
<td><p>インド</p></td>
<td><p>en-IN</p></td>
<td><p>UMLanguagePack. en-IN</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
<tr class="even">
<td><p>英語</p></td>
<td><p>英国</p></td>
<td><p>en-GB</p></td>
<td><p>UMLanguagePack.en-GB</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
<tr class="odd">
<td><p>英語</p></td>
<td><p>米国</p></td>
<td><p>en-US</p></td>
<td><p>メールボックス サーバーのインストールに含まれるもの</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
<tr class="even">
<td><p>フィンランド語</p></td>
<td><p>フィンランド</p></td>
<td><p>fi-Fl</p></td>
<td><p>UMLanguagePack.fi-Fl</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
<tr class="odd">
<td><p>フランス語</p></td>
<td><p>カナダ</p></td>
<td><p>fr-CA</p></td>
<td><p>UMLanguagePack.fr-CA</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
<tr class="even">
<td><p>フランス語</p></td>
<td><p>フランス</p></td>
<td><p>fr-FR</p></td>
<td><p>UMLanguagePack.fr-FR</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
<tr class="odd">
<td><p>ドイツ語</p></td>
<td><p>ドイツ</p></td>
<td><p>de-DE</p></td>
<td><p>UMLanguagePack.de-DE</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
<tr class="even">
<td><p>イタリア語</p></td>
<td><p>イタリア</p></td>
<td><p>it-IT</p></td>
<td><p>UMLanguagePack.it-IT</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
<tr class="odd">
<td><p>日本語</p></td>
<td><p>日本</p></td>
<td><p>ja-JP</p></td>
<td><p>UMLanguagePack.ja-JP</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
<tr class="even">
<td><p>韓国</p></td>
<td><p>韓国語</p></td>
<td><p>ko-KR</p></td>
<td><p>UMLanguagePack.ko-KR</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
<tr class="odd">
<td><p>ノルウェー語 (ブークモール)</p></td>
<td><p>ノルウェー</p></td>
<td><p>nb-NO</p></td>
<td><p>UMLanguagePack.nb-NO</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
<tr class="even">
<td><p>ポーランド語</p></td>
<td><p>ポーランド</p></td>
<td><p>pl-PL</p></td>
<td><p>UMLanguagePack.pl-PL</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
<tr class="odd">
<td><p>ポルトガル語</p></td>
<td><p>ブラジル</p></td>
<td><p>pt-BR</p></td>
<td><p>UMLanguagePack.pt-BR</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
<tr class="even">
<td><p>ポルトガル語</p></td>
<td><p>ポルトガル</p></td>
<td><p>pt-PT</p></td>
<td><p>UMLanguagePack.pt-PT</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
<tr class="odd">
<td><p>ロシア語</p></td>
<td><p>ロシア</p></td>
<td><p>ru-RU</p></td>
<td><p>UMLanguagePack. ru-RU</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
<tr class="even">
<td><p>スペイン語</p></td>
<td><p>スペイン</p></td>
<td><p>es-ES</p></td>
<td><p>UMLanguagePack.es-ES</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
<tr class="odd">
<td><p>スペイン語</p></td>
<td><p>メキシコ</p></td>
<td><p>es-MX</p></td>
<td><p>UMLanguagePack.es-MX</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
<tr class="even">
<td><p>スウェーデン語</p></td>
<td><p>スウェーデン</p></td>
<td><p>sv-SE</p></td>
<td><p>UMLanguagePack.sv-SE</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">ダウンロード可能</a></p></td>
</tr>
</tbody>
</table>


ページのトップへ

## UM 言語コンポーネントと機能

ユニファイド メッセージングには、複数の重要なコンポーネントと機能が含まれています。これらのコンポーネントや機能を使用して、ユーザーと発信者は複数言語のボイス メール システムを操作できます。これらのコンポーネントや機能が適切に動作し、発信者が複数言語でシステムを操作できるようにするには、UM 言語パックをメールボックス サーバーに正しくインストールする必要があります。

## 録音済みのプロンプト

メールボックス サーバーの役割は、既定の音声ガイダンス ファイルと共にインストールされます。これらのオーディオ ファイルには、Outlook Voice Access メニュー、ボイス メールの案内応答、および Exchange ユニファイド メッセージングによって使用される番号の録音が含まれます。メールボックス サーバーは、組織内部と外部の両方から電話を掛けてきた人に対してオーディオ ファイルを再生します。多くのオーディオ ファイルは、TUI と音声ユーザー インターフェイス (VUI) を操作するときに必要な情報を電話ユーザー インターフェイス (TUI) と Outlook Voice Access のユーザーに提供する既定のプロンプトです。これらのプロンプトは、\<*Program Files*\>\\Microsoft\\Exchange Server\\V15\\UnifiedMessaging\\Prompts\\\<language\> にあります。発信者がメニューを操作しやすいようにするためにメールボックス サーバーで使用されるプロンプトを置換または変更してはいけません。

追加の UM 言語パックをインストールした場合、その言語の録音済みのプロンプトもインストールされます。UM 言語パックをインストールすると、その言語の録音済みプロンプトを UM ダイヤル プランと自動応答で使用することができます。

## TTS 言語

ユニファイド メッセージングは音声合成 (TTS) エンジンに依存しています。TTS 機能は Microsoft Speech Server サービスにより提供されます。TTS エンジンは、記述されたテキストを読み取り、発信者が聞くことができる可聴出力に変換します。TTS エンジンは、ユーザーのメールボックスにある次のアイテムを読み取り、変換します。

  - 電子メールとボイス メール メッセージの本文、件名、名前

  - 予定表アイテムの本文、件名、場所、名前

  - 個人用連絡先の名前

  - ユーザーの既定のボイス メールの案内応答


> [!NOTE]
> ユーザーが個人用のボイス メール案内応答を録音すると、ボイス メールの案内応答の TTS バージョンは使用されなくなります。



## 自動音声認識

TTS に加え、ASR のサポートもユニファイド メッセージングに含まれています。ASR 機能は Microsoft Speech Server サービスにより提供されます。ASR により、発信者は音声コマンドを使用してメニューを操作し、メッセージ、個人用連絡先、予定表など、各自のメールボックスのアイテムを操作できます。ASR のサポートは、各言語パックに含まれています。

ページのトップへ

## ボイス メールのプレビュー

UM 言語パックは、ボイス メール プレビューのサポートも提供します。ユーザーが、Outlook や Outlook Web App などのサポート対象の電子メール クライアント内からトランスクリプトを読むことで、音声メッセージをすばやくトリアージすることが可能になります。

発信者が、UM が有効なユーザーに音声メッセージを残すと、音声メッセージ ファイルとそのトランスクリプトは、ユーザーのメールボックスに送信された音声メッセージの本文に置かれます。

すべての UM 言語パックが、ダウンロードできるただ 1 つのファイルです。これらの言語パックには、録音済みのプロンプト、文章校正ファイル、音声合成 (TTS) 翻訳、および ASR が含まれています。ただし、ボイス メール プレビューのサポートはすべての言語パックに含まれているわけではありません。

次の UM 言語パックには、すべてのコンポーネントと機能 (ボイス メール プレビューを含む) のサポートが含まれています。

  - 英語 (米国) - (en-US)

  - 英語 (カナダ) (en-CA)

  - フランス語 (フランス) - (fr-FR)

  - イタリア語 - (it-IT)

  - ポーランド語 (pl-PL)

  - ポルトガル語 (ポルトガル) (pt-PT)

  - スペイン語 (スペイン) (es-ES)

既定では、メールボックス サーバーをインストールすると、サポートされた UM 言語パックがインストールされていれば、サーバーは UM が有効なユーザーにボイス メール プレビューを送信します。

ボイス メール プレビュー機能の拡張トランスクリプションをサポートする、ユニファイド メッセージングのボイス メール プレビュー パートナーがいます。これらのパートナーでは、ASR によって作成されたボイス メール トランスクリプションを修正するための人員を雇用しています。各ボイス メール プレビュー パートナーは、ユニファイド メッセージングと相互運用するための認定が必要となる一連の要件を満たしている必要があります。

ユーザーに送信されたボイス メール プレビューが十分に正確ではないことが判明した場合は、「[ユニファイド メッセージング向けの Microsoft Pinpoint](https://go.microsoft.com/fwlink/p/?linkid=261951)」ページに記載された認定ボイス メール プレビュー パートナーのいずれかに連絡し、追加料金をお支払いの上、認定ボイス メール プレビュー パートナーと契約してください。

UM 言語パックは、[Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/p/?linkid=266542)からダウンロードできます。詳細については、「[UM 言語パックをインストールする](install-a-um-language-pack-exchange-2013-help.md)」を参照してください。

## ユニファイド メッセージング言語

発信者がユニファイド メッセージングの多言語機能を使用できるためには、まず UM 言語パックをインストールする必要があります。次に、他の UM コンポーネントを構成します。

  - 組織のメールボックス サーバーに UM 言語パックをインストールします。

  - 必要な場合は、UM ダイヤル プランの既定の言語を構成します。これにより、UM ダイヤル プランに関連付けられた Outlook Voice Access ユーザーは、自分のメールボックスにアクセスするときに新しい言語を使用できるようになります。ただし、その場合にも、ユーザーは Outlook Web App のオプションで言語設定を構成できます。

  - 自動応答に対して複数の言語を有効にする必要がある場合は、UM 自動応答に対する言語設定を構成します。既定では、UM 自動応答は UM ダイヤル プラン言語を使用します。ただし、この設定を変更して、権限のない発信者が組織に接続し、UM 自動応答で指定した言語の自動応答メニューを操作できるようにすることができます。

## ユニファイド メッセージング言語パック

Setup.exe を使用して UM 言語パックをメールボックス サーバーにインストールします。新しい言語パックをインストールすると、言語パックに関連付けられた言語が使用可能な言語の一覧に追加されます。インストールされている言語は、Exchange 管理シェルで [Get-UMService](https://technet.microsoft.com/ja-jp/library/jj552407\(v=exchg.150\)) コマンドレットを使用して表示できます。

UM 言語パックをインストールすると、選択した言語の TTS エンジンや録音済みプロンプトで使用するファイルがコピーされ、ボイス メール システムに接続したユーザーがこれらのファイルを利用できるようになります。UM 言語パックは、[Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/p/?linkid=266542)からダウンロードできます。詳細については、「[UM 言語パックをインストールする](install-a-um-language-pack-exchange-2013-help.md)」を参照してください。

## UM ダイヤル プラン言語

作成した各 UM ダイヤル プランには、既定の言語設定が含まれています。ユニファイド メッセージングでは、Outlook Voice Access ユーザーがメールボックスにアクセスするときに、ユーザーに対して音声合成変換を使用したり、標準のオーディオ プロンプトを再生しなければならない場合があるため、UM ダイヤル プラン言語設定が必要です。既定のダイヤル プラン言語を選択する必要はありません。

Exchange を初めてインストールした時点では、英語 (米国) が既定の言語であり、ダイヤル プランで使用できる唯一の言語オプションです。UM 言語パックをメールボックス サーバーにインストールすると、ダイヤル プランの既定の言語を構成するときに、言語パックに関連付けられた言語が使用可能なオプションとして一覧表示されます。

既定の言語は発信者にとって重要です。Outlook Voice Access ユーザーがボイス メール システムを呼び出すと、使用される言語は、ユーザーが最初にメールボックスにサインインしたときに設定した Outlook Web App の言語設定に基づきます。ユニファイド メッセージングは Outlook Web App で設定されている言語をユーザーが関連付けられているダイヤル プランで使用可能な言語の一覧と比較します。適切に一致するものがない場合は、既定の UM ダイヤル プラン言語が使用されます。たとえば、フランスのユーザーのみを含むダイヤル プランがある場合、ダイヤル プランの既定の言語設定をフランス語に設定する必要があります。

## UM 自動応答言語

既定では、UM 自動応答は UM ダイヤル プランに関連付けられるため、UM 自動応答を作成すると、UM 自動応答は関連付けられた UM ダイヤル プランの既定の言語設定を使用します。ただし、この設定は UM 自動応答が作成された後で変更できます。

ユニファイド メッセージングでは発信者に対して TTS 変換を使用するか、標準のオーディオ プロンプトを再生する必要がある場合があるため、UM 自動応答言語設定が必要です。ユニファイド メッセージングでは、自動応答のカスタム プロンプトの言語が自動応答の言語設定と一致しているかどうかは確認されません。ただし、ベスト プラクティスとして、自動応答の言語設定がカスタム プロンプトの言語と一致していることを確認してください。そうでない場合、システムである言語から別の言語に変化したことが発信者に聞こえる場合があります。

UM 自動応答言語設定の変更は、発信者に対して複数の異なる言語固有の自動応答を必要とする場合に役立ちます。

## クライアント言語選択プロセス

UM 言語パックを使用すると、発信者と Outlook Voice Access ユーザーは複数の言語でユニファイド メッセージング システムを操作できます。追加の言語パックをメールボックス サーバーにインストールすると、発信者および Outlook Voice Access ユーザーは、自分に適した言語で電子メール メッセージを聞いたりボイス メール システムを操作したりできるようになります。同様に、Outlook Web App ユーザーおよび Outlook 2010 以降のバージョンを使用しているユーザーは、ボイス メール プレビューによる音声メッセージのトランスクリプトをそれぞれの言語で確認できます。

特定の言語をサポートするには、その言語の UM クライアント言語パックを各メールボックス サーバーにインストールする必要があります。

特定の言語の UM 言語パックがインストールされていなかったり、利用できなかったりするような場合には、クライアント フォールバック言語が使用されることがあります。一部の言語の代わりにフォールバック UM クライアント言語を利用できますが、その他の言語ではフォールバック言語を利用することができません。特定の言語の UM 言語パックがインストールされておらず、その言語で利用できるフォールバック言語がない場合は、en-US (US 英語) が使用されます。

次の表に、特定の UM 言語パックがメールボックス サーバーにインストールされていない場合に使用されるクライアント言語とフォールバック言語の一覧を示します。

### UM のクライアント フォールバック言語

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>言語</th>
<th>国/地域名</th>
<th>カルチャ ID</th>
<th>選択される最初の言語 (インストールされている場合)</th>
<th>選択される 2 番目の言語 (インストールされている場合)</th>
<th>選択される 3 番目の言語 (インストールされている場合)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>カタルニア語</p></td>
<td><p>スペイン</p></td>
<td><p>ca-ES</p></td>
<td><p>ca-ES</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>中国語 (香港)</p></td>
<td><p>中国</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-CN</p></td>
<td><p>zh-TW</p></td>
</tr>
<tr class="odd">
<td><p>簡体字中国語</p></td>
<td><p>中国</p></td>
<td><p>zh-CN</p></td>
<td><p>zh-CN</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-TW</p></td>
</tr>
<tr class="even">
<td><p>繁体字中国語</p></td>
<td><p>台湾</p></td>
<td><p>zh-TW</p></td>
<td><p>zh-TW</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-CN</p></td>
</tr>
<tr class="odd">
<td><p>デンマーク語</p></td>
<td><p>デンマーク</p></td>
<td><p>da-DK</p></td>
<td><p>da-DK</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>オランダ語</p></td>
<td><p>オランダ</p></td>
<td><p>nl-NL</p></td>
<td><p>nl-NL</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>英語</p></td>
<td><p>オーストラリア</p></td>
<td><p>en-AU</p></td>
<td><p>en-AU</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>英語</p></td>
<td><p>カナダ</p></td>
<td><p>en-CA</p></td>
<td><p>en-CA</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>英語</p></td>
<td><p>インド</p></td>
<td><p>en-IN</p></td>
<td><p>en-IN</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>英語</p></td>
<td><p>英国</p></td>
<td><p>en-GB</p></td>
<td><p>en-GB</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>英語</p></td>
<td><p>米国</p></td>
<td><p>en-US</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>フィンランド語</p></td>
<td><p>フィンランド</p></td>
<td><p>fi-FL</p></td>
<td><p>fi-FL</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>フランス語</p></td>
<td><p>カナダ</p></td>
<td><p>fr-CA</p></td>
<td><p>fr-CA</p></td>
<td><p>fr-FR</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="even">
<td><p>フランス語</p></td>
<td><p>フランス</p></td>
<td><p>fr-FR</p></td>
<td><p>fr-FR</p></td>
<td><p>fr-CA</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="odd">
<td><p>ドイツ語</p></td>
<td><p>ドイツ</p></td>
<td><p>de-DE</p></td>
<td><p>de-DE</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>イタリア語</p></td>
<td><p>イタリア</p></td>
<td><p>it-IT</p></td>
<td><p>it-IT</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>日本語</p></td>
<td><p>日本</p></td>
<td><p>ja-JP</p></td>
<td><p>ja-JP</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>韓国語</p></td>
<td><p>韓国</p></td>
<td><p>ko-KR</p></td>
<td><p>ko-KR</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ノルウェー語 (ブークモール)</p></td>
<td><p>ノルウェー</p></td>
<td><p>nb-NO</p></td>
<td><p>nb-NO</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ポーランド語</p></td>
<td><p>ポーランド</p></td>
<td><p>pl-PL</p></td>
<td><p>pl-PL</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ポルトガル語</p></td>
<td><p>ブラジル</p></td>
<td><p>pt-BR</p></td>
<td><p>pt-BR</p></td>
<td><p>pt-PT</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="even">
<td><p>ポルトガル語</p></td>
<td><p>ポルトガル</p></td>
<td><p>pt-PT</p></td>
<td><p>pt-PT</p></td>
<td><p>pt-BR</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="odd">
<td><p>ロシア語</p></td>
<td><p>ロシア</p></td>
<td><p>ru-RU</p></td>
<td><p>ru-RU</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>スペイン語</p></td>
<td><p>スペイン</p></td>
<td><p>es-ES</p></td>
<td><p>es-ES</p></td>
<td><p>es-MX</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="odd">
<td><p>スペイン語</p></td>
<td><p>メキシコ</p></td>
<td><p>es-MX</p></td>
<td><p>es-MX</p></td>
<td><p>es-ES</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="even">
<td><p>スウェーデン語</p></td>
<td><p>スウェーデン</p></td>
<td><p>sv-SE</p></td>
<td><p>sv-SE</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


ページのトップへ

