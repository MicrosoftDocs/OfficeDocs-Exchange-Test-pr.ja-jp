---
title: 'アーカイブ ポリシーの変更: Exchange Online Help'
TOCTitle: アーカイブ ポリシーの変更
ms:assetid: 1e3002c2-801a-43ea-ae00-52ab34d76b9c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Hh529919(v=EXCHG.150)
ms:contentKeyID: 49895281
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# アーカイブ ポリシーの変更

 

_**適用先:**Exchange Online, Exchange Server 2013_

Exchange Server 2013 と Exchange Online では、アーカイブ ポリシーを使用して、個人 (オンプレミスの) アーカイブまたはクラウドベース アーカイブにメールボックス アイテムを自動的に移動できます。アーカイブ ポリシーは、**\[アーカイブに移動する\]** 保持アクションを使用する保持タグです。

Exchange セットアップは、**既定の MRM ポリシー** というアイテム保持ポリシーを生成します。このポリシーには、2 年後にアーカイブ メールボックスにアイテムを移動する、既定のポリシー タグ (DPT) が割り当てられています。このポリシーには、ユーザーが自動的にメッセージを移動したり削除するのにフォルダーまたはメールボックス アイテムに適用できる、多数の個人タグも含まれます。アーカイブが有効なメールボックスにアイテム保持ポリシーが割り当てられていない場合、Exchange が**既定の MRM ポリシー**を自動的に適用します。独自のアーカイブ ポリシーとアイテム保持ポリシーを作成して、メールボックス ユーザーに適用することもできます。詳細については、「[保持タグおよびアイテム保持ポリシー](retention-tags-and-retention-policies-exchange-2013-help.md)」を参照してください。

ビジネスの要件に合わせて、既定のポリシーに含める保持タグを変更できます。たとえば、2 年後ではなく 3 年後にアーカイブにアイテムを移動するようにアーカイブ DPT を変更できます。追加の個人タグを作成して**既定の MRM ポリシー**などのアイテム保持ポリシーに追加したり、ユーザーが Outlook Web App オプションから自分のメールボックスに個人タグを追加できるようにすることもできます。

アーカイブ関連のその他の管理タスクについては、以下を参照してください。

  - **Exchange Server 2013:** [Exchange 2013 でインプレース アーカイブを管理する](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)

  - **Exchange Online:** [Exchange Online のアーカイブ メールボックスを有効または無効にする](https://technet.microsoft.com/ja-jp/library/jj984357\(v=exchg.150\))


> [!NOTE]
> Exchange ハイブリッド展開では、オンプレミスのプライマリ メールボックス用のクラウド ベースのアーカイブ メールボックスを有効にすることができます。オンプレミスのメールボックスにアーカイブ ポリシーを割り当てると、アイテムはクラウド ベースのアーカイブに移動されます。アーカイブ メールボックスにアイテムが移動される場合、オンプレミスのメールボックスにアイテムのコピーは保持されません。オンプレミスのメールボックスを保持の対象にすると、アイテムはこれまで通りアーカイブ ポリシーによってクラウド ベースのアーカイブ メールボックスに移動され、保持として指定された期間保持されます。



## 始める前に把握しておくべき情報

  - 推定完了時間: 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「メッセージング レコード管理」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EAC を使用して既定のアーカイブ ポリシーを変更する

1.  **\[コンプライアンス管理\]** \> **\[保持タグ\]** に移動します。

2.  リスト ビューで **\[既定 - 2 年でアーカイブへ移動\]** を選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン")をクリックします。
    

    > [!TIP]
    > <STRONG>[種類]</STRONG> 列をクリックして、種類別に保持タグを並べ替えます。既定のアーカイブ ポリシーが、<STRONG>[既定]</STRONG> として表示され、<STRONG>[アーカイブ]</STRONG> 保持アクションが割り当てられています。また、<STRONG>[名前]</STRONG> をクリックすると名前別に保持タグを並べ替えることができます。



3.  
    
    **\[保持タグ\]**で、以下の設定を表示するか変更し、**\[保存\]**をクリックします。
    
      - **\[名前\]**   ページの一番上にあるボックスを使用してタグ名を表示または変更します。
    
      - **\[保持タグの種類\]**   この読み取り専用フィールドにはタグの種類が表示されます。
    
      - **\[保持アクション\]**   アーカイブ ポリシーの場合、このフィールドは変更しないでください。
    
      - **\[保持期間\]** 次のオプションのいずれか 1 つを選択します。
        
          - **\[なし\]**   このボタンをクリックするとタグが無効になります。DPT を無効にすると、タグはメールボックスに適用されなくなります。
            

            > [!IMPORTANT]
            > 無効の保持タグを適用されたアイテムは、メールボックス アシスタントによって処理されません。タグがアイテムに適用されないようにするには、タグを削除するのではなく無効にすることをお勧めします。タグを削除すると、タグの構成が Active Directory から削除され、メールボックス アシスタントは削除されたタグを削除するよう、すべてのメッセージを処理します。

            

            > [!NOTE]
            > ユーザーが、アイテムが今後削除されないと思いながらタグをそのアイテムに適用した場合、後でそのタグを有効にすると、ユーザーがプライマリ メールボックスに残そうとしたアイテムが削除される可能性があります。

        
          - **\[アイテムの保管日数が次の期間 (単位日) に達したとき\]**   一定の期間経過後にアイテムをアーカイブに移動するには、このボタンをクリックします。既定で、この設定は 2 年後 (730 日) にアーカイブにアイテムを移動するように構成されています。この設定を変更するには、対応するテキスト ボックスに、保持期間の日数を入力します。値の範囲は 1 ～ 24,855 日です。
    
      - **\[コメント\]**   このボックスには、Outlook と Outlook Web App のユーザーに表示されるコメントを入力します。

## シェルを使用してアーカイブ ポリシーを変更する

この例では、1,095 日 (3 年) 後にアイテムを移動するように `Default 2 year move to archive` タグを変更します。

    Set-RetentionPolicyTag "Default 2 year move to archive" -Name "Default 3 year move to archive" -AgeLimitForRetention 1095

この例では、`Default 2 year move to archive` タグを無効にします。

    Set-RetentionPolicyTag "Default 2 year move to archive" -RetentionEnabled $false

この例では、すべてのアーカイブ DPT と個人タグを取得して、無効にします。

    Get-RetentionPolicyTag | ? {$_.RetentionAction -eq "MoveToArchive"} | Set-RetentionPolicyTag -RetentionEnabled $false

構文およびパラメーターの詳細については、「[Set-RetentionPolicyTag](https://technet.microsoft.com/ja-jp/library/dd298042\(v=exchg.150\))」と「[Get-RetentionPolicyTag](https://technet.microsoft.com/ja-jp/library/dd298009\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

[Get-RetentionPolicyTag](https://technet.microsoft.com/ja-jp/library/dd298009\(v=exchg.150\)) コマンドレットでは、保持タグの設定を取得します。

このコマンドは、`Default 2 year move to archive` 保持タグのプロパティを取得し、**Format-List** コマンドレットに出力をパイプライン処理して、すべてのプロパティを一覧形式で表示します。

    Get-RetentionPolicyTag "Default 2 year move to archive" | Format-List

