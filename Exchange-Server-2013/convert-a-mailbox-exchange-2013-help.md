---
title: 'メールボックスを変換する: Exchange Online Help'
TOCTitle: メールボックスを変換する
ms:assetid: dfed045e-a740-4a90-aff9-c58d53592f79
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ710164(v=EXCHG.150)
ms:contentKeyID: 49896520
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックスを変換する

 

_**適用先:**Exchange Online, Exchange Server 2013_

メールボックスを別の種類のメールボックスに変換する方法は、Exchange 2010 の場合と非常によく似ています。変換を行うには、シェルの Set-Mailbox コマンドレットを使用する必要があります。

次に示すメールボックスでは、一つの種類から別の種類へと変換することができます：

  - ユーザー メールボックスからリソース (会議室または機材) メールボックス

  - 共有メールボックスからユーザー メールボックス

  - 共有メールボックスからリソース メールボックス

  - リソース メールボックスからユーザー メールボックス

  - リソース メールボックスから共有メールボックス

ハイブリッド環境で Exchange を使用している組織では、オンプレミスの Exchange 管理ツールを使用して、メールボックスを管理する必要があります。ハイブリッド環境でメールボックスを変換するために、メールボックスをオンプレミスの Exchange に移動させ、メールボックスの種類を変換してから再び Office 365 に移動させることが必要な場合があります。


> [!IMPORTANT]
> ユーザー メールボックスを共有メールボックスに変換する場合、変換する前にメールボックスからモバイル デバイスを削除する必要があります。または、変換した後にメールボックスへのモバイル アクセスをブロックする必要があります。メールボックスを共有メールボックスに変換すると、モバイル機能が正しく動作しなくなるためです。アクセスのブロックの詳細については、「<A href="https://go.microsoft.com/fwlink/p/?linkid=847873">Office 365 から元従業員を削除する</A>」を参照してください。



## シェルを使用してメールボックスを変換する

予想所要時間 : 5 分。

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「受信者プロビジョニングのアクセス許可」。

この例では、共有メールボックス MarketingDept1 をユーザー メールボックスに変換します。

    Set-Mailbox MarketingDept1 -Type Regular

*Type* パラメーターには、次の値を使用できます。

  - Regular

  - Room

  - Equipment

  - Shared

構文およびパラメーターの詳細については、「[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

メールボックスが正常に変換されたことを確認するために、次のシェル コマンドを実行します。

    Get-Mailbox -Identity MarketingDept1 | Format-List RecipientTypeDetails

*RecipientTypeDetails* の値は、*UserMailbox* にすることをお勧めします。

構文およびパラメーターの詳細については、「[Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\))」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。


