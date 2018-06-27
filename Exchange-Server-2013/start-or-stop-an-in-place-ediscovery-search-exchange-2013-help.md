---
title: 'インプレース電子情報開示の検索の開始または停止: Exchange Online Help'
TOCTitle: インプレース電子情報開示の検索の開始または停止
ms:assetid: 0d546763-4bf5-4523-91f4-d181b7ee4ac2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd335090(v=EXCHG.150)
ms:contentKeyID: 49895238
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# インプレース電子情報開示の検索の開始または停止

 

_**適用先:**Exchange Server 2013_

インプレース電子情報開示検索をいつでも停止または再開できます。たとえば、検索するキーワードやメールボックスなどの検索プロパティを変更するには、先に検索を停止する必要があります。必要な変更後に検索を再開できます。


> [!NOTE]
> インプレース電子情報開示検索を再開する場合、検索で指定された検出メールボックスにコピーされた検索結果が削除されます。



## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「インプレース電子情報開示」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EAC を使用してインプレース電子情報開示検索を開始または停止する

1.  **\[コンプライアンス管理\]** \> **\[インプレースの電子情報開示と保持\]** に移動します。

2.  進行中の検索を停止するには、検索を選択してから **\[検索の停止\]** をクリックします。

3.  停止した検索を再開するには、検索を選択してから **\[検索の再開\]** をクリックします。

## シェルを使用してインプレース電子情報開示検索を開始または停止する

電子情報開示検索を開始する方法例については、「[Start-MailboxSearch](https://technet.microsoft.com/ja-jp/library/dd351245\(v=exchg.150\))」の「例 1」を参照してください。

電子情報開示検索を停止する方法例については、「[Stop-MailboxSearch](https://technet.microsoft.com/ja-jp/library/dd351075\(v=exchg.150\))」の「例 1」を参照してください。

