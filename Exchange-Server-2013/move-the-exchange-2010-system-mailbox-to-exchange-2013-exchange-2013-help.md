---
title: 'Exchange 2010 システム メールボックスの Exchange 2013 への移動: Exchange 2013 Help'
TOCTitle: Exchange 2010 システム メールボックスの Exchange 2013 への移動
ms:assetid: a3b03c4e-0bc7-41a2-885c-e9cac37566c8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn249849(v=EXCHG.150)
ms:contentKeyID: 54915173
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2010 システム メールボックスの Exchange 2013 への移動

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-04-07_

Exchange 2010 では、Microsoft Exchange システム メールボックスは、管理者監査ログ、電子情報開示の検索用メタデータ、ユニファイド メッセージング データ (メニュー、ダイヤル プラン、カスタム案内応答など) といった全社的なデータの保存に使用される、調停メールボックスです。Microsoft Exchange システム メールボックスの名前は **SystemMailbox {e0dc1c29-89c3-4034-b678-e6c29d823ed9}**。 表示名は **Microsoft Exchange** です。

既存の Exchange 2010 組織を Exchange 2013 へアップグレードする場合は、Microsoft Exchange システム メールボックスを Exchange 2013 メールボックス サーバーのメールボックス データベースに移動する必要があります。このメールボックスの移動は、Exchange 2013 のインストールを確認した後に行います。このシステム メールボックスを Exchange 2013 へ移動させないと、Exchange 2010 と Exchange 2013 が Exchange 組織に共存する場合には、次の問題が発生します。

  - Exchange 2013 タスクは、管理者監査ログに保存されません。**Search-AdminAuditLog** コマンドレットを実行するか、EAC で管理者監査ログをエクスポートしようとした場合には、「システム メールボックス、SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9} が Exchange 2013 の動作していないサーバー上に配置されているため管理者監査ログを作成できません」というエラーが届きます。イベント ID 5000 の Microsoft Exchange エラーもコマンドが実行されるたびに Windows アプリケーション ログに記録されます。

  - EAC またはシェルを使用した電子情報開示検索を Exchange 2013 で実行することはできません。メールボックスの検索の作成とキューはできますが、開始することができません。**Start-MailboxSearch** コマンドレットが失敗したことを示す、イベント ID 6 のエラーが MsExchange 管理ログに記録されます。ただし、Exchange 2010 のシェルおよび Exchange コントロール パネル (ECP) を使用してメールボックスを検索できます。

さらに、Exchange 2010 ユニファイド メッセージングから Exchange 2013 へのアップグレード作業の一部として、Microsoft Exchange システム メールボックスを Exchange 2013 へ移動する必要があります。

Exchange 2013 へのアップグレードの詳細については、以下のトピックを参照してください。

  - [Exchange 2010 から Exchange 2013 へのアップグレード](upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md)

  - [Exchange 2010 UM から Exchange 2013 UM へのアップグレード](upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md)

## 始める前に把握しておくべき情報

  - 予想所要時間 : 20 分。実際の時間は、システム メールボックスのサイズによって異なります。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「メールボックスの移動および移行のアクセス許可」。

  - Exchange 2013 の次のコマンドを実行して、組織のシステム メールボックスを含む Exchange サーバーとメールボックス データベースの ID とバージョンを取得してください。
    
        Get-Mailbox -Arbitration | FL Name,DisplayName,ServerName,Database,AdminDisplayVersion
    
    **AdminDisplayVersion** プロパティは、サーバーが実行されている Exchange のバージョンを示します。`Version 14.x` の値は Exchange 2010 を示し、`Version 15.x` の値は Exchange 2013 を示します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して、システム メールボックスを移動する

1.  EAC で、**\[受信者\]** \> **\[移行\]** に移動します。

2.  **\[新規作成\]** ![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックしてから **\[別のデータベースに移動\]** をクリックします。

3.  **\[ローカル メールボックスの移動の新規作成\]** ページで **\[移動するユーザーを選択\]** をクリックし、**\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

4.  **\[メールボックスの選択\]** ページで、次のプロパティを持つメールボックスを追加します。
    
      - 表示名が **Microsoft Exchange** である。
    
      - メールボックスの電子メール アドレスのエイリアスが **SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}** である。

5.  **\[OK\]** をクリックし、**\[次へ\]** をクリックします。

6.  **\[移動の構成\]** ページで、移行バッチの名前を入力して、**\[ターゲット データベース\]** ボックスの横の **\[参照\]** をクリックします。

7.  **\[メールボックス データベースの選択\]** ページで、システム メールボックスの移動先のメールボックス データベースを追加します。選択したメールボックス データベースのバージョンがバージョン 15.x (そのデータベースが Exchange 2013 サーバー上にあることを示しています) であることを確認します。

8.  **\[OK\]** をクリックし、**\[次へ\]** をクリックします。

9.  **\[バッチの開始\]** ページで、移行リクエストを自動的に開始して終了するオプションを選択してから、**\[新規作成\]** をクリックします。

## シェルを使用して、システム メールボックスを移動する

まず、Exchange 2013 で次のコマンドを実行して、組織内のすべてのメールボックス データベースの名前とバージョンを取得します。

    Get-MailboxDatabase -IncludePreExchange2013 | FL Name,Server,AdminDisplayVersion

組織のメールボックス データベースの名前を特定したら、Exchange 2013 で次のコマンドを実行して Microsoft Exchange システム メールボックスを Exchange 2013 サーバーにあるメールボックス データベースに移動します。

    Get-Mailbox -Arbitration -Identity "SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}" | New-MoveRequest -TargetDatabase <name of Exchange 2013 database>

## 正常な動作を確認する方法

Microsoft Exchange システム メールボックスを Exchange 2013 サーバー上のメールボックス データベースに正常に移行したことを確認するには、シェルで次のコマンドを実行します。

    Get-Mailbox -Arbitration -Identity "SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}" | FL Database,ServerName,AdminDisplayVersion

**AdminDisplayVersion** プロパティの値が **Version 15.x (Build xxx.x)** の場合、システム メールボックスは Exchange 2013 サーバー上のメールボックス データベースに存在しています。

Microsoft Exchange のシステム メールボックスを Exchange 2013 に移行した後に、次の管理タスクを正常に実行できるようになります。

  - **Search-AdminAuditLog** コマンドレットの実行

  - EAC での管理者監査ログのエクスポート

  - Exchange 2013 での EAC またはシェルを使用した電子情報開示検索の正常な作成と開始

