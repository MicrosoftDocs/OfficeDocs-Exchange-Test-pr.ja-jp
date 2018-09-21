---
title: '管理フォルダーからの移行: Exchange 2013 Help'
TOCTitle: 管理フォルダーからの移行
ms:assetid: 6796a79d-501e-4216-9370-77965bc5835d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd298032(v=EXCHG.150)
ms:contentKeyID: 52057834
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理フォルダーからの移行

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-07_

Microsoft Exchange Server 2013 では、メッセージング レコード管理 (MRM) は保持タグとアイテム保持ポリシーを使用して実行されます。アイテム保持ポリシーは、メールボックスに適用可能な保持タグのグループです。詳細については、「[保持タグおよびアイテム保持ポリシー](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/messaging-records-management/retention-tags-and-policies)」を参照してください。Exchange Server 2007 で導入された MRM テクノロジである管理フォルダーはサポートされていません。

管理フォルダーのあるメールボックスで、メールボックス ポリシーが適用されたものは、アイテム保持ポリシーを使用するように移行できます。そうするには、ユーザーの管理フォルダーのメールボックス ポリシーにリンクした管理フォルダーと同等の保持タグを作成する必要があります。


> [!IMPORTANT]
> 運用環境で管理フォルダーからアイテム保持ポリシーに移行する前に、テスト環境でプロセスをテストすることをお勧めします。




> [!TIP]
> メールボックスの保存機能を有効にして、アイテム保持ポリシーまたは管理フォルダー メールボックス ポリシーの処理を中止できます。メールボックスの保存機能を有効にすると、新しいポリシー設定がテスト メールボックスまたは運用メールボックスのいくつかでテストされるまで、メッセージの削除やアーカイブへの移動ができなくなり、移行シナリオで役に立ちます。詳細については、「<A href="https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/messaging-records-management/mailbox-retention-hold">メールボックスの保存機能を有効にする</A>」を参照してください。



MRM に関連するその他の管理タスクについては、「[メッセージング レコード管理の手順](messaging-records-management-procedures-exchange-2013-help.md)」を参照してください。

## 保持タグと管理フォルダーの比較

保持設定に基づいてユーザーがアイテムを管理フォルダーに移動する必要がある管理フォルダーとは違い、保持タグはメールボックスのフォルダーまたは個別のアイテムに適用できます。この処理は、ユーザーのワークフローと電子メール組織の手法に与える影響を最小限に抑えます。フォルダーに保持タグが適用されている場合、そのフォルダー内のすべてのアイテムは保持設定を継承します。ユーザーは、フォルダー内の個別のアイテムに対して別々の保持タグを適用することにより、保持設定をさらに細かく指定できます。

管理フォルダーは、それぞれに異なるメッセージ クラス (電子メール アイテムまたは予定表アイテムなど) を持つフォルダーに対して、異なる管理コンテンツの設定をサポートしています。保持タグはタグのプロパティで指定されるため、保持タグには異なる管理コンテンツの設定オブジェクトは必要ありません。特定のメッセージ クラスに対する保持タグの作成はサポートされていませんが、ボイス メール メッセージ用の既定のポリシー タグ (DPT) は例外になります。また、保持タグは、管理フォルダー アシスタントによるジャーナリングの使用を許可しません。


> [!NOTE]
> ジャーナル ルールは、ジャーナル用メールボックスにジャーナル レポートを添付したメッセージのコピーを送信するために使用されます。このルールは、ジャーナリング エージェントによってトランスポート パイプラインに適用され、MRM からは独立しています。詳細については、「<A href="journaling-exchange-2013-help.md">ジャーナル</A>」を参照してください。



次の表では、保持タグまたは管理フォルダーを使用した場合に利用可能な、MRM の機能を比較します。

### 保持タグと管理フォルダー

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>保持タグ</th>
<th>管理フォルダー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>既定のフォルダー (受信トレイなど) に対する保存期間の設定の指定</p></td>
<td><p>アイテム保持ポリシー タグ (RPT) を使用する</p></td>
<td><p>管理された既定フォルダーを使用する</p></td>
</tr>
<tr class="even">
<td><p>メールボックス全体に対して保存期間の設定を指定する</p></td>
<td><p>既定のポリシー タグ (DPT) を使用する</p></td>
<td><p>既定の管理フォルダーを使用する</p></td>
</tr>
<tr class="odd">
<td><p>カスタム フォルダーの保存期間の設定を使用する</p></td>
<td><p>個人タグを使用する</p></td>
<td><p>管理されたカスタム フォルダーを使用する</p></td>
</tr>
<tr class="even">
<td><p>管理コンテンツの設定が必要</p></td>
<td><p>いいえ(アイテム保持タグに含まれている保存期間の設定)</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p>異なるメッセージ クラスに対して保存期間の設定を使用する (電子メールのメッセージ、ボイス メール、または予定表アイテムなど)</p></td>
<td><p>いいえ</p></td>
<td><p>○</p></td>
</tr>
<tr class="even">
<td><p>アイテムをユーザーのアーカイブ メールボックスに移動する、アーカイブへ移動の操作をサポートする</p></td>
<td><p>○</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>管理フォルダーへ移動の操作をサポートする</p></td>
<td><p>X</p></td>
<td><p>○</p></td>
</tr>
<tr class="even">
<td><p>管理フォルダー アシスタントを使用したジャーナリングを許可する</p></td>
<td><p>X</p></td>
<td><p>○</p></td>
</tr>
<tr class="odd">
<td><p>ユーザーに適用されるポリシー</p></td>
<td><p>アイテム保持ポリシー</p></td>
<td><p>管理フォルダー メールボックス ポリシー</p></td>
</tr>
<tr class="even">
<td><p>メールボックス ユーザーに適用できるポリシーの最大数</p></td>
<td><p>1</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>管理フォルダー アシスタントによって処理</p></td>
<td><p>○</p></td>
<td><p>○</p></td>
</tr>
<tr class="even">
<td><p>クライアント サポート</p></td>
<td><p>Microsoft Outlook 2010 および OfficeOutlook Web App</p></td>
<td><p>Outlook 2010、Office Outlook 2007、および Outlook Web App</p></td>
</tr>
</tbody>
</table>


## 始める前に把握しておくべき情報

  - 予想所要時間 : 20 分。

  - このトピックの手順には、特定のアクセス許可が必要です。アクセス許可情報については、各手順を参照してください。

  - Exchange 管理センター (EAC) を使用して、アイテム保持ポリシーをベースに保持タグを作成することはできません。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## 管理フォルダーからメールボックス ユーザーを移行する

以下は、ユーザーをこの管理フォルダー メールボックス ポリシーからアイテム保持ポリシーに移行する際の一般的な手順です。それぞれの手順については、後で説明します。

1.  すべての Exchange 2010 および Exchange 2007 メールボックスに適用される管理フォルダー メールボックス ポリシー、各ポリシーの管理フォルダー、および各管理フォルダーの管理コンテンツの設定について、情報を収集します。この情報を収集するには、Exchange 2010 または Exchange 2007 サーバーで EMC またはシェルを使用します。

2.  移行用の保持タグを作成します。

3.  アイテム保持ポリシーを作成し、新しく作成した保持タグをポリシーにリンクします。

4.  管理フォルダー メールボックス ポリシーを削除してから、ユーザー メールボックスにアイテム保持ポリシーを適用します。
    

    > [!IMPORTANT]
    > アイテム保持ポリシーをユーザーに適用して、管理フォルダー アシスタントを実行した後は、ユーザーのメールボックス内の管理フォルダーは管理されていない状態になります。



以下の手順に関して、Contoso 社のメールボックスには管理フォルダー メールボックス ポリシーが適用済みで、以下の管理フォルダーが含まれています。

### Contoso 社の管理フォルダー

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>管理フォルダー</th>
<th>管理コンテンツの設定</th>
<th>保存期間が有効</th>
<th>保存期間</th>
<th>保存期間のアクション</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Corp-DeletedItems</p></td>
<td><p>CS-Corp-DeletedItems</p></td>
<td><p>○</p></td>
<td><p>30 日</p></td>
<td><p>削除して回復を許可する</p></td>
</tr>
<tr class="even">
<td><p>Corp-SentItems</p></td>
<td><p>CS-Corp-SentItems</p></td>
<td><p>○</p></td>
<td><p>1,825 日</p></td>
<td><p>削除済みアイテムに移動する</p></td>
</tr>
<tr class="odd">
<td><p>Corp-JunkMail</p></td>
<td><p>CS-Corp-JunkMail</p></td>
<td><p>○</p></td>
<td><p>30 日</p></td>
<td><p>完全に削除</p></td>
</tr>
<tr class="even">
<td><p>Corp-EntireMailbox</p></td>
<td><p>CS-Corp-EntireMailbox</p></td>
<td><p>○</p></td>
<td><p>365 日</p></td>
<td><p>削除済みアイテムに移動する</p></td>
</tr>
<tr class="odd">
<td><p>30 日</p></td>
<td><p>CS-30Days</p></td>
<td><p>○</p></td>
<td><p>30 日</p></td>
<td><p>削除済みアイテムに移動する</p></td>
</tr>
<tr class="even">
<td><p>5 年間</p></td>
<td><p>CS-5Years</p></td>
<td><p>○</p></td>
<td><p>1,825 日</p></td>
<td><p>削除済みアイテムに移動する</p></td>
</tr>
<tr class="odd">
<td><p>期限切れにしない</p></td>
<td><p>CS-NeverExpire</p></td>
<td><p>X</p></td>
<td><p>365 日</p></td>
<td><p>該当なし</p></td>
</tr>
</tbody>
</table>


## 実行方法

## 手順 1:移行用に保持タグを作成します

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「メッセージング レコード管理」。

この手順に使用できるメソッドは次の 2 つです。

  - **管理フォルダーとそれに対応する管理コンテンツの設定をベースに保持タグを作成する**   この方法では、*ManagedFolderToUpgrade* パラメーターを指定した **New-RetentionPolicyTag** コマンドレットを使用します。このパラメーターを指定すると、対応する保持タグが管理フォルダーに自動的に適用されます。
    

    > [!IMPORTANT]
    > 移植する管理フォルダーに異なるメッセージ クラスのための複数の管理コンテンツ設定がある場合、保持タグは 1 つだけ作成され、移植されたタグの保存期限には、管理コンテンツ設定のメッセージ クラスとは関係なく、すべての管理コンテンツ設定の中で一番後の保存期限が使用されます。<BR>たとえば、管理フォルダー Corp-DeletedItems の次の管理コンテンツ設定を確認します。



  - **手動で保持設定を指定して、保持タグを作成する**   この方法では、*ManagedFolderToUpgrade* パラメーターを指定せずに **New-RetentionPolicyTag** コマンドレットを使用します。このパラメーターを指定しない場合、ポリシーに追加したすべてのアイテム保持ポリシー タグは既定のフォルダーに追加され、既定のポリシー タグはメールボックス全体に適用されます。ただし、ポリシーに追加したいかなる個人用タグも管理フォルダーに自動的に適用されることはありません。


> [!NOTE]
> Exchange 2013 および Exchange 2010 サーバーが混在する環境の場合、Exchange 管理コンソール (EMC) の<STRONG>管理フォルダーの移植</STRONG>ウィザードを Exchange 2010 サーバーで使用すると、管理フォルダーとそれに対応する管理コンテンツの設定を簡単に保持タグに移植できます。



**管理フォルダーに基づいた保持タグを作成する**

この例では、Contoso 管理フォルダー メールボックス ポリシーで示される、対応する管理コンテンツの設定に基づいて、保持タグを作成します。

    New-RetentionPolicyTag Corp-DeletedItems -ManagedFolderToUpgrade Corp-DeletedItems
    New-RetentionPolicyTag Corp-SentItems -ManagedFolderToUpgrade Corp-SentItems
    New-RetentionPolicyTag Corp-JunkMail -ManagedFolderToUpgrade Corp-JunkMail
    New-RetentionPolicyTag Corp-EntireMailbox -ManagedFolderToUpgrade Corp-EntireMailbox
    New-RetentionPolicyTag 30Days -ManagedFolderToUpgrade 30Days
    New-RetentionPolicyTag 5Years -ManagedFolderToUpgrade 5Years
    New-RetentionPolicyTag NeverExpire -ManagedFolderToUpgrade NeverExpire

構文およびパラメーターの詳細については、「[New-RetentionPolicyTag](https://technet.microsoft.com/ja-jp/library/dd335226\(v=exchg.150\))」を参照してください。

**保持タグを手動で作成する**


> [!NOTE]
> また、EAC を使用すると、(管理フォルダーの設定をベースとせずに) 保持タグを手動で作成することもできます。詳細については、「<A href="https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/messaging-records-management/create-a-retention-policy">アイテム保持ポリシーの作成</A>」を参照してください。



この例では、管理フォルダーおよび Contoso 管理フォルダー メールボックス ポリシーで示される、対応する管理コンテンツの設定に基づいて、保持タグを作成します。保存設定は、*ManagedFolderToUpgrade* パラメーターを使用せずに手動で指定されます。

    New-RetentionPolicyTag Corp-DeletedItems -Type DeletedItems -RetentionEnabled $true -AgeLimitForRetention 30 -RetentionAction DeleteAndAllowRecovery
    New-RetentionPolicyTag Corp-SentItems -Type SentItems -RetentionEnabled $true -AgeLimitforRetention 1825 -RetentionAction MoveToDeletedItems
    New-RetentionPolicyTag Corp-JunkMail -Type JunkMail -RetentionEnabled $true -AgeLimitforRetention 30 -RetentionAction PermanentlyDelete
    New-RetentionPolicyTag Corp-EntireMailbox -Type All -RetentionEnabled $true -AgeLimitForRetention 365 -RetentionAction MoveToDeletedItems
    New-RetentionPolicyTag 30Days -Type Personal -RetentionEnabled $true -AgeLimitForRetention 30 -RetentionAction MoveToDeletedItems
    New-RetentionPolicyTag 5Years -Type Personal -RetentionEnabled $true -AgeLimitForRetention 1825 -RetentionAction MoveToDeletedItems
    New-RetentionPolicyTag NeverExpire -Type Personal -RetentionEnabled $false

構文およびパラメーターの詳細については、「[New-RetentionPolicyTag](https://technet.microsoft.com/ja-jp/library/dd335226\(v=exchg.150\))」を参照してください。

## 手順 2:アイテム保持ポリシーを作成する

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「メッセージング レコード管理」。


> [!NOTE]
> また、EAC を使用すると、アイテム保持ポリシーを作成し、そのポリシーに保持タグを追加できます。詳細については、「<A href="https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/messaging-records-management/create-a-retention-policy">アイテム保持ポリシーの作成</A>」を参照してください。



この例では、アイテム保持ポリシー RP-Corp を作成し、新しく作成した保持タグをポリシーにリンクします。

    New-RetentionPolicy RP-Corp -RetentionPolicyTagLinks Corp-DeletedItems,Corp-SentItems,Corp-JunkMail,Corp-EntireMailbox,30Days,NeverExpire

構文およびパラメーターの詳細については、「[New-RetentionPolicy](https://technet.microsoft.com/ja-jp/library/dd297970\(v=exchg.150\))」を参照してください。

## 手順 3:ユーザー メールボックスから管理フォルダー メールボックス ポリシーを削除する

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「アイテム保持ポリシーの適用」。

この例では、Ken Kwok のメールボックスから、管理フォルダー メールボックス ポリシーとすべての管理フォルダーを削除します。メッセージがある管理フォルダーは削除されません。

    Set-Mailbox -Identity Kwok -RemoveManagedFolderAndPolicy RP-Corp

## 手順 4:アイテム保持ポリシーをユーザーのメールボックスに適用する

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「アイテム保持ポリシーの適用」。


> [!NOTE]
> また、EAC を使用するとアイテム保持ポリシーをユーザーに適用できます。詳細については、「<A href="https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/messaging-records-management/apply-retention-policy">メールボックスにアイテム保持ポリシーを適用する</A>」を参照してください。



この例では、新しく作成したアイテム保持ポリシー RP-Corp をメールボックス ユーザー Ken Kwok に適用します。

    Set-Mailbox -Identity Kwok -RetentionPolicy RP-Corp

構文およびパラメーターの詳細については、「[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))」を参照してください。

## このタスクの検証方法

管理フォルダーからアイテム保持ポリシーに移行したことを確認するには、次の手順を実行します。

  - すべてのユーザー メールボックスと、それらに適用されたアイテム保持ポリシーのレポートを生成します。
    
    このコマンドは、組織内すべてのメールボックスに適用されたアイテム保持ポリシーと、それらのアイテム保持の状態を取得します。
    
        Get-Mailbox -ResultSize unlimited -Filter {Name -NotLike "DiscoverySearch*�?} | Format-Table Name,RetentionPolicy,RetentionHoldEnabled -Auto

  - 管理フォルダー アシスタントがアイテム保持ポリシーを使用してメールボックスを処理した後、[Get-RetentionPolicyTag](https://technet.microsoft.com/ja-jp/library/dd298009\(v=exchg.150\)) コマンドレットを使用して、ユーザー メールボックスでプロビジョニングされた保持タグを取得します。
    
    このコマンドは、実際に April Stewart のメールボックスに適用されている保持タグを取得します。
    
        Get-RetentionPolicyTag -Mailbox astewart

