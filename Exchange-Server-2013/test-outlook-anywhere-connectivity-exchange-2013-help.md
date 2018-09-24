---
title: 'Outlook Anywhere の接続のテスト: Exchange 2013 Help'
TOCTitle: Outlook Anywhere の接続のテスト
ms:assetid: 0dc5b68f-2316-446a-84c9-5f1c50dc3776
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee633453(v=EXCHG.150)
ms:contentKeyID: 50555727
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Anywhere の接続のテスト

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

Outlook Anywhere のエンドツーエンド クライアント接続のテストは、シェルまたは Exchange リモート接続アナライザー (ExRCA) を使用して行うことができます。これには、自動検出サービスを介した接続テスト、ユーザー プロファイルの作成、ユーザーのメールボックスへのサインインなどが含まれます。必要な値はすべて自動検出サービスから取得されます。

Outlook Anywhere に関連する追加の管理タスクについては、「[Outlook Anywhere](outlook-anywhere-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 10 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「Outlook Anywhere」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## シェルを使用して Outlook Anywhere をテストする

シェルを使用して Outlook Anywhere の接続をテストするには、**Test-OutlookConnectivity** コマンドレットを使用します。

次のコマンドを実行します。

  ```powershell
  Test-OutlookConnectivity -ProbeIdentity 'OutlookMailboxDeepTestProbe' -MailboxId tony@contoso.com -Hostname contoso.com
  ```


> [!NOTE]
> <EM>OutlookMailboxDeepTestProbe</EM> パラメーター値は、メールボックス サーバーからの接続をテストします。クライアント アクセス サーバーからの接続をテストするには、<EM>ProbeIdentity</EM> パラメーター値に <EM>OutlookMailboxCTPProbe</EM> を使用します。



## Exchange リモート接続アナライザーを使用して Outlook Anywhere の接続をテストする

Exchange リモート接続アナライザー (ExRCA) は、Exchange の各種プロトコルによる接続をテストするための Web ベースのツールです。ExRCA には[こちら](https://go.microsoft.com/fwlink/p/?linkid=167905)からアクセスすることができます。

1.  ExRCA の Web サイトでは、<strong>Microsoft Office Outlook 接続テスト</strong> で <strong>Outlook Anywhere</strong> を選択し、そのページの下部にある \[次へ\] を選択します。

2.  次の画面で、電子メール アドレス、ドメイン、ユーザー名、パスワードなどの必須情報を入力します。

3.  自動検出を使用してサーバー設定を検出するか、手動でサーバー設定を指定するかを選択します。

4.  免責事項を確認した上で承認し、検証コードを入力して <strong>検証</strong> を選択します。

5.  <strong>テストの実行</strong> を選択します。

## 正常な動作を確認する方法

ExRCA テストが完了すると、出力が Web ページに表示されます。エラーがある場合はエラーが列挙されます。

