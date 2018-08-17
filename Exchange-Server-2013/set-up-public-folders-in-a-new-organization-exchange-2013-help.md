﻿---
title: '新しい組織でパブリック フォルダーをセットアップする: Exchange Online Help'
TOCTitle: 新しい組織でパブリック フォルダーをセットアップする
ms:assetid: 7b419906-8977-47f0-8687-a87911b5ebec
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ651147(v=EXCHG.150)
ms:contentKeyID: 49896330
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 新しい組織でパブリック フォルダーをセットアップする

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

**概要**:パブリック フォルダーを設定する方法 (EAC でそれらにアクセス許可を割り当てることを含む)。

このトピックでは、新しい組織またはこれまでパブリック フォルダーがなかった組織でパブリック フォルダーを構成し、機能させる方法について説明します。


> [!NOTE]
> ストレージ クォータおよびパブリック フォルダーの制限に関する詳細については、次のトピックを参照してください。 
> <UL>
> <LI>
> <P>Office 365 のパブリック フォルダーについて詳しくは、「<A href="https://go.microsoft.com/fwlink/?linkid=391188">Exchange Online の制限</A>」を参照してください。</P>
> <LI>
> <P>オンプレミス Exchange Server 2013 のパブリック フォルダーについて詳しくは、「<A href="limits-for-public-folders-exchange-2013-help.md">パブリック フォルダーの制限</A>」を参照してください。</P></LI></UL>



Exchange Server 2013 のパブリック フォルダーに関するその他の管理タスクについては、「[パブリック フォルダーの手順](public-folder-procedures-exchange-2013-help.md)」を参照してください。

Exchange Online のパブリック フォルダーに関するその他の管理タスクについては、「[Office 365 と Exchange Online のパブリック フォルダーの手順](https://technet.microsoft.com/ja-jp/library/jj966272\(v=exchg.150\))」を参照してください。

## 始める前に把握しておくべき情報

  - このタスクの予想所要時間:30 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[共有とコラボレーションのアクセス許可](sharing-and-collaboration-permissions-exchange-2013-help.md)」の「パブリック フォルダー」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 実行方法

## 手順 1:プライマリ パブリック フォルダー メールボックスを作成する

パブリック フォルダーのプライマリ メールボックスには、パブリック フォルダー階層の書き込み可能なコピーと内容が含まれており、組織に対して作成する最初のパブリック フォルダーのメールボックスになります。これ以降のパブリック フォルダー メールボックスは、階層の読み取り専用コピーと内容が含まれたセカンダリ パブリック フォルダー メールボックスになります。

詳細な手順については、「[パブリック フォルダー メールボックスを作成する](create-a-public-folder-mailbox-exchange-2013-help.md)」を参照してください。

## 手順 2:最初のパブリック フォルダーを作成する

詳細な手順については、「[パブリック フォルダーの作成](create-a-public-folder-exchange-2013-help.md)」を参照してください。

## 手順 3:パブリック フォルダーにアクセス許可を割り当てる

パブリック フォルダーを作成したら、<strong>所有者</strong> のアクセス許可レベルを割り当てて、少なくとも 1 人のユーザーがクライアントからパブリック フォルダーにアクセスして、サブフォルダーを作成できるようにする必要があります。この後に作成されるすべてのパブリック フォルダーは、親のパブリック フォルダーのアクセス許可を継承します。

1.  Exchange 管理センター (EAC) で、<strong>パブリック フォルダー</strong> \> <strong>パブリック フォルダー</strong> の順に選択します。

2.  リスト ビューで、パブリック フォルダーを選択します。

3.  詳細ウィンドウの <strong>フォルダーのアクセス許可</strong> で、<strong>管理</strong> をクリックします。

4.  <strong>パブリック フォルダー アクセス許可</strong> で、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

5.  <strong>参照</strong> をクリックして、ユーザーを選択します。

6.  <strong>アクセス許可レベル</strong> 一覧で、レベルを選択します。少なくとも 1 人のユーザーが <strong>所有者</strong> である必要があります。

7.  <strong>保存</strong> をクリックします。

8.  複数のユーザーを追加するには、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックして、上記の手順で該当するアクセス許可を割り当てます。チェック ボックスをオンまたはオフにすることにより、アクセス許可レベルをカスタマイズすることもできます。<strong>所有者</strong> などの定義済みのアクセス許可レベルを編集すると、アクセス許可レベルが <strong>カスタム</strong> に変わります。

シェルを使用してパブリック フォルダーにアクセス許可を割り当てる方法の詳細については、「[Add-PublicFolderClientPermission](https://technet.microsoft.com/ja-jp/library/bb124743\(v=exchg.150\))」を参照してください。

## 手順 4 (オプション):パブリック フォルダーのメールを有効にする

ユーザーがパブリック フォルダーにメールを送信できるようにする場合は、パブリック フォルダーのメールを有効にできます。この手順は省略可能です。パブリック フォルダーのメールを有効にしない場合、ユーザーはアイテムを Outlook からパブリック フォルダーまでドラッグすることで、メッセージをパブリック フォルダーに投稿できます。

1.  EAC で、<strong>パブリック フォルダー</strong> \> <strong>パブリック フォルダー</strong>に移動します。

2.  リスト ビューで、メールを有効にするパブリック フォルダーを選択します。

3.  詳細ウィンドウの <strong>メールの設定 - 無効</strong> で、<strong>有効にする</strong> をクリックします。
    
    パブリック フォルダーのメールを有効にすることを確認する警告が表示されます。<strong>はい</strong> をクリックします。

パブリック フォルダーのメールが有効になり、パブリック フォルダーの名前がパブリック フォルダーのエイリアスになります。該当する名前の受信者が複数いる場合、パブリック フォルダーのエイリアスに番号が追加されます。たとえば、SalesTeam という名前の配布グループがあって、SalesTeam という名前のパブリック フォルダーを作成すると、パブリック フォルダーのエイリアスは SalesTeam1 になります。

シェルを使用してパブリック フォルダーのメールを有効にする方法の詳細については、「[Enable-MailPublicFolder](https://technet.microsoft.com/ja-jp/library/aa998824\(v=exchg.150\))」を参照してください。

