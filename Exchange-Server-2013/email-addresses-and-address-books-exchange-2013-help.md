---
title: '電子メール アドレスとアドレス帳: Exchange 2013 Help'
TOCTitle: 電子メール アドレスとアドレス帳
ms:assetid: b97d0f68-691a-42af-9a6c-4dcc37b28a42
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657488(v=EXCHG.150)
ms:contentKeyID: 49896438
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 電子メール アドレスとアドレス帳

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

受信者 (ユーザー、リソース、連絡先、およびグループを含む) は、Microsoft Exchange がメッセージを配信またはルーティングできる Active Directory 内のメールが有効な任意のオブジェクトです。受信者が電子メール メッセージを送受信するには、電子メール アドレスが必要です。アドレス帳は、ユーザーが電子メールを互いに送信する相手を見つける方法です。アドレス帳を整理するためには、多くの方法があります。Exchange サーバー 2013 のアドレス帳機能の詳細な説明は、「主要な関連用語」を参照してください。

## 主要な関連用語

次の用語は、Exchange サーバー 2013 の電子メール アドレスおよびアドレス帳と関連付けられたコア コンポーネントの定義を示します。

  - **アドレス帳のポリシー**  
    アドレス帳ポリシー (ABP) によって、ユーザーを特定のグループに分割し、組織のグローバル アドレス一覧 (GAL) をカスタマイズ表示することができます。ABP の作成時には、GAL、オフライン アドレス帳 (OAB)、会議室一覧、1 つ以上のアドレス一覧をポリシーに割り当てます。次に ABP をメールボックス ユーザーに割り当て、カスタマイズされた GAL にメールボックス ユーザーが Outlook と Outlook Web App でアクセスできるようにします。目標は、複数の GAL を必要とする社内組織で GAL セグメンテーションを完成するメカニズムを単純にすることです。

<!-- end list -->

  - **アドレス一覧**  
    アドレス一覧は、GAL のサブセットです。各アドレス一覧は、メールが有効な受信者（1 つ以上の種類）の集合になっています（たとえば、ユーザー、連絡先、グループ、パブリック フォルダー、会議、その他のリソース）。アドレス一覧を利用すると受信者とリソースを整理できるので、必要な受信者やリソースを簡単に見つけられるようになります。アドレス一覧は動的に更新されます。したがって、新しい受信者が組織に追加されると、その受信者は自動的に適切なアドレス一覧に追加されます。

<!-- end list -->

  - **電子メール アドレス ポリシー**  
    電子メール アドレス ポリシーによって、受信者のプライマリ電子メール アドレスとセカンダリ電子メール アドレスが生成され、電子メールを送受信できるようになります。既定では、Exchange にはメールが有効な各ユーザー向けの電子メール アドレス ポリシーが含まれています。

<!-- end list -->

  - **階層型アドレス帳**  
    階層型アドレス帳（HAB）では、エンドユーザーが上下関係や管理構造などの組織階層を使用してアドレス帳の受信者を参照できます。通常、ユーザーは既定の GAL と関連付けられた受信者のプロパティに限定され、GAL の構造には組織内の受信者の管理関係や上下関係がたいてい正しく反映されません。組織の一意のビジネス構造にマッピングされる HAB をカスタマイズできることで、ユーザーが内部の受信者を効率的に検索できます。

<!-- end list -->

  - **オフライン アドレス帳**  
    オフライン アドレス帳 (OAB) はダウンロードされたアドレス一覧の集合のコピーであり、Microsoft Outlook ユーザーはサーバーに接続していないときでも OAB の情報にアクセスできます。

## 電子メール アドレスおよびアドレス帳のアクセス許可

次の表は、Exchange 2013 の電子メール アドレスおよびアドレス帳について理解し管理するのに役立つトピックへのリンクを示しています。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/ja-jp/exchange/address-books/address-lists/address-lists">アドレス一覧</a></p></td>
<td><p>受信者を整理し、エンドユーザーにアクセスしやすくするためのアドレス一覧および GAL の詳細情報:</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/ja-jp/exchange/address-books/address-book-policies/address-book-policies">アドレス帳ポリシー</a></p></td>
<td><p>アドレス一覧および GAL を別々の仮想組織に区分するための詳細情報:</p></td>
</tr>
<tr class="odd">
<td><p><a href="details-templates-exchange-2013-help.md">詳細テンプレート</a></p></td>
<td><p>Outlook のアドレス カードをカスタマイズするための詳細情報:</p></td>
</tr>
<tr class="even">
<td><p><a href="email-address-policies-exchange-2013-help.md">電子メール アドレス ポリシー</a></p></td>
<td><p>受信者を見つけやすくするプロキシ電子メール アドレスについての詳細情報:</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/ja-jp/exchange/address-books/hierarchical-address-books/hierarchical-address-books">階層型アドレス帳</a></p></td>
<td><p>組織固有のビジネス構造に合わせて GAL およびアドレス一覧をカスタマイズするための詳細情報:</p></td>
</tr>
<tr class="even">
<td><p><a href="offline-address-books-exchange-2013-help.md">オフライン アドレス帳</a></p></td>
<td><p>組織のアドレス一覧へのオフライン アクセスをユーザーに認めるための詳細情報:</p></td>
</tr>
</tbody>
</table>

