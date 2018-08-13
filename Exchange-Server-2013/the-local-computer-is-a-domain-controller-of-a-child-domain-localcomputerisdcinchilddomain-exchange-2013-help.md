---
title: 'ローカル コンピューターが子ドメインのドメイン コントローラーである'
TOCTitle: ローカル コンピューターが子ドメインのドメイン コントローラーである_LocalComputerIsDCInChildDomain
ms:assetid: 7db1dcc0-d953-41b8-b081-2a47a70950c4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.localcomputerisdcinchilddomain(v=EXCHG.150)
ms:contentKeyID: 48269705
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ローカル コンピューターが子ドメインのドメイン コントローラーである\_LocalComputerIsDCInChildDomain

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2012-06-05_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

ローカル コンピューターが子ドメインのドメイン コントローラーであるため、Microsoft® Exchange Server 2007 セットアップ プログラムを続行できません。

ドメイン コントローラーがグローバル カタログ サーバーでない場合、Exchange 2007 セットアップ プログラムは子ドメインのドメイン コントローラーにインストールを行いません。

この問題を解決するには、ドメイン コントローラーをグローバル カタログ サーバーに昇格させるか、または子ドメインの中のドメイン コントローラー以外のメンバー サーバーに Exchange 2007 をインストールし、その後 Microsoft Exchange セットアップ プログラムを再実行します。

**Exchange サーバーをグローバル カタログ サーバーにしてこの警告を修正するには**

1.  ドメイン コントローラー上で **\[スタート\]** ボタンをクリックし、**\[プログラム\]** をポイントします。次に、**\[管理ツール\]** をクリックし、**\[Active Directory サイトとサービス\]** をクリックします。

2.  コンソール ツリーで、**\[サイト\]** をダブルクリックし、サイトの名前をダブルクリックします。次に、**\[サーバー\]** をダブルクリックします。

3.  対象のドメイン コントローラーをダブルクリックします。

4.  結果ウィンドウで **\[NTDS Settings\]** を右クリックし、**\[プロパティ\]** をクリックします。

5.  **\[全般\]** タブで、**\[グローバル カタログ\]** チェック ボックスをオンにします。

6.  ドメイン コントローラーを再起動します。

