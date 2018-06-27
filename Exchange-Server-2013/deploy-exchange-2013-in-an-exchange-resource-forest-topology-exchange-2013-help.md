---
title: 'Exchange リソース フォレストのトポロジに Exchange 2013 を展開する: Exchange 2013 Help'
TOCTitle: Exchange リソース フォレストのトポロジに Exchange 2013 を展開する
ms:assetid: 537a7b2b-d002-40a6-84ae-fd02635f9e23
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998031(v=EXCHG.150)
ms:contentKeyID: 51407533
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange リソース フォレストのトポロジに Exchange 2013 を展開する

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2016-12-09_

ここでは、Exchange リソース フォレストのトポロジに Microsoft Exchange 2013 を展開する方法について説明します。Exchange リソース フォレストは、専用 Exchange フォレストとも呼ばれます。ここでは、既存の Exchange 2013 トポロジが存在しないことを前提としています。

次の図は、リソース フォレストを持つ Exchange 組織を示しています。

**Exchange リソース フォレストを持つ Exchange 組織の例**

![リソース フォレストを含む複雑な Exchange 組織](images/Aa998031.706725cf-e520-4b89-a275-acd8fb58943a(EXCHG.150).gif "リソース フォレストを含む複雑な Exchange 組織")

## 始める前に把握しておくべき情報

Exchange 2013 で次の手順を実行するには、以下の点を確認してください。

  - 次の 2 つの Active Directory フォレストが存在している。
    
      - 1 つのフォレストには、組織のユーザー アカウントが含まれている。ここでは、このフォレストを "*アカウント フォレスト*" と呼びます。
    
      - もう 1 つのフォレストにはユーザー アカウントが含まれず、Exchange はまだインストールされていない。ここでは、このフォレストを "*Exchange フォレスト*" と呼びます。Exchange 2013 をこのフォレストにインストールするには、プロシージャを使用します。

  - 組織内の複数のフォレストにわたって名前解決のためのドメイン ネーム システム (DNS) が正しく構成されている。DNS が正しく構成されているかどうかを確認するには、組織内の他のフォレストから各フォレストに対して ping を実行します。DNS の構成の詳細については、[「DNS サーバー操作ガイド」](https://go.microsoft.com/fwlink/p/?linkid=282295)を参照してください。

## Exchange リソース フォレストのトポロジに Exchange 2013 を展開する

1.  Exchange フォレストのドメイン コントローラーから、一方向の出力方向の信頼を作成し、Exchange フォレストがアカウント フォレストを信頼するようにします。詳細な手順については、[「信頼の両側に対する一方向かつ出力方向のフォレストの信頼を作成する」](https://go.microsoft.com/fwlink/p/?linkid=69130)を参照してください。
    

    > [!NOTE]
    > フォレストの信頼を作成することをお勧めしますが、フォレストの信頼または外部の信頼のいずれかを作成することが可能です。手順 3. でリンク メールボックスを作成するときに外部の信頼を作成する場合、メールボックスの新規作成ウィザードの <STRONG>[マスター アカウント]</STRONG> ページで、信頼されたフォレストのドメイン コントローラーにアクセスできるユーザー アカウントを指定する必要があります。現在ログオンしている資格情報を使用することはできません。<STRONG>New-Mailbox</STRONG> コマンドレットを使用してリンク メールボックスを作成する場合、<EM>LinkedCredential</EM> パラメーターで、信頼されたフォレストのドメイン コントローラーにアクセスできるユーザー アカウントを指定する必要があります。



2.  Exchange フォレストで、Exchange 2013 をインストールします。単一フォレストのシナリオと同じ方法で Exchange をインストールします。Exchange 2013 をインストールする方法の詳細については、以下のいずれかのトピックを参照してください。
    
      - [Exchange 2013 の新規インストールの展開](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)
    
      - [セットアップ ウィザードを使用した Exchange 2013 のインストール](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)

3.  Exchange フォレストで、Exchange フォレストにメールボックスを持つアカウント フォレスト内のユーザーごとに、外部アカウントに関連付けられているメールボックスを作成します。詳細な手順については、「[リンクされたメールボックスの管理](manage-linked-mailboxes-exchange-2013-help.md)」を参照してください。

