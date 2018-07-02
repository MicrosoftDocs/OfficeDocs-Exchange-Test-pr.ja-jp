---
title: '複数のフォレスト トポロジを Exchange 2013 に展開する: Exchange 2013 Help'
TOCTitle: 複数のフォレスト トポロジを Exchange 2013 に展開する
ms:assetid: d51f2b7d-9045-40cf-8b9f-43787a6fff6d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124734(v=EXCHG.150)
ms:contentKeyID: 51407584
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 複数のフォレスト トポロジを Exchange 2013 に展開する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

ここでは、複数フォレスト トポロジでの Microsoft Exchange Server 2013 の展開の概要を説明します。次の内容に関する情報があります。

  - **サポートされる複数フォレスト トポロジ**   Exchange 2013 は、フォレスト間およびリソース フォレストの 2 種類の複数フォレスト トポロジをサポートします。

  - **GAL 同期**   フォレスト間の環境がある場合、任意のフォレストの GAL に他のフォレストに属するメール受信者を含めるようにする必要があります。

  - **フォレスト間のメールボックスの移動**    Exchange 管理シェルの **New-MoveRequest** コマンドレットおよび **New-MigrationBatch** コマンドレットを使用して、あるフォレストから別のフォレストへとメールボックスを移動することができます。

  - **複数フォレストの管理について**   フォレスト間のアクセス許可の構成と管理を行うアクセス許可モデルについて説明します。

## サポートされている複数フォレスト トポロジ

Exchange 2013 では、以下の複数フォレスト トポロジがサポートされています。

  - **フォレスト間**   フォレスト間トポロジは、Exchange フォレストが複数存在するトポロジです。ここでは、複数のフォレストが存在するトポロジに Exchange 2013 を展開するための作業について概説します。
    
    1.  最初に、Exchange 2013 を各フォレストにインストールする必要があります。詳細については、「[Exchange 2013 の新規インストールの展開](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)」を参照してください。
    
    2.  次に、各フォレストのグローバル アドレス一覧 (GAL) にすべての同期されたフォレストからのユーザーが含まれるように、各フォレストの受信者を同期する必要があります。詳細については、後の「GAL 同期」を参照してください。
    
    3.  最後に、あるフォレスト内のユーザーが別のフォレスト内のユーザーの空き時間情報データを表示できるように、空き時間情報サービスを構成する必要があります。詳細については、「[フォレスト間のトポロジの空き時間情報サービスを構成する](configure-the-availability-service-for-cross-forest-topologies-exchange-2013-help.md)」を参照してください。
    
    フォレスト間トポロジでの Exchange 2013 の展開の詳細については、「[フォレスト間のトポロジで Exchange 2013 を展開する](deploy-exchange-2013-in-a-cross-forest-topology-exchange-2013-help.md)」を参照してください。

  - **リソース フォレスト**   リソース フォレスト トポロジは、1 つの Exchange フォレストと 1 つまたは複数のユーザー アカウント フォレストが存在するトポロジです。ここでは、1 つのリソース フォレストが存在するトポロジに Exchange 2013 を展開するための作業について概説します。
    
    1.  Exchange がインストールされているフォレストが必要です。Exchange フォレストでは、Exchange メールボックスを持つユーザー アカウントを無効にする必要があります。
    
    2.  ユーザー アカウントを含むフォレストが、少なくとも 1 つは必要です。このフォレストには、Exchange をインストール*しない*でください。
    
    3.  次に、Exchange フォレスト内の無効になっているユーザー アカウントと、アカウント フォレスト内のユーザー アカウントを関連付ける必要があります。
    
    リソース フォレスト トポロジでの Exchange 2013 の展開の詳細については、「[Exchange リソース フォレストのトポロジに Exchange 2013 を展開する](deploy-exchange-2013-in-an-exchange-resource-forest-topology-exchange-2013-help.md)」を参照してください。

## GAL 同期

既定では、GAL には単一のフォレストに属するメール受信者が含まれます。フォレスト間の環境がある場合、Microsoft Identity Lifecycle Manager (ILM) 2007 Feature Pack 1 (FP1) を使用して、任意のフォレストの GAL に他のフォレストに属するメール受信者を含めるようにすることをお勧めします。ILM 2007 FP1 により、他のフォレストに属する受信者を表すメール ユーザーが作成されます。ユーザーは GAL でそれらを参照してメールを送信できます。たとえば、フォレスト A のユーザーは、フォレスト B ではメール ユーザーとして表示されます。また、その逆の場合も同様です。送信先フォレスト内のユーザーは、他のフォレストの受信者を表すメール ユーザー オブジェクトを選択してメールを送信できます。

GAL 同期を有効にするには、メールが有効なユーザー、連絡先、およびグループを、指定された Active Directory サービスから集中メタディレクトリにインポートする管理エージェントを作成します。メタディレクトリでは、メールが有効なオブジェクトはメール ユーザーとして表されます。グループはメンバーシップが関連付けられていない連絡先として表されます。次に、管理エージェントは、指定された同期先フォレストの組織単位にこれらのメール ユーザーをエクスポートします。

Forefront Identity Manager (FIM) の詳細については、「[Forefront Identity Manager 2010](https://go.microsoft.com/fwlink/p/?linkid=279864)」を参照してください。

## フォレスト間のメールボックスの移動

フォレスト間のトポロジでは、あるフォレストから別のフォレストにメールボックスを移動する必要がある場合があります。これを行うには、Exchange 管理シェルで **New-MoveRequest** コマンドレットまたは **New-MigrationBatch** コマンドレットを使用する必要があります。フォレストを越えるメールボックスの移動の詳細については、以下のトピックを参照してください。

  - [メールボックスでフォレスト間の移動要求の準備を行う](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)

  - [シェルの Prepare-MoveRequest.ps1 スクリプトを使用して、フォレスト間のメールボックスの移動を準備する](prepare-mailboxes-for-cross-forest-moves-using-the-prepare-moverequest-ps1-script-in-the-shell-exchange-2013-help.md)

  - [サンプル コードを使用してフォレスト間のメールボックス移動を準備する](prepare-mailboxes-for-cross-forest-moves-using-sample-code-exchange-2013-help.md)

## 複数フォレストの管理について

Exchange 2013 では、新しいアクセス許可の機能を使用して複数フォレスト環境を管理します。

Exchange 2013 では、役割ベースのアクセス制御 (RBAC) アクセス許可モデルが使用されます。管理者がメンバーとなっている管理役割グループ、およびエンド ユーザーが割り当てられている管理役割割り当てポリシーによって、各管理者およびエンド ユーザーが実行できる範囲が決定されます。複数フォレストのアクセス許可について理解するには、RBAC について理解しておく必要があります。RBAC、特に役割グループおよび役割の割り当てポリシーの詳細については、「[役割ベースのアクセス制御について](understanding-role-based-access-control-exchange-2013-help.md)」を参照してください。

RBAC アクセス許可モデルを使用して、フォレスト間のアクセス許可を構成および管理できます。複数フォレストのアクセス許可の詳細については、以下のトピックを参照してください。

  - [複数フォレストのアクセス許可について](understanding-multiple-forest-permissions-exchange-2013-help.md)

  - [リンクされた役割グループの管理](manage-linked-role-groups-exchange-2013-help.md)

  - [組み込みの役割グループをミラーするリンクされた役割グループを作成する](create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md)

