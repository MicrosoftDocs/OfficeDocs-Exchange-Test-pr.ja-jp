---
title: 'Outlook の保護ルールを削除する: Exchange 2013 Help'
TOCTitle: Outlook の保護ルールを削除する
ms:assetid: 569fc3be-b269-43f5-8797-73ab0691e685
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee633467(v=EXCHG.150)
ms:contentKeyID: 49896262
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook の保護ルールを削除する

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2016-12-09_

Microsoft Outlook 保護ルールを使用すると、メッセージを送信する前に Outlook 2010 の「[Active Directory Rights Management サービスの概要](https://technet.microsoft.com/ja-jp/library/hh831364.aspx)」のテンプレートを適用することで、メッセージを Information Rights Management (IRM) で保護できます。Outlook 保護ルールが適用されないようにするには、ルールを無効にします。Outlook 保護ルールを削除すると、Active Directory からルールの定義が削除されます。

IRM に関連する追加の管理タスクについては、「[Information Rights Management の手順](information-rights-management-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 推定完了時間: 1 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「権限での保護」。

  - Exchange 管理センター (EAC) を使用して Outlook 保護ルールを削除することはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用して、Outlook の保護ルールを削除する

この例は、Outlook 保護ルール OPR-DG-Finance を削除します。

    Remove-OutlookProtectionRule -Identity "OPR-DG-Finance"

構文およびパラメーターの詳細については、「[Remove-OutlookProtectionRule](https://technet.microsoft.com/ja-jp/library/dd297961\(v=exchg.150\))」を参照してください。

## シェルを使用して、すべての Outlook の保護ルールを削除する

この例は、Exchange 組織内のすべての Outlook 保護ルールを削除します。

    Get-OutlookProtectionRule | Remove-OutlookProtectionRule

構文およびパラメーターの詳細については、「[Get-OutlookProtectionRule](https://technet.microsoft.com/ja-jp/library/dd298004\(v=exchg.150\))」と「[Remove-OutlookProtectionRule](https://technet.microsoft.com/ja-jp/library/dd297961\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

Outlook 保護ルールが正常に削除されたことを確認するには、[Get-OutlookProtectionRule](https://technet.microsoft.com/ja-jp/library/dd298004\(v=exchg.150\)) コマンドレットを使用して Outlook 保護ルールを取得します。Outlook 保護ルールを取得する方法の例については、**Get-OutlookProtectionRule** の「[Examples](https://technet.microsoft.com/ja-jp/dd298004\(exchg.150\)#examples)」を参照してください。

