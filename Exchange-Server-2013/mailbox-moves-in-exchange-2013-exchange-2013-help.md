---
title: 'Exchange 2013 でのメールボックスの移動: Exchange 2013 Help'
TOCTitle: Exchange 2013 でのメールボックスの移動
ms:assetid: 9c0a0bc9-2a39-4cf0-aa6e-6e5ef3fd38b5
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ150543(v=EXCHG.150)
ms:contentKeyID: 48269852
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 でのメールボックスの移動

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-07_

メールボックスを移動する場合、*ソース メールボックス データベース* から *ターゲット メールボックス データベース* に移動します。ターゲット メールボックス データベースは、同じサーバー、別のサーバー、別のドメイン、別の Active Directory サイト、または別のフォレストに置くことができます。

## メールボックス移動の理由

以下のシナリオでメールボックスを移動することが必要となる場合があります。

  - **アップグレード**   既存の Microsoft Exchange Server 2007 または Exchange Server 2010 組織を Exchange Server 2013 にアップグレードする場合、メールボックスを既存の Exchange サーバーから Exchange 2013 メールボックス サーバーに移動する必要があります。

  - **再配置** 再配置目的でメールボックスを移動できます。たとえば、メールボックスを、あるデータベースから、よりサイズの限度が大きな別のデータベースに移動できます。

  - **問題の調査**   メールボックスに関する問題を調査する必要がある場合に、そのメールボックスを別のサーバーに移動できます。たとえば、利用率の高いすべてのメールボックスを、別のサーバーに移動できます。

  - **破損したメールボックス**   メールボックスの破損が発生した場合、メールボックスを別のサーバーまたはデータベースに移動できます。破損したメッセージは移動しません。

  - **物理的な場所の変更**   異なる Active Directory サイトにあるサーバーに、メールボックスを移動できます。たとえば、ユーザーが物理的に別の場所に移動する場合、そのユーザーのメールボックスを新しい場所に近いサーバーに移動できます。

  - **管理役割の分離**Exchange の管理を Windows オペレーティング システムのアカウントの管理から分離することができます。そのような場合は、メールボックスを単一のフォレストからリソース フォレストのシナリオに移動することができます。このシナリオでは、Exchange メールボックスはあるフォレストに存在し、それに関連付けられた Windows ユーザー アカウントは別のフォレストに存在します。

  - **電子メール管理のアウトソーシング**   電子メールの管理をアウトソーシングし、Windows ユーザー アカウントの管理は続けることができます。そのような場合は、メールボックスを単一のフォレストからリソース フォレストのシナリオに移動することができます。

  - **電子メールの管理とユーザー アカウントの管理の統合**   電子メールを分離またはアウトソーシングして管理するモデルから、電子メールとユーザー アカウントを同じフォレスト内から管理するモデルに変更できます。そのような場合は、メールボックスをリソース フォレストのシナリオから単一フォレストに移動できます。このシナリオでは、Exchange のメールボックスと Windows のユーザー アカウントが、同じフォレストに存在します。

## Exchange 2013 の移動

Microsoft Exchange Server 2013 では、*バッチ移動*と*移行エンドポイント*の概念が導入されています。移行エンドポイントは、リモート サーバーと接続を記述し、1 つまたは複数のバッチに関連付けることが可能な管理オブジェクトです。新しいバッチ移動アーキテクチャは、管理機能の強化によって、Mailbox Replication サービス (MRS) の移動が向上しました。Exchange 2013 のバッチ移動アーキテクチャには、次の機能があります。

  - 大きなバッチで複数のメールボックスを移動する機能。

  - 移動中のレポート付き電子メール通知。

  - 移動の自動再試行および自動優先順位付け。

  - プライマリ メールボックスと個人のアーカイブ メールボックスの連携移動または個別移動。

  - 終了前に移動を確認できる、手動移動要求の終了処理。

  - 移行の変更を更新する定期的な差分同期。

Exchange 2013 では、Exchange 2013 管理センター (EAC) および Exchange 管理シェルによって、Exchange 2007 および Exchange 2010 と Exchange 2013 間でメールボックスを移行する必要があります。


> [!NOTE]
> EAC、移動要求、または移行バッチ コマンドレットのいずれかを使用して、Exchange Server 2010 のように Exchange 2013 で単一のメールボックスの移動を実行できます。




> [!NOTE]
> 社内メールボックスを Exchange Server 2003 から Exchange 2013 に移動することはできません。



新しい移動と既存の移動を管理する方法の詳細については、「[社内の移動の管理](manage-on-premises-moves-exchange-2013-help.md)」を参照してください。

## 移行エンドポイント

移行エンドポイントはリモート サーバー情報を取り込み、データとソース調整設定の移行に必要な資格情報を保持します。移行エンドポイントを使用して、リモート移動とフォレスト間の移動の設定を構成できます。ローカル移動では、エンドポイントを使用する必要はありません。(ローカル移動は、2 つの異なる社内 Exchange データベース間でメールボックスを移動します。)

次の一覧は、移行エンドポイントをサポートする移動の種類を示します。

  - **フォレスト間の移動**   2 つの異なる社内 Exchange フォレスト間でメールボックスを移動します。フォレスト間の移動には、Exchange RemoteMove エンドポイントを使用する必要があります。

  - **リモート移動**   ハイブリッド展開では、リモート移動に*オンボード*移行または*オフボード*移行が含まれます。リモート移動には RemoteMove エンドポイントを使用する必要があります。オンボードでは社内 Exchange 組織から Microsoft Office 365 の Exchange Online にメールボックスを移動し、移行バッチのソース エンドポイントとして RemoteMove エンドポイントが使用されます。オフボードでは Office 365 の Exchange Online から社内 Exchange 組織にメールボックスを移動し、移行バッチのターゲット エンドポイントとして Exchange RemoteMove エンドポイントが使用されます。

次の表は、Exchange 2013 で管理できる移行エンドポイントの種類と値を示します。

### 移行エンドポイントの種類の値

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange RemoteMove</th>
<th>Exchange LocalMove</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MaxConcurrentMigrations</p></td>
<td><p>MaxConcurrentMigrations</p></td>
</tr>
<tr class="even">
<td><p>RemoteServer</p></td>
<td><p>Site</p></td>
</tr>
<tr class="odd">
<td><p>ArchiveDomain</p></td>
<td><p>Database</p></td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>ArchiveDatabase</p></td>
</tr>
<tr class="odd">
<td><p>LargeItemLimit</p></td>
<td><p>BadItemLimit</p></td>
</tr>
<tr class="even">
<td><p>Databases</p></td>
<td><p>LargeItemLimit</p></td>
</tr>
<tr class="odd">
<td><p>TargetDeliveryDomain</p></td>
<td><p>PrimaryOnly</p></td>
</tr>
<tr class="even">
<td><p>PrimaryOnly</p></td>
<td><p>ArchiveDatabase</p></td>
</tr>
<tr class="odd">
<td><p>ArchiveDatabase</p></td>
<td><p>DAG</p></td>
</tr>
<tr class="even">
<td><p>ArchiveOnly</p></td>
<td><p>Forest</p></td>
</tr>
</tbody>
</table>


移行エンドポイントの詳細については、EAC の **\[移行\]** ユーザー インターフェイスと「[New-MigrationEndpoint](https://technet.microsoft.com/ja-jp/library/jj218611\(v=exchg.150\))」を参照してください。

新しい移動と既存の移動を管理する方法の詳細については、「[社内の移動の管理](manage-on-premises-moves-exchange-2013-help.md)」を参照してください。

