---
title: '電子情報開示検索結果を探索メールボックスにコピーする: Exchange Online Help'
TOCTitle: 電子情報開示検索結果を探索メールボックスにコピーする
ms:assetid: bff2ce89-9e6f-494a-bd6a-2f2011507845
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn624163(v=EXCHG.150)
ms:contentKeyID: 61183337
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 電子情報開示検索結果を探索メールボックスにコピーする

 

_**適用先:** Exchange Server 2013_

インプレース電子情報開示検索を作成すれば、EAC を使用して結果を探索メールボックスにコピーすることができます。シェルを使用して、**New-MailboxSearch** コマンドレットを使用して作成された電子情報開示検索を開始することもできます。これにより、検索の作成時に指定された探索メールボックスに結果がコピーされます。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分、または検索結果で返されるメールボックス アイテムの数によってはそれより長くかかります

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「インプレース電子情報開示」。

  - EAC またはシェルを使用して電子情報開示検索を作成しなければ、検索結果をコピーすることができません。詳細については、「[インプレース電子情報開示検索を作成する](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/in-place-ediscovery/create-in-place-ediscovery-search)」を参照してください。

  - Exchange 2013 セットアップは、検索結果をコピーするために <strong>探索検索メールボックス</strong> という名前の探索メールボックスを作成します。探索検索メールボックスは既定で Exchange Online 内に作成されます。追加の探索メールボックスを作成できます。詳細については、「[探索メールボックスの作成](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/in-place-ediscovery/create-a-discovery-mailbox)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EAC を使用して検索結果をコピーする

1.  EAC で、<strong>コンプライアンス管理</strong> \> <strong>インプレースの電子情報開示と保持</strong> に移動します。

2.  リスト ビューで、電子情報開示検索を選択します。

3.  <strong>検索</strong> ![\[検索\] アイコン](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "[検索] アイコン") をクリックしてから、ドロップダウン リストで <strong>検索結果のコピー</strong> をクリックします。

4.  <strong>検索結果のコピー</strong> で、次のオプションの中から選択します。
    
      - <strong>検索不能アイテムを含める</strong>   このチェック ボックスをオンにすると、検索できなかったメールボックス アイテム (たとえば、Exchange 検索でインデックスを作成できなかったファイル タイプのファイルが添付されたメッセージ) が含まれます。詳細については、「[Exchange 電子情報開示の検索不能アイテム](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)」を参照してください。
    
      - <strong>重複除外を有効にする</strong>   このチェック ボックスをオンにすると、重複メッセージが除外されます。探索メールボックスには、メッセージの 1 つのインスタンスだけがコピーされます。
    
      - <strong>詳細ログを有効にする</strong>   このチェック ボックスをオンにして、検索結果の詳細ログを含めます。
    
      - <strong>コピーの完了時にメールを送信する</strong>   このチェック ボックスをオンにして、検索の完了時に電子メールによる通知を受け取ります。
    
      - <strong>結果をこの探索メールボックスにコピーする</strong> <strong>参照</strong> をクリックして、検索結果のコピー先にする探索メールボックスを選択します。
        
        ![検索結果のコピー](images/Dn624163.875e25ed-8308-408c-92c4-8c76fc9d9bfc(EXCHG.150).gif "検索結果のコピー")  

5.  <strong>コピー</strong> をクリックして検索結果を指定された探索メールボックスにコピーするプロセスを開始します。

6.  <strong>最新の情報に更新</strong> ![\[最新の情報に更新\] アイコン](images/Dn624163.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "[最新の情報に更新] アイコン") をクリックして、詳細ウィンドウに表示されるコピー状態に関する情報を更新します。

7.  コピーが完了したら、<strong>開く</strong> をクリックして、検索結果を表示する探索メールボックスを開きます。

## シェルを使用して検索結果をコピーする

**New-MailboxSearch** コマンドレットを使用してインプレース電子情報開示検索を作成したら、メッセージを *TargetMailbox* パラメーターで指定した探索メールボックスにコピーするための検索を開始する必要があります。シェルを使用した電子情報開示検索の作成方法については、以下を参照してください。

  - [Use the Shell to create an In-Place eDiscovery search](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/in-place-ediscovery/create-in-place-ediscovery-search)

  - [New-MailboxSearch](https://technet.microsoft.com/ja-jp/library/dd298064\(v=exchg.150\))

たとえば、次のコマンドを実行して、*Fabrikam Investigation* という名前の電子情報開示検索を開始し、検索結果を指定した探索メールボックスにコピーする場合を考えます。

    Start-MailboxSearch "Fabrikam Investigation"

*EstimateOnly* スイッチを使用して検索結果を推定した場合は、検索結果をコピーする前にそのスイッチを外す必要があります。検索結果をコピーする探索メールボックスを指定する必要もあります。たとえば、次のコマンドを使用して、推定のみの検索を作成したとします。

    New-MailboxSearch "FY13 Q2 Financial Results" -StartDate "04/01/2013" -EndDate "06/30/2013" -SourceMailboxes "DG-Finance" -SearchQuery '"Financial" AND "Fabrikam"' -EstimateOnly -IncludeUnsearchableItems

この検索の結果を探索メールボックスにコピーするには、次のコマンドを実行します。
  ```
  Set-MailboxSearch "FY13 Q2 Financial Results" -EstimateOnly $false -TargetMailbox "Discovery Search Mailbox"
  ```
  ```
  Start-MailboxSearch "FY13 Q2 Financial Results"
  ```

## 検索結果のコピーに関する詳細情報

  - 検索結果を探索メールボックスにコピーしたら、それらの検索結果を PST ファイルにエクスポートできます。詳細については、「[電子情報開示検索の結果を PST ファイルへエクスポート](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/in-place-ediscovery/export-search-results)」を参照してください。

  - 検索不能アイテムの詳細については、「[Exchange 電子情報開示の検索不能アイテム](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)」を参照してください。

  - 特定の日付範囲内のメールボックスの内容を (検索条件にキーワードを何も指定せずに) すべてコピーする場合は、その日付範囲内のすべての検索不能アイテムが自動的に検索結果に含まれます。そのため、検索結果をコピーする場合は <strong>検索不能アイテムを含める</strong> チェック ボックスをオンにしないでください。そうしないと、すべての検索不能アイテムの重複コピーが探索メールボックスにコピーされます。

  - 検索結果の探索メールボックスへのコピーに加えて、選択した検索の結果を推定またはプレビューすることもできます。
    
      - <strong>検索結果の推定</strong>   このオプションは、指定された条件に基づいて検索から返されるアイテムの合計サイズと件数の推定値を返します。推定値が EAC の詳細ウィンドウに表示されます。
    
      - <strong>検索結果をプレビューする</strong>   このオプションを使用すれば、検索で返された結果を表示するために探索メールボックスにコピーしなくても、プレビューすることができます。これにより、検索結果が適切かどうかをすばやく判断できます。結果をプレビューしたら、検索結果を絞り込ために検索クエリを修正し、検索を再実行できます。プレビュー ページのアイテムは、実際の検索結果の読み取り専用バージョンであるため、プレビュー ページで移動、編集、削除、または転送を行うことはできません。
    
    詳細については、「[Estimate or preview search results](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/in-place-ediscovery/create-in-place-ediscovery-search)」を参照してください。

