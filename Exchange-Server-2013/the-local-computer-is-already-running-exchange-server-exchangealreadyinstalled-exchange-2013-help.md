---
title: 'ローカル コンピューターで既に Exchange Server が実行されている | Microsoft Dos'
TOCTitle: ローカル コンピューターですでに Exchange Server が実行されている_ExchangeAlreadyInstalled
ms:assetid: 3f168b5d-9910-418f-86fb-e99d852dcb5e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.exchangealreadyinstalled(v=EXCHG.150)
ms:contentKeyID: 48269398
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ローカル コンピューターですでに Exchange Server が実行されている\_ExchangeAlreadyInstalled

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2012-06-05_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

ローカル コンピューターに以前の Microsoft Exchange コンポーネントがインストールされているため、Microsoft® Exchange Server 2007 セットアップ プログラムを続行できません。

Exchange 2007 セットアップ プログラムを実行するには、ローカル コンピューターに既存の Microsoft Exchange コンポーネントがインストールされていない状態にする必要があります。

この問題を解決するには、Microsoft Exchange 2000 Server コンポーネントまたは Microsoft Exchange Server 2003 コンポーネントをすべて削除してから、Microsoft Exchange セットアップ プログラムを再実行します。

**Microsoft Exchange コンポーネントを削除するには、次の操作を行います。**

1.  <strong>スタート</strong> ボタンをクリックし、<strong>設定</strong> をポイントします。次に、<strong>コントロール パネル</strong> をクリックします。

2.  <strong>プログラムの追加と削除</strong> をダブルクリックします。

3.  <strong>現在インストールされているプログラム</strong> ボックスの一覧で、<strong>Microsoft Exchange</strong> をクリックし、<strong>変更と削除</strong> をクリックします。

4.  Microsoft Exchange インストール ウィザードで、<strong>次へ</strong> をクリックします。

5.  \[コンポーネントの選択\] ページのアクションの一覧で、インストールされている各コンポーネントの横にある下向きの矢印をクリックし、<strong>削除</strong> をクリックします。
    

    > [!NOTE]
    > アクションの一覧で、インストール済みのコンポーネントはチェック マークが付けられています。<STRONG>[削除]</STRONG> をクリックすると、このチェック マークが<STRONG>削除</STRONG>に変わります。



6.  <strong>次へ</strong> を 2 回クリックします。

7.  <strong>終了</strong> をクリックします。

