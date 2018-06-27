---
title: 'Exchange Server Supportability Matrix: Exchange 2013 Help'
TOCTitle: Exchange Server Supportability Matrix
ms:assetid: dbac2d40-da8b-469f-a265-1d1f948fe446
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff728623(v=EXCHG.150)
ms:contentKeyID: 54652993
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Server Supportability Matrix

 

_**適用先:**Exchange Server 2007, Exchange Server 2010, Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:**2018-03-20_

この Exchange Server Server のサポート一覧は、サポートされる Microsoft Exchange のバージョンで、任意の構成で使用可能なサポート レベルや必要なコンポーネントに関する情報を Microsoft Exchange 管理者が容易に見つけることができるようにまとめたものです。

## リリース モデル

次の表では、サポートされている Exchange の各バージョンのリリース モデルを識別します。リリース モデルは、X の文字で識別されます。

Exchange の Exchange 2013 より前のバージョンでは、各更新プログラムのロールアップ パッケージは、製品全体に関する累積更新プログラムとなります。このため、更新プログラムのロールアップ パッケージを Exchange Server 2010 に適用すると、その更新プログラムのロールアップ パッケージに含まれるすべての修正が適用されます。これには、以前の更新プログラムのロールアップ パッケージに含まれていたすべての修正が含まれます。Exchange の以前のバージョン用に更新プログラムまたは修正プログラムが作成される場合、その更新プログラムまたは修正プログラムに含まれる 1 つ以上のバイナリ ファイルは累積的です。ファイルの内容に関して累積的です。ただし、Exchange 製品全体に関して累積的ではありません。詳細については、「[Exchange 2010 サービス](https://go.microsoft.com/fwlink/p/?linkid=298627)」を参照してください。

Exchange 2013 では、修正プログラムと Service Pack の配信方法を変更しました。以前のバージョンの Exchange で使われた優先度に基づく修正プログラムのリリースと更新プログラムのロールアップ モデルに代わり、Exchange 2013 以降のバージョンでは定期配信モデルが採用されました。このモデルでは、累積更新プログラムが 3 か月ごとにリリースされます。Exchange 2013 以降の累積的な更新プログラム (CU) は、製品のアップグレードやサービス パック リリースと同様に、そのバージョンの Exchange の完全なリフレッシュとして公開されます。詳細については、「[Exchange 2013 の更新プログラム](updates-for-exchange-2013-exchange-2013-help.md)」を参照してください。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>サービス リリース モデル</th>
<th>Exchange 2016</th>
<th>Exchange 2013</th>
<th>Exchange 2010</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>累積的な更新プログラム</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>更新プログラムのロールアップ</p></td>
<td><p></p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>セキュリティ修正プログラムを個別に配信</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>


## サポート ライフサイクル

Exchange の特定のバージョンや、MicrosoftWindows サーバーまたはクライアント オペレーティング システムのサポート ライフサイクルの詳細については、「[マイクロソフト サポート ライフサイクル](https://go.microsoft.com/fwlink/p/?linkid=55839)」ページを参照してください。Microsoft サポート ライフサイクルの詳細については、「[マイクロソフト サポート ライフサイクル ポリシーに関する FAQ](https://go.microsoft.com/fwlink/p/?linkid=158902)」を参照してください。

## Exchange Server 2007 サポート終了

Exchange 2007 は [Microsoft ライフサイクル ポリシー](https://go.microsoft.com/fwlink/p/?linkid=833210) に従って、2017 年 4 月 11 日にサポートが終了しました。その日付以降、新たなセキュリティ更新プログラム、セキュリティ以外の更新プログラム、無料または有料のアシスト サポート オプションやオンラインの技術情報の更新は提供されなくなります。また、Office 365 の採用の促進とクラウド利用の増加により、Office 製品のカスタム サポート オプションも利用できなくなります。これには Exchange Server や、Office スイート、SharePoint Server、Office Communications Server、Lync Server、Skype for Business Server、Project Server、Visio も含まれます。Exchange 2007 のサポートが終了したため、移行とアップグレードの計画を完了してください。お客様には、Microsoft と Microsoft 認定パートナーが提供する、クラウド移行のための [Microsoft FastTrack](https://go.microsoft.com/fwlink/p/?linkid=238431)、オンプレミスのアップグレードのための[ソフトウェア アシュアランスの展開および計画サービス](https://go.microsoft.com/fwlink/p/?linkid=833211)などの展開によるメリットを利用することをお勧めします。

## サポートされているオペレーティング システムのプラットフォーム

次の表は、Exchange の各バージョンが動作するオペレーティング システム プラットフォームを示しています。サポートされるプラットフォームは X で示しています。


> [!IMPORTANT]
> 以下の表に記載されていない Windows サーバーおよび Windows クライアントのリリースは、Exchange のいずれのバージョンおよびリリースでも使用できません。




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
<th>オペレーティング システム プラットフォーム</th>
<th>Exchange 2016 CU3 以降</th>
<th>Exchange 2016 CU2 以前</th>
<th>Exchange 2013 SP1 以降</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Vista SP2</p></td>
<td><p></p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X1</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2008 SP2</p></td>
<td><p></p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2008 R2 SP1</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows 7 SP1</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
</tr>
<tr class="odd">
<td><p>Windows 8</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
</tr>
<tr class="even">
<td><p>Windows 8.1</p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>Windows 10</p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
<td><p></p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012 R2</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2016</p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>


1Exchange 管理ツールのみ

## サポートされる Active Directory 環境

次の表は、Exchange の各バージョンが通信できる Active Directory 環境を示します。サポートされる環境は X で示しています。Active Directory サーバーとは、書き込み可能なグローバル カタログ サーバーと書き込み可能なドメイン コントローラーの両方を指します。読み取り専用グローバル カタログ サーバーと読み取り専用ドメイン コントローラーはサポートされていません。


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
<th>オペレーティング システム環境</th>
<th>Exchange 2016 CU3 以降</th>
<th>Exchange 2016 CU2 以前</th>
<th>Exchange 2013 SP1 以降</th>
<th>Exchange 2010 SP3 RU5 以降</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Server 2003 SP2 Active Directory サーバー</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2008 SP2 Active Directory サーバー</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2008 R2 SP1 Active Directory サーバー</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012 Active Directory サーバー</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012 R2 Active Directory サーバー</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2016 Active Directory サーバー</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>



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
<th>フォレストの機能レベル</th>
<th>Exchange 2016 CU3 以降</th>
<th>Exchange 2016 CU2 以前</th>
<th>Exchange 2013 SP1 以降</th>
<th>Exchange 2010 SP3 RU5 以降</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Server 2003 のフォレストの機能レベル</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2008 のフォレストの機能レベル</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2008 R2 SP1 のフォレストの機能レベル</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012 のフォレストの機能レベル</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012 R2 のフォレストの機能レベル</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2016 のフォレストの機能レベル</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Outlook Web App または Outlook on the web のプレミアム バージョンで使用がサポートされる Web ブラウザー

次の表に、プレミアム バージョンの Outlook Web App または Outlook on the web と組み合わせて使用するためにサポートされている Web ブラウザーを示します。サポートされているブラウザーは X で識別されます。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>ブラウザー</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 以降</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Edge</p></td>
<td><p>現在のリリースの Microsoft Edge</p></td>
<td><p>該当なし</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer</p></td>
<td><p>現在のまたは 1 つ前のリリースの Internet Explorer</p></td>
<td><p>該当なし</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 11</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 7</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Firefox</p></td>
<td><p>現在のまたは 1 つ前のリリースの Firefox</p></td>
<td><p>該当なし</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="odd">
<td><p>Firefox 3.0.1 以降</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Firefox 12 以降</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Safari</p></td>
<td><p>現在のリリースの Safari</p></td>
<td><p>該当なし</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="even">
<td><p>Safari 3.1 以降</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Safari 5.0 以降</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Chrome</p></td>
<td><p>現在のリリースの Chrome</p></td>
<td><p>該当なし</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="odd">
<td><p>Chrome 3.0.195 またはそれ以降</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Chrome 18 またはそれ以降</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## ベーシック バージョンの Outlook Web App または Outlook on the web で使用するためにサポートされている Web ブラウザー

次の表に、ライト (ベーシック) バージョンの Outlook Web App または Outlook on the web と組み合わせて使用するためにサポートされている Web ブラウザーを示します。サポートされているブラウザーは X で識別されます。


> [!NOTE]
> Outlook Web App Basic (Outlook Web App Light) は、モバイル ブラウザーでの使用をサポートしています。ただし、モバイル ブラウザーでレンダリングまたは認証の問題が発生する場合は、サポートされているブラウザーの完全なクライアントで Outlook Web App Light を使用して、問題が再現できるかどうかを判断します。たとえば、Safari、Chrome、または Internet Explorer で Outlook Web App Light の使用をテストします。完全なクライアントで問題が再現できない場合は、モバイル デバイスのベンダーに問い合わせることをお勧めします。これらのケースでは、必要に応じベンダーと協力して解決にあたります。




<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>ブラウザー</th>
<th>Exchange 2016</th>
<th>Exchange 2013</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Edge</p></td>
<td><p>現在のリリースの Microsoft Edge</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer</p></td>
<td><p>現在のまたは 1 つ前のリリースの Internet Explorer</p></td>
<td><p>該当なし</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 11</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X<span></span></p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 7</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Safari</p></td>
<td><p>現在のリリースの Safari</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Firefox</p></td>
<td><p>現在のまたは 1 つ前のリリースの Firefox</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Chrome</p></td>
<td><p>現在のリリースの Chrome</p></td>
<td><p>該当なし</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="odd">
<td><p>Opera</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## Outlook Web App または Outlook on the web で S/MIME を使用するためにサポートされている Web ブラウザー

次の表に、Outlook Web App または Outlook on the web と組み合わせて S/MIME を使用するためにサポートされている Web ブラウザーを示します。サポートされているブラウザーは X で識別されます。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>ブラウザー</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 以降</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Edge</p></td>
<td><p>現在のリリースの Microsoft Edge</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer</p></td>
<td><p>現在のまたは 1 つ前のリリースの Internet Explorer</p></td>
<td><p>該当なし</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 11</p></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10</p></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 7</p></td>
<td></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## クライアント

次の表は、Exchange の各バージョンとの使用がサポートされているメールボックス クライアントを示しています。サポートされるクライアントは X で示しています。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>クライアント</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 以降</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p></p></td>
<td><p>X1</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2010</p></td>
<td><p>X4</p></td>
<td><p>X2</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2013</p></td>
<td><p>X4</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2016</p></td>
<td><p>X4</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Outlook for Mac for Office 365</p></td>
<td><p>X4</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Phone 7</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Phone 7.5</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Phone 8</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Phone 8.1</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Mobile 10</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Entourage 2008 (EWS)</p></td>
<td><p>X3</p></td>
<td><p>X3</p></td>
<td><p>X3</p></td>
</tr>
</tbody>
</table>


1Outlook 2007 Service Pack 3 と最新の公開更新プログラムが必要です。

2Outlook 2010 Service Pack 1 と最新の公開更新プログラムが必要です。

3EWS のみ。Exchange 2010 で DAV はサポートされていません。

4最新の Office Service Pack と公開更新プログラムでサポートされます。

## ツール

次の表は、Microsoft Exchange Inter-Organization Replication (組織間のレプリケーション) ツール (Exscfg.exe、Exssrv.exe) と一緒に使用できる Microsoft Exchange のバージョンを示しています。このツールは、Exchange 組織間のパブリック フォルダー情報 (空き時間情報を含む) をレプリケートするために使用します。詳細については、[Microsoft Exchange Server の組織間のレプリケーション](https://go.microsoft.com/fwlink/?linkid=22455)を参照してください。サポートされるバージョンは X で示しています。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>ツール</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 以降</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Inter-Organization Replication (組織間のレプリケーション) ツール</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## Microsoft .NET Framework

次の表は、Exchange の各バージョンで一緒に使用できる Microsoft.NET Framework のバージョンを示しています。サポートされるバージョンは X で示しています。


> [!IMPORTANT]
> <STRONG>以下の表に記載されていない .NET Framework のリリースは、どのバージョンとリリースの Exchange によっても一切サポートされていません。</STRONG>これには, .NET Framework のマイナー修正レベルのリリースが含まれます。




> [!NOTE]
> サポートされていない CU から Exchange を現在の CU にアップグレードするときに、中間 CU が利用できない場合、まず Exchange でサポートされている最新バージョンの .NET にアップグレードして、その後すぐに現在の CU にアップグレードする必要があります。この方法では、Exchange サーバーを最新の状態およびサポートされている最新の CU 上で保つ必要がなくなるわけではありません。<BR>マイクロソフトは、この方法を使用すればアップグレードの失敗が発生しないとは主張しません。アップグレードに失敗した場合、Microsoft サポート サービスにお問い合わせいただく場合があります。




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
<th>.NET Framework</th>
<th>Exchange 2016 CU8</th>
<th>Exchange 2016 CU5 - CU7</th>
<th>Exchange 2013 CU19</th>
<th>Exchange 2013 CU16 - CU18</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>.NET Framework 3.5</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X1</p></td>
</tr>
<tr class="even">
<td><p>.NET Framework 3.5 SP1</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>.NET Framework 4.0</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X1、2</p></td>
</tr>
<tr class="even">
<td><p>.NET Framework 4.5</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X1、2 </p></td>
</tr>
<tr class="odd">
<td><p>.NET Framework 4.6.2</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>.NET Framework 4.7.1</p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


1Windows Server 2012 を使用している場合は、Exchange 2010 SP3 を利用する前に, .NET Framework 3.5 をインストールする必要があります。

2Exchange 2010 では .NET .NET Framework 3.5 および .NET .NET Framework 3.5 SP1 ライブラリのみを使用します。.NET .NET Framework 4.5 ライブラリがコンピューターにインストールされていても、それらは使用されません。.NET .NET Framework 4.5 のメジャーまたはマイナー バージョン (.NET .NET Framework 4.5.1, .NET .NET Framework 4.5.2 など) のインストールは, .NET .NET Framework 3.5 または .NET .NET Framework 3.5 SP1 もそのコンピューターにインストールされていれば、サポートされます。

## Windows 管理フレームワーク

次の表に、Exchange の各バージョンと一緒に使用できる、Windows PowerShell コマンドライン インターフェイスを含む Windows 管理フレームワークのバージョンを示します。サポートされているバージョンは X で識別されます。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Windows PowerShell</th>
<th>Exchange 2016</th>
<th>Exchange 2013</th>
<th>Exchange 2010</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows PowerShell 2.0</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Management Framework</p></td>
<td><p>Windows Management Framework のバージョンは、Exchange をインストールしている Windows Server のリリースに組み込まれています。</p></td>
<td><p>Windows Management Framework のバージョンは、Exchange をインストールしている Windows Server のリリースに組み込まれています。</p></td>
<td><p>Windows Management Framework のバージョンは、Exchange をインストールしている Windows Server のリリースに組み込まれています。1</p></td>
</tr>
</tbody>
</table>


1Windows Management Framework 3.0 および Windows Management Framework 4.0 を使用して、Exchange 2010 SP3 RU5 以降を実行しているコンピューターでオペレーティング システム関連の管理タスクを実行できます。ただし、Exchange 2010 コマンドレットと Exchange 2010 スクリプトには Windows PowerShell 2.0 が必要です。Exchange 2010 のコマンドレットとスクリプトと Windows Management Framework 3.0 または Windows Management Framework 4.0 の組み合わせはサポートされません。

## Microsoft 管理コンソール

次の表は、Exchange の各バージョンと一緒に使用できる Microsoft 管理コンソール (MMC) のバージョンを示したものです。サポートされるバージョンは X で示しています。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>MMC</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 以降</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MMC 3.0</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## Windows インストーラー

次の表は、Exchange の各バージョンと一緒に使用できる Windows インストーラーのバージョンを示したものです。サポートされるバージョンは X で示しています。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Windows インストーラー</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 以降</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows インストーラー 4.5</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows インストーラー 5.0</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>

