---
title: 'Exchange 2013 の展開のアクセス許可のリファレンス: Exchange 2013 Help'
TOCTitle: Exchange 2013 の展開のアクセス許可のリファレンス
ms:assetid: b13412d0-0cc4-4c1d-bf31-cae3d3e211a9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee681663(v=EXCHG.150)
ms:contentKeyID: 59635008
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 の展開のアクセス許可のリファレンス

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

ここでは、Microsoft Exchange Server 2013 組織のセットアップで必要なアクセス許可について説明します。管理役割グループに関連付けられたユニバーサル セキュリティ グループ (USG)、およびその他の Windows セキュリティ グループおよびセキュリティ プリンシパルが、さまざまな Active Directory オブジェクトのアクセス制御リスト (ACL) に追加されます。ACL は、各オブジェクトに対して実行できる操作を制御します。どのアクセス許可が各役割グループ、セキュリティ グループ、またはセキュリティ プリンシパルに付与されるかを理解することで、Exchange 2013 をインストールするために必要な最小限のアクセス許可を判断できます。

ACL が通常のプロパティである **ntSecurityDescriptor** に適用されずに、**msExchMailboxSecurityDescriptor** などの他のプロパティに適用される場合があります。ディレクトリ サービスは、Windows セキュリティ記述子に指定されていないセキュリティを適用することはできません。ほとんどの場合、これらの ACL はストア サービスによってレプリケートされ、該当するオブジェクトに ACL が格納されます。残念ながら、これらの ACL を生のバイナリ データ以外の形で参照するためのツールはありません。

それぞれのアクセス許可の表の列には、以下の情報が記載されています。

  - **アカウント**   アクセス許可が付与または拒否されるセキュリティ プリンシパル。

  - **ACE の種類**   アクセス制御エントリ (ACE) の種類。
    
      - **許可 ACE**   許可 ACE は、ACE に関連付けられたユーザーまたはグループがアイテムにアクセスできるようにします。
    
      - **拒否 ACE**   拒否 ACE は、ACE に関連付けられたユーザーまたはグループがアイテムにアクセスできないようにします。

  - **継承**   子オブジェクトで使用される継承の種類。
    
      - **"すべて"** は、アクセス許可が該当のオブジェクトおよびすべてのサブオブジェクトに適用されることを示します。
    
      - **\[指定\]** は、\[プロパティ/適用先\] 行に指定されているオブジェクト クラスにアクセス許可が適用されることを示します。
    
      - **"なし"** は、アクセス許可が対象のオブジェクトのみに適用されることを示します。

  - **アクセス許可**   アカウントに付与されるアクセス許可。

  - **プロパティ/適用先**   アクセス許可の適用先は、所定のプロパティ、プロパティ セット、またはオブジェクト クラスのみである場合があります。ここには、それらの制限付きのアクセス許可を記述しています。

  - **コメント**   この列には、アクセス許可が必要な理由、またはアクセス許可に関する詳細な情報が説明されています (該当する場合のみ)。

表に記載されているアクセス許可は、通常、Active Directory サービス インターフェイス (ADSI) Edit (AdsiEdit.msc) の **\[詳細設定\]** ビューの **\[セキュリティ\]** プロパティ ページの **\[表示/編集\]** タブで使用される名称が記載されています。ADSI Edit の **\[セキュリティ\]** プロパティ ページでは、アクセス許可は大幅に短縮された形で表示されます。LDP ツール (Ldp.exe) には、アクセス マスクが数値で直接表示されます。セットアップ プログラムでは、あらかじめ定義された定数によってアクセス許可を参照します。

次の表に、これらの値の関係を示します。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>ADSI Edit の [概要] ページ</th>
<th>ADSI Edit の [詳細設定] ビューの [表示/編集] タブ</th>
<th>オブジェクトに適用される ACL エントリ</th>
<th>バイナリ値 (LDP でのアクセス マスク)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>フル コントロール</p></td>
<td><p>フル コントロール</p></td>
<td><p><code>WRITE_OWNER | WRITE_DAC | READ_CONTROL | DELETE | ACTRL_DS_CONTROL_ACCESS | ACTRL_DS_LIST_OBJECT | ACTRL_DS_DELETE_TREE | ACTRL_DS_WRITE_PROP | ACTRL_DS_READ_PROP | ACTRL_DS_SELF | ACTRL_DS_LIST | ACTRL_DS_DELETE_CHILD | ACTRL_DS_CREATE_CHILD</code></p></td>
<td><p><code>0x000F01FF</code></p></td>
</tr>
<tr class="even">
<td><p>読み取り</p></td>
<td><p>内容の一覧表示 + すべてのプロパティの読み取り + アクセス許可の読み取り</p></td>
<td><p><code>ACTRL_DS_LIST | ACTRL_DS_READ_PROP | READ_CONTROL</code></p></td>
<td><p><code>0x00020014</code></p></td>
</tr>
<tr class="odd">
<td><p>書き込み</p></td>
<td><p>すべてのプロパティの書き込み + 検証された書き込みすべて</p></td>
<td><p><code>ACTRL_DS_WRITE_PROP | ACTRL_DS_SELF</code></p></td>
<td><p><code>0x00000028</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>内容の一覧表示</p></td>
<td><p><code>ACTRL_DS_LIST</code></p></td>
<td><p><code>0x00000004</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>すべてのプロパティの読み取り</p></td>
<td><p><code>ACTRL_DS_READ_PROP</code></p></td>
<td><p><code>0x00000010</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>すべてのプロパティの書き込み</p></td>
<td><p><code>ACTRL_DS_WRITE_PROP</code></p></td>
<td><p><code>0x00000020</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>削除</p></td>
<td><p><code>DELETE</code></p></td>
<td><p><code>0x00010000</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>サブツリーの削除</p></td>
<td><p><code>ACTRL_DS_DELETE_TREE</code></p></td>
<td><p><code>0x00000040</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>アクセス許可の読み取り</p></td>
<td><p><code>READ_CONTROL</code></p></td>
<td><p><code>0x00020000</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>アクセス許可の修正</p></td>
<td><p><code>WRITE_DAC</code></p></td>
<td><p><code>0x00040000</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>所有者の修正</p></td>
<td><p><code>WRITE_OWNER</code></p></td>
<td><p><code>0x00080000</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>検証された書き込みすべて</p></td>
<td><p><code>ACTRL_DS_SELF</code></p></td>
<td><p><code>0x00000008</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>すべての拡張された権利</p></td>
<td><p><code>ACTRL_DS_CONTROL_ACCESS</code></p></td>
<td><p><code>0x00000100</code></p></td>
</tr>
<tr class="even">
<td><p>すべての子オブジェクトの作成</p></td>
<td><p>すべての子オブジェクトの作成</p></td>
<td><p><code>ACTRL_DS_CREATE_CHILD</code></p></td>
<td><p><code>0x00000001</code></p></td>
</tr>
<tr class="odd">
<td><p>すべての子オブジェクトの削除</p></td>
<td><p>すべての子オブジェクトの削除</p></td>
<td><p><code>ACTRL_DS_DELETE_CHILD</code></p></td>
<td><p><code>0x00000002</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p></p></td>
<td><p><code>ACTRL_DS_LIST_OBJECT</code></p></td>
<td><p><code>0x00000080</code></p></td>
</tr>
</tbody>
</table>


拡張された権利とは、個々のアプリケーションによって指定されるカスタム権利です。これらは、ACL に指定されます。ただし、それらは Active Directory にとって無意味です。特定のアプリケーションは、拡張された権利を適用しています。Exchange の拡張された権利の例として、"パブリック フォルダーの作成" や "インフォメーション ストア内での名前付きプロパティの作成" があります。

Microsoft Exchange Server 2010 のインストール時に設定されるアクセス許可については、「[Exchange 2010 の展開のアクセス許可のリファレンス](https://go.microsoft.com/fwlink/p/?linkid=402924)」を参照してください。

## Active Directory のアクセス許可の準備

このセクションのアクセス許可の表に、`Setup /PrepareAD` コマンドを実行するときに設定されるアクセス許可を示します。


> [!NOTE]
> このセクションで説明されているアクセス許可は、既定のアクセス許可であり、共有型アクセス許可モデルを使用して Exchange 2013 を展開する場合に構成されます。Active Directory 分割型アクセス許可モデルを使用して Exchange 2013 を展開した場合、既定のアクセス許可は異なります。Active Directory 分割型アクセス許可、共有アクセス許可モデル、分割型アクセス許可モデルを使用する場合の、一般的な既定のアクセス許可の変更の詳細については、「<A href="understanding-split-permissions-exchange-2013-help.md">分割型アクセス許可について</A>」の「<A href="understanding-split-permissions-exchange-2013-help.md">Active Directory split permissions</A>」を参照してください。Exchange のインストール時に Active Directory 分割型アクセス許可を使用しない場合は、Exchange は共有型アクセス許可を使用します。



## Microsoft Exchange コンテナーのアクセス許可

次の表に、構成パーティション内の Microsoft Exchange コンテナーに設定されるアクセス許可を示します。

### オブジェクトの識別名: CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<ドメイン\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>インストール アカウント</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フル コントロール</p></td>
<td><p></p></td>
<td><p>これは、<code>/PrepareAD</code> の実行時に使用されるアカウントです。</p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フル コントロール</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フル コントロール</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>読み取り</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>認証ユーザー</p></td>
<td><p>許可 ACE</p></td>
<td><p>なし</p></td>
<td><p>プロパティの読み取り</p>
<p>内容の一覧表示</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>アクセス許可の修正</p></td>
<td><p>msExchSmtpRceiveConnector</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>読み取り</p>
<p>オブジェクトの一覧表示</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>委任セットアップ</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>読み取り</p>
<p>オブジェクトの一覧表示</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Microsoft Exchange 自動検出コンテナーのアクセス許可

次の表に、構成パーティション内の Microsoft Exchange 自動検出コンテナーに設定されるアクセス許可を示します。

### オブジェクトの識別名: CN=Microsoft Exchange Autodiscover,CN=Services,CN=Configuration,DC=\<ドメイン\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>読み取り</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Microsoft Exchange 組織コンテナーのアクセス許可

このセクションのアクセス許可の表に、構成パーティション内の Microsoft Exchange 組織およびサブコンテナーに設定されるアクセス許可を示します。

### オブジェクトの識別名: CN=\<組織\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<ドメイン\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>エンタープライズの管理者</p>
<p>ルート ドメインの管理者</p>
<p>インストール アカウント</p>
<p>組織の管理</p></td>
<td><p>拒否 ACE</p></td>
<td><p>すべて</p></td>
<td><p>送信者</p>
<p>受信者</p></td>
<td><p></p></td>
<td><p>Windows 管理者はメールボックスを開くことが許可されません。</p></td>
</tr>
<tr class="even">
<td><p>エンタープライズの管理者</p>
<p>Schema Admins</p>
<p>ルート ドメインの管理者</p>
<p>インストール アカウント</p>
<p>組織の管理</p></td>
<td><p>拒否 ACE</p></td>
<td><p>すべて</p></td>
<td><p>Exchange Web サービスの偽装</p>
<p>Exchange Web サービス トークンのシリアル化</p></td>
<td><p></p></td>
<td><p>拡張された権利</p></td>
</tr>
<tr class="odd">
<td><p>エンタープライズの管理者</p>
<p>Schema Admins</p>
<p>ルート ドメインの管理者</p>
<p>インストール アカウント</p></td>
<td><p>拒否 ACE</p></td>
<td><p>すべて</p></td>
<td><p>ストアのトランスポート アクセス</p>
<p>ストアの制約付き委任</p>
<p>ストアの読み取りアクセス</p>
<p>ストアの読み取り/書き込みアクセス</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ローカル システム</p></td>
<td><p>許可</p></td>
<td><p>すべて</p></td>
<td><p>すべての拡張された権利</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>認証ユーザー</p></td>
<td><p>拒否 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p><code>msExchAvailabilityUserPassword / msExchAvailabilityAddressSpace</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>認証ユーザー</p></td>
<td><p>許可</p></td>
<td><p>なし</p></td>
<td><p>読み取り</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>アクセス許可の読み取り</p>
<p>内容の一覧表示</p>
<p>プロパティの読み取り</p>
<p>オブジェクトの一覧表示</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>アクセス許可の読み取り</p>
<p>内容の一覧表示</p>
<p>プロパティの読み取り</p>
<p>オブジェクトの一覧表示</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>NT Authority\Network Service</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>読み取り</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>可用性管理サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>アクセス許可の読み取り</p>
<p>内容の一覧表示</p>
<p>プロパティの読み取り</p>
<p>オブジェクトの一覧表示</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>すべての拡張された権利</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>groupType</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchOwningServer</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchMailboxSecurityDescriptor</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchUMServerWritableFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchDatabaseCreated</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchUserCulture</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchMobileMailboxFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>siteFolderGUID</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>siteFolderServer</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchEDBOffline</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>userCertificate</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchUMDtmfMap</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchBlockedSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>Public Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchPatchMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>publicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchUMSpokenName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchUMPinChecksum</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchSafeSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>thumbnailPhoto</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>最上位のパブリック フォルダーの作成</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>最上位のパブリック フォルダーの作成</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>インフォメーション ストアの状態の表示</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>インフォメーション ストアの状態の表示</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>インフォメーション ストアの管理</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>インフォメーション ストアの管理</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>インフォメーション ストア内での名前付きプロパティの作成</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>インフォメーション ストア内での名前付きプロパティの作成</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>パブリック フォルダー ACL の変更</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>パブリック フォルダー ACL の変更</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>パブリック フォルダー クォータの変更</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>パブリック フォルダー クォータの変更</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>パブリック フォルダー管理者 ACL の変更</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>パブリック フォルダー管理者 ACL の変更</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>パブリック フォルダーの有効期限の変更</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>パブリック フォルダーの有効期限の変更</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>パブリック フォルダーのレプリカ一覧の変更</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>パブリック フォルダーのレプリカ一覧の変更</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>パブリック フォルダーの削除済みアイテムの保存期間の変更</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>パブリック フォルダーの削除済みアイテムの保存期間の変更</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>パブリック フォルダーの作成</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>パブリック フォルダーの作成</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メールが有効なパブリック フォルダー</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>すべてのユーザー</p>
<p>NT Authority\Anonymous Logon</p>
<p></p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>インフォメーション ストア内での名前付きプロパティの作成</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>すべてのユーザー</p>
<p>NT Authority\Anonymous Logon</p>
<p></p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>パブリック フォルダーの作成</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>すべてのユーザー</p>
<p>NT Authority\Anonymous Logon</p>
<p></p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>アクセス許可の読み取り</p>
<p>内容の一覧表示</p>
<p>プロパティの読み取り</p>
<p>オブジェクトの一覧表示</p></td>
<td><p><code>/ msExchPrivateMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>すべてのユーザー</p>
<p>NT Authority\Anonymous Logon</p>
<p></p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>アクセス許可の読み取り</p>
<p>内容の一覧表示</p>
<p>プロパティの読み取り</p>
<p>オブジェクトの一覧表示</p></td>
<td><p><code>/ msExchPublicMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>アクセス許可の読み取り</p>
<p>内容の一覧表示</p>
<p>プロパティの読み取り</p>
<p>オブジェクトの一覧表示</p></td>
<td><p><code>/ siteAddressing</code></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### オブジェクトの識別名: CN=すべて Address Lists,CN=Address Lists Container,CN=\<組織\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>内容の一覧表示</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
<tr class="odd">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
</tbody>
</table>


### オブジェクトの識別名: CN=Offline Address Lists,CN=Address Lists Container, CN=\<組織\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>オフライン アドレス帳のダウンロード</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### オブジェクトの識別名: CN=Addressing,CN=\<組織\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>認証ユーザー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>読み取り</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### オブジェクトの識別名: CN=Recipient Policies,CN=\<組織\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
<tr class="even">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
</tbody>
</table>


## 構成パーティション コンテナーのアクセス許可

このセクションのアクセス許可の表に、構成パーティション内のさまざまなコンテナーに対して `Setup /PrepareAD` コマンドによって設定されるアクセス許可を示します。

### オブジェクトの識別名: CN=Sites,CN=Configuration,DC=\<ドメイン\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>組織の管理</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchVersion / site</code></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchVersion / site-link</code></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchPartnerId / site</code></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchMinorPartnerId / site</code></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchResponsibleforSites / site</code></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p></p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchTransportSiteFlags / site</code></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchCost / site-link</code></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p>
<p>Exchange Trusted Subsystem</p>
<p>ローカル システム</p>
<p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>アクセス許可の読み取り</p>
<p>内容の一覧表示</p>
<p>プロパティの読み取り</p>
<p>オブジェクトの一覧表示</p></td>
<td><p><code>/ msExchEdgeSyncEHFConnector</code></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p>
<p>Exchange Trusted Subsystem</p>
<p>ローカル システム</p>
<p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>アクセス許可の読み取り</p>
<p>内容の一覧表示</p>
<p>プロパティの読み取り</p>
<p>オブジェクトの一覧表示</p></td>
<td><p><code>/ msExchEdgeSyncMservConnector</code></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>子供</p></td>
<td><p>子の作成</p>
<p>子の削除</p>
<p>ツリーの削除</p></td>
<td><p><code>msExchEdgeSyncServiceConfig / site</code></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p>
<p>Exchange Trusted Subsystem</p>
<p>ローカル システム</p>
<p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>アクセス許可の読み取り</p>
<p>内容の一覧表示</p>
<p>プロパティの読み取り</p>
<p>オブジェクトの一覧表示</p></td>
<td><p><code>/ msExchEdgeSyncServiceConfig</code></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>子供</p></td>
<td><p>子の作成</p>
<p>子の削除</p>
<p>ツリーの削除</p></td>
<td><p><code>msExchEdgeSyncMservConnector / msExchEdgeSyncServiceConfig</code></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>子供</p></td>
<td><p>子の作成</p>
<p>子の削除</p>
<p>ツリーの削除</p></td>
<td><p><code>msExchEdgeSyncEHFConnector / msExchEdgeSyncServiceConfig</code></p></td>
</tr>
</tbody>
</table>


### オブジェクトの識別名: CN=Deleted Objects,CN=Configuration,DC=\<ドメイン\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>内容の一覧表示</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Organization Administration</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>読み取り</p>
<p>オブジェクトの一覧表示</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>インストール アカウント</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>アクセス許可の読み取り</p>
<p>書き込みアクセス許可</p>
<p>内容の一覧表示</p>
<p>プロパティの読み取り</p>
<p>オブジェクトの一覧表示</p></td>
<td><p></p></td>
<td><p>これは、<code>/PrepareAD</code> の実行時に使用されるアカウントです。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>読み取り</p>
<p>オブジェクトの一覧表示</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ネットワーク サービス</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>内容の一覧表示</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Exchange 管理グループのアクセス許可

`Setup /PrepareAD` コマンドでは、組織内の管理グループの以下のアクセス許可も構成されます。

### オブジェクトの識別名: CN=\<管理グループ\>,CN=Administrative Groups,CN=\<組織\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>受信者更新サービスへのアクセス</p></td>
<td><p><code>msExchExchangeServer</code></p></td>
<td><p>Exchange Recipient Administrators が受信者にプロキシ アドレス情報をスタンプすることが可能になります。</p></td>
</tr>
<tr class="even">
<td><p>ローカル システム</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>受信者更新サービスへのアクセス</p></td>
<td><p><code>msExchExchangeServer</code></p></td>
<td><p>サーバーが受信者にプロキシ アドレス情報をスタンプすることが可能になります。</p></td>
</tr>
<tr class="odd">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>受信者更新サービスへのアクセス</p></td>
<td><p><code>msExchExchangeServer</code></p></td>
<td><p>Exchange Public Folder Administrators が受信者にプロキシ アドレス情報をスタンプすることが可能になります。</p></td>
</tr>
</tbody>
</table>


### オブジェクトの識別名: CN=Advanced Security Settings,CN=\<管理グループ\>,CN=Administrative Groups,CN=\<組織\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>許可 ACE</p></td>
<td><p>なし</p></td>
<td><p>内容の一覧表示</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### オブジェクトの識別名: CN=Encryption,CN=Advanced Security Settings,CN=\<管理グループ\>,CN=Administrative Groups,CN=\<組織\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>許可 ACE</p></td>
<td><p>なし</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### オブジェクトの識別名: CN=Arrays,CN=\<管理グループ\>,CN=Administrative Groups,CN=\<組織\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>許可 ACE</p></td>
<td><p>なし</p></td>
<td><p>内容の一覧表示</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### オブジェクトの識別名: CN=Database Availability Groups,CN=\<管理グループ\>,CN=Administrative Groups,CN=\<組織\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>許可 ACE</p></td>
<td><p>なし</p></td>
<td><p>内容の一覧表示</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### オブジェクトの識別名: CN=Databases,CN=\<管理グループ\>,CN=Administrative Groups,CN=\<組織\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>許可 ACE</p></td>
<td><p>なし</p></td>
<td><p>内容の一覧表示</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### オブジェクトの識別名: CN=Servers,CN=\<管理グループ\>,CN=Administrative Groups,CN=\<組織\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>拒否 ACE</p></td>
<td><p>すべて</p></td>
<td><p>受信者</p></td>
<td><p></p></td>
<td><p>Exchange サーバーはメールボックスを開くことが許可されません。</p></td>
</tr>
<tr class="even">
<td><p>認証ユーザー</p></td>
<td><p>許可 ACE</p></td>
<td><p>なし</p></td>
<td><p>内容の一覧表示</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Microsoft Exchange セキュリティ グループ コンテナーのアクセス許可

このセクションのアクセス許可の表に、ルート ドメイン パーティション内の Microsoft Exchange セキュリティ グループ コンテナーに設定されるアクセス許可を示します。

### オブジェクトの識別名: OU=Microsoft Exchange Security Groups,DC=\<ルート ドメイン\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フル コントロール</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>子の作成</p></td>
<td><p><code>/ Group</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>削除</p></td>
<td><p><code>/ group</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>Member / group</code></p></td>
</tr>
</tbody>
</table>


### オブジェクトの識別名: CN=Organization Management,OU=Microsoft Exchange Security Groups,DC=\<ルート ドメイン\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フル コントロール</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### オブジェクトの識別名: CN=パブリック フォルダーの管理,OU=Microsoft Exchange Security Groups,DC=\<ルート ドメイン\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フル コントロール</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### オブジェクトの識別名: CN=ExchangeLegacyInterop,OU=Microsoft Exchange Security Groups,DC=\<ルート ドメイン\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フル コントロール</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### オブジェクトの識別名: CN=Exchange Servers,OU=Microsoft Exchange Security Groups,DC=\<ルート ドメイン\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フル コントロール</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Root Domain Administrators</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メンバーの読み取り</p>
<p>メンバーの書き込み</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Child Domain Administrators</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メンバーの読み取り</p>
<p>メンバーの書き込み</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## ドメインの準備

次の表に、`Setup /PrepareDomain` コマンドを実行するときに設定されるアクセス許可を示します。


> [!NOTE]
> このセクションで説明されているアクセス許可は、既定のアクセス許可であり、共有型アクセス許可モデルを使用して Exchange 2013 を展開する場合に構成されます。Active Directory 分割型アクセス許可モデルを使用して Exchange 2013 を展開した場合、既定のアクセス許可は異なります。Active Directory 分割型アクセス許可、共有アクセス許可モデル、分割型アクセス許可モデルを使用する場合の、一般的な既定のアクセス許可の変更の詳細については、「<A href="understanding-split-permissions-exchange-2013-help.md">分割型アクセス許可について</A>」の「<A href="understanding-split-permissions-exchange-2013-help.md">Active Directory split permissions</A>」を参照してください。Exchange のインストール時に Active Directory 分割型アクセス許可を使用しない場合は、Exchange は共有型アクセス許可を使用します。



### オブジェクトの識別名: DC=\<ドメイン\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>認証ユーザー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p>トランスポート サービスの読み取りアクセス許可を付与します。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>groupType</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchMailboxSecurityDescriptor</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchUMServerWritableFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchUserCultulre</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p><code>memberOf</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p><code>canonicalName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>レプリケーションの同期</p></td>
<td><p></p></td>
<td><p>拡張された権利</p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>子の作成</p>
<p>子の削除</p>
<p>子のリスト</p></td>
<td><p><code>msExchActiveSyncDevices / User</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>子の作成</p>
<p>子の削除</p>
<p>子のリスト</p></td>
<td><p><code>msExchActiveSyncDevices / inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchSafeSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchMobileMailboxFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchSafeRecipientsHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>userCertificate</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchUMDtmfMap</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchBlockedSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchUMSpokenName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchUMPinChecksum</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>thumbnailPhoto</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>読み取り</p>
<p>オブジェクトの一覧表示</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フル コントロール</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>読み取り</p>
<p>オブジェクトの一覧表示</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>Public Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フル コントロール</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>pwdLastSet</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>WriteDACL</p></td>
<td><p><code>/ user</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>WriteDACL</p>
<p></p></td>
<td><p><code>/ inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>ツリーの削除</p></td>
<td><p><code>/ user</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>ツリーの削除</p>
<p></p></td>
<td><p><code>/ inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>sAMAccountName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>子の作成</p>
<p>削除</p></td>
<td><p><code>/ contact</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>子の作成</p>
<p>削除</p></td>
<td><p><code>/ inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>子の作成</p>
<p>削除</p></td>
<td><p><code>/ user</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>子の作成</p>
<p>削除</p></td>
<td><p><code>/ organizationUnit</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>子の作成</p>
<p>削除</p></td>
<td><p><code>/ group</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>子の作成</p>
<p>子の削除</p></td>
<td><p><code>/ computer</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>Member</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>wwwHomePage</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>countryCode</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>managedBy</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>次回のログオン時にパスワードをリセット</p></td>
<td><p></p></td>
<td><p>拡張された権利</p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>パスワードの変更</p></td>
<td><p><code> / user</code></p></td>
<td><p>拡張された権利</p></td>
</tr>
<tr class="odd">
<td><p>委任セットアップ</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p><code>User Account Restrictions</code></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### オブジェクトの識別名: CN=AdminSDHolder,CN=System,DC=\<ドメイン\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>認証ユーザー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p>トランスポート サービスの読み取りアクセス許可を付与します。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>groupType</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchMailboxSecurityDescriptor</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchUMServerWritableFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchUserCultulre</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p><code>memberOf</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p><code>canonicalName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>レプリケーションの同期</p></td>
<td><p></p></td>
<td><p>拡張された権利</p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>子の作成</p>
<p>子の削除</p>
<p>子のリスト</p></td>
<td><p><code>msExchActiveSyncDevices / User</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>子の作成</p>
<p>子の削除</p>
<p>子のリスト</p></td>
<td><p><code>msExchActiveSyncDevices / inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchSafeSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchMobileMailboxFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchSafeRecipientsHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>userCertificate</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchUMDtmfMap</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchBlockedSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchUMSpokenName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchUMPinChecksum</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>thumbnailPhoto</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>読み取り</p>
<p>オブジェクトの一覧表示</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フル コントロール</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>読み取り</p>
<p>オブジェクトの一覧表示</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>Public Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フル コントロール</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>pwdLastSet</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>sAMAccountName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>Member</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>wwwHomePage</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>countryCode</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows アクセス許可</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>managedBy</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>委任セットアップ</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p><code>User Account Restrictions</code></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### オブジェクトの識別名: CN=Deleted Objects,DC=\<ドメイン\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>内容の一覧表示</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### オブジェクトの識別名: CN=Microsoft Exchange System Objects,DC=\<ドメイン\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの読み取り</p>
<p>内容の一覧表示</p>
<p>アクセス許可の読み取り</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>認証ユーザー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>アクセス許可の読み取り</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>認証ユーザー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
</tr>
<tr class="even">
<td><p>認証ユーザー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p><code>adminDisplayName</code></p></td>
</tr>
<tr class="odd">
<td><p>認証ユーザー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p><code>modifyTimeStamp</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>拒否 ACE</p></td>
<td><p>すべて</p></td>
<td><p>ツリーの削除</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>アクセス許可の読み取り</p>
<p>内容の一覧表示</p>
<p>PropertyDelete ツリーの読み込み</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>子の作成</p>
<p></p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>子の作成</p>
<p>子の削除</p></td>
<td><p><code>/ publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>子の作成</p>
<p></p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>子の削除</p>
<p></p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>子の削除</p>
<p></p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>/ publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>パスワードの変更</p>
<p>次回のログオン時にパスワードをリセット</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>アクセス許可の読み取り</p>
<p>内容の一覧表示</p>
<p>プロパティの読み取り</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>子の作成</p>
<p>子の削除</p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>子の作成</p>
<p>子の削除</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>mail / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>displayNamePrintable / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>displayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>textEncodedORAddress / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>proxyAddresses / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>cn / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>showInAddressBook / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>Exchange Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p>legacyExchangeDN / publicFolder</p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>Exchange Personal Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>msDSPhoneticDisplayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>msExchPFContacts / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>garbageCollPeriod / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>name / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>msExchPublicDelegates / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>アクセス許可の読み取り</p>
<p>内容の一覧表示</p>
<p>プロパティの読み取り</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>mail / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>displayNamePrintable / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>displayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>textEncodedORAddress / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>proxyAddresses / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>cn / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>showInAddressBook / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>Exchange Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>legacyExchangeDN / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>Exchange Personal Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>msDSPhoneticDisplayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>msExchPFContacts / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>garbageCollPeriod / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>name / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>パブリック フォルダー管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>msExchPublicDelegates / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>アクセス許可の読み取り</p>
<p>内容の一覧表示</p>
<p>プロパティの読み取り</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>mail / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>displayNamePrintable / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>displayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>textEncodedORAddress / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>proxyAddresses / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>cn / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>showInAddressBook / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>Exchange Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>legacyExchangeDN / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>Exchange Personal Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>msDSPhoneticDisplayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>msExchPFContacts / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>garbageCollPeriod / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>name / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p>
<p>プロパティの書き込み</p></td>
<td><p><code>msExchPublicDelegates / publicFolder</code></p></td>
</tr>
</tbody>
</table>


### オブジェクトの識別名: CN=Exchange Install Domain Servers,CN=Microsoft Exchange System Objects,DC=\<ドメイン\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フル コントロール</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## サーバーの役割インストール

クライアント アクセスとメールボックスの各サーバーの役割のインストール時に、ローカル コンピューターの管理者セキュリティ グループに "組織の管理" USG が追加されます。これにより、"組織の管理" という名前の管理役割グループのメンバーがサーバーを管理できるようになります。

次のアクセス許可の表に、クライアント アクセスまたはメールボックスのサーバーの役割をインストールするときに設定されるアクセス許可を示します。

### オブジェクトの識別名: CN=\<サーバー\>,CN=Servers,CN=\<管理グループ\>,CN=Administrative Groups,CN=\<組織\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MACHINE$</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>アクセス許可の読み取り</p>
<p>内容の一覧表示</p>
<p>プロパティの読み取り</p>
<p>オブジェクトの一覧表示</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>MACHINE$</p></td>
<td><p>許可 ACE</p></td>
<td><p>なし</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p><code>msExchServerSite</code></p>
<p><code>msExchEdgeSyncCredential</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>ストアのトランスポート アクセス</p>
<p>ストアの制約付き委任</p>
<p>ストアの読み取り専用アクセス</p>
<p>ストアの読み取り/書き込みアクセス</p></td>
<td><p></p></td>
<td><p>拡張された権利</p></td>
</tr>
<tr class="even">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>Exchange Web サービス トークンのシリアル化</p></td>
<td><p></p></td>
<td><p>拡張された権利</p>
<p>メールボックス サーバーの役割オブジェクトにのみ付与します。</p></td>
</tr>
<tr class="odd">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>アクセス許可の読み取り</p>
<p>内容の一覧表示</p>
<p>プロパティの読み取り</p>
<p>オブジェクトの一覧表示</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ローカル システム</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>アクセス許可の読み取り</p>
<p>内容の一覧表示</p>
<p>プロパティの読み取り</p>
<p>オブジェクトの一覧表示</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>委任セットアップ</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フル コントロール</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>委任セットアップ</p></td>
<td><p>拒否 ACE</p></td>
<td><p>すべて</p></td>
<td><p>子の作成</p>
<p>子の削除</p></td>
<td><p><code>/ msExchPublicMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>認証ユーザー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>委任セットアップ</p></td>
<td><p>拒否 ACE</p></td>
<td><p>すべて</p></td>
<td><p>受信者</p>
<p>送信者</p></td>
<td><p></p></td>
<td><p>拡張された権利</p></td>
</tr>
</tbody>
</table>


## データベース可用性グループ

このセクションのアクセス許可の表では、データベース可用性グループおよびそのメンバーに関して設定されたアクセス許可を示します。

### オブジェクトの識別名: CN=\<DAGName\>,CN=Database Availability Groups,CN=\<管理グループ\>,CN=Administrative Groups,CN=\<組織\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>許可 ACE</p></td>
<td><p>なし</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## エッジ トランスポート

エッジ トランスポート サーバーをインストールし、Exchange 組織とのエッジ サブスクリプションを確立する場合、エッジ トランスポート サーバーを組織にインストールするときに、次のアクセス許可の表に示されているアクセス許可が設定されます。

### オブジェクトの識別名: CN=\<サーバー\>,CN=Servers,CN=\<管理グループ\>,CN=Administrative Groups,CN=\<組織\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>プロパティの書き込み</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>認証ユーザー</p></td>
<td><p>許可 ACE</p></td>
<td><p>なし</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p></p></td>
<td><p>ACE が <code>msExchExchangeServer</code> クラス オブジェクト <code>defaultSecurityDescriptor</code> のスキーマで定義されます。</p></td>
</tr>
</tbody>
</table>


## メールボックス サーバーのインストール

まだ存在しない場合、メールボックス サーバーの初回インストール時に、以下のコンテナーが作成されます。次のアクセス許可の表に、適用されるアクセス許可を示します。

### オブジェクトの識別名: CN=Availability Configuration,CN=\<組織\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>指定</p></td>
<td><p>プロパティの読み取り</p></td>
<td><p><code>msExchAvailabilityUserPassword / msExchAvailabilityAddressSpaceObjects</code></p></td>
<td><p>拡張された権利</p></td>
</tr>
</tbody>
</table>


### オブジェクトの識別名: CN=Default \<サーバー\>,CN=SMTP Receive Connectors,CN=Protocols,CN=\<サーバー\>,CN=Servers,CN=\<管理グループ\>,CN=\<組織\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>拒否 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フォレスト ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>拒否 ACE</p></td>
<td><p>すべて</p></td>
<td><p>組織ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>すべての送信者を受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>すべての送信者を受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>すべての送信者を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知のセキュリティ識別子 (SID) です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>すべての送信者を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>すべての送信者を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、外部的にセキュリティで保護されたサーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>EXCH50 を受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>EXCH50 を受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>EXCH50 を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>EXCH50 を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>EXCH50 を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、外部的にセキュリティで保護されたサーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージを任意の受信者に発信する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージを任意の受信者に発信する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージを任意の受信者に発信する</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージを任意の受信者に発信する</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージを任意の受信者に発信する</p></td>
<td><p></p></td>
<td><p>これは、外部的にセキュリティで保護されたサーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XShadow の許可</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XShadow の許可</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>ルーティング ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>ルーティング ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>ルーティング ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>ルーティング ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>ルーティング ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p>これは、外部的にセキュリティで保護されたサーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XSessionParams を受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XSessionParams を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XSessionParams を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フォレスト ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フォレスト ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フォレスト ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XAttr を受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XAttr を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XAttr を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XProxyFrom を受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フォレスト XProxyFrom を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フォレスト XProxyFrom を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XSysProbe を受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フォレスト XSysProbe を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フォレスト XSysProbe を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XMessageContext 拡張プロパティを送信する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XMessageContext 拡張プロパティを送信する</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XMessageContext 拡張プロパティを送信する</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XMessageContext 高速インデックスを送信する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XMessageContext 高速インデックスを送信する</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XMessageContext 高速インデックスを送信する</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XMessageContext AD 受信者キャッシュを送信する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XMessageContext AD 受信者キャッシュを送信する</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XMessageContext AD 受信者キャッシュを送信する</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>認証フラグを受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>認証フラグを受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>認証フラグを受け入れる</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>認証フラグを受け入れる</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>認証フラグを受け入れる</p></td>
<td><p></p></td>
<td><p>これは、外部的にセキュリティで保護されたサーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>スパム対策を省略する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>スパム対策を省略する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>スパム対策を省略する</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>スパム対策を省略する</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>スパム対策を省略する</p></td>
<td><p></p></td>
<td><p>これは、外部的にセキュリティで保護されたサーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージ サイズの制限を省略する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージ サイズの制限を省略する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージ サイズの制限を省略する</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージ サイズの制限を省略する</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージ サイズの制限を省略する</p></td>
<td><p></p></td>
<td><p>これは、外部的にセキュリティで保護されたサーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>組織ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>組織ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>組織ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージをサーバーに発信する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージをサーバーに発信する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージをサーバーに発信する</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージをサーバーに発信する</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージをサーバーに発信する</p></td>
<td><p></p></td>
<td><p>これは、外部的にセキュリティで保護されたサーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>権限のあるドメインの送信者を受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>権限のあるドメインの送信者を受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>権限のあるドメインの送信者を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>権限のあるドメインの送信者を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>権限のあるドメインの送信者を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、外部的にセキュリティで保護されたサーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>認証ユーザー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージを任意の受信者に発信する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>認証ユーザー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>ルーティング ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>認証ユーザー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>スパム対策を省略する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>認証ユーザー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージをサーバーに発信する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### オブジェクトの識別名: CN=Client \<サーバー\>,CN=SMTP Receive Connectors,CN=Protocols,CN=\<サーバー\>,CN=Servers,CN=\<管理グループ\>,CN=\<組織\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>認証ユーザー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージを任意の受信者に発信する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>認証ユーザー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>ルーティング ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>認証ユーザー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>スパム対策を省略する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>認証ユーザー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージをサーバーに発信する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XSessionParams を受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XSessionParams を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XSessionParams を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>すべての送信者を受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>すべての送信者を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知のセキュリティ識別子 (SID) です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>すべての送信者を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>すべての送信者を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、外部的にセキュリティで保護されたサーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>Exch50 を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>Exch50 を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>Exch50 を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、外部的にセキュリティで保護されたサーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>Exch50 を受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージを任意の受信者に発信する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージを任意の受信者に発信する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージを任意の受信者に発信する</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージを任意の受信者に発信する</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージを任意の受信者に発信する</p></td>
<td><p></p></td>
<td><p>これは、外部的にセキュリティで保護されたサーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XShadow の許可</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XShadow の許可</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>ルーティング ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>ルーティング ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>ルーティング ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>ルーティング ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>ルーティング ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p>これは、外部的にセキュリティで保護されたサーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フォレスト ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フォレスト ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フォレスト ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XAttr を受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XAttr を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XAttr を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XProxyFrom を受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フォレスト XProxyFrom を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フォレスト XProxyFrom を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>認証フラグを受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>認証フラグを受け入れる</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>認証フラグを受け入れる</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>認証フラグを受け入れる</p></td>
<td><p></p></td>
<td><p>これは、外部的にセキュリティで保護されたサーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XSysProbe を受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フォレスト XSysProbe を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フォレスト XSysProbe を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>認証フラグを受け入れる</p></td>
<td><p></p></td>
<td><p>これは、外部的にセキュリティで保護されたサーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>スパム対策を省略する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>スパム対策を省略する</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>スパム対策を省略する</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>スパム対策を省略する</p></td>
<td><p></p></td>
<td><p>これは、外部的にセキュリティで保護されたサーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XMessageContext 拡張プロパティを送信する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XMessageContext 拡張プロパティを送信する</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XMessageContext 拡張プロパティを送信する</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XMessageContext 高速インデックスを送信する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XMessageContext 高速インデックスを送信する</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XMessageContext 高速インデックスを送信する</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージ サイズの制限を省略する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージ サイズの制限を省略する</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージ サイズの制限を省略する</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージ サイズの制限を省略する</p></td>
<td><p></p></td>
<td><p>これは、外部的にセキュリティで保護されたサーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>組織ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>組織ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>組織ヘッダーを受け入れる</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XMessageContext AD 受信者キャッシュを送信する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XMessageContext AD 受信者キャッシュを送信する</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XMessageContext AD 受信者キャッシュを送信する</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージをサーバーに発信する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージをサーバーに発信する</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージをサーバーに発信する</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>メッセージをサーバーに発信する</p></td>
<td><p></p></td>
<td><p>これは、外部的にセキュリティで保護されたサーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>権限のあるドメインの送信者を受け入れる</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>権限のあるドメインの送信者を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>権限のあるドメインの送信者を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>権限のあるドメインの送信者を受け入れる</p></td>
<td><p></p></td>
<td><p>これは、外部的にセキュリティで保護されたサーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## SMTP 送信コネクタの作成

次の表に、送信コネクタの作成時に設定されるアクセス許可を示します。

### オブジェクトの識別名: CN=\<コネクタ名\>,CN=Connections,CN=\<ルーティング グループ\>,CN=Routing Groups, CN=\<管理グループ\>,CN=\<組織\>

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
<th>アカウント</th>
<th>ACE の種類</th>
<th>継承</th>
<th>アクセス許可</th>
<th>プロパティ/適用先</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NT AUTHORITY\ANONYMOUS LOGON</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>ルーティング ヘッダーを送信する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>組織ヘッダーを送信する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>組織ヘッダーを送信する</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>組織ヘッダーを送信する</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フォレスト ヘッダーを送信する</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フォレスト ヘッダーを送信する</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>フォレスト ヘッダーを送信する</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XShadow の送信</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XShadow の送信</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>XShadow の送信</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>ルーティング ヘッダーを送信する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-10</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>ルーティング ヘッダーを送信する</p></td>
<td><p></p></td>
<td><p>これは、パートナー サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>ルーティング ヘッダーを送信する</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>ルーティング ヘッダーを送信する</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>ルーティング ヘッダーを送信する</p></td>
<td><p></p></td>
<td><p>これは、外部的にセキュリティで保護されたサーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-24</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>ルーティング ヘッダーを送信する</p></td>
<td><p></p></td>
<td><p>これは、従来の Exchange サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>Exch50 を送信する</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>Exch50 を送信する</p></td>
<td><p></p></td>
<td><p>これは、メールボックス サーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>Exch50 を送信する</p></td>
<td><p></p></td>
<td><p>これは、エッジ トランスポート サーバー用の既知の SID です。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>Exch50 を送信する</p></td>
<td><p></p></td>
<td><p>これは、外部的にセキュリティで保護されたサーバー用の既知の SID です。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-24</p></td>
<td><p>許可 ACE</p></td>
<td><p>すべて</p></td>
<td><p>Exch50 を送信する</p></td>
<td><p></p></td>
<td><p>これは、従来の Exchange サーバー用の既知の SID です。</p></td>
</tr>
</tbody>
</table>

