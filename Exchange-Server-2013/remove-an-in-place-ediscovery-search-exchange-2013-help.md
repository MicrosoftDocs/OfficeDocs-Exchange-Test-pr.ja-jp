---
title: 'インプレース電子情報開示検索の削除: Exchange Online Help'
TOCTitle: インプレース電子情報開示検索の削除
ms:assetid: 78461a78-1255-4a26-9d36-c6b8eb82a4f9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd298078(v=EXCHG.150)
ms:contentKeyID: 49896327
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# インプレース電子情報開示検索の削除

 

_**適用先:** Exchange Server 2013_

Microsoft Exchange Server 2013 では、インプレースの電子証拠開示を使用して、メールボックスのコンテンツを検索できます。インプレースの電子証拠開示検索はいつでも削除できます。インプレースの電子証拠開示検索を削除すると、検索結果が探索メールボックスから削除されます。


> [!NOTE]
> インプレースの電子証拠開示検索を削除すると、探索メールボックスにコピーされたすべての検索結果が削除されます。



## 始める前に把握しておくべき情報

  - 推定完了時間: 2 ～ 5 分。

  - インプレース保持が有効になっているインプレースの電子証拠開示検索を削除するには、最初に検索からインプレース保持を削除する必要があります。詳細については、「[インプレース保持を作成または削除する](create-or-remove-an-in-place-hold-exchange-2013-help.md)」を参照してください。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「インプレース電子情報開示」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

## 必要な作業

## EAC を使用してインプレースの電子証拠開示検索を削除する

1.  <strong>コンプライアンス管理</strong> \> <strong>インプレースの電子証拠開示と保持</strong> に移動します。

2.  リスト ビューで、削除するインプレースの電子証拠開示検索を選択し、<strong>削除</strong>![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") をクリックします。

## シェルを使用してインプレースの電子証拠開示検索を削除する

インプレースの電子証拠開示検索を削除する方法の例については、「[Remove-MailboxSearch](https://technet.microsoft.com/ja-jp/library/dd298130\(v=exchg.150\))」の「例」のセクションを参照してください。

## 正常な動作を確認する方法

インプレースの電子証拠開示検索が正常に削除されたことを確認するには、次のいずれかの操作を実行します。

  - EAC を使用して、検索が <strong>インプレースの電子証拠開示と保持</strong> タブのリスト ビューに表示されないことを確認します。

  - **Get-MailboxSearch** コマンドレットを使用して、インプレースの電子証拠開示検索を取得します。インプレースの電子証拠開示検索を取得する方法の例については、「[Get-MailboxSearch](https://technet.microsoft.com/ja-jp/library/dd351021\(v=exchg.150\))」の「例」のセクションを参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。


