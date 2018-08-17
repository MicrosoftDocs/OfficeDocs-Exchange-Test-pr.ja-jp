---
title: 'IIS 7 コンポーネントがインストールされていない'
TOCTitle: IIS 7 コンポーネントがインストールされていない_LonghornIIS7BasicAuthNotInstalled
ms:assetid: 2eb3290c-9ce2-4c01-ad47-a26ef60bddb5
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.longhorniis7basicauthnotinstalled(v=EXCHG.150)
ms:contentKeyID: 48269321
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# IIS 7 コンポーネントがインストールされていない\_LonghornIIS7BasicAuthNotInstalled

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2015-03-09_

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

1.  <strong>スタート</strong> ボタンをクリックし、<strong>管理ツール</strong> をクリックします。次に、<strong>サーバー マネージャー</strong> をクリックします。

2.  ナビゲーション ウィンドウで、<strong>役割</strong> を展開し、<strong>Web サーバー (IIS)</strong> を右クリックします。次に、<strong>役割サービスの追加</strong> を選択します。

3.  <strong>役割サービスの選択</strong> ウィンドウで、<strong>IIS</strong> まで下にスクロールします。

4.  <strong>セキュリティ</strong> エリアで、次のチェック ボックスをオンにします。
    
      - **基本認証**
    
      - **ダイジェスト認証**
    
      - **Windows 認証**

5.  <strong>パフォーマンス</strong> エリアで、次のチェック ボックスをオンにします。
    
      - **静的な圧縮**
    
      - **動的な圧縮**

6.  <strong>役割サービスの選択</strong> ウィンドウで <strong>次へ</strong> をクリックし、<strong>インストール選択の確認</strong> ウィンドウで <strong>インストール</strong> をクリックします。

7.  <strong>閉じる</strong> をクリックして、役割サービスの追加ウィザードを終了します。

**Windows Server 2008 サーバー マネージャーを使用したメールボックス サーバーの役割用の IIS 7 コンポーネントのインストール**

1.  <strong>スタート</strong> ボタンをクリックし、<strong>管理ツール</strong> をクリックします。次に、<strong>サーバー マネージャー</strong> をクリックします。

2.  ナビゲーション ウィンドウで、<strong>役割</strong> を展開し、<strong>Web サーバー (IIS)</strong> を右クリックします。次に、<strong>役割サービスの追加</strong> を選択します。

3.  <strong>役割サービスの選択</strong> ウィンドウで、<strong>IIS</strong> まで下にスクロールします。

4.  <strong>セキュリティ</strong> エリアで、次のチェック ボックスをオンにします。
    
      - **基本認証**
    
      - **Windows 認証**

5.  <strong>役割サービスの選択</strong> ウィンドウで <strong>次へ</strong> をクリックし、<strong>インストール選択の確認</strong> ウィンドウで <strong>インストール</strong> をクリックします。

6.  <strong>閉じる</strong> をクリックして、役割サービスの追加ウィザードを終了します。

