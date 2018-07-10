---
title: 'メールボックスでフォレスト間の移動要求の準備を行う: Exchange 2013 Help'
TOCTitle: メールボックスでフォレスト間の移動要求の準備を行う
ms:assetid: fdbed4fc-a77e-40d5-a211-863b05d74784
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee633491(v=EXCHG.150)
ms:contentKeyID: 49896569
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# メールボックスでフォレスト間の移動要求の準備を行う

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2017-11-22_

**概要:**  Exchange 2013でフォレスト間の移動用のメールボックスを準備する方法について説明します。

メールボックスを移動し、Exchange 管理シェルを使用して、移行をサポートしている Microsoft Exchange 2013**New-MoveRequest**と**New-MigrationBatch**のコマンドレットでは具体的には。Exchange 管理センター (EAC) 経由でメールボックスを移動することもできます。2013 の Exchange フォレストに Exchange 2010 と Exchange 2013 メールボックスを移動することに注意してください。

ExchangeのフォレストとExchange 2013フォレストにメールボックスを移動するにExchange 2013の移動先のフォレストは、 Active Directory属性の指定されたセットを使用して有効なメールが有効なユーザーを含める必要があります。少なくとも 1 つのExchange 2013クライアント アクセス サーバーがフォレストに展開する場合は、フォレストは、 Exchange 2013のフォレストと見なされます。

メールボックス移動を準備するには、移動先フォレストに必要な属性を持つ、メールが有効なユーザーを作成する必要があります。必要な属性を持つ、メールが有効なユーザーを作成するには、次の 2 つ方法が推奨されます。

  - フォレスト間のグローバル アドレス一覧 (GAL) 同期用に Microsoft Identity Lifecycle Manager (ILM) を展開した場合、メールが有効なユーザーを作成するための推奨される方法は、ILM 2007 Feature Pack 1 (FP1) のService Pack 1 (SP1) を使用することです。ILM をカスタマイズして移動元メールボックス ユーザーと移動先メール ユーザーを同期する方法の学習に使用できるサンプル コードが用意されています。
    
    サンプル コードをダウンロードする方法など、詳細については、「[サンプル コードを使用してフォレスト間のメールボックス移動を準備する](prepare-mailboxes-for-cross-forest-moves-using-sample-code-exchange-2013-help.md)」を参照してください。

  - ILM/MIIS 以外の Active Directory ツールを使用して移動先メール ユーザーを作成した場合、*Identity* パラメーターを指定して **Update-Recipient** コマンドレットを使用し、移動先メール ユーザー用の **LegacyExchangeDN** を作成するアドレス一覧サービスを実行します。Active Directory の読み取りおよび書き込みと、**Update-Recipient** コマンドレットを呼び出すサンプルの Windows PowerShell スクリプトが用意されています。
    
    サンプル スクリプトの使用の詳細については、「[シェルの Prepare-MoveRequest.ps1 スクリプトを使用して、フォレスト間のメールボックスの移動を準備する](prepare-mailboxes-for-cross-forest-moves-using-the-prepare-moverequest-ps1-script-in-the-shell-exchange-2013-help.md)」を参照してください。

移動先メール ユーザーを作成した後、**New-MoveRequest** または **New-MigrationBatch** コマンドレットを実行して、メールボックスを移動先 Exchange 2013 フォレストに移動できます。

リモート移動要求の詳細については、以下のトピックを参照してください。

  - [New-MigrationBatch](https://technet.microsoft.com/ja-jp/library/jj219166\(v=exchg.150\))

  - [New-MoveRequest](https://technet.microsoft.com/ja-jp/library/dd351123\(v=exchg.150\))

リモートのメールボックス移動とリモートの従来のメールボックス移動の詳細については、「[Exchange 2013 でのメールボックスの移動](mailbox-moves-in-exchange-2013-exchange-2013-help.md)」を参照してください。

ここからは、メールボックス移動に必要な Active Directory メール ユーザーの属性を説明します。これらの属性は、メールボックス移動を準備するコードまたはスクリプトのいずれかを使用する場合に構成されます。ただし、Active Directory エディターを使用して、これらの属性を手動でコピーできます。

## メールボックス移動に必要な Active Directory ユーザー属性

リモート メールボックス移動をサポートするために、移動先 Exchange 2013 フォレストのメール ユーザー オブジェクトはこのセクションで説明した Active Directory 属性を持つ必要があります。

  - 必須の属性

  - 省略可能な属性

  - リンクされた属性

  - リンクされたユーザー属性

  - リソース メールボックスの属性

  - 追加の属性

## 必須の属性

次の表は、**New-MoveRequest** コマンドレットが正常に機能するために、移動先メール ユーザーの ILM で構成される必要のある属性の最低限のセットを示しています。

### メール ユーザーの属性

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>メール ユーザーの Active Directory 属性</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>displayName</strong></p></td>
<td><p>移動元メールボックスの対応する属性をコピーする、または新しい値を生成します。</p></td>
</tr>
<tr class="even">
<td><p><strong>Mail</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>mailNickname</strong></p></td>
<td><p>移動元メールボックスの対応する属性をコピーする、または新しい値を生成します。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchArchiveGUID and msExchArchiveName</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。属性は、移動元メールボックスが Exchange 2010 である場合のみ使用可能です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMailboxGUID</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchRecipientDisplayType</strong></p></td>
<td><p>-2147483642 (10 進数)//0x80000006 (16 進数) と同等。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchRecipientTypeDetails</strong></p></td>
<td><p>128 (10 進数) /0x80 (16 進数)。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchUserCulture</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchVersion</strong></p></td>
<td><p>44220983382016 (10 進数)。</p></td>
</tr>
<tr class="even">
<td><p><strong>cn</strong></p></td>
<td><p>移動元メールボックスの対応する属性をコピーする、または新しい値を生成します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>proxyAddresses</strong></p></td>
<td><p>移動元メールボックスの <strong>proxyAddresses</strong> 属性をコピーします。さらに、移動元メールボックスの <strong>LegacyExchangeDN</strong> を X500 アドレスとして、移動先メール ユーザーの <strong>proxyAddresses</strong> 属性にコピーします。</p>

> [!NOTE]
> 移動元メールボックス ユーザーの <STRONG>proxyAddresses</STRONG> には、移動先フォレストの権限を持つドメインと一致する SMTP アドレスが含まれる必要があります。これにより <STRONG>New-MoveRequest</STRONG> コマンドレットは、移動元のメールが有効なユーザー (メールボックス移動要求の完了後、移動元メールボックス ユーザーから変換された) の <STRONG>targetAddress</STRONG> を正しく選択し、メールのルーティングが機能し続けるようにすることができます。


</td>
</tr>
<tr class="even">
<td><p><strong>sAMAccountName</strong></p></td>
<td><p>移動元メールボックスの対応する属性をコピーする、または新しい値を生成します。</p>
<p>移動先メール ユーザーが属する移動先フォレスト ドメイン内で値が一意であることを確認します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>targetAddress</strong></p></td>
<td><p>移動元メールボックスの <strong>proxyAddresses</strong> 属性の SMTP アドレスに設定します。</p>
<p>この SMTP アドレスは移動元フォレストの権限のあるドメインに属している必要があります。</p></td>
</tr>
<tr class="even">
<td><p><strong>userAccountControl</strong></p></td>
<td><p>定数：514 //0x202 と同等、ACCOUNTDISABLE | NORMAL_ACCOUNT。</p></td>
</tr>
<tr class="odd">
<td><p><strong>userPrincipalName</strong></p></td>
<td><p>移動元メールボックスの対応する属性をコピーする、または新しい値を生成します。メール ユーザーのログオンが無効になっているため、この <strong>userPrincipalName</strong> は使用されません。</p></td>
</tr>
</tbody>
</table>


## 省略可能な属性

**New-MoveRequest** コマンドレットが正常に機能するのに、次の属性の構成は必須ではありません。ただし、これらを同期することにより、メールボックスの移動後は、エンド ツー エンドのユーザー エクスペリエンスが向上されます。移動先フォレストの GAL はこの移動先メール ユーザーを表示するため、次の GAL 関連の属性を設定する必要があります。

### GAL 関連の属性

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>メール ユーザーの Active Directory 属性</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>c</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>co</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>countryCode</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>company</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>department</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>facsimileTelephoneNumber</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>givenName</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>homePhone</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>info</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>initials</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>l</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>mobile</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchAssistantName</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchHideFromAddressLists</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>otherHomePhone</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>otherTelephone</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>pager</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>physicalDeliveryOfficeName</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>postalCode</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>sn</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>st</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>streetAddress</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>telephoneAssistant</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>telephoneNumber</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>title</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
</tbody>
</table>


## リンクされた属性

リンクされた属性は、ローカル フォレスト内の他の Active Directory オブジェクトを参照する Active Directory 属性です。リンクされた属性は、移動元フォレストのメールボックスから移動先フォレストのメール ユーザーに直接コピーできません。最初に、移動元メールボックスの属性が参照する移動元フォレスト内で Active Directory オブジェクトを検索する必要があります。次に、上記の移動元フォレスト内の Active Directory オブジェクトに対し、移動先フォレスト内で対応する Active Directory オブジェクトを検索します。最後に、移動先フォレスト内の Active Directory オブジェクトを参照する移動先メール ユーザーの属性を設定します。

### リンクされた属性

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>メール ユーザーの Active Directory 属性</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>altRecipient</strong></p></td>
<td><p>移動元メールボックスの <strong>altRecipient</strong> 属性に対応しています。</p></td>
</tr>
<tr class="even">
<td><p><strong>deliverAndRedirect</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。この属性は <strong>altRecipient</strong> と共に設定する必要のあるブール値です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Manager</strong> (およびそのバックリンク)</p></td>
<td><p>移動元メールボックスの altRecipient 属性に対応しています。</p></td>
</tr>
<tr class="even">
<td><p><strong>MemberOf</strong> (バックリンク)</p></td>
<td><p>これは、グループ メンバー属性のバックリンクです。</p></td>
</tr>
<tr class="odd">
<td><p><strong>publicDelegates</strong> (とそのバックリンク)</p></td>
<td><p>移動元メールボックスの <strong>publicDelegates</strong> 属性に対応しています。</p></td>
</tr>
</tbody>
</table>


## リンクされたユーザー属性

メールボックスを Exchange 2013 リソース フォレストに移動する場合、リソース フォレスト内のメールボックスは *リンクされたメールボックス* と見なされます。このシナリオでは、リンクされたメール ユーザーを (移動先) リソース フォレストに作成する必要があります。リンクされたメール ユーザーを作成するには、次の表に示す属性を設定する必要があります。

### リンクされたメール ユーザー属性

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>メール ユーザーの Active Directory 属性</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>msExchMasterAccountHistory</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMasterAccountSid</strong></p></td>
<td><p>移動元メールボックスに <strong>msExchMasterAccountSid</strong> がある場合は、それをコピーします。ない場合は、移動元メールボックスの <strong>objectSid</strong> をコピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchRecipientDisplayType</strong></p></td>
<td><p>定数:-1073741818 (10 進数) // * 符号なし * 0xC0000006 と同等。</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> 移動元フォレストと移動先フォレストの間にフォレストの信頼がある場合にのみ、リンクされたメールボックスを作成することができます。



移動元オブジェクトが無効で **msExchMasterAccountSid** 属性が self (リソース メールボックス、共有メールボックス) に設定されている場合、移動先ユーザーに何もスタンプしないでください。

移動元オブジェクトが無効で **msExchMasterAccountSid** 属性が設定されていない場合、このメールボックスは無効です。

移動元オブジェクトが有効で **msExchMasterAccountSid** 属性が設定されている場合、このメールボックスは無効です。

## リソース メールボックスの属性

リソース メールボックスを Exchange 2013 フォレストに移動する場合、次の表に示す属性を移動先メール ユーザーに設定する必要があります。

### リソース メールボックスの属性

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>メール ユーザーの Active Directory 属性</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>msExchRecipientDisplayType</strong></p></td>
<td><p>移動元メールボックスが会議室の場合:</p>
<ul>
<li><p><strong>定数</strong>   -2147481850 (10 進数)// * 符号なし * 0x80000706 と同等。</p></li>
</ul>
<p>移動元メールボックスが備品用メールボックスの場合:</p>
<ul>
<li><p><strong>定数</strong>   -2147481594 (10 進数)// * 符号なし * 0x80000806 と同等。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>msExchResourceCapacity</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchResourceDisplay</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchResourceMetaData</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchResourceSearchProperties</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
</tbody>
</table>


## 追加の属性

Exchange 2007 で、メールボックスの移動時に、**Move-Mailbox** コマンドレットは次の表に示した属性もコピーします。組織で必要な場合は、必要に応じてこれらの属性をコピーできます。

### リソース メールボックスの属性

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>メール ユーザーの Active Directory 属性</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>comment</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>deletedItemFlags</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>delivContLength</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>departmentNumber</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>description</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>division</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>employeeID</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>employeeNumber</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>employeeType</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>extensionAttribute1-15</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>homePostalAddress</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>internationalISDNNumber</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ipPhone</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>language</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>lmPwdHistory</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>localeID</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>mAPIRecipient</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>middleName</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msDS-PhoneticCompanyName</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>msDS-PhoneticDepartment</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msDS-PhoneticDisplayName</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>msDS-PhoneticFirstName</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msDS-PhoneticLastName</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchBlockedSendersHash</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchELCExpirySuspensionEnd</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchELCExpirySuspensionStart</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchELCMailboxFlags</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchExternalOOFOptions</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMessageHygieneFlags</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMessageHygieneSCLDeleteThreshold</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMessageHygieneSCLJunkThreshold</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMessageHygieneSCLQuarantineThreshold</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMessageHygieneSCLRejectThreshold</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMDBRulesQuota</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchPoliciesExcluded</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchSafeRecipientsHash</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchSafeSendersHash</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchUMSpokenName</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>otherFacsimileTelephoneNumber</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>otherIpPhone</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>otherMobile</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>otherPager</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>preferredDeliveryMethod</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>personalPager</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>personalTitle</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>photo</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>pOPCharacterSet</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>pOPContentFormat</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>postalAddress</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>postOfficeBox</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>primaryInternationalISDNNumber</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>primaryTelexNumber</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>showInAdvancedViewOnly</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>street</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>terminalServer</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>textEncodedORAddress</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>thumbnailLogo</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>thumbnailPhoto</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>url</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>userCert</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>userCertificate</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="even">
<td><p><strong>userSMIMECertificate</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>wWWHomePage</strong></p></td>
<td><p>移動元メールボックスの対応する属性を直接コピーします。</p></td>
</tr>
</tbody>
</table>

