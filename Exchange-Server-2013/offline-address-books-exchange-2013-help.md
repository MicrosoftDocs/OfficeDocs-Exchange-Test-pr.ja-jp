---
title: 'オフライン アドレス帳: Exchange 2013 Help'
TOCTitle: オフライン アドレス帳
ms:assetid: a6bcb072-4ab9-400e-a5d0-c05264629097
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb232155(v=EXCHG.150)
ms:contentKeyID: 49896399
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# オフライン アドレス帳

 

_**適用先:** Exchange Server 2010, Exchange Server 2013_

_**トピックの最終更新日:** 2014-11-16_

オフライン アドレス帳 (OAB) はダウンロードされたアドレス一覧の集合のコピーであり、Microsoft Outlook ユーザーはサーバーに接続していないときでもアドレス帳にアクセスできます。Microsoft Exchange は新しい OAB ファイルを生成し、そのファイルを圧縮してローカルの共有に格納します。オフラインで作業するユーザーに対して、どのアドレス一覧を使用可能にするかを決定できます。また、アドレス帳の配布方法を構成することもできます。

アドレス一覧の詳細については、「[アドレス一覧](https://docs.microsoft.com/ja-jp/exchange/address-books/address-lists/address-lists)」を参照してください。


> [!IMPORTANT]
> OAB データは、メールボックス アシスタントである Microsoft Exchange OABGen サービスにより生成されます。セキュリティ記述子を使用して、Active Directory の特定の受信者をユーザーが表示できないようにしている場合、OAB をダウンロードしたユーザーは、このような非表示の受信者を表示することができます。したがって、アドレス一覧から受信者を非表示にするには、<A href="https://technet.microsoft.com/ja-jp/library/aa998596(v=exchg.150)">Set-PublicFolder</A>、<A href="https://technet.microsoft.com/ja-jp/library/aa995950(v=exchg.150)">Set-MailContact</A>、<A href="https://technet.microsoft.com/ja-jp/library/aa995971(v=exchg.150)">Set-MailUser</A>、<A href="https://technet.microsoft.com/ja-jp/library/bb123796(v=exchg.150)">Set-DynamicDistributionGroup</A>、<A href="https://technet.microsoft.com/ja-jp/library/bb123981(v=exchg.150)">Set-Mailbox</A>、および <A href="https://technet.microsoft.com/ja-jp/library/bb124955(v=exchg.150)">Set-DistributionGroup</A> の各コマンドレットで、<EM>HiddenFromAddressListsEnabled</EM> パラメーターを設定します。または、非表示の受信者を含まない新しい既定の OAB を作成できます。OAB のアドレス一覧を追加または削除する方法の詳細については、「<A href="add-an-address-list-to-or-remove-an-address-list-from-an-offline-address-book-exchange-2013-help.md">オフライン アドレス帳でのアドレス一覧の追加または削除</A>」を参照してください。



OAB に関連する管理タスクについては、「[オフライン アドレス帳の手順](https://docs.microsoft.com/ja-jp/exchange/address-books/offline-address-books/offline-address-book-procedures)」を参照してください。

**目次**

Exchange のバージョン間での OAB の移動

OAB Version 4 と Outlook クライアント

Web ベースの配布

OAB に関する考慮事項

## Exchange のバージョン間での OAB の移動

Exchange 2007 および Exchange 2010 では、**Move-OfflineAddressBook** コマンドレットを使用して OAB の生成を別のメールボックス サーバーに移動しました。Exchange 2013 では OAB (バージョン 4) のみをサポートします。これは、Exchange 2010 での既定のバージョンと同じバージョンです。Exchange 2013 に他の OAB バージョンを生成させ、組織のメールボックスが置かれているメールボックス サーバーで OAB が生成されるように構成することはできません。したがって、Exchange 2013 で OAB の生成を移動するには、組織のメールボックスを移動する必要があります。OAB の生成は、他の Exchange 2013 のメールボックス データベースにのみ移動することができます。OAB の生成は Exchange の以前のバージョンには移動できません。Exchange 2013 の OAB の組織のメールボックスを見つけるには、次のシェル コマンドを実行します。

    Get-Mailbox -Arbitration | where {$_.PersistedCapabilities -like "*oab*"}

それから **MoveRequest** コマンドレットを使用してメールボックスを移動します。

## OAB Version 4 と Outlook クライアント

Exchange 2013 は OAB Version 4 のみをサポートします。OAB Version 4 は Exchange 2003 Service Pack 2 (SP2) で導入され、Outlook 2007、Outlook 2010、および Outlook 2013 によりサポートされています。この Unicode OAB を使用すると、クライアント コンピューターが OAB 全体をダウンロードせずに差分更新を受け取ることができ、ファイルのサイズを削減できます。

## OAB Version 4 を使用する Outlook クライアント

Outlook 2013、Outlook 2010、Outlook 2007、および OAB バージョン 4 を使用するクライアントの場合、changes.oab ファイルのサイズが OAB ファイル全体のサイズの半分 (またはそれ以上) であるときは、Outlook は OAB 全体のダウンロードを開始します。

## Web ベースの配布

*Web ベースの配布* は、Outlook 2013、Outlook 2010、または Outlook 2007 のオフライン作業中のクライアントが OAB にアクセスできるようにする配布方法です。

Web ベースの配布の使用には、次のような複数の利点があります。

  - より多くの同時接続クライアント コンピューターをサポート。

  - 帯域幅の使用量が減少。

  - OAB 配布ポイントに対する管理の強化。Web ベースの配布では、配布ポイントは HTTPS Web アドレスであり、クライアント コンピューターはそこから OAB をダウンロードできます。

Web ベースの配布の利点を最大限に活用するには、クライアント コンピューターが Outlook 2013、Outlook 2010 または Outlook 2007 を実行している必要があります。

Web ベースの配布は、正しく機能するために以下のコンポーネントに依存します。

  - **OAB の生成プロセス** これは、Exchange によって OAB が作成および更新されるプロセスです。OAB を作成および更新するために、OABGen サービスは組織のメールボックスがあるメールボックス サーバーで実行されます。OAB の配布をサポートするには、このサーバーが Exchange のメールボックス サーバーである必要があります。

  - **OAB の配布** クライアントが OAB の配布要求を開始する場合、要求はクライアント アクセス サーバーを介して転送されます。クライアント アクセス サーバーは、OAB ファイルをホストしているメールボックス サーバーに要求を転送します。その後、OAB ファイルはメールボックス サーバーからクライアントに直接配布されます。

  - **OAB 仮想ディレクトリ** OAB 仮想ディレクトリは、Web ベースの配布方法で使用される配布ポイントです。既定では、Exchange がインストールされると、インターネット インフォメーション サービス (IIS) の既定の内部 Web サイトに **OAB** という名前の新しい仮想ディレクトリが作成されます。組織のファイアウォールの外部から Outlook に接続するクライアント側のユーザーがいる場合は、外部の Web サイトを追加できます。また、シェルで **New-OABVirtualDirectory** コマンドレットを実行すると、ローカルの Exchange サーバー上の既定の IIS Web サイトに OAB という名前の新しい仮想ディレクトリが作成されます。詳細については、「[オフライン アドレス帳仮想ディレクトリを作成する](https://docs.microsoft.com/ja-jp/exchange/address-books/offline-address-books/create-virtual-directory)」を参照してください。

  - **自動検出サービス**   これは、Outlook 2013、Outlook 2010、Outlook 2007、および Exchange にアクセスするようにクライアントが自動的に構成される一部のモバイル デバイスで使用可能な機能です。このサービスはクライアント アクセス サーバーで実行され、特定のクライアント接続に対して正しい OAB URL を返します。

## OAB に関する考慮事項

単一の OAB を使用するか、複数の OAB を使用するかにかかわらず、OAB 戦略を計画および実装する際には、以下の要素を考慮することをお勧めします。

  - 組織内の各 OAB のサイズ。詳細については、後の「OAB のサイズに関する考慮事項」を参照してください。

  - OAB のダウンロードの数。

  - 親識別名の変更の数と頻度。

  - SMTP アドレスの不一致。

  - ディレクトリに加えられた変更の全体的な数。

## OAB のサイズに関する考慮事項

一部の組織では、OAB のファイルが小さいので、リモート ユーザーが適宜ダウンロードする場合があります。このような組織では、OAB のダウンロードは問題になりません。ただし、大規模なディレクトリを持つ大きな組織や、Outlook 2003 キャッシュ モードで Exchange を展開している組織の場合は、配慮が必要です。特に、地域のデータセンターに Exchange サーバーを統合している組織の場合は、問題になる可能性があります。

OAB のサイズは、数 MB から数百 MB までさまざまです。OAB のサイズには、次の要素が影響します。

  - 社内での証明書の使用。公開キー基盤 (PKI) 証明書の数が増えると、OAB も大きくなります。PKI 証明書の規模は、1 から 3 KB です。これは、OAB のサイズに最も大きな影響を与えます。

  - Active Directory 内のメール受信者の数。

  - Active Directory 内の配布グループの数。

  - メールボックスが有効なオブジェクトまたはメールが有効なオブジェクトごとに社内で Active Directory に追加する情報。たとえば、組織によって、各ユーザーにアドレス プロパティを設定する場合と、設定しない場合があります。

