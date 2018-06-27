---
title: 'Office Communications Server 2007 R2 および Lync Server との共存: Exchange 2013 Help'
TOCTitle: Office Communications Server 2007 R2 および Lync Server との共存
ms:assetid: f12d65c7-0b2c-46a1-a14a-802a76296fa1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ851069(v=EXCHG.150)
ms:contentKeyID: 50555895
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Office Communications Server 2007 R2 および Lync Server との共存

 

_**適用先:**Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:**2015-03-09_

Communications Server 2007 R2 および Lync Server は、インスタント メッセージング (IM)、プレゼンス、マルチパーティ IM を含む、数多くのエンド ユーザー機能を提供します。また、これらのボイス メール機能は、Exchange ユニファイド メッセージング (UM)と統合できます。Lync Server 2010 または 2013 を統合する展開では、ユーザーをエンタープライズ VoIP に対して有効にすることができます。これにより、ボイス メールが有効なユーザーは Lync Server コンポーネントを使用してそのボイス メールにアクセスできます。

UM を Office Communications Server または Lync Server の以前のバージョンと統合している場合は、一部の機能を使用できません。高解像度フォト、統合連絡先ストア、Lync Archiving Integration などの、新しい拡張エンドユーザー機能を全面的に活用するには、ユーザーが Lync Server 2013 および Exchange Server 2013 上でユーザー アカウントを持ち、最新バージョンの Lync 2013 クライアント ソフトウェアを使用する必要があります。たとえば、Lync Server 2010 上のエンタープライズ VoIP で有効になっているユーザーは統合連絡先ストアを使用できません。同じように、Lync 2010 では、高解像度フォトは表示できません。

Exchange UM と Office Communications Server 2007 R2 または Lync Server 2010 を統合している場合は、組織で展開されている Office Communications Server 2007 R2 または Lync 2010 サーバーに追加修正プログラム、ロールアップ、累積的な更新プログラム、およびサービス パックをインストールする必要があります。インストールする必要があるプログラムは、展開技術や Exchange UM と統合する製品バージョンによって異なります。

## 必要な修正プログラム、ロールアップ、累積的な更新プログラム、およびサービス パック

次の表では、UM との統合のために各製品バージョンで必要な修正プログラムを示します。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Office Communications Server 2007 R2</p></td>
<td><p>Office Communications Server 2007 R2 累積的更新プログラム 10 以降。</p></td>
</tr>
<tr class="even">
<td><p>Lync Server 2010</p></td>
<td><p>Lync Server 2010 累積的更新プログラム 3 以降。</p></td>
</tr>
<tr class="odd">
<td><p>Lync Server 2013</p></td>
<td><p>更新プログラムは必要ありません。</p></td>
</tr>
</tbody>
</table>

