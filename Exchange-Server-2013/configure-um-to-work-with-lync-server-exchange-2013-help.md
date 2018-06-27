---
title: 'Lync Server で動作するように UM を構成する: Exchange 2013 Help'
TOCTitle: Lync Server で動作するように UM を構成する
ms:assetid: 29bdddbf-75d5-4c92-988e-c8506ecc7a1c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ966276(v=EXCHG.150)
ms:contentKeyID: 52057806
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Lync Server で動作するように UM を構成する

 

_**適用先:**Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:**2013-06-11_

Microsoft Lync Server を Exchange ユニファイド メッセージング (UM) と統合しているときは、ExchUcUtil.ps1 スクリプトをシェルで実行する必要があります。ExchUcUtil.ps1 スクリプトは次の処理を行います。

  - Lync Server プールごとに UM IP ゲートウェイを作成します。
    

    > [!IMPORTANT]
    > ExchUcUtil.ps1 スクリプトは、1 つまたは複数の UM IP ゲートウェイを作成します。スクリプトで作成した 1 つのゲートウェイを除き、すべての UM IP ゲートウェイでの発信呼び出しを無効にする必要があります。これにはスクリプトを実行する前に作成した UM IP ゲートウェイでの発信呼び出しを無効にすることが含まれます。UM IP ゲートウェイでの発信呼び出しを無効にするには、「<A href="disable-outgoing-calls-on-um-ip-gateways-exchange-2013-help.md">UM IP ゲートウェイで送信呼び出しを無効にする</A>」を参照してください。



  - UM IP ゲートウェイごとに UM ハント グループを作成します。各ハント グループのパイロット ID は、UM IP ゲートウェイと関連する Lync Server フロント エンド プールまたは Standard Edition サーバーによって使用される UM SIP URI ダイヤル プランを指定します。

  - UM ダイヤル プラン、自動応答、UM IP ゲートウェイ、UM ハント グループなど、Active Directory UM コンテナー オブジェクトを読み取るアクセス許可を Lync Server に与えます。


> [!IMPORTANT]
> Lync Server 2013 が展開されているフォレストを信頼するように各 UM フォレストを構成し、各 UM フォレストを信頼するように、Lync Server 2013 が展開されているフォレストを構成する必要があります。Exchange UM を複数のフォレストにインストールする場合は、UM フォレストごとに Exchange サーバーの統合手順を実行するか、Lync Server ドメインを指定する必要があります。たとえば、<EM>ExchUcUtil.ps1 –Forest:&lt;lync-domain-controller-fqdn&gt;</EM> などです。



Lync Server とユニファイド メッセージングの統合に関連するその他の管理タスクについては、「[Exchange 2013 UM および Lync Server の展開の概要](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[Exchange 2013 コマンドレット](https://technet.microsoft.com/ja-jp/library/bb124413\(v=exchg.150\))」の「アクセス許可のコマンドレット」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## シェルを使用して ExchUcUtil.ps1 スクリプトを実行する

Microsoft Lync Server と同じトポロジにある組織の Exchange サーバーで ExchUcUtil.ps1 スクリプトを実行します。シェルを使用してメールボックス サーバーからスクリプトを実行するか、クライアント アクセス サーバーのリモート Windows PowerShell を使用してスクリプトを実行することもできます。組織のクライアント アクセス サーバーでスクリプトを実行すると、クライアント アクセス サーバーがリモート Windows PowerShell セッションを組織のメールボックス サーバーにプロキシ処理します。


> [!IMPORTANT]
> ExchUcUtil.ps1 スクリプトは、1 つまたは複数の UM IP ゲートウェイを作成します。スクリプトで作成した 1 つのゲートウェイを除き、すべての UM IP ゲートウェイでの発信呼び出しを無効にする必要があります。これにはスクリプトを実行する前に作成した UM IP ゲートウェイでの発信呼び出しを無効にすることが含まれます。UM IP ゲートウェイでの発信呼び出しを無効にするには、「<A href="disable-outgoing-calls-on-um-ip-gateways-exchange-2013-help.md">UM IP ゲートウェイで送信呼び出しを無効にする</A>」を参照してください。




> [!IMPORTANT]
> Exchange 組織管理役割のアクセス許可を保有するか、Exchange 組織管理者セキュリティ グループのメンバーである必要があります。



1.  Exchange 管理シェルを開きます。

2.  `C:\Windows\System32` プロンプトに「**cd “\<drive letter\>\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts\>.ExchUcUtil.ps1”**」と入力し、Enter キーを押します。

## 正常な動作を確認する方法

ExchUcUtul.ps1 スクリプトが正常に完了したことを確認するには、以下を実行します。

  - **Get-UMIPGateway** コマンドレットか EAC を使用し、作成された新しい UM IP ゲートウェイを表示します。

  - **Get-UMHuntGroup** コマンドレットか EAC を使用し、作成された新しい UM ハント グループを表示します。

