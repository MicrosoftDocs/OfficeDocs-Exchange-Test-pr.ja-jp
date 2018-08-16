---
title: 'パブリック フォルダーの削除: Exchange Online Help'
TOCTitle: パブリック フォルダーの削除
ms:assetid: 334b831d-e372-4d85-a407-5c8a5d0e78de
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997202(v=EXCHG.150)
ms:contentKeyID: 49896184
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# パブリック フォルダーの削除

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

組織で使用しなくなったパブリック フォルダーを削除する必要があります。削除する必要があるパブリック フォルダーを特定するには、「[パブリック フォルダーおよびパブリック フォルダー アイテムの統計情報の表示](view-statistics-for-public-folders-and-public-folder-items-exchange-2013-help.md)」を参照してください。

パブリック フォルダーの管理に関するその他の管理タスクについては、「[パブリック フォルダーの手順](public-folder-procedures-exchange-2013-help.md)」を参照してください。

パブリック フォルダーに関するその他の管理タスクについては、「[Office 365 と Exchange Online のパブリック フォルダーの手順](https://technet.microsoft.com/ja-jp/library/jj966272\(v=exchg.150\))」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間: 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[共有とコラボレーションのアクセス許可](sharing-and-collaboration-permissions-exchange-2013-help.md)」の「パブリック フォルダー」。

  - 電子メールが有効なパブリック フォルダーは削除できません。そのようなパブリック フォルダーを削除するには、そのパブリック フォルダーで電子メールを無効にする必要があります。詳細については、「[パブリック フォルダーのメールの有効化またはメールの無効化](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EAC を使用してパブリック フォルダーを削除する

1.  <strong>パブリック フォルダー</strong> \> <strong>パブリック フォルダー</strong> に移動します。

2.  リスト ビューで、削除するパブリック フォルダーを選択します。フォルダー名をクリックすると、そのフォルダー内のサブフォルダーが表示されます (存在する場合)。その時点で、特定のサブフォルダーをクリックして選択すると、削除できます。
    
    フォルダーまたはサブフォルダーを削除するには、フォルダー行で下線付きのフォルダー名以外の任意の場所をクリックし、\[**削除**![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン")\] をクリックします。下線付きのフォルダー名をクリックしても、\[**削除**\] オプションは選択できません。
    
    ![削除するパブリック フォルダーの選択](images/Aa997202.8666290d-3f19-4c70-afe3-45569762718b(EXCHG.150).png "削除するパブリック フォルダーの選択")  

3.  そのパブリック フォルダーを削除してよいか、確認を求める警告ボックスが表示されます。<strong>はい</strong> をクリックして続行します。

## シェルを使用してパブリック フォルダーを削除する

この例では、パブリック フォルダー Help Desk\\Resolved を削除します。このコマンドは Resolved パブリック フォルダーにサブフォルダーがないことを前提に実行します。

    Remove-PublicFolder -Identity "\Help Desk\Resolved"

この例では、変更を加えずに上記のコマンドをテストします。

    Remove-PublicFolder -Identity "\HelpDesk\Resolved" -WhatIf

この例では、コマンドが再帰的に実行されて、パブリック フォルダー Marketing とそのサブフォルダーすべてを削除します。

    Remove-PublicFolder -Identity "\Marketing" -Recurse:$True

構文およびパラメーターの詳細については、「[Remove-PublicFolder](https://technet.microsoft.com/ja-jp/library/bb124894\(v=exchg.150\))」を参照してください。

