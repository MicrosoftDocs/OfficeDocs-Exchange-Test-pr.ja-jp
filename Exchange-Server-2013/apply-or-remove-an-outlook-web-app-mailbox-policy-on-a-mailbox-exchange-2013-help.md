---
title: 'Outlook Web App のメールボックス ポリシーをメールボックスで適用または削除する: Exchange Online Help'
TOCTitle: Outlook Web App のメールボックス ポリシーをメールボックスで適用または削除する
ms:assetid: 51d8e269-b0d5-4bc7-9b3d-0460871e54fa
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd876884(v=EXCHG.150)
ms:contentKeyID: 49896248
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Web App のメールボックス ポリシーをメールボックスで適用または削除する

 

_**適用先:**Exchange Online, Exchange Server 2013_

Outlook Web App メールボックス ポリシーを 1 つまたは複数のメールボックスに適用したり、EAC またはシェルを使用して削除したりすることができます。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:10 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「Outlook Web App メールボックス ポリシー」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## Outlook Web App メールボックス ポリシーを適用する

## EAC を使用して Outlook Web App メールボックス ポリシーを適用する

1.  EAC で、**\[受信者\]** \> **\[メールボックス\]** をクリックします。

2.  作業ウィンドウで、Outlook Web App メールボックス ポリシーを適用するメールボックスをクリックして選択します。 複数のメールボックスを選択することもできます。

3.  **1 つのメールボックスを選択した場合。**
    
    1.  \[詳細\] ウィンドウで下にスクロールして **\[メール接続\]** を表示して、**\[詳細の表示\]** をクリックします。
    
    2.  **\[参照\]** をクリックして、表示される使用可能なメールボックス ポリシーから選択します。
    
    3.  **\[保存\]** をクリックして、選択したポリシーを選択したメールボックスに割り当てます。
    
    **複数のメールボックスを選択した場合。**
    
    1.  \[詳細\] ウィンドウで下にスクロールして **\[Outlook Web App\]** を表示して、**\[ポリシーを割り当てる\]** をクリックします。
    
    2.  **\[参照\]** をクリックして、表示される使用可能なメールボックス ポリシーから選択します。
    
    3.  **\[保存\]** をクリックして、選択したポリシーを選択したメールボックスに割り当てます。

## シェルを使用して既存のメールボックスに Outlook Web App メールボックス ポリシーを適用する

この例では、"Calendar" という名前の Outlook Web App メールボックス ポリシーをユーザー tony@contoso.com のメールボックスに適用します。

    Set-CASMailbox -Identity tony@contoso.com -OwaMailboxPolicy:Calendar

構文およびパラメーターの詳細については、「[Set-CASMailbox](https://technet.microsoft.com/ja-jp/library/bb125264\(v=exchg.150\))」を参照してください。

## Outlook Web App メールボックス ポリシーを削除する

## EAC を使用して Outlook Web App のメールボックス ポリシーを削除する

1.  EAC で、**\[受信者\]** \> **\[メールボックス\]** をクリックします。

2.  作業ウィンドウで、Outlook Web App メールボックス ポリシーを削除するメールボックスをクリックして選択します。

3.  \[詳細\] ウィンドウで下にスクロールして **\[メール接続\]** を表示して、**\[詳細の表示\]** をクリックします。
    
    メールボックス ポリシーが割り当てられている場合は、**\[クリア\]** をクリックしてメールボックスから削除します。

4.  **\[保存\]** をクリックして変更を保存します。

## シェルを使用して既存のメールボックスから Outlook Web App メールボックス ポリシーを削除する

この例では、ユーザー tony@contoso.com のメールボックスから Outlook Web App メールボックス ポリシー を削除します。

    Set-CASMailbox -Identity tony@contoso.com -OwaMailboxPolicy:$null

構文およびパラメーターの詳細については、「[Set-CASMailbox](https://technet.microsoft.com/ja-jp/library/bb125264\(v=exchg.150\))」を参照してください。

