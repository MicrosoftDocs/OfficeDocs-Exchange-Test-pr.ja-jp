---
title: 'Outlook 2016 for Mac によるパブリック フォルダーへのアクセス: Exchange Online Help'
TOCTitle: Outlook 2016 for Mac によるパブリック フォルダーへのアクセス
ms:assetid: bc9b8226-bd8b-4edc-882b-4f19cfe118eb
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Mt788631(v=EXCHG.150)
ms:contentKeyID: 74115362
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook 2016 for Mac によるパブリック フォルダーへのアクセス

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016, Office 365_

**概要**:ユーザーによるパブリック フォルダーへのアクセスを可能にする、Outlook 2016 for Mac でサポートされている最新の Exchange トポロジ。

Outlook 2016 for Mac クライアントの [2016 年 4 月の更新](https://go.microsoft.com/fwlink/?linkid=82920) のリリース、[Exchange 2013 の累積的な更新プログラム 14 (CU14)](https://go.microsoft.com/fwlink/p/?linkid=84943)、[Exchange 2016 の累積的な更新プログラム 2 (CU 2)](https://go.microsoft.com/fwlink/p/?linkid=84979) により、Outlook 2016 for Mac のユーザーはこれまで以上の種類のトポロジでパブリック フォルダーにアクセスできるようになりました。

## Outlook for Mac の制限事項

すべてのバージョンの Outlook for Mac は Exchange のパブリック フォルダーにアクセスできますが、これらのクライアントは最近まで、次の展開シナリオではパブリック フォルダーにアクセスできませんでした。

  - **従来のパブリック フォルダーとの共存。**ユーザーのメールボックスが Exchange 2013 または Exchange 2016 サーバーにある場合、ユーザーは Outlook for Mac を使って、Exchange 2010 SP3 以降を実行しているサーバー上に配置されたパブリック フォルダーにアクセスできませんでした。他のクライアントは、このシナリオでこれらの従来のパブリック フォルダーにアクセスできます。

  - **ハイブリッド トポロジ。**Exchange Online をベースとするメールボックスを利用するオンプレミスのユーザーは、Outlook for Mac を使ってオンプレミスの最新のパブリック フォルダーにアクセスすることはできませんでした。同様に、Exchange 2013 または Exchange 2016 のオンプレミスのメールボックスを使っているユーザーは、Outlook for Mac を使って Exchange Online に配置されたパブリック フォルダーにアクセスできませんでした。

## Outlook 2016 for Mac

Outlook 2016 for Mac の 2016 年 4 月の更新、さらに Exchange 2013 の CU14 および Exchange 2016 の CU2 によって、上記のシナリオにおいて Outlook 2016 for Mac クライアントを使えるようになりました。

次の表は、Outlook 2016 for Mac クライアントのユーザーが Exchange 2013、Exchange 2016、および Exchange Online のパブリック フォルダーにアクセスする場合にサポートされるトポロジをまとめたものです。


> [!NOTE]
> 次の表に示すシナリオでは、Outlook 2016 for Mac の 2016 年 4 月更新プログラムがすべてのクライアントに適用されているものとします。




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
<th>パブリック フォルダーの配置先</th>
<th>ユーザーのメールボックスが Exchange 2010 SP3 以降にある</th>
<th>ユーザーのメールボックスが Exchange 2013 CU13 以降にある</th>
<th>ユーザーのメールボックスが Exchange 2016 CU2 以降にある</th>
<th>ユーザーのメールボックスが Office 365/Exchange Online にある</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2010 SP3 以降</p></td>
<td><p>サポートされている</p></td>
<td><p>サポートされている</p></td>
<td><p>サポートされている</p></td>
<td><p>サポート対象外</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server 2013 CU13 以降</p></td>
<td><p>サポート対象外</p></td>
<td><p>サポートされている</p></td>
<td><p>サポートされている</p></td>
<td><p>サポートされている</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server 2016 CU2 以降</p></td>
<td><p>サポート対象外</p></td>
<td><p>サポートされている</p></td>
<td><p>サポートされている</p></td>
<td><p>サポートされている</p></td>
</tr>
<tr class="even">
<td><p>Office 365 / Exchange Online</p></td>
<td><p>サポート対象外</p></td>
<td><p>サポートされている</p></td>
<td><p>サポートされている</p></td>
<td><p>サポートされている</p></td>
</tr>
</tbody>
</table>


次の記事では、共存トポロジまたはハイブリッド トポロジで Exchange 組織内のパブリック フォルダーを展開する方法について説明します。Outlook 2016 for Mac クライアントに 2016 年 4 月の更新プログラムをインストールしていれば、ユーザーは次の資料に記載されている構成内のパブリック フォルダーにアクセスできます。

  - [ユーザー メールボックスが Exchange 2013 サーバー上に存在するレガシ パブリック フォルダーを構成する](configure-legacy-public-folders-where-user-mailboxes-are-on-exchange-2013-servers-exchange-2013-help.md)

  - [ハイブリッド展開用に Exchange 2013 パブリック フォルダーを構成する](configure-exchange-2013-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)

  - [ハイブリッド展開用に Exchange Online パブリック フォルダーを構成する](configure-exchange-online-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)

