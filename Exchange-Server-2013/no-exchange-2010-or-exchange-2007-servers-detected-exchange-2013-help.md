---
title: 'Exchange 2010 または Exchange 2007 サーバーが検出されなかった: Exchange 2013 Help'
TOCTitle: Exchange 2010 または Exchange 2007 サーバーが検出されなかった
ms:assetid: 789cabab-c769-4a16-a6c8-3db82cff8861
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.noe14serverwarning(v=EXCHG.150)
ms:contentKeyID: 48269681
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2010 または Exchange 2007 サーバーが検出されなかった

 

_**適用先:**Exchange Server_

_**トピックの最終更新日:**2012-11-08_

組織に Exchange Server 2010 または Exchange Server 2007 サーバーの役割が存在しないため、Microsoft Exchange Server 2013 セットアップ プログラムはこの警告を表示しました。


> [!NOTE]
> Exchange Server 2013 のインストールを続行すると、あとで、Exchange 2010 または Exchange&nbsp;2007 サーバーを組織に追加できなくなります。



Exchange 2013 を展開する前に次の要因について検討してください。これらの要因によって、Exchange 2013 の展開の前の段階で Exchange 2010 または Exchange 2007 サーバーの展開が必要になることがあります。

  - **サードパーティまたは社内で開発されたアプリケーション**   Exchange の以前のバージョンに対応して開発されたアプリケーションが、Exchange 2013 と互換性がないことがあります。これらのアプリケーションをサポートするために、Exchange 2010 または Exchange 2007 のサーバーを維持しなければならない場合があります。

  - **共存または移行要件**   組織へのメールボックスの移行を計画している場合、一部のソリューションで Exchange 2010 サーバーまたは Exchange 2007 サーバーの使用が必要になることがあります。

Exchange 2010 または Exchange 2007 のサーバーを展開する必要があると判断した場合は、Exchange 2013 を展開する前に、これらのサーバーを展開する必要があります。Active Directory は、Exchange のバージョンごとに、次の順序で準備する必要があります。

1.  Exchange 2007

2.  Exchange 2010

3.  Exchange 2013

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

探しているものは見つかりましたか？検索したい情報に関する[フィードバックを送信](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback)してください。

