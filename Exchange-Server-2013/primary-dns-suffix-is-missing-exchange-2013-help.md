---
title: 'プライマリ DNS サフィックスに が存在しない: Exchange 2013 Help'
TOCTitle: プライマリ DNS サフィックスに が存在しない
ms:assetid: 310765bf-a650-4a3d-a5e4-6173b559d4f6
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.fqdnmissing(v=EXCHG.150)
ms:contentKeyID: 61204835
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# プライマリ DNS サフィックスに が存在しない

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2014-01-15_

Microsoft Exchange Server 2013 セットアップは、Exchange をインストールしているコンピューターのプライマリ ドメイン ネーム システム (DNS) サフィックスが構成されていないために続行できません。

この問題を解決するには、以下の手順を使用してコンピューターにプライマリ DNS サフィックスを追加し、セットアップを再度実行します。


> [!IMPORTANT]
> Exchange 2013 をインストールした後にコンピューター名やプライマリ DNS サフィックスを変更することは、サポートされていません。



1.  エッジ トランスポートの役割をインストールするコンピューターに、ローカルの Administrators グループのメンバーであるユーザーとしてログオンします。

2.  **\[コントロール パネル\]** を開いてから **\[システム\]** をダブルクリックします。

3.  **\[コンピューター名、ドメインおよびワークグループの設定\]** セクションで、**\[設定の変更\]** をクリックします。

4.  **\[システムのプロパティ\]** ウィンドウで **\[コンピューター名\]** タブが選択されていることを確認してから、**\[変更…\]** をクリックします。

5.  **\[コンピューター名/ドメイン名の変更\]** で **\[詳細…\]** をクリックします。

6.  **\[このコンピューターのプライマリ DNS サフィックス\]** にエッジ トランスポート サーバーの DNS ドメイン名を入力します。たとえば、「contoso.com」と入力します。

7.  **\[OK\]** をクリックして各ウィンドウを閉じます。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

探しているものは見つかりましたか？検索したい情報に関する[フィードバックを送信](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback)してください。

