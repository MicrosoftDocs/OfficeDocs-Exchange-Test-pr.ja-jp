---
title: 'Simple Mail Transport Protocol が現在インストールされている'
TOCTitle: Simple Mail Transport Protocol が現在インストールされている_SMTPSvcInstalled
ms:assetid: f786a93c-876d-4f4e-adb6-4dfea3d820d1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.smtpsvcinstalled(v=EXCHG.150)
ms:contentKeyID: 48270256
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Simple Mail Transport Protocol が現在インストールされている\_SMTPSvcInstalled

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2012-06-05_

コンピューターに Microsoft Windows Server™ 2003 の SMTP (Simple Mail Transfer Protocol) サービスがインストールされているため、Microsoft® Exchange Server 2007 セットアップ プログラムを続行できません。

Microsoft Exchange セットアップ プログラムを実行するには、Exchange 2007 に使用するサーバーに SMTP サービスをインストールしないようにする必要があります。

この問題を解決するには、SMTP サービスをアンインストールしてから Microsoft Exchange セットアップ プログラムを再実行します。

**コントロール パネルの \[Windows コンポーネントの追加と削除\] を使用して SMTP サービスをアンインストールするには、次の操作を行います。**

1.  <strong>スタート</strong> ボタンをクリックし、<strong>コントロール パネル</strong> をクリックします。

2.  <strong>プログラムの追加と削除</strong> をダブルクリックします。

3.  <strong>Windows コンポーネントの追加と削除</strong> をクリックします。

4.  <strong>コンポーネント</strong> ボックスの一覧で、<strong>アプリケーション サーバー</strong> チェック ボックスをオンにし、<strong>詳細</strong> をクリックします。

5.  <strong>インターネット インフォメーション サービス マネージャー</strong> を選択し、<strong>詳細</strong> をクリックします。

6.  <strong>SMTP サービス</strong> を選択し、チェック ボックスをオフにします。

7.  <strong>OK</strong> を 2 回クリックして <strong>コンポーネント</strong> ボックスの一覧に戻り、<strong>次へ</strong> をクリックします。

8.  SMTP サービスがアンインストールされたら、<strong>完了</strong> をクリックします。

