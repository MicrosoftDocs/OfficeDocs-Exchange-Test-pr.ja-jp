---
title: 'Exchange 2013 管理ツールをインストールする: Exchange 2013 Help'
TOCTitle: Exchange 2013 管理ツールをインストールする
ms:assetid: 71fcbe4c-783b-4f77-aabb-a21aa7a4ef23
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb232090(v=EXCHG.150)
ms:contentKeyID: 49129531
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 管理ツールをインストールする

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2013-01-28_

Microsoft Exchange Server 2013 管理ツールを使用すると、Exchange 組織をリモートから構成および管理できます。Exchange 2013 管理ツールには、Exchange 管理シェルおよび Exchange ツールボックスが含まれます。ここでは、Setup.exe または無人セットアップ モードを使用して Exchange 2013 管理ツールをインストールする方法について説明します。


> [!NOTE]
> Exchange 管理センター (EAC) をリモートから使用する場合には、この手順を実行する必要はありません。EAC は、Exchange 2013 クライアント アクセス サーバーの役割を実行しているコンピューター上でホストされる Web ベースのコンソールです。EAC へのリモートからのアクセスの詳細については、「<A href="exchange-admin-center-in-exchange-2013-exchange-2013-help.md">Exchange 2013 の Exchange 管理者センター</A>」を参照してください。



Exchange 2013 の管理の詳細については、「[Exchange 2013 の Exchange 管理者センター](exchange-admin-center-in-exchange-2013-exchange-2013-help.md)」および「[Exchange 2013 で Powershell を使用する (Exchange 管理シェル)](https://technet.microsoft.com/ja-jp/library/bb123778\(v=exchg.150\))」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 10 分

  - Exchange 2013 をインストールする前に、リリース ノートを読んだことを確認してださい。詳細については、「[Exchange 2013 のリリース ノート](release-notes-for-exchange-2013-exchange-2013-help.md)」を参照してください。

  - 管理ツールをインストールするコンピューターは、サポートされているオペレーティング システム (Windows Server 2012 または Windows 8 など) が搭載され、十分な空きディスク領域があり、Active Directory ドメインのメンバーであり、さらにその他の要件も満たしている必要があります。システム要件の詳細については、「[Exchange 2013 のシステム要件](exchange-2013-system-requirements-exchange-2013-help.md)」を参照してください。

  - Exchange 2013 セットアップを実行するには、Microsoft .NET Framework 4.5、Windows Management Framework 3.0、およびその他の必要なソフトウェアをインストールしておく必要があります。すべてのサーバーの役割の前提条件を理解するには、「[Exchange 2013 の前提条件](exchange-2013-prerequisites-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## セットアップを使用して Exchange 2013 管理ツールをインストールする

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
    
    <strong>サーバーの役割の選択</strong> ページで、<strong>管理ツール</strong> が選択されていることを確認します。
    
    セットアップ ウィザードを使用して必要な Windows の前提条件をインストールするには、<strong>Exchange Server のインストールに必要な Windows Server の役割および機能を自動的にインストールする</strong> を選択します。Windows の一部の機能のインストールを完了するには、コンピューターの再起動が必要となることがあります。このオプションを選択しない場合、Windows 機能を手動でインストールする必要があります。
    

    > [!NOTE]
    > このオプションは Exchange で必要とされる Windows 機能のみをインストールします。他の前提条件は手動でインストールする必要があります。詳細については、「<A href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 の前提条件</A>」を参照してください。

    
    続行するには、<strong>次へ</strong> をクリックします。

9.  <strong>インストール容量とインストール先</strong> ページで、既定のインストール先を使用するか、<strong>参照</strong> をクリックして新しいインストール先を選択します。Exchange のインストール先に使用可能なディスク容量が十分にあることを確認します。続行するには、<strong>次へ</strong> をクリックします。

10. 
    
    組織内で Exchange 2013 セットアップを初めて実行する場合は、<strong>Exchange 組織</strong> ページで Exchange 組織の名前を入力します。Exchange 組織の名前には、以下の文字のみを含めることができます。
    
      - A ～ Z
    
      - a ～ z
    
      - 0 ～ 9
    
      - スペース (先頭または末尾を除く)
    
      - ハイフンまたはダッシュ
        

        > [!NOTE]
        > 組織名の長さは、64 文字以下です。組織名を省略 (空白に) することはできません。

    
    Active Directory 分割型アクセス許可モデルを使用する場合は、<strong>Active Directory 分割型アクセス許可セキュリティモデルを Exchange 組織に適用する</strong> を選択します。
    

    > [!NOTE]
    > 大半の組織では、Active Directory 分割型アクセス許可モデルを適用する必要はありません。Active Directory セキュリティ プリンシパルと Exchange の構成の管理を分ける必要がある場合は、役割ベースのアクセス制御 (RBAC) 分割型アクセス許可が有用です。詳細については、<STRONG>[?]</STRONG> をクリックしてください。

    
    続行するには、<strong>次へ</strong> をクリックします。

11. 
    
    <strong>インストールの前提条件の確認</strong> ページで、状態を表示して、組織およびサーバーの役割の前提条件の確認が正しく完了したかどうかを確認します。正常に完了しなかった場合は、Exchange 2013 のインストール前に報告されたエラーをすべて解決する必要があります。前提条件エラーを解決する際に、セットアップを終了する必要はありません。報告されたエラーを解決したら <strong>戻る</strong> をクリックし、その後 <strong>次へ</strong> をクリックして、前提条件の確認を再度実行します。また、報告された警告も必ず確認してください。準備確認が問題なく完了したら、<strong>次へ</strong> をクリックして Exchange 2013 をインストールします。

12. 
    
    <strong>完了</strong> ページで、<strong>終了</strong> をクリックします。

13. Exchange 2013 のインストールの完了後、コンピューターを再起動します。

## 無人セットアップ モードを使用して Exchange 2013 管理ツールをインストールする

1.  Exchange 2013 管理ツールをインストールするコンピューターにログオンします。

2.  Exchange 2013 インストール ファイルが格納されているネットワーク上の場所に移動します。

3.  コマンド プロンプトで、次のコマンドを実行します。
    

    > [!IMPORTANT]
    > ユーザー アクセス コントロール (UAC) を有効にした場合は、昇格したコマンド プロンプトから <CODE>Setup.exe</CODE> を実行してください。

    
    ```powershell
    Setup.exe /Role:ManagementTools /IAcceptExchangeServerLicenseTerms
    ```

詳細については、「[無人モードを使用した Exchange 2013 のインストール](install-exchange-2013-using-unattended-mode-exchange-2013-help.md)」を参照してください。

