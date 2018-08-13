---
title: 'アドレス帳ポリシーの削除: Exchange Online Help'
TOCTitle: アドレス帳ポリシーの削除
ms:assetid: c20c6f82-2f75-4116-9be1-c5af10113f71
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Hh529946(v=EXCHG.150)
ms:contentKeyID: 49896457
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# アドレス帳ポリシーの削除

 

_**適用先:** Exchange Online, Exchange Server 2013_

アドレス帳ポリシー (ABP) を削除するには、この手順を使用します。

ABP に関連する追加の管理タスクについては、「[アドレス帳ポリシーの手順](address-book-policy-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[電子メール アドレスおよびアドレス帳のアクセス許可](email-address-and-address-book-permissions-exchange-2013-help.md)」の「アドレス帳ポリシー」。

  - ユーザーのメールボックスまたは回復可能な削除によって削除されたメールボックスに関連付けられている ABP は削除できません。ABP がユーザーに割り当てられているかどうかを確認するには、次のシェル コマンドを実行します。
    
    `Get-Mailbox | Where $._AddressBookPolicy -eq <AddressBookPolicyName>`
    
    ABP が回復可能な削除によって削除されたメールボックスに割り当てられているかどうかを確認するには、次のコマンドを実行します。
    
    `Get-Mailbox -SoftDeletedMailbox | Where $._AddressBookPolicy -eq <AddressBookPolicyName>`

  - ユーザーのメールボックスから ABP を削除するには、メールボックスのプロパティの **\[メールボックスの機能\]** ページか、**Set-Mailbox** コマンドレットを使用します。

  - Exchange 管理センター (EAC) を使用して ABP を削除することはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用して ABP を削除する

この例では、ABP\_TailspinToys という ABP を削除します。

    Remove-AddressBookPolicy -Identity "ABP_TailspinToys"

構文およびパラメーターの詳細については、「[Remove-AddressBookPolicy](https://technet.microsoft.com/ja-jp/library/hh529929\(v=exchg.150\))」を参照してください。

