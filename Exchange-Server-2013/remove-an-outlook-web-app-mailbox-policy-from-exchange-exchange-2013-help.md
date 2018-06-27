---
title: 'Exchange から Outlook Web App のメールボックス ポリシーを削除する: Exchange Online Help'
TOCTitle: Exchange から Outlook Web App のメールボックス ポリシーを削除する
ms:assetid: edab7bac-b62c-4b82-8f21-dcac77cf0e8f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd351239(v=EXCHG.150)
ms:contentKeyID: 49896543
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange から Outlook Web App のメールボックス ポリシーを削除する

 

_**適用先:**Exchange Online, Exchange Server 2013_

EAC またはシェルを使用して、Exchange 組織から MicrosoftOutlook Web App メールボックス ポリシーを削除できます。

Outlook Web App メールボックス ポリシーに関連する追加の管理タスクについては、「[Outlook Web App メールボックス ポリシー](outlook-web-app-mailbox-policies-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:3 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「Outlook Web App メールボックス ポリシー」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して Outlook Web App のメールボックス ポリシーを削除する

1.  EAC で、**\[アクセス許可\]** \> **\[Outlook Web App policies\]** の順にクリックします。

2.  結果ウィンドウで、削除するメールボックス ポリシーをクリックして選択します。

3.  **\[削除\]** をクリックします。

4.  確認ウィンドウで **\[はい\]** をクリックしてメールボックス ポリシーを削除するか、**\[いいえ\]** をクリックして削除を取り消します。

## シェルを使用して Outlook Web App メールボックス ポリシーを削除する

この例では、`Policy1` という名前の Outlook Web App メールボックス ポリシーを削除します。

    Remove-OwaMailboxPolicy -Name Policy1 

構文およびパラメーターの詳細については、「[Remove-OwaMailboxPolicy](https://technet.microsoft.com/ja-jp/library/dd298103\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

Outlook Web App メールボックス ポリシーが正常に削除されたことを確認するには、次の手順を実行します。

  - EAC で、**\[アクセス許可\]** \> **\[Outlook Web App policies\]** の順にクリックします。削除したポリシーは一覧に表示されなくなります。

