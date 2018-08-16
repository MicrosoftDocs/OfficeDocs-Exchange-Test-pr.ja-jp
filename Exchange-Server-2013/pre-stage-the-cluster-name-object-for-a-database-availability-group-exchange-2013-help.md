---
title: 'データベース可用性グループのクラスター名オブジェクトを事前設定する: Exchange 2013 Help'
TOCTitle: データベース可用性グループのクラスター名オブジェクトを事前設定する
ms:assetid: 51ebf2f6-8a02-44ef-a489-ca361cb0f63a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff367878(v=EXCHG.150)
ms:contentKeyID: 48269499
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# データベース可用性グループのクラスター名オブジェクトを事前設定する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-08-14_

コンピューター アカウントの作成が制限されている場合や、コンピューター アカウントが既定のコンピューター コンテナー以外のコンテナーに作成されている環境では、クラスタ名オブジェクト (CNO) を事前に設定し、それに権限を割り当てることによって CNO を支給することができます。Windows Server 2012 および Windows Server 2012 R2 DAG メンバーも、コンピューター オブジェクトに対する Windows でのアクセス許可変更のため、CNO の事前設定が必要になります。Windows Server 2012 または Windows Server 2012 R2 を実行しているメールボックス サーバーを使用してデータベース可用性グループ (DAG) を展開している場合、クラスター管理アクセス ポイントのない DAG を展開している場合を除いて、CNO を事前に設定して準備する必要があります。クラスター管理アクセス ポイントのない DAG は、CNO を使用しません。そのため、それらの DAG では事前設定は必要ありません。

CNO のコンピューター アカウントを作成して無効にし、以下の作業のいずれかを実行します。

  - DAG に追加している最初のメールボックス サーバーのコンピューター アカウントに対して、コンピューター アカウントのフル コントロールを割り当てます。

  - コンピューター アカウントのフル コントロールを Exchange Trusted Subsystem ユニバーサル セキュリティ グループ (USG) に割り当てます。

## 始める前に把握しておくべき情報

  - 予想所要時間: 1 分

  - Active Directory にコンピューター オブジェクトを作成できるアクセス許可のあるアカウントを使用する必要があります。

  - 次の手順を完了した後、Active Directory レプリケーションが行われるまで待機します。オブジェクトのレプリケーション後は、最初のメンバーを DAG に追加できます。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## CNO の事前設定

1.  \[Active Directory ユーザーとコンピューター\] を開きます。

2.  フォレスト ノードを展開します。

3.  新しいアカウントを作成する組織単位 (OU) を右クリックして、<strong>新規作成</strong>、<strong>コンピューター</strong> の順に選択します。

4.  <strong>新しいオブジェクト - コンピューター</strong> で、CNO のコンピューター アカウント名を <strong>コンピューター名</strong> ボックスに入力します。これは DAG に使用する名前です。<strong>OK</strong> をクリックして、アカウントを作成します。

5.  新しいコンピューター アカウントを右クリックし、<strong>アカウントを無効にする</strong> をクリックします。<strong>はい</strong> をクリックして、無効化アクションを確認してから、<strong>OK</strong> をクリックします。

## CNO にアクセス許可を割り当てる

1.  \[Active Directory ユーザーとコンピューター\] を開きます。

2.  拡張機能が有効になっていない場合、<strong>表示</strong>、<strong>拡張機能</strong> の順にクリックして拡張機能を有効にします。

3.  新しいコンピューター アカウントを右クリックし、<strong>プロパティ</strong> をクリックします。

4.  <strong>\<コンピューター名\> プロパティ</strong> の <strong>セキュリティ</strong> タブで、<strong>追加</strong> をクリックして、DAG に追加する最初のノードのコンピューター アカウントを追加するか、Exchange Trusted Subsystem USG を追加します。
    
      - Exchange Trusted Subsystem を追加するには、<strong>選択するオブジェクト名を入力してください</strong> フィールドに「**Exchange Trusted Subsystem**」と入力します。<strong>OK</strong> をクリックして、USG を追加します。Exchange Trusted Subsystem USG を選択し、<strong>Exchange Trusted Subsystem のアクセス許可</strong> フィールドで、<strong>許可</strong> 列の <strong>フル コントロール</strong> を選択します。<strong>OK</strong> をクリックして、アクセス許可設定を保存します。
    
      - DAG に追加する最初のノードのコンピューター アカウントを追加するには、<strong>オブジェクトの種類</strong> をクリックします。<strong>オブジェクトの種類</strong> ダイアログ ボックスで、<strong>ビルトイン セキュリティ プリンシパル</strong>、<strong>グループ</strong>、および<strong>\[ユーザー\]</strong> チェック ボックスをオフにします。<strong>コンピューター</strong> チェック ボックスをオンにし、<strong>OK</strong> をクリックします。<strong>選択するオブジェクト名を入力してください</strong> ボックスで、DAG に追加する最初のメールボックス サーバーの名前を入力して、<strong>OK</strong> をクリックします。最初のノードのコンピューター アカウントを選択し、<strong>\<ノード名\> のアクセス許可</strong> フィールドで <strong>許可</strong> 列の <strong>フル コントロール</strong> を選択します。<strong>OK</strong> をクリックして、アクセス許可設定を保存します。

## 正常な動作を確認する方法

CNO が正常に作成されたことを確認するには、次の手順を実行します。

1.  \[Active Directory ユーザーとコンピューター\] を開きます。

2.  フォレスト ノードを展開します。

3.  アカウントを作成した OU を開き、そのアカウントが一覧表示されていることを確認します。

