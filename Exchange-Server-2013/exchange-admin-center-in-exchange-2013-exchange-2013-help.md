---
title: 'Exchange 2013 の Exchange 管理者センター: Exchange 2013 Help'
TOCTitle: Exchange 2013 の Exchange 管理者センター
ms:assetid: a9aea11a-6ba3-4f4a-a76e-79072e7cfc7d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ150562(v=EXCHG.150)
ms:contentKeyID: 48269909
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 の Exchange 管理者センター

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-17_

Exchange 管理センター (EAC) は、Microsoft Exchange Server 2013 の Web ベースの管理コンソールで、社内、オンライン、およびハイブリッド Exchange 展開用に最適化されています。Exchange Server 2010 の管理に使用されていた 2 つのインターフェイスである Exchange 管理コンソール (EMC) と Exchange コントロール パネル (ECP) は、EAC によって置き換えられました。

Web ベースの EAC が提供する利点の 1 つは、ECP IIS 仮想ディレクトリ内からのインターネット アクセスとイントラネット アクセスを分割できることです。この機能により、組織の外部から EAC へのインターネット アクセスをユーザーに許可するかどうかを制御し、同時に Outlook Web App オプションへのエンド ユーザーによるアクセスを許可できます。詳細については、「[Exchange 管理センターへのアクセスをオフにする](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md)」を参照してください。

このトピックの Exchange Online バージョンについては、「[Exchange Online の Exchange 管理センター](https://technet.microsoft.com/ja-jp/library/jj200743\(v=exchg.150\))」を参照してください。

このトピックの Exchange Online Protection バージョンについては、「[Exchange Online Protection の Exchange 管理センター](https://technet.microsoft.com/ja-jp/library/jj723141\(v=exchg.150\))」を参照してください。

目次

EACへのアクセスについて

EAC で共通のユーザー インターフェイス要素

サポート対象ブラウザー

## EACへのアクセスについて

EAC は現在 Web ベースの管理コンソールであるため、Web ブラウザーから ECP 仮想ディレクトリ URL を使用してコンソールにアクセスする必要があります。ほとんどの場合、EAC の URL は次のようになります。

  - **\[内部 URL\]:`https://<CASServerName>/ecp`**   内部 URL を使用して、組織のファイアウォール内から EAC にアクセスします。

  - **\[外部 URL\]:`https://mail.contoso.com/ecp`**   外部 URL を使用して、組織のファイアウォールの外部から EAC にアクセスします。組織によっては EAC への外部アクセスをオフにすることもできます。詳細については、「[Exchange 管理センターへのアクセスをオフにする](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md)」を参照してください。

EAC の内部 URL または外部 URL を特定するには、[Get-EcpVirtualDirectory](https://technet.microsoft.com/ja-jp/library/dd351058\(v=exchg.150\)) コマンドレットを使用できます。詳細については、「[Exchange 管理センターの内部 URL および外部 URL を検索する](find-the-internal-and-external-urls-for-the-exchange-admin-center-exchange-2013-help.md)」を参照してください。

共存シナリオで、Exchange 2010 および Exchange 2013 を同じ組織で実行し、メールボックスが現在も Exchange 2010 メールボックス サーバーにある場合、ブラウザーは Exchange 2010 ECP が既定となります。URL に Exchange バージョンを追加することで EAC にアクセスできます。たとえば、仮想ディレクトリがクライアント アクセス サーバー CAS15-NA にホストされている EAC にアクセスするには、次の URL を使用します。`https://CAS15-NA/ecp/?ExchClientVer=15`。反対に、メールボックスが Exchange 2013 メールボックス サーバーにあり、Exchange 2010 ECP にアクセスする場合には、次の URL を使用します。`https://CAS14-NA/ecp/?ExchClientVer=14`.

## EAC で共通のユーザー インターフェイス要素

ここでは、EAC 全体で共通のユーザー インターフェイス要素について説明します。

![Exchange 管理センター](images/JJ150562.cd617bc0-19ef-47d2-bba1-4e9546b12e0c(EXCHG.150).gif "Exchange 管理センター")

## 社内外のナビゲーション

社内外にまたがるナビゲーションでは、Exchange Online 展開と社内 Exchange 展開間を簡単に切り替えることができます。Exchange Online 組織がない場合、リンクは Office 365 サインアップのページにつながります。詳細については、「[Exchange Server のハイブリッド展開](https://technet.microsoft.com/ja-jp/library/jj200581\(v=exchg.150\))」を参照してください。

## 機能ウィンドウ

EAC で実行する多くのタスクで、これがナビゲーションの第 1 階層になります。機能ウィンドウは、Exchange 2010 における EMC からのコンソール ツリーに似ていますが、Exchange 2013 では機能ウィンドウはサーバーの役割ではなく機能領域ごとに整理されているため、より少ないクリック回数で必要な場所にたどりつけます。

  - **受信者   **ここで、メールボックス、グループ、リソース メールボックス、連絡先、共有メールボックス、およびメールボックスの移行や移動を管理します。

  - **アクセス許可   **ここで、管理者の役割、ユーザーの役割、および Outlook Web App ポリシーを管理します。

  - **コンプライアンス マネジメント   **ここで、インプレース電子証拠開示、インプレース保持、監査、データ損失防止 (DLP)、保持ポリシー、保持タグ、およびジャーナル ルールを管理します。

  - **組織   **ここで、フェデレーション共有、Outlook Apps、およびアドレス一覧など、Exchange 組織にかかわるタスクを管理します。

  - **保護   **ここで、組織のマルウェア対策保護を管理します。

  - **メール フロー   **ここで、ルール、配信レポート、承認済みドメイン、電子メール アドレス ポリシー、および送信/受信コネクタを管理します。

  - **モバイル   **ここで、組織への接続を許可するモバイル デバイスを管理します。モバイル デバイスのアクセスおよびモバイル デバイス メールボックス ポリシーを管理できます。

  - **パブリック フォルダー   **Exchange 2010 では、ツールボックス内の EMC の外側にあるパブリック フォルダー管理コンソールを使用してパブリック フォルダーを管理する必要がありました。Exchange 2013 では、**\[パブリック フォルダー\]** 機能領域内でパブリック フォルダーを管理できます。

  - **ユニファイド メッセージング   **ここで、UM ダイヤル プランおよび UM IP ゲートウェイを管理します。

  - **サーバー   **ここで、メールボックスおよびクライアント アクセス サーバー、データベース、データベース可用性グループ、仮想ディレクトリ、ならびに証明書を管理します。

  - **ハイブリッド   **ここで、ハイブリッド組織の設定および構成を行います。

## タブ

タブは、ナビゲーションの第 2 階層になります。各機能領域にはさまざまなタブが含まれており、それぞれのタブは完全な機能を表しています。このルールの唯一の例外は、\[ハイブリッド\] 機能領域です。最初に、ハイブリッド構成ウィザードを使用して組織のハイブリッド展開を可能にする必要があります。

## ツールバー

ほとんどのタブは、クリックするとツールバーが表示されます。ツールバーには、特定のアクションを実行する複数のアイコンがあります。次の表は、最も一般的なアイコンとそのアクションを示しています。アイコンに関連付けられたアクションを表示するには、そのアイコンにポインターを合わせます。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>アイコン</th>
<th>名前</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="[追加] アイコン" alt="[追加] アイコン" /></p></td>
<td><p>追加、新規</p></td>
<td><p>このアイコンを使用して、新しいオブジェクトを作成します。これらの一部のアイコンには下方向キーが関連付けられており、これをクリックして、作成可能な追加のオブジェクトを表示できます。たとえば、<strong>[受信者]</strong> &gt; <strong>[メールボックス]</strong> では、下方向キーをクリックすると、追加オプションとして <strong>[ユーザー メールボックス]</strong> および <strong>[リンクされたメールボックス]</strong> が表示されます。</p></td>
</tr>
<tr class="even">
<td><p><img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="編集アイコン" alt="編集アイコン" /></p></td>
<td><p>編集</p></td>
<td><p>このアイコンを使用してオブジェクトを編集します。</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif" title="[削除] アイコン" alt="[削除] アイコン" /></p></td>
<td><p>削除</p></td>
<td><p>このアイコンを使用してオブジェクトを削除します。一部の削除アイコンには下方向キーがあり、これをクリックして追加オプションを表示できます。</p></td>
</tr>
<tr class="even">
<td><p><img src="images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif" title="[検索] アイコン" alt="[検索] アイコン" /></p></td>
<td><p>検索</p></td>
<td><p>このアイコンを使用して、検索するオブジェクトの検索文字列を入力できる検索ボックスを開きます。さらに検索オプションを調べるには、「<a href="https://technet.microsoft.com/ja-jp/library/jj156853(v=exchg.150)">受信者 &gt; 高度な検索</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/Dn624163.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif" title="[最新の情報に更新] アイコン" alt="[最新の情報に更新] アイコン" /></p></td>
<td><p>最新の情報に更新</p></td>
<td><p>このアイコンを使用してリスト ビューを更新します。</p></td>
</tr>
<tr class="even">
<td><p><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="[その他のオプション] アイコン" alt="[その他のオプション] アイコン" /></p></td>
<td><p>その他のオプション</p></td>
<td><p>このアイコンを使用して、そのタブのオブジェクトに対して実行できる他のアクションを表示します。たとえば、<strong>[受信者]</strong> &gt; <strong>[メールボックス]</strong> でこのアイコンをクリックすると、次のオプションが表示されます。<strong>[無効にする]</strong>、<strong>[列の追加/削除]</strong>、<strong>[データを CSV ファイルにエクスポートする]</strong>、<strong>[メールボックスに接続する]</strong>、<strong>[詳細検索]</strong>。</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif" title="上矢印アイコン" alt="上矢印アイコン" />   <img src="images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif" title="下矢印アイコン" alt="下矢印アイコン" /></p></td>
<td><p>上方向キーと下方向キー</p></td>
<td><p>これらのアイコンを使用して、オブジェクトの優先度を上下に移動します。たとえば、<strong>[メール フロー]</strong> &gt; <strong>[電子メール アドレス ポリシー]</strong> で電子メール アドレス ポリシーの優先度を上げるには、上矢印をクリックします。これらの方向キーを使用してパブリック フォルダー階層を移動し、リスト ビューのルールを上下に移動できます。</p></td>
</tr>
<tr class="even">
<td><p><img src="images/JJ657480.ed7f7abf-39d8-4f43-a918-ccb3bff87ef5(EXCHG.150).gif" title="[コピー] アイコン" alt="[コピー] アイコン" /></p></td>
<td><p>コピー</p></td>
<td><p>このアイコンを使用してオブジェクトをコピーします。これにより、元のオブジェクトを変更せずにオブジェクトを変更できます。たとえば、<strong>[アクセス許可]</strong> &gt; <strong>[管理者の役割]</strong> でリスト ビューから役割を選択し、このアイコンをクリックすると、既存の役割グループを基にして新しい役割グループが作成されます。</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif" title="[削除] アイコン" alt="[削除] アイコン" /></p></td>
<td><p>削除</p></td>
<td><p>このアイコンを使用して、一覧からアイテムを削除します。たとえば、<strong>[パブリック フォルダー アクセス許可]</strong> ダイアログ ボックスでユーザーを選択し、このアイコンをクリックすることにより、パブリック フォルダーへのアクセスが許可されたユーザーの一覧からユーザーを削除できます。</p></td>
</tr>
</tbody>
</table>


## リスト ビュー

タブを選択すると、通常、リスト ビューが表示されます。EAC のリスト ビューは、ECP に存在した制限を取り除くように設計されています。ECP では最大 500 オブジェクトのみを表示でき、詳細ウィンドウに表示されないオブジェクトを表示する場合は、検索とフィルター オプションを使用して特定のオブジェクトを探す必要があります。Exchange 2013 では、EAC リスト ビュー内からの表示可能限度は、社内展開で約 20,000 オブジェクト、Exchange Online で約 10,000 オブジェクトです。さらに、ページングが含まれているため、結果をページングできます。**\[受信者\]** リスト ビューにおいても、ページ サイズの構成や CSV ファイルへのデータのエクスポートが可能です。

## 詳細ウィンドウ

リスト ビューからオブジェクトを選択すると、そのオブジェクトに関する情報が詳細ウィンドウに表示されます。場合によっては (たとえば、受信者オブジェクトの場合など)、詳細ウィンドウに簡単な管理タスクが含まれます。たとえば、**\[受信者\]** \> **\[メールボックス\]** に移動し、リスト ビューからメールボックスを選択した場合は、そのメールボックスのアーカイブを有効または無効にするオプションが詳細ウィンドウに表示されます。詳細ウィンドウを使用して、複数のオブジェクトを一括編集できます。単に CTRL キーを押して一括編集するオブジェクトを選択し、詳細ウィンドウからオプションを使用します。たとえば、複数のメールボックスを選択すると、ユーザーの連絡先および組織の情報、カスタム属性、メールボックス クォータ、Outlook Web App の設定などを一括更新できます。

## 通知

EAC には、長期間実行されるプロセスの状態を表示する通知ビューアーが含まれており、プロセスの完了時に通知が行われます。さらに、特に長期間実行されるプロセス (移動要求など) の場合、電子メールによる通知の受信をオプトインすることもできます。

## \[自分\] タイルとヘルプ

*\[自分\] タイル*では、EAC からのサインアウトおよび他のユーザーとしてサインインが行えます。ヘルプ ![ヘルプ アイコン](images/JJ150562.a32eac4e-345d-4236-a284-204390aff4ee(EXCHG.150).gif "ヘルプ アイコン") ドロップ ダウン メニューから次のアクションを行えます。

  - **ヘルプ**   ![ヘルプ アイコン](images/JJ150562.a32eac4e-345d-4236-a284-204390aff4ee(EXCHG.150).gif "ヘルプ アイコン") をクリックして、オンライン ヘルプ コンテンツを表示します。

  - **ヘルプ バブルを無効にする**   ヘルプ バブルは、オブジェクトを作成または編集する際に、フィールドのコンテキスト ヘルプを表示します。ヘルプ バブルのヘルプをオフにしたり、無効になっている場合はオンにすることができます。

  - **著作権およびプライバシー   **プライバシーまたは著作権のリンクをクリックして、Exchange 2013 に関する著作権およびプライバシーの情報を確認します。

## サポート対象ブラウザー

EAC での操作性を最高にするには、「プレミアム」と表示されているオペレーティング システムとブラウザーの組み合わせを使用してください。


> [!NOTE]
> 上記の表に記載されていないオペレーティング システムとブラウザーの組み合わせは、タッチ操作を含めて、サポートされません。



  - **プレミアム:**  すべての機能がサポートされ、完全にテストされています。

  - **サポート:**  プレミアムと同じ機能がサポートされます。ただし、サポート対象ブラウザーに機能がなく、ブラウザーとオペレーティング システムの組み合わせでサポートされないことがあります。

  - **サポート外:**  ブラウザーとオペレーティング システムは、サポートされていないかテストされていません。


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Web ブラウザー</p></td>
<td><p>Windows XP および Windows Server 2003</p></td>
<td><p>Windows Vista</p></td>
<td><p>Windows 7 と Windows Server 2008</p></td>
<td><p>Windows 8 と Windows Server 2012</p></td>
<td><p>Mac OSX</p></td>
<td><p>Linux</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td><p>サポート</p></td>
<td><p>サポート</p></td>
<td><p>Premium</p></td>
<td><p>サポート外</p></td>
<td><p>サポート外</p></td>
<td><p>サポート外</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td><p>サポート外</p></td>
<td><p>サポート</p></td>
<td><p>Premium</p></td>
<td><p>サポート外</p></td>
<td><p>サポート外</p></td>
<td><p>サポート外</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10 以降</p></td>
<td><p>サポート外</p></td>
<td><p>サポート</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>サポート外</p></td>
<td><p>サポート外</p></td>
</tr>
<tr class="odd">
<td><p>Firefox 11 以降</p></td>
<td><p>サポート</p></td>
<td><p>サポート</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>サポート</p></td>
</tr>
<tr class="even">
<td><p>Safari 5.1 以降</p></td>
<td><p>サポート外</p></td>
<td><p>サポート外</p></td>
<td><p>サポート外</p></td>
<td><p>サポート外</p></td>
<td><p>Premium</p></td>
<td><p>サポート外</p></td>
</tr>
<tr class="odd">
<td><p>Chrome 18 またはそれ以降</p></td>
<td><p>サポート</p></td>
<td><p>サポート</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>サポート外</p></td>
</tr>
</tbody>
</table>

