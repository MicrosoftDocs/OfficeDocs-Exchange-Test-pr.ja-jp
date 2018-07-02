---
title: 'メール ユーザーへのアドレス帳ポリシーの割り当て: Exchange Online Help'
TOCTitle: メール ユーザーへのアドレス帳ポリシーの割り当て
ms:assetid: bdfe6575-24c0-47d0-9cfb-ece910db248b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Hh529942(v=EXCHG.150)
ms:contentKeyID: 49896447
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メール ユーザーへのアドレス帳ポリシーの割り当て

 

_**適用先:** Exchange Online, Exchange Server 2013_

アドレス帳ポリシー (ABP) を作成したら、それをメールボックス ユーザーに割り当てる必要があります。 ユーザー アカウントの作成時に、既定の ABP は割り当てられません。 ABP をユーザーに割り当てないと、そのユーザーは Outlook および Outlook Web App によって組織全体のグローバル アドレス一覧 (GAL) にアクセスできるようになります。 詳細については、「[アドレス帳ポリシー](address-book-policies-exchange-2013-help.md)」を参照してください。

ABP に関連する追加の管理タスクについては、「[アドレス帳ポリシーの手順](address-book-policy-procedures-exchange-2013-help.md)」を参照してください。

この手順を使用するシナリオについて「[シナリオ: アドレス帳ポリシーの展開](scenario-deploying-address-book-policies-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間: 5 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[電子メール アドレスおよびアドレス帳のアクセス許可](email-address-and-address-book-permissions-exchange-2013-help.md)」の「アドレス帳ポリシー」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EAC を使用してメールボックス ユーザーに ABP を割り当てる

1.  **\[受信者\]** \> **\[メールボックス\]** に移動します。

2.  リスト ビューで、ポリシーを割り当てるユーザーを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[メールボックス機能\]** をクリックします。

4.  **\[アドレス帳ポリシー\]** の一覧で、このユーザーに割り当てる ABP を選択します。

5.  **\[保存\]** をクリックします。

## EAC を使用して複数のメールボックス ユーザーに ABP を割り当てる

1.  **\[受信者\]** \> **\[メールボックス\]** に移動します。

2.  リスト ビューでは、Ctrl キーを使用して複数のユーザーを選択します。

3.  詳細ウィンドウで、**\[その他のオプション\]** をクリックします。

4.  **\[アドレス帳ポリシー\]** で **\[更新\]** をクリックします。

5.  **\[アドレス帳ポリシーを選択\]** の一覧で、これらのユーザーに適用する ABP を選択します。

6.  **\[保存\]** をクリックします。

## シェルを使用して、メールボックス ユーザーに ABP を割り当てる

この例では、All Fabrikam という ABP を既存のメールボックス ユーザー joe@fabrikam.com に割り当てます。

    Set-Mailbox -Identity joe@fabrikam.com -AddressBookPolicy "All Fabrikam"

この例では、ABP\_EngineeringDepartment という ABP を、`CustomAttribute11` 値に「Engineering Department」を含むメールボックス ユーザー全員に割り当てます。

    Get-Mailbox -Filter {(CustomAttribute11 -like "Engineering Department")} | Set-Mailbox -AddressBookPolicy ABP_EngineeringDepartment

構文およびパラメーターの詳細については、「[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))」と「[Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\))」を参照してください。

