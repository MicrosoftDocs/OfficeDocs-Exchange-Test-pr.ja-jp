---
title: 'アイテム保持ポリシーへの保持タグの追加、またはアイテム保持ポリシーからの保持タグの削除: Exchange Online Help'
TOCTitle: アイテム保持ポリシーへの保持タグの追加、またはアイテム保持ポリシーからの保持タグの削除
ms:assetid: 3a5196ce-2764-453d-9bc1-5ec22d06b40d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd362328(v=EXCHG.150)
ms:contentKeyID: 49896205
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# アイテム保持ポリシーへの保持タグの追加、またはアイテム保持ポリシーからの保持タグの削除

 

_**適用先:** Exchange Online, Exchange Server 2013_

ポリシーの作成時またはそれ以降いつでも、保持タグをアイテム保持ポリシーに追加できます。保持ポリシーの作成方法 (同時に保持タグを追加する方法を含む) については、「[アイテム保持ポリシーの作成](create-a-retention-policy-exchange-2013-help.md)」を参照してください。

保持ポリシーには、次の保持タグを含めることができます。

  - サポートされている既定のフォルダー用の 1 つまたは複数の保持ポリシー タグ (RPT)

  - <strong>アーカイブに移動する</strong>アクションを伴う 1 つの既定ポリシー タグ (DPT)

  - <strong>削除して回復を許可する</strong> または <strong>完全に削除</strong> アクションを持つ 1 つの DPT。

  - ボイス メール用の 1 つの DPT

  - 個人タグの数

保持タグの詳細については、「[保持タグおよびアイテム保持ポリシー](retention-tags-and-retention-policies-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 推定完了時間: 10 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「メッセージング レコード管理」。

  - 保持タグは、保持ポリシーにリンクされ、管理フォルダー アシスタントによってメールボックスが処理されるまで、メールボックスには適用されません。メールボックスを処理できるように管理フォルダー アシスタントを開始するには、「[管理フォルダー アシスタントの構成](configure-the-managed-folder-assistant-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EAC を使用して保持タグを追加する、または保持タグを削除する

1.  <strong>コンプライアンス管理</strong>\><strong>アイテム保持ポリシー</strong> に移動します。

2.  リスト ビューで、保持タグを追加するアイテム保持ポリシーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>アイテム保持ポリシー</strong> で、以下の設定を使用します。
    
      - <strong>追加</strong> ![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン")   保持タグをポリシーに追加するには、このボタンをクリックします。
    
      - <strong>削除</strong> ![\[削除\] アイコン](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[削除] アイコン")   一覧からタグを選択し、このボタンをクリックしてポリシーからタグを削除します。

## シェルを使用して保持タグを追加する、または保持タグを削除する

この例では、既にリンクされた保持タグを持っていない保持ポリシー RetPolicy-VPs に、保持タグ VPs-Default、VPs-Inbox、および VPs-DeletedItems を追加します。


> [!NOTE]
> ポリシーにリンクされた保持タグがある場合には、このコマンドは既存のタグを置き換えます。



    Set-RetentionPolicy -Identity "RetPolicy-VPs" -RetentionPolicyTagLinks "VPs-Default","VPs-Inbox","VPs-DeletedItems"

この例では、VPs-DeletedItems という保持タグを、既に他の保持タグがリンクされている RetPolicy-VPs というアイテム保持ポリシーに追加します。

    $TagList = (Get-RetentionPolicy "RetPolicy-VPs").RetentionPolicyTagLinks
    $TagList.Add((Get-RetentionPolicyTag 'VPs-DeletedItems').DistinguishedName)
    Set-RetentionPolicy "RetPolicy-VPs" -RetentionPolicyTagLinks $TagList

この例では、保持タグ VPs-Inbox を保持ポリシー RetPolicy-VPs から削除します。

    $TagList = (Get-RetentionPolicy "RetPolicy-VPs").RetentionPolicyTagLinks
    $TagList.Remove((Get-RetentionPolicyTag 'VPs-Inbox').DistinguishedName)
    Set-RetentionPolicy "RetPolicy-VPs" -RetentionPolicyTagLinks $TagList

構文およびパラメーターの詳細については、「[Set-RetentionPolicy](https://technet.microsoft.com/ja-jp/library/dd335196\(v=exchg.150\))」と「[Get-RetentionPolicy](https://technet.microsoft.com/ja-jp/library/dd298086\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

アイテム保持ポリシーに対して保持タグを正しく追加または削除できたことを確認するには、[Get-RetentionPolicy](https://technet.microsoft.com/ja-jp/library/dd298086\(v=exchg.150\)) コマンドレットを使用して *RetentionPolicyTagLinks* プロパティを確認します。

この例では、**Get-RetentionPolicy** コマンドレットを使用して Default MRM ポリシーに追加した保持タグを取得し、**Format-Table** コマンドレットにパイプライン処理して各タグの名前プロパティだけを出力します。

    (Get-RetentionPolicy "Default MRM Policy").RetentionPolicyTagLinks | Format-Table name

