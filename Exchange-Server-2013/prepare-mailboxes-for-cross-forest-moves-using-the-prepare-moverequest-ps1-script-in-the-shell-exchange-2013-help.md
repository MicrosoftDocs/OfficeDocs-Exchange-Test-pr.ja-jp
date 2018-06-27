---
title: 'シェルの Prepare-MoveRequest.ps1 スクリプトを使用して、フォレスト間のメールボックスの移動を準備する: Exchange 2013 Help'
TOCTitle: シェルの Prepare-MoveRequest.ps1 スクリプトを使用して、フォレスト間のメールボックスの移動を準備する
ms:assetid: 2cea59fb-69b7-4a2f-833f-de4d93cf1810
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee861103(v=EXCHG.150)
ms:contentKeyID: 49895318
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# シェルの Prepare-MoveRequest.ps1 スクリプトを使用して、フォレスト間のメールボックスの移動を準備する

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2017-11-22_

**概要:** Exchange 管理シェルの準備-MoveRequest.ps1 スクリプトを使用してフォレスト間のメールボックスの移動とExchange 2013での移行を管理する方法について説明します。

マイクロソフトのExchange 2013には、メールボックスを移動し、 **New-MoveRequest** 、 **New-MigrationBatch**コマンドレットを使用して、移行がサポートされています。Exchange 管理センター (EAC) 経由でメールボックスを移動することもできます。Exchange 2013ターゲット フォレストに、 Exchangeのソース フォレストから、Exchange 2010 または Exchange 2013 メールボックスを移動できます。

**New-MoveRequest** コマンドレットと **New-MigrationBatch** コマンドレットを実行するには、メール ユーザーが移動先 Exchange フォレストに存在し、最低限必要な Active Directory 属性の集合が設定されている必要があります。

ここで説明するサンプルの Windows PowerShell スクリプトは、メールボックスのユーザーを Exchange 2013 の移動元のフォレストから Exchange 2013 の移動先のフォレストにメールが有効なユーザーとして同期させることで、このタスクをサポートしています。スクリプトは移動元フォレストのメールボックス ユーザーの Active Directory 属性を移動先フォレストにコピーし、**Update-Recipient** コマンドレットを使用して、移動先のオブジェクトをメールが有効なユーザーに変換します。

スクリプトの使用と記述の詳細については、「 [Exchange 管理シェルを使用したスクリプトの作成](https://technet.microsoft.com/ja-jp/library/bb123798\(v=exchg.150\))」を参照してください。フォレスト間の移動の準備については、「[メールボックスでフォレスト間の移動要求の準備を行う](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)」を参照してください。

リモート移動要求に関連する他の管理タスクについては、「[社内の移動の管理](manage-on-premises-moves-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 次の場所でスクリプトを見つけます。Program Files\\Microsoft\\Exchange Server\\V15\\Scripts

  - サンプル スクリプトの実行に必要なものを以下に示します。
    
      - Exchange元のフォレスト、現在のメールボックスが存在します。Exchange 2010 または Exchange 2013 メールボックスを指定できます。
    
      - メールボックスの移動先となる、Exchange 2013 がインストールされた移動先のフォレスト。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## Prepare-MoveRequest.ps1 スクリプトを使用してメールボックスのフォレスト間の移動を準備する

移動先の Exchange 2013 フォレストにおいて、Exchange 2013 を実行しているサーバーの役割上でシェルからスクリプトを実行します。スクリプトによって移動元のフォレストからメールボックスの属性がコピーされます。

特定の認証資格情報をリモート フォレストのドメイン コントローラーに割り当てるには、まず Windows PowerShell **Get-Credential** コマンドレットを実行して、ユーザー入力を一時変数に保存します。**Get-Credential** コマンドレットを実行すると、リモート フォレストのドメイン コントローラーの電子メール サーバーの認証時に使用されるアカウントのユーザー名とパスワードの入力が求められます。Prepare-MoveRequest.ps1 スクリプトでは、テンポラリ変数を使用します。**Get-Credential** コマンドレットの詳細については、「[Get-Credential](https://go.microsoft.com/fwlink/p/?linkid=142122)」を参照してください。


> [!NOTE]
> このスクリプトを呼び出すときは、ローカル フォレストとリモート フォレストに対して 2 つの別の資格情報を使用することを確認してください。



1.  次のコマンドを実行して、ローカル フォレストとリモート フォレストの資格情報を取得します。
    
        $LocalCredentials = Get-Credential
        $RemoteCredentials = Get-Credential

2.  以下のコマンドを実行して、Prepare-MoveRequest.ps1 スクリプトの *LocalForestCredential* パラメーターと *RemoteForestCredential* パラメーターに資格情報を渡します。
    
        Prepare-MoveRequest.ps1 -Identity JohnSmith@Fabrikan.com -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $RemoteCredentials -LocalForestDomainController DC001.Contoso.com -LocalForestCredential $LocalCredentials

## スクリプトのパラメーター セット

次の表は、スクリプトのパラメーター セットの説明です。

### Prepare-MoveRequest.ps1 スクリプトのパラメーター セット

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>必須</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p><em>Identity</em> パラメーターは、移動元フォレストのメールボックスを一意に識別します。Identity には次のいずれかを指定できます。</p>
<ul>
<li><p>共通名 (CN)</p></li>
<li><p>Alias</p></li>
<li><p><strong>proxyAddress</strong> プロパティ</p></li>
<li><p><strong>objectGuid</strong> プロパティ</p></li>
<li><p><strong>DisplayName</strong> プロパティ</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>RemoteForestCredential</em></p></td>
<td><p>必要</p></td>
<td><p><em>RemoteForestCredential</em> パラメーターには、移動元フォレスト Active Directory からデータをコピーするアクセス許可を持つ管理者を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><em>RemoteForestDomainController</em></p></td>
<td><p>必要</p></td>
<td><p><em>RemoteForestDomainController</em> パラメーターには、メールボックスが存在する移動元フォレストのドメイン コントローラーを指定します。</p></td>
</tr>
<tr class="even">
<td><p><em>DisableEmailAddressPolicy</em></p></td>
<td><p>省略可能</p></td>
<td><p><em>DisableEmailAddressPolicy</em> パラメーターでは、移動先フォレストで <strong>MailUser</strong> オブジェクトを作成するときに電子メール アドレス ポリシー (EAP) を無効にするかどうかを指定します。</p>
<p>このパラメーターを指定すると、移動先フォレストの EAP は適用されません。</p>

> [!NOTE]
> このパラメーターを指定すると、<STRONG>MailUser</STRONG> オブジェクトはスタンプされたローカル フォレスト ドメインに電子メール アドレス マッピングを持ちません。これは通常 EAP によってスタンプされます。


</td>
</tr>
<tr class="odd">
<td><p><em>LinkedMailUser</em></p></td>
<td><p>省略可能</p></td>
<td><p><em>LinkedMailUser</em> スイッチには、リモート フォレストのメールボックス ユーザー用に、リンクした MailUser を ローカル フォレストに作成するかどうかを指定します。</p>
<p>スイッチが入力されると、スクリプトは移動元のメールボックスにリンクした移動先の <strong>MailUser</strong> オブジェクトを作成します。スイッチが省略されると、スクリプトは通常の移動先の <strong>MailUser</strong> オブジェクトを作成します。</p></td>
</tr>
<tr class="even">
<td><p><em>LocalForestCredential</em></p></td>
<td><p>省略可能</p></td>
<td><p><em>LocalForestCredential</em> パラメーターには、移動先フォレスト Active Directory に対して書き込みのアクセス許可を持つ管理者を指定します。</p>
<p>Active Directory のアクセス許可の問題を回避するために、このパラメーターを明示的に指定することをお勧めします。</p>
<p>リモート フォレストとローカル フォレストに信頼関係が構成されている場合、リモート ユーザー アカウントがローカル フォレストの Active Directory を変更するアクセス許可を有している場合であっても、リモート フォレストのユーザー アカウントをローカル フォレストの資格情報として使用しないでください。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalForestDomainController</em></p></td>
<td><p>省略可能</p></td>
<td><p><em>LocalForestDomainController</em> パラメーターには、メールが有効なユーザーを作成する、移動先フォレストのドメイン コントローラーを指定します。</p>
<p>ランダム ドメイン コントローラーが選択された場合に起こりうる、ローカル フォレストのドメイン コントローラーの複製遅延の問題を回避するために、このパラメーターを指定することをお勧めします。</p></td>
</tr>
<tr class="even">
<td><p><em>MailboxDeliveryDomain</em></p></td>
<td><p>省略可能</p></td>
<td><p><em>MailboxDeliveryDomain</em> パラメーターには、移動元のフォレストの権限を持つドメインを指定して、スクリプトが移動元のメールボックス ユーザーの <strong>proxyAddress</strong> プロパティを、移動先のメールが有効なユーザーの <strong>targetAddress</strong> プロパティとして正しく選択できるようにします。</p>
<p>既定では、移動元メールボックス ユーザーのプライマリ SMTP アドレスは、移動先のメールが有効なユーザーの <strong>targetAddress</strong> プロパティとして設定されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>OverWriteLocalObject</em></p></td>
<td><p>省略可能</p></td>
<td><p><em>OverWriteLocalObject</em> パラメーターは、Active Directory 移行ツールで作成されたユーザー用に使用します。プロパティは、既存のメール連絡先から新たに作成されたメール ユーザーにコピーされます。ただし、このコピーの後、スクリプトによって、移動元フォレスト ユーザーからも新たに作成されたメール ユーザーにプロパティがコピーされます。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetMailUserOU</em></p></td>
<td><p>省略可能</p></td>
<td><p><em>TargetMailuserOU</em> パラメーターには、移動先のメールが有効なユーザーの作成先の組織単位 (OU) を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><em>UseLocalObject</em></p></td>
<td><p>省略可能</p></td>
<td><p><em>UseLocalObject</em> パラメーターには、作成予定のメールが有効なユーザーと競合するローカル フォレストのオブジェクトが検出された場合に、既存のローカル オブジェクトを要求された移動先のメールが有効なユーザーに変換するかどうかを指定します。</p></td>
</tr>
</tbody>
</table>


## 例

このセクションには、Prepare-MoveRequest.ps1 スクリプトの使用方法の例がいくつか含まれています。

## 例: 1 名のリンクされたメールが有効なユーザー

この例では、リモート フォレストとローカル フォレストの間に信頼関係がある場合に、1 名のリンクされたメールが有効なユーザーをローカル フォレストに準備します。

1.  次のコマンドを実行して、ローカル フォレストとリモート フォレストの資格情報を取得します。
    
        $LocalCredentials = Get-Credential
        $RemoteCredentials = Get-Credential

2.  次のコマンドを実行して、Prepare-MoveRequest.ps1 スクリプトの *LocalForestCredential* パラメーターと *RemoteForestCredential* パラメーターに資格情報を渡します。
    
        Prepare-MoveRequest.ps1 -Identity JamesAlvord@Contoso.com -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $RemoteCredentials -LocalForestDomainController DC001.Contoso.com -LocalForestCredential $LocalCredentials -LinkedMailUser 

## 例: パイプライン処理

メールボックスの ID の一覧を指定すると、この例はパイプライン処理をサポートします。

1.  次のコマンドを実行します。
    
        $UserCredentials = Get-Credential

2.  次のコマンドを実行して、資格情報を Prepare-MoveRequest.ps1 スクリプト内の *RemoteForestCredential* パラメーターに渡します。
    
        "IanP@Contoso.com", "JoeAn@Contoso.com" | Prepare-MoveRequest.ps1 -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $UserCredentials

## 例: .csv ファイルを使用してメールが有効なユーザーを一括作成する

メールボックス ID の一覧を含む .csv ファイルを移動元のフォレストから生成できます。それにより、このファイルの内容をスクリプトに入力して、移動先のメールが有効なユーザーを一括作成します。

たとえば, .csv ファイルの内容は次のようになります。

Identity

Ian@contoso.com

John@contoso.com

Cindy@contoso.com

この例では, .csv ファイルを呼び出して移動先にメールが有効なユーザーを一括作成します。

1.  次のコマンドを実行して、リモート フォレストの資格情報を取得します。
    
        $UserCredentials = Get-Credential

2.  次のコマンドを実行して、資格情報を Prepare-MoveRequest.ps1 スクリプト内の *RemoteForestCredential* パラメーターに渡します。
    
        Import-Csv Test.csv | Prepare-MoveRequest.ps1 -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $UserCredentials

## 移動先のオブジェクトごとのスクリプトの動作

ここでは、移動先オブジェクトのいくつかのシナリオに関連してスクリプトがどのように動作するかを説明します。

## 移動先のメールが有効なオブジェクトの重複

スクリプトが移動元のメールボックス ユーザーから移動先のメールが有効なユーザーを作成しようとして、ローカルのメールが有効なオブジェクトの重複を検出すると、以下のロジックを使用します。

  - 移動元のメールボックス ユーザーの **masterAccountSid** 属性が、移動先のオブジェクトのいずれかの **objectSid** 属性または **masterAccountSid** 属性に等しい場合。
    
      - 移動先のオブジェクトがメールが有効でない場合、スクリプトはメールが有効でないオブジェクトからメールが有効なユーザーへの変換をサポートしていないため、エラーを返します。
    
      - 移動先のオブジェクトがメールが有効な場合、移動先のオブジェクトは重複しています。

  - 移動元のメールボックス ユーザーの **proxyAddress** プロパティ (smtp/x500 のみ) が移動先のオブジェクトの **proxyAddress** プロパティ (smtp/x500 のみ) に等しい場合、移動先のオブジェクトは重複しています。

スクリプトは重複するオブジェクトについてユーザーに入力を求めます。

移動先のメールが有効なオブジェクトが、メールが有効なユーザーまたは連絡先の場合、フォレストにまたがる (Identity Lifecycle Management 2007 Service Pack 1 ベースの) グローバル アドレス一覧 (GAL) 同期展開によって作成された可能性が高いです。そして、ユーザーは移動先のメールが有効なオブジェクトをメールボックスの移行に使用するために、*UseLocalObject* パラメーターを指定してスクリプトを再度実行します。

## メールが有効なユーザー

移動先のオブジェクトがメールが有効なユーザーで、スクリプトによって移動元のメールボックス ユーザーから移動先のメールが有効なユーザーに以下の属性がコピーされます。

  - **msExchMailboxGUID**

  - **msExchArchiveGUID**

  - **msExchArchiveName**

*LinkedMailUser* パラメーターを設定すると、スクリプトは移動元の **objectSid**/**masterAccountSid** 属性をコピーします。

## メールが有効な連絡先

移動先のオブジェクトがメールが有効な連絡先の場合、スクリプトは既存の連絡先を削除して、そのすべての属性を新しいメールが有効なユーザーにコピーします。またスクリプトは次の属性を移動元のメールボックス ユーザーからコピーします。

  - **msExchMailboxGUID**

  - **msExchArchiveGUID**

  - **msExchArchiveName**

  - **sAMAccountName**

  - **userAccountControl** (514 に設定 //0x202 に相当、ACCOUNTDISABLE | NORMAL\_ACCOUNT)

  - **userPrincipalName**

*LinkedMailUser* パラメーターを設定すると、スクリプトは移動元の **objectSid**/**masterAccountSid** 属性をコピーします。

## LegacyExchangeDN 属性

移動先のオブジェクトをメールが有効なユーザーに変換するために **Update-Recipient** コマンドレットが呼ばれると、移動先のメールが有効なユーザーのために新しい **LegacyExchangeDN** 属性が生成されます。スクリプトは、移動先のメールが有効なユーザーの **LegacyExchangeDN** 属性を x500 アドレスとして、移動元のメールボックス ユーザーの **proxyAddress** プロパティにコピーします。

