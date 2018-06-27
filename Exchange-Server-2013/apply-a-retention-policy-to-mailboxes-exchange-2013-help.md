---
title: 'メールボックスにアイテム保持ポリシーを適用する: Exchange Online Help'
TOCTitle: メールボックスにアイテム保持ポリシーを適用する
ms:assetid: 6ccc80db-d201-44f7-8d4b-473a89c14b2f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd298052(v=EXCHG.150)
ms:contentKeyID: 49896301
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックスにアイテム保持ポリシーを適用する

 

_**適用先:**Exchange Online, Exchange Server 2013_

アイテム保持ポリシーを使用すると、1 つまたは複数の保持タブをグループ化して、それらをメールボックスに適用してメッセージ保持設定を適用することができます。メールボックスには複数のアイテム保持ポリシーを設定することはできません。


> [!NOTE]
> メッセージは、ポリシーにリンクしたアイテム保持タグで定義された設定に基づいて期限が切れます。これらの設定には、メッセージをアーカイブに移動するか、または完全に削除するといった処理が含まれます。アイテム保持ポリシーを複数のメールボックスに適用する前に、ポリシーのテストを実行し、ポリシーに関連づけられた各アイテム保持タグを検査することを推奨します。



メッセージング レコード管理 (MRM) に関連する追加の管理タスクについては、「[メッセージング レコード管理の手順](messaging-records-management-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間: 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「アイテム保持ポリシーの適用」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EAC を使用して単一のメールボックスにアイテム保持ポリシーを適用する

1.  **\[受信者\]** \> **\[メールボックス\]** に移動します。

2.  リスト ビューで、アイテム保持ポリシーを適用するメールボックスを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[ユーザー メールボックス\]** で、**\[メールボックスの機能\]** をクリックします。

4.  **\[アイテム保持ポリシー\]**で、メールボックスに適用するポリシーを選択し、**\[保存\]** をクリックします。

## EAC を使用して複数のメールボックスにアイテム保持ポリシーを適用する

1.  **\[受信者\]** \> **\[メールボックス\]** に移動します。

2.  リスト ビューで、Shift キーまたは Ctrl キーを使用して複数のメールボックスを選択します。

3.  詳細ウィンドウで、**\[その他のオプション\]** をクリックします。

4.  **\[アイテム保持ポリシー\]** 下で **\[更新\]** をクリックします。

5.  **\[アイテム保持ポリシーの一括割り当て\]**で、メールボックスに適用するアイテム保持ポリシーを選択し、**\[保存\]** をクリックします。

## シェルを使用して単一のメールボックスにアイテム保持ポリシーを適用する

この例では、Morris のメールボックスにアイテム保持ポリシー RP-Finance を適用します。

    Set-Mailbox "Morris" -RetentionPolicy "RP-Finance"

構文およびパラメーターの詳細については、「[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))」を参照してください。

## シェルを使用して複数のメールボックスにアイテム保持ポリシーを適用する

この例では、古いポリシー Old-Retention-Policy が適用されているすべてのメールボックスに対して、新しいアイテム保持ポリシー New-Retention-Policy を適用します。

    $OldPolicy={Get-RetentionPolicy "Old-Retention-Policy"}.distinguishedName
    Get-Mailbox -Filter {RetentionPolicy -eq $OldPolicy} -Resultsize Unlimited | Set-Mailbox -RetentionPolicy "New-Retention-Policy"

この例では、RetentionPolicy-Corp アイテム保持ポリシーを Exchange 組織のすべてのメールボックスに適用します。

    Get-Mailbox -ResultSize unlimited | Set-Mailbox -RetentionPolicy "RetentionPolicy-Corp"

この例では、RetentionPolicy-Finance アイテム保持ポリシーを Finance 組織単位のすべてのメールボックスに適用します。

    Get-Mailbox -OrganizationalUnit "Finance" -ResultSize Unlimited | Set-Mailbox -RetentionPolicy "RetentionPolicy-Finance"

構文およびパラメーターの詳細については、「[Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\))」と「[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

アイテム保持ポリシーが適用されたことを確認するには、[Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\)) コマンドレットを実行して、そのメールボックス (1 つまたは複数) のアイテム保持ポリシーを取得します。

この例では、Morris のメールボックスのアイテム保持ポリシーを取得します。

    Get-Mailbox Morris | Select RetentionPolicy

このコマンドは、RP-Finance アイテム保持ポリシーが適用されたすべてのメールボックスを取得します。

    Get-Mailbox -ResultSize unlimited | Where-Object {$_.RetentionPolicy -eq "RP-Finance"} | Format-Table Name,RetentionPolicy -Auto

