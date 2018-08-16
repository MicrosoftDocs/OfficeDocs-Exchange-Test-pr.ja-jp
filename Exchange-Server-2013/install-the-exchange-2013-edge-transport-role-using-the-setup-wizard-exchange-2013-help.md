---
title: 'セットアップ ウィザードを使用して Exchange 2013 エッジ トランスポートの役割をインストールする: Exchange 2013 Help'
TOCTitle: セットアップ ウィザードを使用して Exchange 2013 エッジ トランスポートの役割をインストールする
ms:assetid: b8e51b0b-201e-4c64-92c8-3ac0db04b6e2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn635117(v=EXCHG.150)
ms:contentKeyID: 61204841
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# セットアップ ウィザードを使用して Exchange 2013 エッジ トランスポートの役割をインストールする

 

_**適用先:** Exchange Server, Exchange Server 2013_

_**トピックの最終更新日:** 2014-06-19_

このトピックでは、Microsoft Exchange Server 2013 セットアップ ウィザードを使用して Exchange 2013 エッジ トランスポート サーバーの役割をコンピューターにインストールする方法について説明します。エッジ トランスポートの役割は、Exchange 2013 Service Pack 1 (SP1) 以降で使用できます。Exchange 2013 の計画および展開の詳細については、「[計画と展開](planning-and-deployment-for-exchange-2013-installation-instructions.md)」を参照してください。

エッジ トランスポート サーバーの役割は、組織の内部 Active Directory フォレストの外部の境界ネットワークにインストールすることをお勧めします。エッジ トランスポート サーバーの役割はドメインによって結合されたコンピューターにインストールできますが、これを行うことで有効になるのは Windows 機能および設定のドメイン管理のみです。エッジ トランスポートの役割自体は Active Directory を使用しません。代わりに、Active Directory Lightweight Directory Services (AD LDS) Windows 機能を使用して、構成情報および受信者情報を格納します。エッジ トランスポートの役割の詳細については、「[エッジ トランスポート サーバー](edge-transport-servers-exchange-2013-help.md)」を参照してください。

Exchange 2013 メールボックスやクライアント アクセスの役割をコンピューターにインストールする場合は、「[セットアップ ウィザードを使用した Exchange 2013 のインストール](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)」を参照してください。エッジ トランスポートの役割は、メールボックスやクライアント アクセスのサーバーの役割と同じコンピューター上にインストールすることはできません。


> [!TIP]
> Exchange Server 展開アシスタントについて聞いたことがありますか。これは、いくつかの質問を通して特別にカスタマイズされた展開チェックリストを作成することにより、組織への Exchange 2013 の迅速な展開を支援する無料のオンライン ツールです。この詳細については、「<A href="exchange-server-deployment-assistant-exchange-2013-help.md">Exchange Server 展開アシスタント</A>」にアクセスしてください。



インストール後に実行するタスクの詳細については、「[Exchange 2013 のインストール後のタスク](exchange-2013-post-installation-tasks-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 40 分

  - Exchange 2013 をインストールする前に、リリース ノートを読んだことを確認してださい。詳細については、「[Exchange 2013 のリリース ノート](release-notes-for-exchange-2013-exchange-2013-help.md)」を参照してください。

  - Exchange 2013 をインストールするコンピューターには、サポートされるオペレーティング システム (Windows Server 2008 R2 SP1、Windows Server 2012 R2、または Windows Server 2012 など) や十分なディスク スペースが必要であり、他の要件を満たす必要があります。システム要件の詳細については、「[Exchange 2013 のシステム要件](exchange-2013-system-requirements-exchange-2013-help.md)」を参照してください。

  - Exchange 2013 セットアップを実行するには, .NET Framework 4.5、Windows Management Framework、およびその他の必要なソフトウェアをインストールしておく必要があります。すべてのサーバーの役割の前提条件を理解するには、「[Exchange 2013 の前提条件](exchange-2013-prerequisites-exchange-2013-help.md)」を参照してください。

  - プライマリ DNS サフィックスをコンピューターで構成する必要があります。たとえば、コンピューターの完全修飾ドメイン名が edge.contoso.com である場合、コンピューターの DNS サフィックスは contoso.com になります。詳細については、「[プライマリ DNS サフィックスに \[ms.exch.setupreadiness.FqdnMissing\] が存在しない](primary-dns-suffix-is-missing-exchange-2013-help.md)」を参照してください。

  - Exchange 2007 および Exchange 2010 ハブ トランスポート サーバーは、Exchange 2013 エッジ トランスポート サーバーとの間に EdgeSync サブスクリプションを作成する前に、更新しなければなりません。この更新プログラムをインストールしていない場合、EdgeSync サブスクリプションは正しく動作しません。詳細については、「[Exchange 2013 のシステム要件](exchange-2013-system-requirements-exchange-2013-help.md)」の「サポートされる共存シナリオ」を参照してください。

  - 使用するアカウントが、エッジ トランスポートの役割をインストールするコンピューターでローカル管理者グループのメンバーであることを確認します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!NOTE]
> サーバーに Exchange をインストールした後は、サーバー名を変更しないでください。Exchange のサーバーの役割をインストールした後でサーバーの名前を変更することは、サポートされていません。



## Exchange Server 2013 のインストール


> [!NOTE]
> 最新バージョンの Exchange 2013 をダウンロードする場合は、「<A href="updates-for-exchange-2013-exchange-2013-help.md">Exchange 2013 の更新プログラム</A>」を参照してください。



1.  Exchange 2013 をインストールするコンピューターにログオンします。

2.  Exchange 2013 インストール ファイルが格納されているネットワーク上の場所に移動します。

3.  `Setup.exe` をダブルクリックして、Exchange 2013 のセットアップを開始します。
    

    > [!IMPORTANT]
    > ユーザー アクセス制御 (UAC) が有効になっている場合は、<CODE>Setup.exe</CODE> を右クリックして <STRONG>[管理者として実行]</STRONG> を選択する必要があります。



4.  <strong>更新プログラムの確認</strong> ページで、インターネットに接続して、Exchange 2013 の製品およびセキュリティの更新プログラムをダウンロードするようにセットアップするかどうかを選択します。<strong>インターネットに接続して更新プログラムを確認する</strong> を選択すると、セットアップ プログラムは更新プログラムをダウンロードし、それらを適用してから処理を続行します。<strong>後で更新プログラムを確認する</strong> を選択すると、後から手動で更新プログラムをダウンロードしてインストールできます。今すぐ更新プログラムをダウンロードしてインストールすることをお勧めします。続行するには、<strong>次へ</strong> をクリックします。

5.  
    
    <strong>概要</strong> ページで、組織への Exchange のインストール プロセスを開始します。このページの指示に従ってインストールを行います。コンテンツの展開に役に立ついくつかのリンクが一覧表示されます。セットアップを続行する前にこれらのリンクにアクセスすることをお勧めします。続行するには、<strong>次へ</strong> をクリックします。

6.  
    
    <strong>使用許諾契約書</strong> ページで、ソフトウェア ライセンス条項を確認します。条項に同意する場合は、<strong>使用許諾契約書に同意します</strong> をクリックしてから、<strong>次へ</strong> をクリックします。

7.  
    
    <strong>推奨の設定</strong> ページで、推奨設定を使用するかどうかを選択します。<strong>推奨の設定を使用</strong> を選択した場合は、コンピューター ハードウェアに関するエラー レポート/情報およびユーザーによる Exchange の使用状況が、Exchange により Microsoft に自動的に送信されます。<strong>推奨の設定を使用しない</strong> を選択した場合、これらの設定は無効のままになりますが、セットアップが完了した後にいつでも有効にできます。これらの設定および Microsoft に送信された情報がどのように使用されるかに関する詳細については、<strong>?</strong> をクリックしてください。

8.  
    
    <strong>サーバーの役割の選択</strong> ページで、<strong>エッジ トランスポート</strong> を選択します。エッジ トランスポートの役割がインストールされているコンピューターに対しては、メールボックス サーバーの役割もクライアント アクセス サーバーの役割も追加できません。いずれかのサーバーの役割をインストールすると、管理ツールが自動的にインストールされます。
    
    セットアップ ウィザードを使用して必要な Windows の前提条件をインストールするには、<strong>Exchange Server のインストールに必要な Windows Server の役割と機能を自動的にインストールする</strong> を選択します。Windows の一部の機能のインストールを完了するには、コンピューターの再起動が必要となることがあります。このオプションを選択しない場合、Windows 機能を手動でインストールする必要があります。
    

    > [!NOTE]
    > このオプションは Exchange で必要とされる Windows 機能のみをインストールします。他の前提条件は手動でインストールする必要があります。詳細については、「<A href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 の前提条件</A>」を参照してください。

    
    続行するには、<strong>次へ</strong> をクリックします。

9.  <strong>インストール容量とインストール先</strong> ページで、既定のインストール先を使用するか、<strong>参照</strong> をクリックして新しいインストール先を選択します。Exchange のインストール先に使用可能なディスク容量が十分にあることを確認します。続行するには、<strong>次へ</strong> をクリックします。

10. 
    
    <strong>インストールの前提条件の確認</strong> ページで、状態を表示して、組織およびサーバーの役割の前提条件の確認が正しく完了したかどうかを確認します。正常に完了しなかった場合は、Exchange 2013 のインストール前に報告されたエラーをすべて解決する必要があります。前提条件のエラーを解決しているときに、セットアップを終了する必要はありません。報告されたエラーを解決したら <strong>戻る</strong> をクリックし、その後 <strong>次へ</strong> をクリックして、前提条件の確認を再度実行します。報告された警告も確認してください。準備確認が問題なく完了したら、<strong>次へ</strong> をクリックして Exchange 2013 をインストールします。

11. 
    
    <strong>完了</strong> ページで、<strong>終了</strong> をクリックします。

12. Exchange 2013 のインストールの完了後、コンピューターを再起動します。

13. 「[Exchange 2013 のインストール後のタスク](exchange-2013-post-installation-tasks-exchange-2013-help.md)」に記述されているタスクを実行して、展開を完了します。

## 正常な動作を確認する方法

Exchange 2013 が正常にインストールされたことを確認するには、「[Exchange 2013 のインストールの確認](verify-an-exchange-2013-installation-exchange-2013-help.md)」を参照してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

探しているものは見つかりましたか？検索したい情報に関する[フィードバックを送信](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback)してください。

