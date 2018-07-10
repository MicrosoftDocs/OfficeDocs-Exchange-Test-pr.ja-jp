---
title: 'Exchange 2013 でインプレース アーカイブを管理する: Exchange 2013 Help'
TOCTitle: Exchange 2013 でインプレース アーカイブを管理する
ms:assetid: 49ef4a3e-d209-4fb2-80a3-6132b0f69bd0
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ651146(v=EXCHG.150)
ms:contentKeyID: 49896234
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 でインプレース アーカイブを管理する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-02-01_

インプレース アーカイブを使用すると、個人用ストア ファイル (.pst) を使用する必要がなくなり、組織のメッセージ保持および電子情報開示の要件を満たすことができるため、組織のメッセージング データを管理しやすくなります。アーカイブが有効な場合、ユーザーは MicrosoftOutlook および Outlook Web App を使用してアクセス可能なアーカイブ メールボックスにメッセージを保存できます。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「インプレース アーカイブ」。

  - ユーザーのアーカイブより古いバージョンの Exchange 上に、プライマリ メールボックスを置くことはサポートされていません。まだプライマリ メールボックスが Exchange 2010 上にある場合は、アーカイブを Exchange 2013 に移動すると同時に Exchange 2013 へプライマリ メールボックスを移動する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## メールボックスを作成し、社内アーカイブを有効にする

## EAC を使用する

1.  **\[受信者\]** \> **\[メールボックス\]** に移動します。

2.  **\[新規作成\]** \> **\[ユーザー メールボックス\]** の順にクリックします。

3.  **\[新しいユーザー メールボックス\]** ページの **\[エイリアス\]** ボックスに、そのユーザーのエイリアスを入力します。
    

    > [!NOTE]
    > このボックスに何も入力しない場合は、<STRONG>[ユーザー ログイン名]</STRONG> ボックスに入力した値がエイリアスとして使用されます。



4.  次のいずれかのオプションを選択します。
    
      - **\[既存のユーザー\]**   このボタンをクリックしてから **\[参照\]** をクリックすると、**\[ユーザーの選択 - フォレスト全体\]** ダイアログ ボックスが開きます。このダイアログ ボックスには、メールが有効でないか Exchange メールボックスを持っていないフォレスト内の Active Directory ユーザー アカウントの一覧が表示されます。メールを有効にするユーザー アカウントを選択し、**\[OK\]** をクリックします。このオプションを選択した場合、ユーザー アカウント情報は Active Directory にすでに存在するため、この情報を入力する必要はありません。
    
      - **\[新しいユーザー\]**   Active Directory の新しいユーザー アカウントを作成し、ユーザーのメールボックスを作成するには、このボタンをクリックします。このオプションを選択した場合、ユーザー アカウントの必須項目を指定する必要があります。
    

    > [!NOTE]
    > ユーザー メールボックスと関連付けられる Active Directory アカウントは、Exchange サーバーと同じフォレストに存在する必要があります。信頼されたフォレストに存在するユーザー アカウント用にメールボックスを作成するには、リンクされたメールボックスを作成する必要があります。詳細については、「<A href="manage-linked-mailboxes-exchange-2013-help.md">リンクされたメールボックスの管理</A>」を参照してください。



5.  **\[その他のオプション\]** をクリックし、次の設定を構成します。
    
      - **\[メールボックス データベース\]**   メールボックスを格納するメールボックス データベースを選択するには、**\[参照\]** をクリックします。データベースを選択しない場合は、Exchange から自動的に 1 つのデータベースが割り当てられます。
    
      - **\[アーカイブ\]**   メールボックスのアーカイブ メールボックスを作成するには、このチェック ボックスをオンにします。アーカイブ メールボックスを作成する場合は、既定のアイテム保持ポリシー設定または定義するアイテム保持ポリシー設定に基づいて、メールボックス アイテムがプライマリ メールボックスからアーカイブに自動的に移動します。
        
        **\[参照\]** をクリックして、アーカイブ メールボックスを格納するローカル フォレストに存在するデータベースを選択します。
        
        詳細については、「[Exchange 2013 のインプレース アーカイブ](in-place-archiving-in-exchange-2013-exchange-2013-help.md)」を参照してください。
    
      - **\[アドレス帳ポリシー\]**   メールボックスのアドレス帳ポリシー (ABP) を選択するには、この一覧を使用します。ABP には、グローバル アドレス一覧 (GAL)、オフライン アドレス帳 (OAB)、会議室一覧、およびアドレス一覧のセットが含まれます。ABP をメールボックス ユーザーに割り当て、各ユーザーに Outlook および Outlook Web App のカスタマイズされた GAL へのアクセス権を付与します。詳細については、「[アドレス帳ポリシー](address-book-policies-exchange-2013-help.md)」を参照してください。

6.  完了したら、**\[保存\]** をクリックしてメールボックスを作成します。

## シェルを使用する

この例では、Active Directory に Chris Ashton というユーザーを作成し、メールボックス データベース DB01 にメールボックスを作成して、アーカイブを有効にします。次回のログオン時に、パスワードを再設定する必要があります。パスワードの初期値を設定するために、この例では $password という変数を作成し、パスワードの入力を求めるメッセージを表示して、そのパスワードを SecureString オブジェクトとして変数に設定します。

    $password = Read-Host "Enter password" -AsSecureString
    New-Mailbox -UserPrincipalName chris@contoso.com -Alias chris -Archive -Database "DB01" -Name ChrisAshton -OrganizationalUnit Users -Password $password -FirstName Chris -LastName Ashton -DisplayName "Chris Ashton" 

構文およびパラメーターの詳細については、「[New-Mailbox](https://technet.microsoft.com/ja-jp/library/aa997663\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

社内アーカイブを使用するユーザーのメールボックスが正常に作成されたことを確認するには、次の手順のいずれかを実行します。

  - EAC で、**\[受信者\]** \> **\[メールボックス\]** の順に移動し、一覧から新しいユーザー メールボックスを選択します。詳細ウィンドウの **\[インプレース アーカイブ\]** で、**\[有効\]** に設定されていることを確認します。**\[詳細の表示\]** をクリックすると、アーカイブの状態と作成されたメールボックス データベースを含めた、アーカイブのプロパティが表示されます。

  - シェルで、次のコマンドを実行して、新しいユーザー メールボックスとアーカイブについての情報を表示します。
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress,*Archive*

  - シェルで **Test-ArchiveConnectivity** コマンドレットを使用して、アーカイブへの接続をテストします。アーカイブ接続をテストする方法の例は、「[Test-ArchiveConnectivity](https://technet.microsoft.com/ja-jp/library/hh529914\(v=exchg.150\))」の「例」セクションを参照してください。

## 既存のメールボックスに対して社内アーカイブを有効にする

メールボックスを持っているがアーカイブを有効にしていない既存のユーザーに対してアーカーブを作成することもできます。これを既存のユーザーに対する*アーカイブの有効化*といいます。

## EAC を使用する

1.  **\[受信者\]** \> **\[メールボックス\]** に移動します。

2.  メールボックスを選択します。

3.  詳細ウィンドウの **\[インプレース アーカイブ\]** で、**\[有効にする\]** をクリックします。
    

    > [!TIP]
    > Shift キーまたは Ctrl キーを使用して複数のメールボックスを選択して、アーカイブを一括して有効にすることもできます。複数のメールボックスを選択した後に、詳細ウィンドウで、<STRONG>[その他のオプション]</STRONG> をクリックします。次に、<STRONG>[アーカイブ]</STRONG> で <STRONG>[有効にする]</STRONG> をクリックします。



4.  **\[インプレース アーカイブの作成\]** ページで、**\[OK\]** をクリックして Exchange でアーカイブ用のデータベースが自動的に選択されるようにするか、**\[参照\]** をクリックしてデータベースを指定します。

## シェルを使用する

この例では、Tony Smith のメールボックスのアーカイブを有効にします。

    Enable-Mailbox "Tony Smith" -Archive

この例では、社内またはクラウドベースのアーカイブが有効化されておらず、名前の先頭に DiscoverySearchMailbox が付いていないデータベース DB01 内のメールボックスを取得します。**Enable-Mailbox** コマンドレットに結果をパイプして、メールボックス データベース DB01 のすべてのメールボックスに対してアーカイブを有効にします。

    Get-Mailbox -Database DB01 -Filter {ArchiveGuid -Eq $null -AND ArchiveDomain -eq $null -AND Name -NotLike "DiscoverySearchMailbox*"} | Enable-Mailbox -Archive

構文およびパラメーターの詳細については、「[Enable-Mailbox](https://technet.microsoft.com/ja-jp/library/aa998251\(v=exchg.150\))」と「[Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

既存のメールボックスに対して社内アーカイブが正常に有効になったことを確認するには、次の手順のいずれかを実行します。

  - EAC で、**\[受信者\]** \> **\[メールボックス\]**に移動して、一覧からメールボックスを選択します。詳細ウィンドウの **\[インプレース アーカイブ\]** で、**\[有効\]** に設定されていることを確認します。**\[詳細の表示\]** をクリックすると、アーカイブの状態と作成されたメールボックス データベースを含めた、アーカイブのプロパティが表示されます。

  - シェルで、次のコマンドを実行して、新しいアーカイブについての情報を表示します。
    
        Get-Mailbox <Name> | FL Name,*Archive*

  - シェルで **Test-ArchiveConnectivity** コマンドレットを使用して、アーカイブへの接続をテストします。アーカイブ接続をテストする方法の例は、「[Test-ArchiveConnectivity](https://technet.microsoft.com/ja-jp/library/hh529914\(v=exchg.150\))」の例を参照してください。

## 社内アーカイブを無効にする

トラブルシューティングの目的で、ユーザーのアーカイブを無効にしたい場合や、インプレース アーカイブをサポートしないバージョンの Exchange にメールボックスを移動したい場合があります。社内アーカイブを無効にしても、メールボックスの保持期間が経過して社内アーカイブが完全に削除されるまで、アーカイブ内の全情報はメールボックス データベース内に保持されます。(既定では、Exchange は、アーカイブ メールボックスに含まれる切断されたメールボックスを 30 日間保持します)。


> [!IMPORTANT]
> アーカイブを無効にすると、メールボックスからアーカイブが削除され、そのアーカイブはメールボックス データベース内で削除対象としてマークされます。



社内アーカイブをそのメールボックスに再接続する場合は、*Archive* パラメーターと共に [Connect-Mailbox](https://technet.microsoft.com/ja-jp/library/aa997878\(v=exchg.150\)) コマンドレットを指定します。

## EAC を使用する

1.  **\[受信者\]** \> **\[メールボックス\]** に移動します。

2.  メールボックスを選択します。

3.  詳細ウィンドウの **\[インプレース アーカイブ\]** で、**\[無効にする\]** をクリックします。
    

    > [!TIP]
    > Shift キーまたは Ctrl キーを使用して複数のメールボックスを選択して、アーカイブを一括して無効にすることもできます。複数のメールボックスを選択した後に、詳細ウィンドウで、<STRONG>[その他のオプション]</STRONG> をクリックします。次に、<STRONG>[アーカイブ]</STRONG> で <STRONG>[無効にする]</STRONG> をクリックします。



## シェルを使用する

次の使用例は、Chris Ashton のメールボックス用のアーカイブを無効にします。これは、メールボックスを無効にしません。

    Disable-Mailbox -Identity "Chris Ashton" -Archive

構文およびパラメーターの詳細については、「[Disable-Mailbox](https://technet.microsoft.com/ja-jp/library/aa997210\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

アーカイブが正常に無効になったことを確認するには、次の手順を実行します。

  - EAC で、メールボックスを選択します。次に、詳細ウィンドウの **\[インプレース アーカイブ\]** で、そのアーカイブの状態を確認します。

  - シェルで、次のコマンドを実行して、メールボックス ユーザーのアーカイブ プロパティを確認します。
    
        Get-Mailbox -Identity "Chris Ashton" | Format-List *Archive*
    
    アーカイブが無効になると、アーカイブ関連プロパティに次の値が返されます。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>プロパティ</th>
    <th>値</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>ArchiveDatabase (社内アーカイブの場合)</p></td>
    <td><p>&lt;空&gt;</p></td>
    </tr>
    <tr class="even">
    <td><p>ArchiveState</p></td>
    <td><p><code>None</code></p></td>
    </tr>
    <tr class="odd">
    <td><p>DisabledArchiveDatabase (社内アーカイブの場合)</p></td>
    <td><p>&lt;メールボックス データベースの名前&gt;</p></td>
    </tr>
    <tr class="even">
    <td><p>DisabledArchiveGuid</p></td>
    <td><p>&lt;無効なアーカイブの GUID&gt;</p></td>
    </tr>
    </tbody>
    </table>


## 社内アーカイブを接続する

アーカイブ メールボックスを無効にすると、このメールボックスは切断されます。切断されたアーカイブメール ボックスは、指定された期間中、メールボックス データベースに保持されます。既定では、Exchange は、切断されたアーカイブを 30 日間保持します。この期間中に、アーカイブは、既存のメールボックスと関連付けることにより、回復することができます。削除済みメールボックスの保持期間を変更して、削除済みメールボックスまたはアーカイブの保持期間をより長くまたはより短くすることができます。


> [!NOTE]
> ユーザーのアーカイブを無効にしてから、このユーザーのアーカイブを有効にすると、このユーザーは新しいアーカイブを取得することになります。新しいアーカイブには、ユーザーの切断されたアーカイブ内に保存されていたデータが含まれなくなります。切断されたユーザーのアーカイブにユーザーを再接続する場合は、この手順を実行する必要があります。




> [!NOTE]
> 切断されたアーカイブをメールボックス ユーザーに接続する場合、EAC を使用することはできません。



## シェルを使用する

1.  アーカイブの名前がわからない場合は、次のコマンドを実行してシェルで名前を表示できます。この例では、メールボックス データベース DB01 を取得して **Get-MailboxStatistics** コマンドレットにパイプ処理し、データベース上のすべてのメールボックスのメールボックス統計を取得します。次に、**Where-Object** コマンドレットを使用して、結果をフィルター処理し、切断されたアーカイブの一覧を取得します。このコマンドを実行すると、GUID やアイテム数などの各アーカイブについての追加情報が表示されます。
    
        Get-MailboxDatabase "DB01" | Get-MailboxStatistics | Where {($_.DisconnectDate -ne $null) -and ($_.IsArchiveMailbox -eq $true)} | Format-List

2.  アーカイブをプライマリ メールボックスに接続します。この例では、Chris Ashton のアーカイブを Chris Ashton のプライマリ メールボックスに接続して、アーカイブの ID として GUID を使用します。
    
        Enable-Mailbox -ArchiveGuid "8734c04e-981e-4ccf-a547-1c1ac7ebf3e2" -ArchiveDatabase "DB01" -Identity "Chris Ashton"

構文およびパラメーターの詳細については、以下のトピックを参照してください。

  - [Get-MailboxDatabase](https://technet.microsoft.com/ja-jp/library/bb124924\(v=exchg.150\))

  - [Get-MailboxStatistics](https://technet.microsoft.com/ja-jp/library/bb124612\(v=exchg.150\))

  - [Enable-Mailbox](https://technet.microsoft.com/ja-jp/library/aa998251\(v=exchg.150\))

## 正常な動作を確認する方法

切断したアーカイブがメールボックス ユーザーに正常に接続されたことを確認するには、次のシェル コマンドを実行して、メールボックス ユーザーのアーカイブ プロパティを取得して、*ArchiveGuid* および *ArchiveDatabase* プロパティに返された値を確認します。

    Get-Mailbox -Identity "Chris Ashton" | Format-List *Archive*

