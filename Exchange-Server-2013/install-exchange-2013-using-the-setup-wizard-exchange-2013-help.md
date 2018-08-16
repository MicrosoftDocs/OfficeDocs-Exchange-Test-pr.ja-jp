﻿---
title: 'セットアップ ウィザードを使用した Exchange 2013 のインストール: Exchange 2013 Help'
TOCTitle: セットアップ ウィザードを使用した Exchange 2013 のインストール
ms:assetid: da690d47-3384-4430-a69e-0cd4d3bf80a7
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124778(v=EXCHG.150)
ms:contentKeyID: 48270141
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.ExSetupUI.SetupWizardForm.IntroductionPage
ms.translationtype: HT
---

# セットアップ ウィザードを使用した Exchange 2013 のインストール

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-06-19_

ここでは、Microsoft Exchange Server 2013 セットアップ ウィザードを使って、Exchange 2013 のメールボックスとクライアント アクセスの役割をコンピューターにインストールする方法について説明します。Exchange 2013 の計画および展開の詳細については、「[計画と展開](planning-and-deployment-for-exchange-2013-installation-instructions.md)」を参照してください。

Exchange 2013 のエッジ トランスポートの役割をコンピューターにインストールする場合は、「[セットアップ ウィザードを使用して Exchange 2013 エッジ トランスポートの役割をインストールする](install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md)」を参照してください。メールボックスやクライアント アクセスのサーバーの役割と同じコンピューター上にエッジ トランスポートの役割をインストールすることはできません。


> [!TIP]
> Exchange Server 展開アシスタントについて聞いたことがありますか。これは、いくつかの質問を通して特別にカスタマイズされた展開チェックリストを作成することにより、組織への Exchange 2013 の迅速な展開を支援する無料のオンライン ツールです。この詳細については、「<A href="exchange-server-deployment-assistant-exchange-2013-help.md">Exchange Server 展開アシスタント</A>」にアクセスしてください。




> [!NOTE]
> Exchange 2013 を実行しているコンピューターにいずれかのサーバーの役割をインストールした後は、Exchange 2013 セットアップ ウィザードを使用して他のサーバーの役割をこのコンピューターに追加することはできません。サーバーの役割をコンピューターに追加する必要がある場合は、コントロール パネルの [プログラムの追加と削除] を使用するか、コマンド プロンプト ウィンドウで Setup.exe を使用する必要があります。



インストール後に実行するタスクの詳細については、「[Exchange 2013 のインストール後のタスク](exchange-2013-post-installation-tasks-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 60 分

  - Exchange 2013 をインストールする前に、リリース ノートを読んだことを確認してださい。詳細については、「[Exchange 2013 のリリース ノート](release-notes-for-exchange-2013-exchange-2013-help.md)」を参照してください。

  - 各組織では、Active Directory フォレスト内に最低でも 1 つのクライアント アクセス サーバーと 1 つのメールボックス サーバーが必要です。また、メールボックス サーバーを含む各 Active Directory サイトには、クライアント アクセス サーバーが少なくとも 1 つ含まれている必要があります。サーバーの役割を分離している場合は、最初にメールボックス サーバーの役割をインストールすることをお勧めします。

  - Exchange 2013 をインストールするコンピューターは、サポートされているオペレーティング システム (Windows Server 2008 R2 と Service Pack 1 (SP1) または Windows Server 2012) が搭載されていて、十分な空きディスク領域を備え、Active Directory ドメインのメンバーであり、さらにその他の要件も満たしている必要があります。システム要件の詳細については、「[Exchange 2013 のシステム要件](exchange-2013-system-requirements-exchange-2013-help.md)」を参照してください。

  - Exchange 2013 セットアップを実行するには、Microsoft .NET Framework 4.5、Windows Management Framework 3.0、およびその他の必要なソフトウェアをインストールしておく必要があります。すべてのサーバーの役割の前提条件を理解するには、「[Exchange 2013 の前提条件](exchange-2013-prerequisites-exchange-2013-help.md)」を参照してください。

  - 次の手順を実行するには、これまでに Active Directory スキーマを準備していない場合、使用するアカウントに Schema Admins グループのメンバーシップが委任されていることを確認する必要があります。組織に最初の Exchange 2013 サーバーをインストールしている場合は、Enterprise Admins グループのメンバーシップを持つアカウントを使用する必要があります。既にスキーマを準備していて、組織に最初の Exchange 2013 サーバーをインストールしていない場合は、使用するアカウントが Exchange 2013 "Organization Management/組織の管理" 役割グループのメンバーである必要があります。
    
    "Delegated Setup/委任されたセットアップ" 役割グループのメンバーである管理者は、"Organization Management/組織の管理" 役割管理グループのメンバーによって既に準備された Exchange 2013 サーバーを展開できます。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!NOTE]
> サーバーに Exchange をインストールした後は、サーバー名を変更しないでください。Exchange のサーバーの役割をインストールした後でサーバーの名前を変更することは、サポートされていません。



## Exchange Server 2013 のインストール

組織に最初の Exchange 2013 サーバーをインストールしており、Active Directory の準備手順が実行されていない場合は、Enterprise Administrators グループのメンバーシップを持つアカウントを使用する必要があります。Active Directory スキーマを準備していない場合、使用するアカウントは Schema Admins グループのメンバーでもある必要があります。Active Directory for Exchange 2013 の準備については、「[Active Directory とドメインを準備する](prepare-active-directory-and-domains-exchange-2013-help.md)」を参照してください。このスキーマと Active Directory の準備のステップをすでに実行している場合は、使用するアカウントが "Delegated Setup management/委任セットアップ" 管理役割グループまたは "Organization Management/組織の管理" 管理役割グループのメンバーである必要があります。


> [!NOTE]
> 最新バージョンの Exchange 2013 をダウンロードするには、「<A href="updates-for-exchange-2013-exchange-2013-help.md">Exchange 2013 の更新プログラム</A>」を参照してください。



1.  Exchange 2013 をインストールするコンピューターにログオンします。

2.  Exchange 2013 インストール ファイルが格納されているネットワーク上の場所に移動します。

3.  `Setup.exe` をダブルクリックして、Exchange 2013 のセットアップを開始します。
    

    > [!IMPORTANT]
    > ユーザー アクセス制御 (UAC) が有効になっている場合は、<CODE>Setup.exe</CODE> を右クリックして <STRONG>[管理者として実行]</STRONG> を選択する必要があります。



4.  <strong>更新プログラムの確認</strong> ページで、インターネットに接続して、Exchange 2013 の製品およびセキュリティの更新プログラムをダウンロードするようにセットアップするかどうかを選択します。<strong>インターネットに接続して更新プログラムを確認する</strong> を選択すると、セットアップ プログラムは更新プログラムをダウンロードし、それらを適用してから処理を続行します。<strong>後で更新プログラムを確認する</strong> を選択すると、後から手動で更新プログラムをダウンロードしてインストールできます。今すぐ更新プログラムをダウンロードしてインストールすることをお勧めします。続行するには、<strong>次へ</strong> をクリックします。

5.  
    
    <strong>概要</strong> ページで、組織への Exchange のインストール プロセスを開始します。このページの指示に従ってインストールを行います。コンテンツの展開に役に立ついくつかのリンクが一覧表示されます。セットアップを続行する前にこれらのリンクにアクセスすることをお勧めします。続行するには、<strong>次へ</strong> をクリックします。

6.  
    
    <strong>使用許諾契約書</strong> ページで、ソフトウェア ライセンス条項を確認します。条項に同意する場合は、<strong>使用許諾契約書に同意します</strong> をクリックしてから、<strong>次へ</strong> をクリックします。

7.  
    
    <strong>推奨の設定</strong> ページで、推奨設定を使用するかどうかを選択します。<strong>推奨の設定を使用</strong> を選択した場合は、コンピューター ハードウェアに関するエラー レポート/情報およびユーザーによる Exchange の使用状況が、Exchange により Microsoft に自動的に送信されます。<strong>推奨の設定を使用しない</strong> を選択した場合、これらの設定は無効のままになりますが、セットアップが完了した後にいつでも有効にできます。これらの設定および Microsoft に送信された情報がどのように使用されるかに関する詳細については、<strong>?</strong> をクリックしてください。

8.  
    
    <strong>サーバーの役割の選択</strong> ページで、このコンピューターに <strong>メールボックスの役割</strong>、<strong>クライアント アクセスの役割</strong>、両方の役割、または <strong>管理ツール</strong> のみをインストールするかどうかを選択します。このインストール中にこれらをインストールしないよう選択した場合は、後でその他のサーバーの役割を追加できます。1 つの組織には、1 つ以上のメールボックスの役割と 1 つ以上のクライアント アクセス サーバーの役割をインストールする必要があります。それらをインストールするのは、同一のコンピューターでも異なるコンピューターでもかまいません。いずれかのサーバーの役割をインストールすると、管理ツールが自動的にインストールされます。
    
    セットアップ ウィザードを使用して必要な Windows の前提条件をインストールするには、<strong>Exchange Server のインストールで必要な Windows サーバーの役割と機能を自動的にインストールする</strong> を選択します。Windows の一部の機能のインストールを完了するために、コンピューターの再起動が必要になることがあります。このオプションを選択しない場合、Windows 機能を手動でインストールする必要があります。
    

    > [!NOTE]
    > このオプションは Exchange で必要とされる Windows 機能のみをインストールします。他の前提条件は手動でインストールする必要があります。詳細については、「<A href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 の前提条件</A>」を参照してください。

    
    続行するには、<strong>次へ</strong> をクリックします。

9.  <strong>インストール容量とインストール先</strong> ページで、既定のインストール先を使用するか、<strong>参照</strong> をクリックして新しいインストール先を選択します。Exchange のインストール先に使用可能なディスク容量が十分にあることを確認します。続行するには、<strong>次へ</strong> をクリックします。

10. 
    
    このコンピューターが組織内の最初の Exchange サーバーである場合は、<strong>Exchange 組織</strong> ページで Exchange 組織の名前を入力します。Exchange 組織の名前には、以下の文字のみを含めることができます。
    
      - A ～ Z
    
      - a ～ z
    
      - 0 ～ 9
    
      - スペース (先頭または末尾を除く)
    
      - ハイフンまたはダッシュ
        

        > [!NOTE]
        > 組織名の長さは、64 文字以下です。組織名を省略 (空白に) することはできません。

    
    Active Directory 分割型アクセス許可モデルを使用する場合は、<strong>Active Directory 分割アクセス許可セキュリティモデルを Exchange 組織に適用する</strong> を選択します。
    

    > [!NOTE]
    > 大半の組織では、Active Directory 分割型アクセス許可モデルを適用する必要はありません。Active Directory セキュリティ プリンシパルと Exchange の構成の管理を分ける必要がある場合は、役割ベースのアクセス制御 (RBAC) 分割型アクセス許可が有用です。詳細については、<STRONG>[?]</STRONG> をクリックしてください。

    
    続行するには、<strong>次へ</strong> をクリックします。

11. メールボックスの役割をインストールする場合は、<strong>マルウェア保護の設定</strong> ページで、マルウェアのスキャンを有効にするか無効にするかを選択します。マルウェアのスキャンは、無効にしても後から有効にすることができます。続行するには、<strong>次へ</strong> をクリックします。

12. 
    
    <strong>インストールの前提条件の確認</strong> ページで、状態を表示して、組織およびサーバーの役割の前提条件の確認が正しく完了したかどうかを確認します。正常に完了しなかった場合は、Exchange 2013 のインストール前に報告されたエラーをすべて解決する必要があります。前提条件のエラーを解決しているときに、セットアップを終了する必要はありません。報告されたエラーを解決したら <strong>戻る</strong> をクリックし、その後 <strong>次へ</strong> をクリックして、前提条件の確認を再度実行します。報告された警告も確認してください。準備確認が問題なく完了したら、<strong>次へ</strong> をクリックして Exchange 2013 をインストールします。

13. 
    
    <strong>完了</strong> ページで、<strong>終了</strong> をクリックします。

14. Exchange 2013 のインストールの完了後、コンピューターを再起動します。

15. 「[Exchange 2013 のインストール後のタスク](exchange-2013-post-installation-tasks-exchange-2013-help.md)」に記述されているタスクを実行して、展開を完了します。

## 正常な動作を確認する方法

Exchange 2013 が正常にインストールされたことを確認するには、「[Exchange 2013 のインストールの確認](verify-an-exchange-2013-installation-exchange-2013-help.md)」を参照してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

探しているものは見つかりましたか？検索したい情報に関する[フィードバックを送信](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback)してください。

