---
title: 'インプレース電子情報開示検索の変更: Exchange Online Help'
TOCTitle: インプレース電子情報開示検索の変更
ms:assetid: 3162743c-cc12-4997-91e0-bcbfea8bcb17
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd335182(v=EXCHG.150)
ms:contentKeyID: 49896194
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# インプレース電子情報開示検索の変更

 

_**適用先:** Exchange Server 2013_

インプレースの電子情報開示検索を作成すると、それを変更して検索パラメーターを変更できます。たとえば、検索するメールボックス、日付の範囲、キーワード、ログ オプションを変更できるほか、検索結果を保存する検索メールボックスを別に指定できます。検索のプロパティに加えられた変更は、検索を再開するときに使用されます。


> [!NOTE]
> インプレースの電子情報開示検索を実行している場合は、変更する前に停止する必要があります。検索を再開すると、前回の検索実行時の結果は検索メールボックスから削除されます。ただし、以前の検索のログは保存されています。



## 始める前に把握しておくべき情報

  - 予想所要時間: 2 ～ 5 分。

  - インプレース電子情報開示検索が作成されていますが、実行はしてはいません。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「インプレース電子情報開示」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

## 必要な作業

## EAC を使用してインプレース電子情報開示検索を変更する

1.  <strong>コンプライアンス管理</strong> \> <strong>インプレースの電子情報開示と保持</strong> に移動します。

2.  リスト ビューで、変更するインプレース電子情報開示検索を選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン")をクリックします。

3.  <strong>インプレース電子情報開示と保持</strong> では以下の設定を変更できます。
    
      - <strong>名前</strong> ページでは、検索の名前とオプションの説明を変更します。
    
      - <strong>メールボックス</strong> ページでは、検索するメールボックスを変更します。すべてのメールボックスを検索したり、特定のメールボックスを選択して検索したりできます。
        

        > [!IMPORTANT]
        > <STRONG>[すべてのメールボックスを検索する]</STRONG> オプションで Exchange 2013 メールボックス サーバーのすべてのメールボックスを保持することはできません。インプレース ホールドを作成するには、<STRONG>[検索するメールボックスを指定する]</STRONG> を選択する必要があります。詳細については、「<A href="https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/create-or-remove-in-place-holds">インプレース保持を作成または削除する</A>」を参照してください。

    
      - <strong>検索クエリ</strong> ページでは、以下のフィールドを変更します。
        
          - <strong>すべてのユーザーのメールボックスの内容を含める</strong>   このオプションを選択すると、選択したメールボックス内のすべてのコンテンツを保持できます。
        
          - <strong>条件に基づいてフィルター処理する</strong>   このオプションを選択すると、キーワード、開始日、終了日、送信者および受信者のアドレス、メッセージの種類などの検索条件を指定できます。
    
      - <strong>インプレース保持</strong> ページで <strong>選択したメールボックス内の検索クエリに一致したコンテンツを保持する</strong> チェック ボックスをオンにし、以下のオプションをどれか 1 つ選択して、アイテムをインプレース保持にします。
        
          - <strong>無期限に保持</strong>   このオプションを選択すると、返されたアイテムを無期限に保持できます。保持されたアイテムは、検索からメールボックスを削除するか、検索を削除するまで保持されます。
        
          - <strong>受信日を基準としてアイテムを保持する日数を指定する</strong> このオプションを使用すると、特定の期間だけアイテムを保持できます。たとえば、組織ですべてのメッセージを 7 年以上保持することが求められている場合に、このオプションを使用できます。*時間ベースの*インプレース保持を保持ポリシーと併用して、アイテムが 7 年後に削除されるようにできます。
            

            > [!IMPORTANT]
            > メールボックスやアイテムを法的な目的のためにインプレース ホールドに置く場合、通常、アイテムを無期限に保持し、訴訟や捜査が終了したときに保持を解除することをお勧めします。



4.  <strong>保存</strong> をクリックします。

## シェルを使用してインプレース電子情報開示検索を変更する

この例では、インプレース電子情報開示検索 Search-Project Contoso を変更して、DG-ProjectManagers 配布グループのメンバーに所属するメールボックスを検索します。

    Set-MailboxSearch -Identity "Search-Project Contoso" -SourceMailboxes "DG-ProjectManagers"

## 正常な動作を確認する方法

インプレース電子情報開示検索を正しく変更できたことを確認するには、以下の手順の 1 つを実行します。

  - EAC を使用して検索のプロパティを確認する

  - シェルの **Get-MailboxSearch** コマンドレットを使用して、検索のプロパティを確認します。メールボックス検索のプロパティの確認方法については、「[Get-MailboxSearch](https://technet.microsoft.com/ja-jp/library/dd351021\(v=exchg.150\))」の「例」セクションを参照してください。


> [!NOTE]
> Exchange Online の <STRONG>Get-MailboxSearch</STRONG> を使用して電子情報開示検索に関する情報を取得する場合、<CODE>Get-MailboxSearch "Contoso Legal Case"</CODE> のように、検索プロパティの完全なリストを返す検索の名前を指定する必要があります。パラメーターを使用しないで <STRONG>Get-MailboxSearch</STRONG> コマンドレットを実行する場合、以下のプロパティは返されません。 
> <UL>
> <LI>
> <P>SourceMailboxes</P>
> <LI>
> <P>Sources</P>
> <LI>
> <P>SearchQuery</P>
> <LI>
> <P>ResultsLink</P>
> <LI>
> <P>PreviewResultsLink</P>
> <LI>
> <P>Errors</P></LI></UL>その理由は、組織内のすべての電子情報開示検索についてそれらのプロパティを返すためには多大なリソースが必要となるためです。


