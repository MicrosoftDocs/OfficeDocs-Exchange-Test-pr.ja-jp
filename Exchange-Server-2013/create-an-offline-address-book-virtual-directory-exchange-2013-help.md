---
title: 'オフライン アドレス帳仮想ディレクトリを作成する: Exchange Online Help'
TOCTitle: オフライン アドレス帳仮想ディレクトリを作成する
ms:assetid: 2c70e21f-2b12-414a-9e8c-65634a767c72
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa996917(v=EXCHG.150)
ms:contentKeyID: 49895316
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# オフライン アドレス帳仮想ディレクトリを作成する

 

_**適用先:**Exchange Server 2013_

OAB 仮想ディレクトリは、OAB の分散です。 既定では、Microsoft Exchange Server 2013 がインストールされると、インターネット インフォメーション サービス (IIS) の既定の内部 Web サイトに OAB という名前の新しい仮想ディレクトリが作成されます。 組織のファイアウォールの外部から Microsoft Outlook に接続するクライアント側のユーザーがいる場合は、外部の Web サイトを追加できます。 また、シェルで **New-OABVirtualDirectory** コマンドレットを実行すると、ローカルの Exchange サーバー上の既定の IIS Web サイトに OAB という名前の新しい仮想ディレクトリが作成されます。

OAB 仮想ディレクトリの作成は共通タスクではありません。Exchange で許可されているのは、OAB という名前の OAB 仮想ディレクトリ 1 つです。既存の OAB 仮想ディレクトリに問題が発生した場合だけ、OAB 仮想ディレクトリを作成し、以前の OAB 仮想ディレクトリは削除してください。

OAB に関連するその他の管理タスクについては、「[オフライン アドレス帳の手順](offline-address-book-procedures-exchange-2013-help.md)」を参照してください。


> [!IMPORTANT]
> OAB 仮想ディレクトリを作成する前に、その変更についてユーザーが認識していることを確認してください。 この手順を実行すると、ユーザーの OAB ダウンロード処理が中断される場合があります。



## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。[電子メール アドレスおよびアドレス帳のアクセス許可](email-address-and-address-book-permissions-exchange-2013-help.md) の「オフライン アドレス帳」。

  - ローカルの Exchange サーバーにクライアント アクセス サーバーの役割がインストールされている。

  - 既定の IIS Web サイト (例、/w3svc/1/root) がある。

  - OAB という名前の仮想ディレクトリが存在していない。

  - 既定では Web ベースの配布が有効になっており、これ以上の構成は必要ありませんが、OAB 配布ポイントの SSL (Secure Sockets Layer) を有効にすることをお勧めします。

  - Exchange 管理センター (EAC) を使用してこの手順を実行することはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用して OAB 仮想ディレクトリを作成する

すべての設定を既定のままにして OAB 仮想ディレクトリを作成する場合は、パラメーターを指定しないで **New-OABVirtualDirectory** コマンドレットを実行できます。 カスタム設定を使用して OAB 仮想ディレクトリを作成するには、次の手順を使用します。


> [!NOTE]
> OAB 仮想ディレクトリを作成する場合は、SSL を有効にすることをお勧めします。



この例では、SSL が有効になっていて、外部 URL が存在する CAS\_SERVER01 という名前のクライアント アクセス サーバー上に OAB 仮想ディレクトリを作成します。

    New-OABVirtualDirectory -Server CASServer01 -RequireSSL $true -ExternalURL "https://www.contoso.com/OAB"

新しい OAB 仮想ディレクトリを作成した後、Web ベースの配布を使用する各 OAB の設定を編集して OAB 仮想ディレクトリに再接続する必要があります。 詳細については、「[オフライン アドレス帳の生成スケジュールを変更する](change-the-offline-address-book-generation-schedule-exchange-2013-help.md)」を参照してください。

構文およびパラメーターの詳細については、「[New-OabVirtualDirectory](https://technet.microsoft.com/ja-jp/library/bb123735\(v=exchg.150\))」を参照してください。

