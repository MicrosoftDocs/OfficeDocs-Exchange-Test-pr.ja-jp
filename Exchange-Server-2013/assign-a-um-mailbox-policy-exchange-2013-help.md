---
title: 'UM メールボックス ポリシーの割り当て: Exchange Online Help'
TOCTitle: UM メールボックス ポリシーの割り当て
ms:assetid: c8da6cbe-3d22-4fff-8b5a-416b1c8adb6c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb201728(v=EXCHG.150)
ms:contentKeyID: 49896469
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM メールボックス ポリシーの割り当て

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユーザーのユニファイド メッセージング（UM）およびボイス メールを有効にする場合は、ユーザーのメールボックスに関連付けられた UM メールボックス ポリシーを選択する必要があります。 ユーザーの UM を有効にした後も、そのユーザーのメールボックスと関連付けられた UM メールボックス ポリシーを変更できます。

UM メールボックス ポリシーを作成し、UM が有効なユーザーのメールボックスの集合に、ポリシーやセキュリティ設定の共通セットを適用します。 UM メールボックス ポリシーを使用すると、次のような設定を適用できます。

  - PIN ポリシー

  - ダイヤルの制限

  - その他の一般的な UM メールボックス ポリシー プロパティ


> [!NOTE]
> UM ダイヤル プランを作成するたびに、既定の UM メールボックス ポリシーが作成されます。 既定の UM メールボックス ポリシーを削除したり、組織のニーズに基づいて追加の UM メールボックス ポリシーを作成したりすることができます。



ボイス メールが有効なユーザーに関連するその他の管理タスクについては、「[ユーザーのボイス メール設定の管理](manage-voice-mail-settings-for-a-user-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス ポリシー」。

  - これらの手順を実行する前に、既存の Exchange 受信者のユニファイド メッセージングが有効になっていることを確認してください。詳細な手順については、「[ボイス メール用にユーザーを有効にする](enable-a-user-for-voice-mail-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[New-UMMailboxPolicy](https://technet.microsoft.com/ja-jp/library/aa998300\(v=exchg.150\))」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して UM が有効なユーザーに割り当てられた UM メールボックス ポリシーを変更する

1.  EAC で、<strong>受信者</strong> \> <strong>メールボックス</strong>に移動します。

2.  リスト ビューで、UM メールボックス ポリシーを変更するメールボックスを選択します。

3.  詳細ペインの <strong>Phone and Voice Features (電話と音声の機能)</strong> \> <strong>ユニファイド メッセージング</strong> で <strong>詳細の表示</strong> をクリックします。

4.  <strong>UM メールボックス</strong> ページで、<strong>UM メールボックスの設定</strong> をクリックし、次に<strong>編集</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

5.  <strong>UM メールボックス</strong> ページ \> で、<strong>UM メールボックス ポリシー</strong> の横にある<strong>参照</strong> をクリックし、ユーザーの UM メールボックス ポリシーを見つけます。

6.  <strong>保存</strong> をクリックします。

## シェルを使用して UM が有効なユーザーに割り当てられた UM メールボックス ポリシーを変更する

この例では、UM が有効な Tony Smith というユーザーと、`MyUMMailboxPolicy` という UM メールボックス ポリシーを関連付けます。

    Set-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy

