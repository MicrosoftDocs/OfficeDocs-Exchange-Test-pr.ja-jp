---
title: '重複した Microsoft Exchange システム オブジェクト コンテナーが Active Directory に存在する'
TOCTitle: 重複した Microsoft Exchange システム オブジェクト コンテナーが Active Directory に存在する
ms:assetid: cd0f45ab-89de-4653-b50d-c1157c2329d5
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.adiniterrorrule(v=EXCHG.150)
ms:contentKeyID: 48270055
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 重複した Microsoft Exchange システム オブジェクト コンテナーが Active Directory に存在する

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2013-02-18_

Active Directory ドメイン名前付けコンテキストに重複する Microsoft Exchange システム オブジェクト コンテナーが検出されたため、Microsoft Exchange Server 2013 のセットアップが継続できません。重複した Microsoft Exchange システム オブジェクト コンテナーが検出された場合、セットアップを継続するためには重複したコンテナーを削除する必要があります。重複した Microsoft Exchange System Objects コンテナーが存在する場合は、再び **DomainPrep** を実行しても問題を解決できません。重複した Microsoft Exchange システム オブジェクト コンテナーを識別して削除する必要があります。

この問題を解決するには、次の操作を行います。

1.  管理者の資格情報を使用してドメイン コントローラーにログオンします。

2.  <strong>管理ツール</strong> で、<strong>Active Directory ユーザーとコンピューター</strong> をクリックします。

3.  <strong>Active Directory ユーザーとコンピューター</strong> 管理コンソール ウィンドウで、ツールバー メニューから <strong>表示</strong> をクリックし、<strong>高度な機能</strong> を選択します。

4.  重複した Microsoft Exchange システム オブジェクト コンテナーを特定します。

5.  重複した Microsoft Exchange システム オブジェクト コンテナーに有効な Active Directory オブジェクトが含まれないことを確認します。

6.  重複した Microsoft Exchange システム オブジェクト コンテナーを右クリックし、<strong>削除</strong> をクリックします。

7.  Active Directory ダイアログ ボックスで <strong>はい</strong> をクリックして削除を確認します。


> [!NOTE]
> 変更をすぐにレプリケートするには、ドメイン コントローラー間のレプリケーションを手動で開始する必要があります。



問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

探しているものは見つかりましたか？検索したい情報に関する[フィードバックを送信](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback)してください。

