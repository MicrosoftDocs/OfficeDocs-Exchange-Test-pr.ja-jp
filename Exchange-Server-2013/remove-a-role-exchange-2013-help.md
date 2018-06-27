---
title: '役割を削除する: Exchange 2013 Help'
TOCTitle: 役割を削除する
ms:assetid: 2fb6f453-f37a-4636-8353-3f9927f81298
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd335178(v=EXCHG.150)
ms:contentKeyID: 49896188
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 役割を削除する

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2012-10-03_

不要になった管理役割を組織から削除できます。 削除できるのは、自分で作成した管理役割だけです。 組み込みの管理役割を削除することはできません。Microsoft Exchange Server 2013 での管理役割の詳細については、「[管理の役割について](understanding-management-roles-exchange-2013-help.md)」を参照してください。

役割に関連する他の管理タスクについては、 「[高度な権限](advanced-permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「管理役割」。

  - これらの手順を実行するには、シェルを使用する必要があります。

  - 管理役割を削除する前に、その管理役割の割り当てをすべて削除する必要があります。 役割の割り当てを削除する方法の詳細については、「[ユーザーまたは USG から役割を削除する](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## 子の役割を持たない管理役割を削除する

子の役割を持たない役割を削除するには、次の構文を使用します。

    Remove-ManagementRole <role name>

この例では、"Seattle Server Administrators/Seattle のサーバー管理者" 役割を削除します。

    Remove-ManagementRole "Seattle Server Administrators"

構文およびパラメーターの詳細については、「[Remove-ManagementRole](https://technet.microsoft.com/ja-jp/library/dd351170\(v=exchg.150\))」を参照してください。

## 子の役割を持つ管理役割を削除する

削除する役割に子の役割がある場合は、子の役割もすべて削除する必要があります。 *Recurse* スイッチを使用しない限り、子の役割を持つ役割を削除しようとすると、エラー メッセージが表示されます。 役割を削除するときに *Recurse* スイッチを使用すると、指定した役割とそのすべての子の役割が削除されます。


> [!NOTE]
> <EM>Recurse</EM> スイッチを使用する場合、削除するよう指定した役割の子の役割もすべて削除されます。 このコマンドを実行する前に、どの役割が削除されるかを理解しておく必要があります。



削除したい役割のみが削除されることを確認するには、*WhatIf* スイッチを自分のコマンドで使用して、それが正しいことを確認します。 以下の構文を使用します。

    Remove-ManagementRole <role name> -Recurse -WhatIf

*WhatIf* スイッチは、変更をコミットせずにコマンドを実行し、削除される役割を報告します。 *WhatIf* スイッチの詳細については、「[WhatIf、Confirm、および ValidateOnly スイッチ](whatif-confirm-and-validateonly-switches-exchange-2013-help.md)」を参照してください。

削除したい役割のみが削除されることを確認したら、同じコマンドを *WhatIf* スイッチなしで実行します。 この例では、"London Administrators/London の管理者" 役割とそのすべての子の役割を削除します。

    Remove-ManagementRole "London Administrators" -Recurse

構文およびパラメーターの詳細については、「[Remove-ManagementRole](https://technet.microsoft.com/ja-jp/library/dd351170\(v=exchg.150\))」を参照してください。

## 対象範囲外の管理役割を削除する

対象範囲外の役割を削除するには、このトピックで前に「子の役割を持たない管理役割を削除する」と「子の役割を持つ管理役割を削除する」で説明した手順と同じ手順を使用できます。 唯一異なるのは、対象範囲外の役割を削除する場合で、コマンドを実行するときに *UnScopedTopLevel* スイッチを指定する必要があります。 この例では、対象範囲外の役割とそのすべての子の役割を削除します。

    Remove-ManagementRole "Custom IT Scripts" -Recurse -UnScopedTopLevel

他の役割を削除する場合と同様に、*WhatIf* スイッチを使用して正しい役割を削除していることを確認します。

構文およびパラメーターの詳細については、「[Remove-ManagementRole](https://technet.microsoft.com/ja-jp/library/dd351170\(v=exchg.150\))」を参照してください。

