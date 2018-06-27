---
title: 'IIS 7 コンポーネントがインストールされていない_LonghornIIS7DigestAuthNotInstalled: Exchange 2013 Help'
TOCTitle: IIS 7 コンポーネントがインストールされていない_LonghornIIS7DigestAuthNotInstalled
ms:assetid: 5c0523d3-f1ba-4197-9c9f-715673dc1436
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.longhorniis7digestauthnotinstalled(v=EXCHG.150)
ms:contentKeyID: 48269545
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# IIS 7 コンポーネントがインストールされていない\_LonghornIIS7DigestAuthNotInstalled

 

_**適用先:**Exchange Server_

_**トピックの最終更新日:**2015-03-09_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2010 セットアップ プログラムまたは Microsoft Exchange Server 2007 セットアップ プログラムは、必須の Internet Information Server (IIS) 7 コンポーネントがインストールされていないため、クライアント アクセス サーバー (CAS) の役割またはメールボックス サーバーの役割を、Microsoft Windows Server 2008 ベースのコンピューターまたは Windows Server 2008 R2 ベースのコンピューターにインストールできません。

Exchange 2010 セットアップ プログラムおよび Exchange 2007 セットアップ プログラムを実行するには、CAS の役割をインストールする Windows Server 2008 ベースのコンピューターまたは Windows Server 2008 R2 ベースのコンピューターに、以下の IIS 7 コンポーネントがインストールされている必要があります。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>CAS サーバーの役割に必要な IIS 7 コンポーネント</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>動的なコンテンツの圧縮</p></td>
</tr>
<tr class="even">
<td><p>静的なコンテンツの圧縮</p></td>
</tr>
<tr class="odd">
<td><p>基本認証</p></td>
</tr>
<tr class="even">
<td><p>Windows 認証</p></td>
</tr>
<tr class="odd">
<td><p>IIS 7 ダイジェスト認証</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET</p></td>
</tr>
<tr class="odd">
<td><p>クライアント証明書のマッピング</p></td>
</tr>
<tr class="even">
<td><p>ディレクトリの参照</p></td>
</tr>
<tr class="odd">
<td><p>HTTP エラー</p></td>
</tr>
<tr class="even">
<td><p>HTTP ログ</p></td>
</tr>
<tr class="odd">
<td><p>HTTP リダイレクト</p></td>
</tr>
<tr class="even">
<td><p>トレース</p></td>
</tr>
<tr class="odd">
<td><p>ISAPI フィルター</p></td>
</tr>
<tr class="even">
<td><p>要求監視</p></td>
</tr>
<tr class="odd">
<td><p>静的なコンテンツ</p></td>
</tr>
</tbody>
</table>


Exchange 2010 セットアップ プログラムおよび Exchange 2007 セットアップ プログラムを実行するには、メールボックス サーバーの役割をインストールする Windows Server 2008 ベースのコンピューターまたは Windows Server 2008 R2 ベースのコンピューターに、以下の IIS 7 コンポーネントがインストールされている必要があります。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>メールボックス サーバーの役割に必要な IIS 7 コンポーネント</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>基本認証</p></td>
</tr>
<tr class="even">
<td><p>Windows 認証</p></td>
</tr>
</tbody>
</table>


この問題を解決するには、適切な手順に従って、必要な IIS 7 コンポーネントを対象のコンピューターにインストールしてから、Microsoft Exchange セットアップ プログラムを再度実行してください。

**Windows Server 2008 サーバー マネージャーを使用した CAS サーバーの役割用の IIS 7 コンポーネントのインストール**

1.  **\[スタート\]** ボタンをクリックし、**\[管理ツール\]** をクリックします。次に、**\[サーバー マネージャー\]** をクリックします。

2.  ナビゲーション ウィンドウで、**\[役割\]** を展開し、**\[Web サーバー (IIS)\]** を右クリックします。次に、**\[役割サービスの追加\]** を選択します。

3.  **\[役割サービスの選択\]** ウィンドウで、**\[IIS\]** まで下にスクロールします。

4.  **\[セキュリティ\]** エリアで、次のチェック ボックスをオンにします。
    
      - **基本認証**
    
      - **ダイジェスト認証**
    
      - **Windows 認証**

5.  **\[パフォーマンス\]** エリアで、次のチェック ボックスをオンにします。
    
      - **静的な圧縮**
    
      - **動的な圧縮**

6.  **\[役割サービスの選択\]** ウィンドウで **\[次へ\]** をクリックし、**\[インストール選択の確認\]** ウィンドウで **\[インストール\]** をクリックします。

7.  **\[閉じる\]** をクリックして、役割サービスの追加ウィザードを終了します。

**Windows Server 2008 サーバー マネージャーを使用したメールボックス サーバーの役割用の IIS 7 コンポーネントのインストール**

1.  **\[スタート\]** ボタンをクリックし、**\[管理ツール\]** をクリックします。次に、**\[サーバー マネージャー\]** をクリックします。

2.  ナビゲーション ウィンドウで、**\[役割\]** を展開し、**\[Web サーバー (IIS)\]** を右クリックします。次に、**\[役割サービスの追加\]** を選択します。

3.  **\[役割サービスの選択\]** ウィンドウで、**\[IIS\]** まで下にスクロールします。

4.  **\[セキュリティ\]** エリアで、次のチェック ボックスをオンにします。
    
      - **基本認証**
    
      - **Windows 認証**

5.  **\[役割サービスの選択\]** ウィンドウで **\[次へ\]** をクリックし、**\[インストール選択の確認\]** ウィンドウで **\[インストール\]** をクリックします。

6.  **\[閉じる\]** をクリックして、役割サービスの追加ウィザードを終了します。

