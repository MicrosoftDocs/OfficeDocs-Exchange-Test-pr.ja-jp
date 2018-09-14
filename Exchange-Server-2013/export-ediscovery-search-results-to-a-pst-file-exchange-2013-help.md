---
title: '電子情報開示検索の結果を PST ファイルへエクスポート: Exchange 2013 Help'
TOCTitle: 電子情報開示検索の結果を PST ファイルへエクスポート
ms:assetid: bc47f5f9-d056-4b69-b669-ae65fad541c8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn440164(v=EXCHG.150)
ms:contentKeyID: 59634965
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 電子情報開示検索の結果を PST ファイルへエクスポート

 

_**適用先:** Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:** 2017-09-07_

PST ファイルとも呼ばれる Outlook データ ファイルに埋め込み、電子的証拠開示検索の結果をエクスポートするのには、 Exchange 管理センター (EAC) で、電子的証拠開示のエクスポート ツールを使用できます。管理者は、人事マネージャーやレコード マネージャーなど、組織内で他の人または訴訟事件の弁護士の反対に、検索の結果を配布できます。検索結果は、PST ファイルにエクスポートするまたは他のユーザーで開くことがそれらを表示または検索結果に返されるメッセージを印刷するように Outlook。PST ファイルは、サード ・ パーティ製の電子的証拠開示およびレポート作成アプリケーションで開くこともできます。このトピックでは、これを行うと同様にする必要があります任意の問題をトラブルシューティングする方法を説明します。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 予想所要時間は、エクスポートされる検索結果の件数とサイズに応じて変わります。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」トピックの「インプレース電子情報開示」。

  - PST ファイルに検索結果をエクスポートするのにを使用するコンピューターは、次のシステム要件を満たす必要があります。
    
      - 32 ビットおよび 64 ビット バージョンの Windows 7 およびそれ以降のバージョン
    
      - Microsoft.NET Framework 4.7
    
      - サポートされているブラウザー:
        
          - Internet Explorer 10 以降
            
            または
        
          - Mozilla Firefox または Google Chrome。これらのどちらかのブラウザーを使用する場合は、*ClickOnce* 拡張機能をインストールしてください。ClickOnce アドインをインストールする場合は、「[Mozilla ClickOnce add-ons](https://addons.mozilla.org/en-us/firefox/search/?q=clickonce%26cat=1%2c0%26appver=%26platform=)」または「[ClickOnce for Google Chrome](https://chrome.google.com/webstore/search/clickonce?_category=extensions)」を参照してください。

  - エクスポートするアカウントに接続されたアクティブなメールボックスが必要です。

  - Internet Explorer でローカル イントラネット設定を適切に設定してください。ローカル イントラネット ゾーンに **https://&#42;.outlook.com** が追加されていることを確認します。

  - 信頼済みサイト ゾーンに、次に示す URL が表示されていないことを確認します。
    
      - https://&#42;.outlook.com
    
      - https://r4.res.outlook.com
    
      - https://&#42;.res.outlook.com

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## Exchange 管理センター を使用してインプレース電子情報開示の検索結果を PST にエクスポートする

1.  <strong>コンプライアンス管理</strong> \> <strong>インプレースの電子証拠開示と保持</strong> に移動します。

2.  リスト表示で、結果をエクスポートするインプレース電子情報開示検索を選択してから、<strong>PST ファイルへエクスポート</strong> をクリックします。
    
    ![PST ファイルにエクスポート](images/Dn440164.1ebee2ac-89b3-49fa-b70c-a07c9a65f958(EXCHG.150).gif "PST ファイルにエクスポート")  

3.  <strong>電子情報開示の PST エクスポート ツール</strong> ウィンドウで、次の操作を行います。
    
      - <strong>参照</strong> をクリックして、PST ファイルをダウンロードする場所を指定します。
    
      - <strong>重複除外を有効にする</strong> チェックボックスをクリックして重複メッセージを除外します。PST ファイルにメッセージの単一インスタンスのみを含めるには。
    
      - <strong>検索不能アイテムを含める</strong> チェック ボックスをオンにすると、検索できなかったメールボックス アイテム (たとえば、Exchange 検索でインデックスが作成できなかった種類のファイルが添付されたメッセージ) が含まれます。検索できないアイテムは、別の PST ファイルにエクスポートされます。
        

        > [!IMPORTANT]
        > メールボックスに検索不能アイテムが大量に含まれている場合、eDiscovery 検索結果のエクスポート時に検索不能アイテムを含めるのに時間がかかります。検索結果をエクスポートする時間を短縮し、PST エクスポート ファイルが大規模にならないようにするために、次の推奨事項を考慮してください。 
        > <UL>
        > <LI>
        > <P>それぞれが少数のソース メールボックスを検索する複数の eDiscovery 検索を作成します。</P>
        > <LI>
        > <P>特定の日付範囲内のメールボックスの内容を (検索条件にキーワードを何も指定せずに) すべてエクスポートする場合、その日付範囲内にあるすべての検索不能アイテムが自動的に検索結果に含まれます。このため、<STRONG>[検索不能アイテムを含める]</STRONG> チェックボックスを選択しないでください。</P></LI></UL>



4.  <strong>開始</strong> をクリックして、検索結果を PST ファイルにエクスポートします。
    
    エクスポート プロセスに関するステータス情報が含まれているウィンドウが表示されます。

## 詳細情報

  - PST エクスポート ファイルのサイズは、検索の検索不能アイテムのみをエクスポートすることで縮小できます。これを行うには、検索を作成または編集し、将来の開始日を指定してから、すべてのキーワードを <strong>キーワード</strong> ボックスから削除します。これにより、検索結果が返されなくなります。検索結果をコピーまたはエクスポートする場合、<strong>検索不能アイテムを含める</strong> チェックボックスを選択すると、検索不能アイテムのみが探索メールボックスにコピーされるか、PST ファイルにエクスポートされます。

  - 重複除外を有効にした場合は、すべての検索結果は、単一の PST ファイルにエクスポートされます。重複除外を有効にしない場合は、検索に含まれる各メールボックスの別の PST ファイルがエクスポートされます。上述したように、検索できないアイテムは、別の PST ファイルにエクスポートします。

  - 検索結果が含まれている PST ファイルに加えて、他の 2 つのファイルもエクスポートされます。
    
      - たとえば、エクスポートされた電子情報開示検索の名前、エクスポートの日時、重複除外および検索不能アイテムが有効かどうか、検索クエリー、および検索されたソースのメールボックスなど、PST エクスポート要求についての情報を含む構成ファイル (.txt ファイル形式)。
    
      - 各メッセージのエントリを含む検索結果ログ (.csv ファイル形式) を含む検索結果が返されています。各エントリは、メッセージが置かれている元のメールボックスを識別します。重複除外を有効にした場合は、重複したメッセージを含むすべてのメールボックスを特定します。

  - 検索の名前が、エクスポートされる各ファイルのファイル名の最初の部分です。さらにエクスポート要求の日時が、各 PST ファイルおよび結果ログのファイル名に付加されます。

  - 重複除外および検索不能アイテムの詳細については以下を参照してください。
    
      - [Estimate, preview, and copy search results](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery)
    
      - [Exchange 電子情報開示の検索不能アイテム](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)

  - SharePoint または SharePoint Online の電子情報開示センターから電子情報開示検索の結果をエクスポートする場合は、「[電子情報開示コンテンツのエクスポートとリポートの作成](https://go.microsoft.com/fwlink/p/?linkid=324757)」を参照してください。

## トラブルシューティング


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>現象</th>
<th>考えられる原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PST ファイルにエクスポートできません。</p></td>
<td><ul>
<li><p>アカウントに接続されている、アクティブなメールボックスがありません。PST をエクスポートするには、アクティブなアカウントが必要です。</p></li>
<li><p>Internet Explorer のバージョンの有効期限が切れています。バージョン 10 以降の IE に更新してください。または、別のブラウザーをお試しください。</p></li>
<li><p><strong>[条件に基づいてフィルター処理する]</strong> クエリに入力した検索条件が間違っています。たとえば、メール アドレスの代わりにユーザー名が入力されています。条件に基づいてフィルター処理する方法について詳しくは、「<a href="modify-an-in-place-ediscovery-search-exchange-2013-help.md">インプレース電子情報開示検索の変更</a>」をご覧ください。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>特定のコンピューターで検索結果をエクスポートできません。別のコンピューターではエクスポートが正常に動作します。</p></td>
<td><p><strong>[資格情報マネージャー]</strong> に間違った Windows 資格情報が保存されています。ユーザーの資格情報をクリアし、もう一度ログインします。</p></td>
</tr>
<tr class="odd">
<td><p>eDiscovery PST エクスポート ツールが起動しません。</p></td>
<td><p>Internet Explorer でローカル イントラネット ゾーンが適切に設定されていません。ローカル イントラネット ゾーンとして信頼されたサイトに、*.outlook.com、*.office365.com、*.sharepoint.com、*.onmicrosoft.com が追加されていることを確認してください。</p>
<p>これらのサイトを IE の信頼済みゾーンに追加するには、「<a href="https://windows.microsoft.com/en-us/windows/security-zones-adding-removing-websites#1tc=windows-7">セキュリティ ゾーン: Web サイトの追加または削除</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

