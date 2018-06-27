---
title: 'IIS が 32 ビット互換モードである_IIS32BitMode: Exchange 2013 Help'
TOCTitle: IIS が 32 ビット互換モードである_IIS32BitMode
ms:assetid: 742dfc32-353c-46a2-830e-68aed6a68ce0
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.iis32bitmode(v=EXCHG.150)
ms:contentKeyID: 48269653
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# IIS が 32 ビット互換モードである\_IIS32BitMode

 

_**適用先:**Exchange Server_

_**トピックの最終更新日:**2012-06-05_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

この 64 ビット コンピューターでは Microsoft インターネット インフォメーション サービス (IIS) が 32 ビット モードで実行されているため、Microsoft® Exchange Server 2007 セットアップ プログラムを続行できません。

Exchange 2007 では、IIS が 64 ビット コンピューターで実行される場合、IIS は完全な 64 ビット モードであることが必要になります。

この問題を解決するには、IIS を 64 ビット モードに切り替えて、Microsoft Exchange セットアップ プログラムを再実行します。

**IIS を 64 ビット モードに切り替えるには**

1.  コマンド プロンプトを開きます。

2.  次のように入力します。
    
    **cscript c:\\inetpub\\adminscripts\\adsutil.vbs SET /w3svc/AppPools/Enable32BitAppOnWin64 False**

3.  Enter キーを押します。

