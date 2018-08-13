---
title: 'Exchange 2013/Exchange 2010 ハイブリッド展開でのハイブリッド管理: Exchange 2013 Help'
TOCTitle: Exchange 2013/Exchange 2010 ハイブリッド展開でのハイブリッド管理
ms:assetid: 613ad2c2-bb7a-4810-b572-71945bd103f1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn393961(v=EXCHG.150)
ms:contentKeyID: 59635066
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013/Exchange 2010 ハイブリッド展開でのハイブリッド管理

このトピックは処理中です。  

_<strong>適用先:</strong>Exchange Online, Exchange Server, Exchange Server 2013_

_<strong>トピックの最終更新日:</strong>2016-12-09_

Exchange 2010 のオンプレミスの組織に Microsoft Exchange Server 2013 を実行しているサーバーをインストールすると、自動的に、Exchange 2013 管理ツールがそのサーバー上にインストールされます。次のツールを使用して、オンプレミスの Exchange 組織と Exchange Online 組織の両方のハイブリッド機能を構成して管理します。

  - **Exchange 管理センター**   EAC は 使いやすい Exchange 2013 に同梱された Web ベースの管理コンソールで、オンプレミス、オンライン、またはハイブリッドの Exchange 展開用に最適化されています。EAC は、Exchange Server 2010 の管理に使用されるインターフェイスの Exchange 管理コンソール (EMC) と Exchange コントロール パネル (ECP) を補完するものです。

  - **Exchange 管理シェル**Exchange 管理シェル は Windows PowerShell ベースのコマンド ライン インターフェイスです。

## Exchange 管理センター

EAC では、Exchange サーバーと Exchange Online 組織の両方で、多くの展開タスクと大部分の一般的な日常管理タスクを実行できます。既定のインストール先は、すべての Exchange 2013 サーバーです。また、Web ベースの管理コンソールであるため、ネットワーク内のその他のコンピューターの Web ブラウザーを使用してアクセスするか、ECP 仮想ディレクトリ URL を使用してインターネット経由でアクセスすることもできます。


> [!IMPORTANT]
> Exchange 2010 メールボックス サーバー上に配置されたメールボックスを持つアカウント (ドメイン管理者アカウントなど) を使用して EAC にアクセスする場合は、ブラウザーで次のアドレスを使用して EAC にアクセスする必要があります。<BR>https://<EM>&lt;FQDN of Exchange 2013 Client Access server&gt;</EM>/ECP? ExchClientVer=15



EAC では、Office 365 の社内外にまたがるナビゲーション タブを選択して Exchange Online 組織にアクセスします。社内外にまたがるナビゲーションでは、Exchange Online 組織と社内 Exchange 組織間を簡単に切り替えることができます。ハイブリッド展開を構成した場合は、Office 365 タブを選択することで、Exchange Online 組織と受信者オブジェクトを管理できます。Exchange Online 組織がない場合は、Office 365 リンクを選択すると、Office 365 のサインアップ ページが表示されます。

EAC の詳細については、「[Exchange 2013 の Exchange 管理者センター](https://technet.microsoft.com/ja-jp/library/jj150562\(v=exchg.150\))」を参照してください。

## Exchange 管理シェル

この Exchange 管理シェル を使用すると、EAC で実行できるあらゆるタスクのほか、Exchange 管理シェル でしか実行できないいくつかのタスクも実行できます。この Exchange 管理シェル は、Exchange 2013 管理ツールがインストールされるときにコンピューターにインストールされる Windows PowerShell スクリプトとコマンドレットを集めたものです。これらのスクリプトとコマンドレットは、Exchange 管理シェル アイコンを使用して Exchange 管理シェル を開いたときにのみ読み込まれます。Windows PowerShell を直接開いても、これらの Exchange スクリプトとコマンドレットは読み込まれないため、オンプレミスの組織は管理できません。


> [!NOTE]
> 以下で説明する Exchange Online 組織への手動接続と同様の方法で、Windows PowerShell をローカルのオンプレミスの組織に手動で接続することはできます。ただし、オンプレミスの Exchange サーバーの管理は、Exchange 管理シェル アイコンを使用して Exchange 管理シェル を開いて行うことを強くお勧めします。



管理ツールがインストールされているコンピューター上で Exchange 管理シェル アイコンを使用して Exchange 管理シェル を開くと、オンプレミスの組織を管理できます。ただし、このアイコンを使用して Exchange 管理シェル を開いても Exchange Online 組織は管理できません。これは、Exchange 管理シェル アイコンを使用して Exchange 管理シェル を開くとユーザーが自動的にローカルの Exchange サーバーに接続されるためです。

Windows PowerShell を使用して Exchange Online 組織を管理する場合は、Exchange 管理シェル アイコンの使用は避け、Windows PowerShell を直接開く必要があります。Windows PowerShell を開いた後、接続先を手動で指定できます。手動で接続を確立するときは、Office 365 のテナント組織の管理者アカウントを指定した後、コマンドを使用して接続を確立します。接続が確立したら、実行のアクセス許可がある Exchange コマンドレットを使用できるようになります。詳細については、「[Windows PowerShell の使用](http://go.microsoft.com/fwlink/p/?linkid=209660)」を参照してください。

Exchange 管理シェル の使用経験がなく、Exchange 管理シェル の仕組みやコマンド構文などの基本事項を調べる場合は、「[Exchange 2013 で Powershell を使用する (Exchange 管理シェル)](https://technet.microsoft.com/ja-jp/library/bb123778\(v=exchg.150\))」を参照してください。

