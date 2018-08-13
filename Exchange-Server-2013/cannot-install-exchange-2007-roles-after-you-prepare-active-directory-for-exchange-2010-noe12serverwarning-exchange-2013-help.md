---
title: 'Exchange 2010 用に Active Directory を準備した後、Exchange 2007 の役割をインストールできない'
TOCTitle: Exchange 2010 用に Active Directory を準備した後、Exchange 2007 の役割をインストールできない_NoE12ServerWarning
ms:assetid: 4e579f69-0de9-421c-ba31-4e63a25e6a45
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.noe12serverwarning(v=EXCHG.150)
ms:contentKeyID: 48269489
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2010 用に Active Directory を準備した後、Exchange 2007 の役割をインストールできない\_NoE12ServerWarning

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2016-12-09_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2010**Setup /PrepareAD** を実行している場合、Microsoft Exchange Server アナライザー ツールは、既存の Active Directory トポロジに対してクエリを実行し、Microsoft Exchange Server 2007 サーバーの役割が存在しているかどうかを判断します。Exchange 2007 サーバーの役割が検出されない場合、次の警告メッセージが表示されます。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>セットアップは 'Setup /PrepareAD' を介して Exchange Server 2010 用の組織を準備しようとしており、Exchange Server 2007 の役割はこのトポロジで検出されませんでした。この処理の後、Exchange Server 2007 の役割をインストールすることはできません。</p></td>
</tr>
</tbody>
</table>


Exchange Server 2010 を導入する前に次の要因を検討してください。場合によっては、Exchange 2007 を導入する前にすべてのサーバーの役割がインストールされた Exchange 2007 サーバーを導入する必要が生じることがあります。

  - **サード パーティ製または社内開発のアプリケーション**   Exchange 2003 用に開発されたアプリケーションが Exchange 2010 との互換性を備えておらず、アップグレードまたは入れ替えが必要となる場合があります。これらのアプリケーションと関連するユーザーを Exchange 2003 で維持するか、Exchange 2007 へ移動するか、または Exchange 2010 と互換性のあるバージョンでソフトウェアを入れ替えることができます。

  - **共存または移行要件**   メールボックスを組織に移行することを計画している場合は、Exchange 2007 を導入して Microsoft Transporter Suite を使用するか、サード パーティの共存または移行ソリューションを使用することができます。Microsoft Transporter Suite をダウンロードするには、Microsoft ダウンロード センターの「[Microsoft Transporter Suite](http://go.microsoft.com/fwlink/?linkid=82688)」へ移動します。

また、組織にとっての選択肢を評価するときには、必ず次の質問項目を検討してください。

  - Exchange 2003 のサポートが終了する前に、依存しているアプリケーションを Exchange 2010 へ移行する戦略を立てているか?詳細については、マイクロソフト サポート ライフ サイクルの Web ページ ([https://go.microsoft.com/fwlink/?LinkID=55839](https://go.microsoft.com/fwlink/?linkid=55839)) を参照してください。

  - あなたの戦略では WebDAV および Web サービスの共存が必要ですか (Exchange 2007)?

  - Exchange、または共存または移行要件を満たすことができる他の Microsoft テクノロジをサポートするサード パーティ製品を検討しましたか?

  - ハードウェア ライフサイクルはどのように考えていますか (できるだけ多くの既存の 32 ビット サーバーを使い続ける、または新しい 64 ビット サーバーを購入する)?

  - 移行についてはどのような計画ですか (できるだけ早くすべてのサーバーを移行する、または段階的な戦略で移行する)?同様に、異なるバージョンの Exchange の共存についてどのようなスケジュールを立てていますか?

Exchange 2010 を導入する前に Exchange 2007 サーバーを導入する必要があると判断した場合は、すべてのサーバーの役割を備えた単一の Exchange 2007 を導入すれば、将来的に Exchange 2007 サーバーを組織内に導入できます。Exchange 2007 サーバーを Exchange 2003 組織に導入するには、次の手順を実行します。

1.  Exchange 2007**Setup /PrepareSchema** を実行します。

2.  Exchange 2007**Setup /PrepareAD** を実行します。

3.  受信者を含むすべてのドメイン、Exchange 2003 サーバー、または Exchange サーバーが使用できるグローバル カタログ上で、Exchange 2007**Setup /PrepareDomain** を実行します。

4.  Exchange 2007 サーバーに 4 つのサーバー役割 (ハブ トランスポート、クライアント アクセス、メールボックス、およびユニファイド メッセージング) をすべてインストールします。

