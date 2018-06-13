---
title: 'オンプレミスの Exchange ハイブリッドを使用して Office 365 グループを構成する: Exchange 2013 Help'
TOCTitle: オンプレミスの Exchange ハイブリッドを使用して Office 365 グループを構成する
ms:assetid: 184dfcfe-4b8e-450a-adc6-e647213b9501
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Mt668829(v=EXCHG.150)
ms:contentKeyID: 72513061
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# オンプレミスの Exchange ハイブリッドを使用して Office 365 グループを構成する

 

_**トピックの最終更新日:**2016-12-06_

オンプレミスの Exchange ユーザーがハイブリッド展開で Office 365 グループを使用できるようにする方法を説明します。

グループは、チームの通信、会議のスケジュール、およびドキュメントのコラボレーションを容易にするための Office 365 のサービスです。グループに送信した電子メール メッセージから、グループの OneDrive for Business または SharePoint ライブラリに保存してあるファイルまで、グループ内で共有している情報はすべて、グループのメンバー全員が利用することができます。オンプレミスの Exchange 組織と Office 365 の間でハイブリッド展開を設定してある場合、このトピックの手順を実行すると、Office 365 で作成されたグループをオンプレミスのユーザーが使用できるようになります。


> [!IMPORTANT]
> オンプレミスのユーザーによる Office 365 グループの使用は、Exchange ハイブリッド展開での新しい機能です。まだ新しいため、設定の段階で問題が発生するかもしれません。考えられる問題を修正する方法については、このトピックの最後にある「既知の問題」のセクションを参照してください。



## 前提条件

開始する前に、以下のことが完了していることを確認します。

  - テナント用に Azure Active Directory プレミアム ライセンスを購入している。これは、Azure Active Directory Connect でのグループの書き戻し機能を有効にするために必要です。

  - Exchange のオンプレミスの組織と Office 365 の間でハイブリッド展開を設定しており、正しく機能することが確認されている。Exchange ハイブリッド展開の詳細については、次を参照してください。
    
      - [Exchange Server のハイブリッド展開](exchange-server-hybrid-deployments-exchange-2013-help.md)
    
      - [ハイブリッド展開の前提条件](hybrid-deployment-prerequisites-exchange-2013-help.md)

  - サポートされている Exchange のバージョンがインストールされている。Office 365 グループとのオンプレミス Exchange の統合が、Exchange 2016 の CU1 以降のリリース、および Exchange 2013 の CU11 以降のリリースで可能。ただし、Exchange ハイブリッドでは最新の Exchange 2013 または Exchange 2016 の累積的な更新プログラム (CU) をオンプレミス Exchange サーバーにインストールしておく必要があります。最新の CU をインストールできない場合、現在の CU の直前にリリースされた更新プログラムを使用できます。

  - Azure Active Directory Connect (Azure AD Connect) を使用してシングル サインオンを構成している。これは、グループ電子メール メッセージの **\[グループ ファイルを表示\]** またはクラウド添付リンクをユーザーがクリックできるようにするために必要です。
    
    Exchange ハイブリッド展開でシングル サインオン用に Azure AD Connect を構成する場合は、パスワード同期を使用することをお勧めします。Active Directory フェデレーション サービス (AD FS) は、大規模な組織に所属している場合、複雑なオンプレミス Active Directory 展開 (たとえば、複数の Active Directory フォレスト) がある場合、他の Microsoft 製品が AD FS に Office 365 で作業するように要求する場合、または、コンプライアンス ポリシーのため、オンプレミス ネットワークの外部でパスワードを同期できない場合にのみ使用してください。シングル サインオンの詳細については、「[オンプレミス ID と Azure Active Directory との統合](http://go.microsoft.com/fwlink/p/?linkid=723513)」を参照してください。

## Azure AD Connect でグループの書き戻しを有効にする

1.  Azure AD Connect ウィザードで、**\[同期オプションのカスタマイズ\]** を選択して **\[次へ\]** をクリックします。

2.  **\[Azure AD に接続する\]** ページで、Office 365 とオンプレミスの資格情報を入力します。**\[次へ\]** をクリックします。

3.  **\[オプション機能\]** ページで、以前に構成したオプションがまだ選択されていることを確認します。最も一般的に選択されるオプションは、**\[Exchange ハイブリッド\]** と **\[パスワード ハッシュの同期\]** です。

4.  **\[グループの書き戻し\]** を選択して **\[次へ\]** をクリックします。

5.  **\[書き戻し\]** ページで、Office 365 からオンプレミスの組織に同期するオブジェクトを格納する Active Directory 組織単位 (OU) を選択し、**\[次へ\]** をクリックします。

6.  **\[構成の準備完了\]** ページで、**\[構成\]** をクリックします。

7.  ウィザードが完了したら、**\[構成の完了\]** ページで **\[終了\]** をクリックします。

8.  Active Directory ドメイン コントローラーで \[Active Directory ユーザーとコンピューター\] を開き、**AAD\_** で始まるユーザー アカウントを見つけます。このアカウントの名前をメモします。

9.  オンプレミス Exchange サーバー上で Exchange 管理シェルを開き、次のコマンドを実行します。
    
        $AzureADConnectSWritebackAccount = <AAD_ account name from step 8>
        
        $GroupsOU = <writeback Active Directory OU selected in step 5>
        
        Import-Module "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1"
        
        Initialize-ADSyncGroupWriteBack -ADConnectorAccount $AzureADConnectSWritebackAccount -GroupWriteBackContainerDN $GroupsOU

## グループ ドメインを設定する

Office 365 グループのプライマリ SMTP ドメインは、*グループ ドメイン*と呼ばれます。既定では、組織の既定の承認済みドメインが、グループ ドメインとして選択されています。専用のグループ ドメインを追加する場合、ドメインは次の手順で追加できます。Office 365 グループ向けのマルチドメイン サポートに関する詳細については、「[Office 365 グループ - 管理者向けヘルプの複数のドメインのサポート](https://support.office.com/ja-jp/article/multi-domain-support-for-office-365-groups-admin-help-7cf5655d-e523-4bc3-a93b-3ccebf44a01a)」を参照してください

1.  Office 365 の組織に新しいドメインを追加します。Office 365 にドメインを追加するには、「[Office 365 にユーザーとドメインを追加する](https://support.office.com/ja-jp/article/add-users-and-domain-to-office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611?ui=en-us%26rs=en-us%26ad=us)」を参照してください

2.  次のコマンドを使用して、オンプレミス Exchange 組織の承認済みドメインとしてグループ ドメインを追加します。これにより、ハイブリッド送信コネクタを Office 365 のグループ ドメインへの送信メールの配信に使用することができます。
    
        New-AcceptedDomain -Name groups.contoso.com -DomainName groups.contoso.com -DomainType InternalRelay

3.  DNS プロバイダーで次のパブリック DNS レコードを作成します。
    
    
    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><p>DNS レコードの名前</p></th>
    <th><p>DNS レコードの種類</p></th>
    <th><p>DNS レコードの値</p></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>groups.contoso.com</p></td>
    <td><p>MX</p></td>
    <td><p>groups-contoso-com.mail.protection.outlook.com</p>

    > [!NOTE]
    > この DNS レコード値のフォーマットは、<EM>&lt;domain key&gt;</EM>.mail.protection.outlook.com です。ドメイン キーの確認方法については、「<A href="https://support.office.com/ja-jp/article/gather-the-information-you-need-to-create-office-365-dns-records-77f90d4a-dc7f-4f09-8972-c1b03ea85a67?ui=en-us%26rs=en-us%26ad=us">Office 365 の DNS レコードの作成に必要な情報を収集する</A>」を参照してください。


</td>
    </tr>
    <tr class="even">
    <td><p>autodiscover.groups.contoso.com</p></td>
    <td><p>CNAME</p></td>
    <td><p>autodiscover.outlook.com</p></td>
    </tr>
    </tbody>
    </table>
    

    > [!NOTE]
    > グループ ドメインの MX DNS レコードがオンプレミス Exchange サーバーに設定されている場合、オンプレミス Exchange 組織と Office 365 グループのユーザー間のメール フローが正しく動作しません。



4.  次のコマンドを使用して、ハイブリッド構成のウィザードによってオンプレミス Exchange 組織に作成したハイブリッド送信コネクタにグループ ドメインを追加します。
    
        Set-SendConnector -Identity "Outbound to Office 365" -AddressSpaces "contoso.mail.onmicrosoft.com","groups.contoso.com"
    

    > [!NOTE]
    > 送信コネクタが更新されていない場合、またはグループ ドメインがオンプレミス Exchange 組織の承認済みドメインとして追加されていない場合、グループが外部送信者からのメールを受信するよう設定されていないかぎり、オンプレミスのメールボックスから送信されたメールはグループに配信されません。



## 正常な動作を確認する方法

Exchange ハイブリッド展開でグループを正常に動作させるには、オンプレミスのメールボックス、およびオンプレミスの組織から Office 365 に移動したメールボックスを使用してグループをテストする必要があります。それぞれのテストを実行するには、次のセクションの手順に従います。

## オンプレミスのメールボックスを使用してテストする

1.  オンプレミスのメールボックスを Office 365 グループに追加します。

2.  Office 365 のメールボックスを同じ Office 365 グループに追加します。

3.  Outlook on the web を使用して Office 365 のメールボックスにログインします。

4.  Office 365 のメールボックスを使用してグループにメッセージを投稿します。

5.  Outlook 2016 または Outlook on the web を使用してオンプレミスのメールボックスを開きます。

6.  そのメールボックスで、Office 365 グループに送信された投稿を含む電子メール メッセージを受信したことを確認します。

7.  同じメールボックスでメッセージに対する返信を作成し、グループに送信します。

8.  グループのすべてのメンバーがそのメッセージを表示できることを確認します。

## Office 365 に移動したメールボックスを使用してテストする

1.  メールボックスをオンプレミス Exchange 組織から Office 365 に移動します。

2.  Office 365 グループにメールボックスを追加します。

3.  新しいブラウザー セッションで、Office 365 に移動したメールボックスにログインします。

4.  Outlook on the web で、そのグループが左のナビゲーション バーに表示されていることを確認します。

5.  グループにメッセージを投稿します。

6.  グループのすべてのメンバーがそのメッセージを表示できることを確認します。

## 既知の問題

  - **Office 365 に移動したメールボックスにグループが表示されない** ユーザーがオンプレミス Exchange 組織を Office 365 に移動すると、Outlook または Outlook on the web の左のナビゲーション ウィンドウにグループが表示されません。問題を解決するには、所属するすべてのグループからメールボックスを削除し、もう一度各グループに追加します。

  - **オンプレミス Exchange グローバル アドレス一覧 (GAL) に新しいグループが表示されない** Office 365 に新しいグループを作成しても、オンプレミスの GAL には自動的に表示されません。この問題を解決するには、オンプレミス Exchange サーバー上で Exchange 管理シェルを開き、次のコマンドを実行します。
    
        Update-Recipient "<group name>"

  - **グループがオンプレミスのユーザーからのメッセージを受信しない** 次の条件が当てはまる場合、オンプレミスのユーザーは Office 365 グループにメールを送信できません。
    
      - グループ ドメインがオンプレミス Exchange 組織の権限のあるドメインとして設定されている。
    
      - グループが新しく作成されており、その情報がオンプレミス Active Directory に書き戻されていない。
    
    この問題は、Azure AD Connect で Office 365 とオンプレミスの組織との同期が次回実行されるときに自然に解消します。Azure AD Connect の同期は 30 分ごとに実行されます。

  - **オンプレミスのユーザーがグループ メッセージ フッターにあるリンクを使用できない** オンプレミスのユーザーは、送信された各グループ メッセージのフッターに含まれる **\[グループ スレッドを表示\]** や **\[退会する\]** のリンクを使用できません。オンプレミス ユーザーがグループから退会するには、グループ管理者に連絡する必要があります。

  - **グループのセカンダリ SMTP アドレスに送信したメッセージが配信されない** 1 グループに複数の電子メール アドレスを追加すると、プライマリ SMTP アドレスのみがオンプレミスの Active Directory に書き戻されます。オンプレミスのユーザーがグループのセカンダリ SMTP アドレスにメッセージを送信しようとすると、メッセージの配信が失敗します。この問題を回避するには、各グループに設定する SMTP アドレスを 1 つだけにします。

  - **オンプレミスのユーザーをグループの管理者にできない** オンプレミスのユーザーはグループ スペースに直接アクセスできません。このため、グループの管理者としては追加できません。

  - **一元化されたメール フローを有効にした場合、グループへの外部メールの配信が失敗することがある** 一元化されたメール フローが有効な場合、グループが外部の送信者からのメールを許可していても、外部のユーザーからグループへ送信されたメールは配信できません。

  - **オンプレミスのユーザーは、グループとしてメールを送信できない** オンプレミスのユーザーが Office 365 のグループとしてメッセージを送信しようとすると、たとえそのグループとして送信するためのアクセス許可が付与されていても、permission denied エラーが表示されます。グループとして送信するためのアクセス許可は、Exchange Online メールボックス ユーザーの場合にのみ有効に機能します。

  - **Outlook の左側のナビゲーション ウィンドウからグループを選択しても、グループのメールボックスが開かない** Outlook は自動検出 URL を使用してグループのメールボックスを開きます。グループのプライマリ電子メール アドレスが、Office 365 の自動検出 URL (autodiscover.outlook.com) をポイントしていないドメインにある場合、Outlook はグループのメールボックスを開けません。問題を解決するには、Office 365 の自動検出 URL をポイントするドメイン内のプライマリ アドレスを使用して、グループをプロビジョニングすることができます。各グループのメールボックスに対して Office 365 の自動検出 URL をポイントするプライマリ電子メール アドレスを追加する電子メール アドレス ポリシーを設定できます。詳細については、「[Office 365 グループ - 管理者向けヘルプの複数のドメインのサポート](https://support.office.com/ja-jp/article/multi-domain-support-for-office-365-groups-admin-help-7cf5655d-e523-4bc3-a93b-3ccebf44a01a)」を参照してください。

