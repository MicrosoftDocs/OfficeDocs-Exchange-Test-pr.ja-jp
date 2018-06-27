---
title: '組織の関係を削除する: Exchange 2013 Help'
TOCTitle: 組織の関係を削除する
ms:assetid: ff211394-f58b-4da7-bb3a-df6abcb5950e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657513(v=EXCHG.150)
ms:contentKeyID: 49896571
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 組織の関係を削除する

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-01-04_

組織上の関係によって、Exchange 組織内のユーザーは予定表の空き時間情報を Office 365 組織や別の Exchange 社内組織と共有できます。組織上の関係を削除して、他の組織との予定表の共有を無効にすることができます。

予定表を他の組織と共有するには、その前に、Azure Active Directory 認証システムとの認証関係 (「フェデレーション」とも呼ばれる) をセットアップすること、および最小限のソフトウェア要件を満たしていることが必要です。フェデレーション共有の詳細については、「[共有](sharing-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。 「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「予定表と共有のアクセス許可」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

## 必要な作業

## EAC を使用して組織の関係を削除する

1.  社内組織の Exchange 2013 サーバーで、**\[組織\]** \> **\[共有\]** に移動します。

2.  **\[組織の共有\]** の下で組織の関係を選択し、**\[削除\]**![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") をクリックして組織の関係を削除します。

3.  表示される警告で、**\[はい\]** をクリックします。

## シェルを使用して組織の関係を削除する

この例では、Exchange 組織から組織の関係 Contoso を削除します。

    Remove-OrganizationRelationship -Identity "Contoso"

構文およびパラメーターの詳細については、「[Remove-OrganizationRelationship](https://technet.microsoft.com/ja-jp/library/ee332362\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

組織の関係が正常に削除されたことを確認するには、次のいずれかの手順を実行します。

  - EAC で、**\[組織\]** \> **\[共有\]** に移動して、**\[組織の共有\]** のリスト ビューに組織の関係が表示されないことを確認します。

  - 次のシェル コマンドを実行して、組織の関係の情報が削除されていることを確認します。
    
        Get-OrganizationRelationship | Format-List


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。


