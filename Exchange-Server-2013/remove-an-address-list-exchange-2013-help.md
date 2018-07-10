---
title: 'アドレス一覧の削除: Exchange 2013 Help'
TOCTitle: アドレス一覧の削除
ms:assetid: 39a313f3-41d4-4c8f-af67-df2316f3687f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997294(v=EXCHG.150)
ms:contentKeyID: 49896203
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# アドレス一覧の削除

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-14_

ここでは、アドレス一覧の削除方法を説明します。 既定のグローバル アドレス一覧 (GAL) は削除できません。

アドレス一覧に関連する追加の管理タスクについては、「[アドレス一覧の手順](address-list-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - [電子メール アドレスおよびアドレス帳のアクセス許可](email-address-and-address-book-permissions-exchange-2013-help.md) トピックのこの手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「アドレス一覧」エントリ。

  - 子アドレス一覧が含まれている親アドレス一覧を削除することはできません。 ただし、キーボードの Ctrl キーを押しながら、親アドレス一覧と子アドレス一覧を選択すると、子アドレス一覧と親アドレス一覧の両方を削除することができます。 子アドレス一覧を削除しないで親アドレス一覧を削除しようとすると、エラーが表示されます。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EAC を使用してアドレス一覧を削除する

1.  **\[組織\]** \> **\[アドレス一覧\]** に移動します。

2.  削除するアドレス一覧をリスト ビューで選択し、**\[削除\]**![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") をクリックします。

3.  警告の **\[はい\]** をクリックしてアドレス一覧を削除します。

## シェルを使用してアドレス一覧を削除する

この例では、子アドレス一覧が含まれていない Sales Department というアドレス一覧を削除します。

    Remove-AddressList -Identity "Sales Department"

「**Y**」と入力してこのアドレス一覧を削除することを確認し、Enter キーを押します。

構文およびパラメーターの詳細については、「[Remove-AddressList](https://technet.microsoft.com/ja-jp/library/bb124342\(v=exchg.150\))」を参照してください。

## シェルを使用して子アドレス一覧を含むアドレス一覧を削除する

この例では、アドレス一覧 Departments と、その子のアドレス一覧をすべて削除します。

    Remove-AddressList -Identity Departments -Recursive

「**Y**」と入力して親アドレス一覧とその子アドレス一覧を削除することを確認し、Enter キーを押します。

構文およびパラメーターの詳細については、「[Remove-AddressList](https://technet.microsoft.com/ja-jp/library/bb124342\(v=exchg.150\))」を参照してください。

