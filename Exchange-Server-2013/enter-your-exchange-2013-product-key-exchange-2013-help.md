---
title: 'Exchange 2013 プロダクト キーを入力する: Exchange 2013 Help'
TOCTitle: Exchange 2013 プロダクト キーを入力する
ms:assetid: ccb14685-4bdc-42a4-a985-35cd2a1a415c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124582(v=EXCHG.150)
ms:contentKeyID: 51407581
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.EnterProductKeyWizardForm.EnterProductKeyWizardPage
ms.translationtype: HT
---

# Exchange 2013 プロダクト キーを入力する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

プロダクト キーは、購入した Exchange Server 2013 が Standard Edition ライセンスか Enterprise Edition ライセンスかを示します。購入したプロダクト キーが Enterprise Edition ライセンスの場合は、Standard Edition ライセンスで使用可能なすべてに加えて、サーバーあたり 6 つ以上のデータベースをマウントできます。Exchange ライセンスの詳細については、「[Exchange 2013: エディションとバージョン](exchange-2013-editions-and-versions-exchange-2013-help.md)」を参照してください。

プロダクト キーを入力しなかった場合は、サーバーは自動的に試用版としてライセンスされます。評価版は Exchange Standard Edition サーバーと同じように機能するため、購入前に Exchange を試してみたい場合や、ラボでテストを実行したい場合に最適です。試用版としてライセンスされた Exchange サーバーは最大 180 日間しか使用できないという点だけが異なります。180 日以降もサーバーを使用し続けたい場合は、プロダクト キーを入力する必要があります。そうしなかった場合は、Exchange 管理センター (EAC) に、サーバーをライセンスするためのプロダクト キーの入力を促すアラームが表示されます。


> [!TIP]
> このページの訪問者のなかには、Office をインストールまたはアクティブ化する方法についての情報を探しているユーザーがいます。あなたがその一人である場合は、次のページを参照してください。 
> <UL>
> <LI>
> <P><A href="http://go.microsoft.com/fwlink/p/?linkid=403360">Office のインストール</A></P>
> <LI>
> <P><A href="http://go.microsoft.com/fwlink/p/?linkid=403361">Office プロダクト キーに関するヘルプ</A></P></LI></UL>Exchange 2010 サーバーでプロダクト キーを入力する場合は、「<A href="http://go.microsoft.com/fwlink/p/?linkid=403370">Exchange 2010 プロダクト キーの入力</A>」を参照してください。<BR>Exchange 2013 サーバーでプロダクト キーを入力する場合は、ここが正しい場所です。お読みください。



## 始める前に把握しておくべき情報

  - この手順の予想所要時間:5 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[Exchange およびシェル インフラストラクチャのアクセス許可](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)」の「プロダクト キー」。

  - メールボックス サーバーの役割を実行している Exchange サーバーのライセンスを認証する場合、プロダクト キーを入力した後に Microsoft Exchange Information Store サービスをサーバー上で再起動する必要があります。

  - Exchange サーバーを Standard Edition ライセンスから Enterprise Edition ライセンスにアップグレードする場合は、このトピックの手順に従います。

  - Exchange サーバーを Enterprise Edition ライセンスから Standard Edition ライセンスにダウングレードする場合は、Exchange を再インストールする必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EAC を使用してプロダクト キーを入力する

1.  https://\<*クライアント アクセス サーバーの名前*\>/ecp を参照して、EAC を開きます。

2.  <strong>ドメイン\\ユーザー名</strong> と <strong>パスワード</strong> にユーザー名とパスワードを入力し、<strong>サインイン</strong> をクリックします。

3.  <strong>サーバー</strong> \> <strong>サーバー</strong> の順に移動します。ライセンス認証するサーバーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

4.  (省略可能) サーバーを Standard Edition ライセンスから Enterprise Edition ライセンスにアップグレードする場合は、<strong>全般</strong> ページの <strong>プロダクト キーを変更する</strong> を選択します。このオプションが表示されるのは、サーバーがすでにライセンスされている場合のみです。

5.  <strong>全般</strong> ページで、<strong>有効なプロダクト キーを入力してください</strong> テキスト ボックスにプロダクト キーを入力します。

6.  <strong>保存</strong> をクリックします。

7.  メールボックス サーバーの役割を実行する Exchange サーバーのライセンスを認証した場合、次のことを実行して Microsoft Exchange Information Store サービスを再起動します。
    
    1.  <strong>コントロール パネル</strong> を開き、<strong>管理ツール</strong> に移動してから、<strong>サービス</strong> を開きます。
    
    2.  <strong>Microsoft Exchange Information Store</strong> を右クリックし、<strong>再起動</strong> をクリックします。

## シェルを使用してプロダクト キーを入力する

この例では、**set-ExchangeServer** コマンドレットを使用してプロダクト キーを入力します。


> [!NOTE]
> このコマンドは、同じサーバーを Standard Edition ライセンスから Enterprise Edition ライセンスにアップグレードする際にも実行できます。



```powershell
Set-ExchangeServer ExServer01 -ProductKey aaaaa-aaaaa-aaaaa-aaaaa-aaaaa
```

構文およびパラメーターの詳細については、「[Set-ExchangeServer](https://technet.microsoft.com/ja-jp/library/bb123716\(v=exchg.150\))」を参照してください。

メールボックス サーバーの役割を実行する Exchange サーバーのライセンスを認証した場合、次のことを実行して Microsoft Exchange Information Store サービスを再起動します。

1.  <strong>コントロール パネル</strong> を開き、<strong>管理ツール</strong> に移動してから、<strong>サービス</strong> を開きます。

2.  <strong>Microsoft Exchange Information Store</strong> を右クリックし、<strong>再起動</strong> をクリックします。

## 正常な動作を確認する方法

EAC を使用して、サーバーが Standard Edition または Enterprise Edition として正しくライセンスされたことを確認するには、次の手順を実行します。

1.  <strong>ドメイン\\ユーザー名</strong> と <strong>パスワード</strong> にユーザー名とパスワードを入力し、<strong>サインイン</strong> をクリックします。

2.  <strong>サーバー</strong> \> <strong>サーバー</strong> の順に移動します。

3.  表示するサーバーを選択し、サーバーの詳細ウィンドウを確認します。プロダクト キーが承認されている場合は、Exchange 2013 のエディションと共に **"ライセンス済み"** と表示されます。

シェルを使用して、サーバーが Standard Edition または Enterprise Edition として正しくライセンスされたことを確認するには、次の手順を実行します。

1.  シェルを開きます。

2.  特定の Exchange サーバーのライセンス状況を確認するには次のコマンドを実行します。
    
    ```powershell
        Get-ExchangeServer ExServer01 | Format-Table Edition,*Trial*
    ```

3.  (省略可能) 組織内のすべての Exchange サーバーのライセンス状況を確認するには次のコマンドを実行します。
    ```powershell    
        Get-ExchangeServer | Format-Table Name, Edition, *Trial* -Auto
    ```

