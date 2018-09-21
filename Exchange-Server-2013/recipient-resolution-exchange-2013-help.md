﻿---
title: '受信者の解決: Exchange 2013 Help'
TOCTitle: 受信者の解決
ms:assetid: 09deda5a-d405-45b1-a3ff-fefd3d76cdea
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb430743(v=EXCHG.150)
ms:contentKeyID: 52057793
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 受信者の解決

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-03-17_

*受信者の解決*とは、メッセージ内のすべての受信者を展開して解決する処理です。受信者の解決では、受信者と Microsoft Exchange 組織内の対応する Active Directory オブジェクトを照合します。受信者の展開では、すべての配布グループを各受信者のリストに展開します。受信者の解決により、メッセージ制限と代替受信者を各受信者に正しく適用できるようになります。

Microsoft Exchange Server 2013 組織では、メールボックス サーバーのトランスポート サービスのカテゴライザーが受信者の解決を実行します。各メッセージの分類は、新着メッセージが送信キューに置かれた後で実行されます。メッセージが配信キューに置かれる前に、メッセージのコンテンツ変換およびルーティングに加えて受信者の解決が実行されます。受信者の解決はルーティングの前に実行されます。受信者の解決を実行するカテゴライザーのコンポーネントは、一般的に*リゾルバー*と呼ばれます。

**目次**

最上位の解決

展開

分割および受信者の展開の制御

受信者の解決の診断

## 最上位の解決

*最上位の解決*は、受信者の解決の第 1 段階です。最上位の解決では、受信メッセージ内の各受信者が Active Directory 内の対応する受信者オブジェクトに関連付けられます。最上位の解決の実行時に、カテゴライザーはメッセージ内に存在する送信者および元の未展開の受信者の電子メール アドレスを含む一覧を作成します。カテゴライザーは次に、この電子メール アドレスの一覧を使用して Active Directory に対してクエリを実行し、対応する電子メール アドレス属性を持つ、メールが有効なオブジェクトを検索します。対応するオブジェクトが見つかると、その Active Directory オブジェクトのプロパティを後で使用するためにキャッシュします。送信者に対するメッセージの制限も適用されます。

## 受信者の電子メール アドレス

最上位の解決では最初に、*メッセージ エンベロープ*からメッセージおよび元の未展開の受信者一覧が作成されます。メッセージ エンベロープには、SMTP メッセージング サーバー間でメッセージを送信するために使用されるコマンドが含まれています。送信者の電子メール アドレスは **MAIL FROM:**  コマンドに含まれています。各受信者の電子メール アドレスは、個別の **RCPT TO:**  コマンドに含まれています。エンベロープ送信者およびエンベロープ受信者は、通常、メッセージ ヘッダーの `To:`、`From:`、`Cc:`、および `Bcc:` ヘッダー フィールド内の送信者および受信者から作成されます。ただし、常にそうであるとは限りません。メッセージの `To:`、`From:`、`Cc:`、および `Bcc:` のヘッダー フィールドは容易に偽造することができ、メッセージ送信時に使用された実際の送信者または受信者の電子メール アドレスと一致しない場合があります。

## カプセル化された電子メール アドレス

標準の SMTP 電子メール アドレスは、RFC 2821 および RFC 2822 の仕様に従い、たとえば chris@contoso.com のようになります。ただし、電子メール アドレスは、有効な SMTP アドレス内にカプセル化された SMTP 以外の電子メール アドレスにすることもできます。Exchange では、IMCEA (Internet Mail Connector Encapsulated Address) のカプセル化手法を使用するカプセル化されたアドレスがサポートされます。

このカプセル化手法では、SMTP 電子メール アドレスでは無効な文字のエンコードが必要になります。英数字、等号記号 (=)、およびハイフン (-) はエンコードを必要としません。他の文字は、以下のエンコード構文を使用します。

  - スラッシュ (/) はアンダースコア (\_) に置き換えられます。

  - 他の US-ASCII 文字は、プラス記号 (+) と 16 進で記述された 2 桁の ASCII 値に置き換えられます。たとえば、スペース文字のエンコード値は `+20` です。

IMCEA カプセル化手法では、次の構文を使用します。`IMCEA<Type>-<address>@<domain>`

プレースホルダー \<*Type*\> は、SMTP 以外のアドレスの種類を識別します。たとえば、`EX`、`X400`、`FAX` などです。


> [!NOTE]
> <CODE>SMTP</CODE> と <CODE>X500</CODE> は理論的には &lt;<EM>Type</EM>&gt; の有効な値ですが、Exchange の受信者の解決では、これらの種類を使用する IMCEA でエンコードされたアドレスはすべて拒否されます。



プレースホルダー \<*address*\> は、エンコードされた元のアドレスです。プレースホルダー \<*domain*\> は、contoso.com など、SMTP 以外のアドレスをカプセル化するために使用される SMTP ドメインを表します。

IMCEA カプセル化手法では、ドメインが Exchange 組織の既定の承認済みドメインに一致する場合にのみ、アドレスのカプセル化が解除されます。承認済みドメインの詳細については、「[承認済みドメイン](accepted-domains-exchange-2013-help.md)」を参照してください。

Exchange での SMTP 電子メール アドレスの最大長は 571 文字です。この制限の内訳は次のとおりです。

  - アドレスの名前部分が 315 文字

  - ドメイン名が 255 文字

  - アドレスの名前部分とドメイン名を区切るアット マーク (@) 文字

なお、電子メール アドレス全体が 571 文字より短くても、アドレスの名前の部分が 315 文字を超えていると、Exchange では IMCEA カプセル化手法でエンコードされたメッセージがサポートされませんので注意してください。

## アドレス解決

メッセージごとに、送信者の電子メール アドレスおよびすべての受信者の電子メール アドレスは、Active Directory に対するクエリで使用される一覧に追加されます。カプセル化されたアドレスは、電子メール アドレスの一覧に追加される前にカプセル化が解除されます。Active Directory のクエリは、同時に最大 20 個の電子メール アドレスで実行されます。Active Directory のクエリで一時的なエラーが発生した場合、メッセージは送信キューに戻され、Microsoft Exchange トランスポート サービスに関連する `%ExchangeInstallPath%Bin\EdgeTransport.exe.config` XML アプリケーション構成ファイルの *ResolverRetryInterval* キーで指定されている時間分遅延されます。既定値は 30 分です。

次の表は、Active Directory 内の受信者オブジェクトを示しています。Exchange の受信者の種類の詳細については、「[受信者](recipients-exchange-2013-help.md)」を参照してください。

### Active Directory 内の受信者オブジェクト

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Active Directory の受信者の種類</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DistributionGroup</p></td>
<td><p>メールが有効なグループ オブジェクトです。配布グループ オブジェクトの種類は次のとおりです。</p>
<ul>
<li><p><strong>MailUniversalDistributionGroup</strong>   ユニバーサル配布グループ オブジェクト</p></li>
<li><p><strong>MailUniversalSecurityGroup</strong>   電子メール アドレスを持つユニバーサル セキュリティ グループ (USG) オブジェクト</p></li>
<li><p><strong>MailNonUniversalGroup</strong>   電子メール アドレスを持つローカル セキュリティ グループ オブジェクトまたはグローバル セキュリティ グループ オブジェクト</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>DynamicDistributionGroup</p></td>
<td><p>Active Directory クラス <strong>msExchDynamicDistributionList</strong> を持つオブジェクトです。詳細については、「<a href="https://docs.microsoft.com/ja-jp/exchange/recipients-in-exchange-online/manage-dynamic-distribution-groups/manage-dynamic-distribution-groups">動的配布グループの管理</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>Mailbox</p></td>
<td><p>電子メール アドレスおよび定義済みの <em>Database</em> パラメーターを持つユーザー オブジェクトです。</p></td>
</tr>
<tr class="even">
<td><p>MailUser</p></td>
<td><p>定義済みの <em>Database</em> パラメーターがない電子メール アドレスを持つユーザー オブジェクトです。詳細については、「<a href="https://docs.microsoft.com/ja-jp/exchange/recipients-in-exchange-online/manage-mail-users">メール ユーザーの管理</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>MailContact</p></td>
<td><p>電子メール アドレスを持つ連絡先オブジェクトです。通常、メール連絡先は Exchange 組織外の受信者に使用されます。また、メール連絡先はフォレスト間 Exchange 環境でも使用されます。詳細については、「<a href="https://docs.microsoft.com/ja-jp/exchange/recipients-in-exchange-online/manage-mail-contacts">メール連絡先の管理</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>MailPublicFolder</p></td>
<td><p>電子メール アドレスを持つパブリック フォルダー オブジェクトです。</p></td>
</tr>
<tr class="odd">
<td><p>MicrosoftExchangeRecipient</p></td>
<td><p>Active Directory クラス <strong>msExchExchangeServerRecipient</strong> を持つオブジェクトです。Microsoft Exchange 受信者オブジェクトの詳細については、「<a href="recipients-exchange-2013-help.md">受信者</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>SystemAttendantMailbox</p></td>
<td><p>Active Directory クラス <strong>exchangeAdminService</strong> を持つオブジェクトです。Exchange 組織には、システム アテンダント メールボックスが 1 つだけ存在します。</p></td>
</tr>
<tr class="odd">
<td><p>SystemMailbox</p></td>
<td><p>電子メール アドレスを持ち、Microsoft Exchange システム オブジェクト コンテナー内に配置されるユーザー オブジェクトです。Exchange 組織には、メールボックス データベースごとに 1 つのシステム メールボックスが存在します。</p></td>
</tr>
</tbody>
</table>


重要なプロパティが欠けているオブジェクト、または重要なプロパティの形式が正しくないオブジェクトは、Active Directory クエリによって無効なオブジェクトとして分類されます。たとえば、電子メール アドレスを持たない動的配布グループ オブジェクトは無効と見なされます。無効なオブジェクトとして分類される受信者にメッセージが送信されると、配信不能レポート (NDR) が生成されます。

電子メール アドレスごとに、受信者 ID、受信者の種類、メッセージの制限、電子メール アドレス、代替受信者など、可能性のあるすべての受信者プロパティを取得するための初期クエリが 1 回実行されます。該当する受信者のプロパティは、後で使用するためにキャッシュされます。受信者の解決では、受信者の解決方法の類似性、および該当する受信者プロパティの類似性に基づいて受信者が分類されます。

アドレス解決に使用される LDAP フィルターは次のとおりです。

  - 電子メール アドレスの種類が **EX** の場合、LDAP フィルターは、受信者の **legacyExchangeDN** Active Directory 属性、または受信者の **proxyAddresses** Active Directory 属性に基づきます。**legacyExchangeDN** Active Directory 属性が優先されます。

  - その他の電子メール アドレスの種類の場合はすべて、受信者の **proxyAddresses** Active Directory 属性が LDAP フィルターとして使用されます。

メッセージで使用されている電子メール アドレスが、対応する Active Directory オブジェクトのプライマリ SMTP アドレスと一致しない場合、カテゴライザーはメッセージの電子メール アドレスを書き換えてプライマリ SMTP アドレスと一致させます。元の電子メール アドレスは、メッセージ エンベロープの **RCPT TO:**  コマンドの `ORCPT=` エントリに保存されます。

## 送信者に対するメッセージ制限

送信者に対するメッセージ サイズの制限で使用されるサイズは、メッセージ ヘッダー内の **X-MS-Exchange-Organization-OriginalSize:**  ヘッダー フィールドの値です。Exchange は、メッセージが Exchange 組織に入ったときに、このヘッダー フィールドを使用して元のメッセージ サイズを記録します。指定したメッセージ サイズの制限に照らしてメッセージをチェックする場合、現在のメッセージ サイズと上記の元のメッセージ サイズ ヘッダーの値のうち小さい方の値が使用されます。コンテンツ変換、エンコード、およびエージェント処理のためにメッセージのサイズが変わる場合があります。このヘッダー フィールドが存在しない場合は、現在のメッセージ サイズの値を使用してこのフィールドが作成されます。メッセージが大きすぎる場合は NDR が生成され、以降のメッセージ処理は停止します。

送信者に対する受信者の制限は、メッセージを処理する最初のメールボックス サーバーのトランスポート サーバーでのみ適用されます。元の未展開のメッセージ エンベロープの受信者数が、送信者に対する受信者制限と比較されます。元の未展開のメッセージ エンベロープの受信者数は、入れ子になった配布リストがリモート展開サーバーを使用する場合に Microsoft Exchange Server 2003 で発生するメッセージの不完全配信の問題を回避するために使用されます。

メッセージの送信者およびすべての受信者は、メッセージに拡張プロパティをスタンプすることで、解決済みとしてマークされます。メッセージに対して再び受信者の解決を実行する必要がある場合、この拡張プロパティによって最上位の解決をバイパスできます。Microsoft Exchange Transport サービスが再起動されることによって、メッセージに対して再び受信者の解決を実行しなければならない場合があります。

ページのトップへ

## 展開

展開は、最上位の解決の後に実行されます。展開では、入れ子になった受信者が個々の受信者に完全に展開されます。すべての受信者を展開するには、展開処理を複数回行う必要がある場合があります。展開の必要がない受信者もありますが、展開処理はすべての受信者に対して実行する必要があります。また、展開処理では、すべての種類の受信者に対して、受信者に対するメッセージの制限が適用されます。

次の一覧は、展開を必要とする受信者の種類の説明です。

  - **配布グループおよび動的配布グループ**   配布グループは、**memberOf** Active Directory プロパティに基づいて展開されます。動的配布グループは、Active Directory クエリの定義を使用して展開されます。グループに対して *ExpansionServer* パラメーターが設定されている場合、そのグループは現在のサーバーでは展開されません。その配布グループは、展開のために指定されたサーバーにルーティングされます。
    

    > [!NOTE]
    > 展開サーバーとして組織内の特定のトランスポート サーバーを選択した場合は、配布グループの使用がその展開サーバーの可用性に依存するようになります。その展開サーバーが使用できなくなると、配布グループに送信されたメッセージがすべて配信されなくなります。配布グループ用に特定の展開サーバーを使用することを計画している場合は、サービス中断のリスクを軽減するために、これらのサーバーに高可用性ソリューションを実装することを検討してください。



  - **代替受信者** *ForwardingAddress* パラメーターがメールボックスおよびメールが有効なパブリック フォルダーに設定されている場合があります。*ForwardingAddress* パラメーターは、すべてのメッセージを指定された代替受信者にリダイレクトします。これは、*転送される受信者*と呼ばれます。*ForwardingAddress* パラメーターと *DeliverToMailboxAndForward* パラメーターが `$true` に設定されている場合、メッセージは元の受信者と代替受信者に配信されます。これは、*配信および転送される受信者*と呼ばれます。

  - **連絡先チェーン** *連絡先チェーン*とは、*ExternalEmailAddress* パラメーターが Exchange 組織内の別の受信者の電子メール アドレスに設定されているメール ユーザーまたはメール連絡先です。

## 受信者ループの検出

配布グループ、代替受信者、および連絡先チェーンが展開されるとき、カテゴライザーは*受信者ループ*をチェックします。受信者ループとは、同じ受信者に対するメッセージ配信が無限に繰り返されてしまう、受信者構成の問題です。次の一覧は、さまざまな種類の受信者ループの説明です。

  - **無害な受信者ループ**   無害な受信者ループの場合、メッセージは正常に配信されます。以下に、無害な受信者ループが発生する 2 つのシナリオを示します。
    
      - 2 つの配布グループに互いがメンバーとして含まれている場合。
    
      - メールボックスまたはメールが有効なパブリック フォルダーが、互いに対して配信および転送するように設定されている場合。これが発生するのは、両方の受信者の *DeliverToMailboxAndForward* パラメーターに `$true` が設定されており *ForwardingAddress* パラメーターに互いのアドレスが設定されている場合です。
    
    無害な受信者ループが検出されると、メッセージは受信者に配信されますが、同じ受信者にメッセージを配信するための以降の処理は行われません。

  - **壊れた受信者ループ**   壊れた受信者ループの場合、メッセージを正常に配信できません。壊れた受信者ループの例としては、メールボックスまたはメールが有効なパブリック フォルダーの *ForwardingAddress* パラメーターに互いのアドレスが設定されている場合が挙げられます。カテゴライザーによって壊れた受信者ループが検出された場合、現在の受信者に対する展開処理は停止され、受信者に対して NDR が生成されます。

受信者ループの検出によって、メッセージ配信の重複を防ぐことはできません。たとえば、次の条件が満たされる場合、配布グループ C ではメッセージ配信の重複が発生します。

  - 配布グループ B および配布グループ C は配布グループ A のメンバーである。

  - 配布グループ C は配布グループ B のメンバーでもある。

## 配布グループの配信レポートのリダイレクト

配布グループの展開時に、メッセージの種類が調べられ、配信レポート メッセージかどうかが判断されます。メッセージが配信レポートの場合は、配布グループのリダイレクトの設定が調べられ、配信レポートのリダイレクトが必要かどうかが判断されます。配信レポートは配布グループとそのメンバーシップに関する不要な情報を公開する場合があるため、配信レポートを抑制したほうがいい場合があります。

次の一覧は、配布グループおよび動的配布グループで使用できる配信レポートのリダイレクト設定の説明です。

  - **ReportToManagerEnabled**   このパラメーターは、配布グループの管理者に配信レポートを送信できるようにします。有効な値は `$true` または `$false` です。既定値は `$false` です。配布グループの場合、管理者は **Set-Group** コマンドレットの *ManagedBy* パラメーターによって制御されます。動的配布グループの場合、管理者は **Set-DynamicDistributionGroup** コマンドレットの *ManagedBy* パラメーターによって制御されます。

  - **ReportToOriginatorEnabled**   このパラメーターは、この配布グループに送信された電子メール メッセージの送信者に配信レポートを送信できるようにします。有効な値は `$true` または `$false` です。既定値は `$true` です。
    

    > [!NOTE]
    > <EM>ReportToManagerEnabled</EM> パラメーターおよび <EM>ReportToOriginatorEnabled</EM> パラメーターの値を両方とも <CODE>$true</CODE> にすることはできません。一方のパラメーターを <CODE>$true</CODE> に設定する場合は、他方を <CODE>$false</CODE> に設定する必要があります。両方のパラメーターの値を <CODE>$false</CODE> にすることは可能です。これにより、すべての配信レポート メッセージのすべてのリダイレクトが抑制されます。



以下に、使用可能な配信レポート メッセージの一覧を示します。

  - **配信レポート (DR)**   このレポートは、メッセージが目的の受信者に配信されたことを確認するためのものです。

  - **配信状態通知 (DSN)**   このレポートには、メッセージ配信の結果が記述されます。DSN メッセージの詳細については、「[Exchange 2013 の DSN と NDR](dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md)」を参照してください。

  - **メッセージ ディスポジション通知 (MDN)**   このレポートには、受信者に正しく配信された後のメッセージの状態が記述されます。開封通知 (RN) および未開封通知 (NRN) はどちらも MDN メッセージの例です。MDN メッセージは RFC 2298 で定義されており、メッセージ ヘッダーの **Disposition-Notification-To:**  ヘッダー フィールドによって制御されます。`Disposition-Notification-To:` ヘッダー フィールドを使用する MDN 設定は、さまざまなメッセージ サーバーと互換性があります。MDN 設定は、Microsoft Outlookおよび Exchange の MAPI プロパティを使用して定義することもできます。

  - **配信不能レポート (NDR)**   このレポートは、メッセージを指定された受信者に配信できなかったことをメッセージ送信者に伝えます。

  - **未開封通知 (NRN)**   このレポートは、メッセージが開封前に削除されたことを示します。

  - **不在 (OOF)**   このレポートは、受信者が電子メール メッセージに応答しないことを示します。頭字語 OOF は、以前の Microsoft メッセージング システムで、これに該当する通知が "out of facility" と名付けられていたことに由来します。

  - **開封通知 (RN)**   このレポートは、メッセージが開封されたことを示します。

  - **取り消し状況レポート**   このレポートは、特定の受信者に対する取り消し要求の状態を示します。取り消し要求は、送信者が Outlook を使用して送信済みメッセージを取り消そうとしたときに発生します。

配信レポート メッセージが配布グループに送信されたとき、次のような設定が行われている場合はレポート メッセージが削除されます。

  - レポート リダイレクトが設定されていない。または、レポート リダイレクト先がメッセージ送信者に設定されている。

  - レポート リダイレクト先が配布グループ管理者に設定されており、配信レポート メッセージが NDR ではない。

配信レポート メッセージが配布グループに送信されると、配信レポート メッセージは配布グループ マネージャーに配信されることがあります。このようになるのは、レポートのリダイレクト先が配布グループ管理者に設定されており、レポート メッセージが NDR であるときです。

配信レポート メッセージではないメッセージが配布グループに送信されると、そのメッセージは配布グループのメンバーに配信されます。次の一覧は、レポート要求設定についてまとめたものです。

  - レポート リダイレクト先がメッセージ送信者に設定されている場合、レポート要求設定は変更されません。

  - レポート リダイレクトが設定されていない場合、レポート要求設定はすべて抑制されます。メッセージ エンベロープ内の各受信者の **RCPT TO:**  に、`NOTIFY=NEVER` エントリが追加されます。

  - レポート リダイレクト先が配布グループ マネージャーに設定されている場合、配布グループ管理者に送信される NDR メッセージを除いて、レポート要求設定はすべて抑制されます。

## 受信者に対するメッセージ制限

展開処理では、受信者に対して構成されているメッセージ制限も適用されます。この制限は受信者ごとに個別に構成するか、Exchange 組織のすべてのハブ トランスポート サーバー用に組織的に構成できます。次の表では、受信者に対して構成されるメッセージ制限について説明します。

### 受信者に対するメッセージ制限

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>ソース</th>
<th>パラメーター</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-TransportConfig</strong></p></td>
<td><p><em>MaxReceiveSize</em></p></td>
<td><p><em>MaxReceiveSize</em> パラメーターは、受信者に対して構成されたメッセージ制限に使用されるサイズがメッセージ ヘッダー内の <strong>X-MS-Exchange-Organization-OriginalSize:</strong> ヘッダー フィールドの値であることを指定します。Exchange は、メッセージが Exchange 組織に入ったときに、このヘッダー フィールドを使用して元のメッセージ サイズを記録します。指定したメッセージ サイズの制限に照らしてメッセージをチェックする場合、現在のメッセージ サイズと上記の元のメッセージ サイズ ヘッダーの値のうち小さい方の値が使用されます。コンテンツ変換、エンコード、およびエージェント処理によって、メッセージのサイズが変わる場合があります。このヘッダー フィールドが存在しない場合は、現在のメッセージ サイズの値を使用してこのフィールドが作成されます。メッセージが大きすぎる場合は NDR が生成され、以降のメッセージ処理は停止します。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-MailUser</strong></p></td>
<td><p><em>RequireSenderAuthenticationEnabled</em></p></td>
<td><p><em>RequireSenderAuthenticationEnabled</em> パラメーターは、受信者に送信されるすべてのメッセージが認証された送信者からのものであることを要求します。このパラメーターの値が <code>$true</code> に設定されている場合、認証されていない送信者からのメッセージは拒否されます。システムおよびシステム アテンダント メールボックスにメッセージを送信するすべての送信者は、認証を受ける必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-MailUser</strong></p></td>
<td><p><em>AcceptMessagesOnlyFromSendersOrMembers</em></p>
<p><em>RejectMessagesFromSendersOrMembers</em></p></td>
<td><p><em>AcceptMessagesOnlyFromSendersOrMembers</em> パラメーターは、特定の送信者または配布グループのメンバーに受信者へのメッセージ送信を許可する場合に、その送信者または配布グループを指定します。なお、このパラメーターでは、古いパラメーター <em>AcceptMessagesOnlyFrom</em> と <em>AcceptMessagesOnlyFromDLMembers</em> の機能が組み合わせられています。</p>
<p><em>RejectMessagesFromSendersOrMembers</em> パラメーターは、特定の送信者または配布グループのメンバーに受信者へのメッセージ送信を許可しない場合に、その送信者または配布グループを指定します。なお、このパラメーターでは、古いパラメーター <em>RejectMessagesFrom</em> と <em>RejectMessagesFromDLMembers</em> の機能が組み合わせられています。</p>
<p>カテゴライザーは、受信者のアクセス許可を 2 つのパスで確認します。最初のパスでは、送信者が <em>AcceptOnlyMessagesFromSendersOrMembers</em> または <em>RejectMessagesFromSendersOrMembers</em> パラメーターに含まれているかどうかを判断します。送信者がどちらのパラメーターにも含まれていない場合、このパラメーター内の配布グループが完全に展開されます。このような配布グループの完全な展開には、時間がかかる場合があります。これらのパラメーターでは、配布グループの入れ子の深さを最小限に抑えることをお勧めします。</p></td>
</tr>
</tbody>
</table>


認証された送信者によって送信される特定の種類のメッセージは、制限から除外されます。次の一覧は、受信者の制限から除外されるメッセージを示しています。

  - **Microsoft Exchange 受信者によって送信されるすべてのメッセージ**   これらのメッセージには、内部メッセージ送信者に送信される DSN メッセージ、ジャーナル レポート、クォータ メッセージ、およびその他のシステム生成メッセージが含まれます。Microsoft 受信者の詳細については、「[受信者](recipients-exchange-2013-help.md)」を参照してください。

  - **外部ポストマスターのアドレスによって送信されるすべてのメッセージ**   これらのメッセージには、外部のメッセージ送信者に送信される DSN メッセージ、およびその他のシステム生成メッセージが含まれます。外部ポストマスターのアドレスの詳細については、「[外部ポストマスターのアドレスを構成する](configure-the-external-postmaster-address-exchange-2013-help.md)」を参照してください。

特定の種類のメッセージは、Exchange 組織から外部ドメインに送信されるときにブロックされます。この設定は、**Set-RemoteDomain** コマンドレットの以下のパラメーターによって制御されます。

  - *AllowedOOFType*

  - *AutoForwardEnabled*

  - *AutoReplyEnabled*

  - *DeliveryReportEnabled*

  - *NDREnabled*

詳細については、「[リモート ドメイン](remote-domains-exchange-2013-help.md)」を参照してください。

ページのトップへ

## 分割および受信者の展開の制御

メッセージ受信者の完全な一覧は受信者の解決によって展開および解決されるため、同じメッセージの異なるコピーの作成が必要となる場合があります。以下のシナリオは、このような場合について説明しています。

  - **メッセージ受信者が異なるメッセージ設定を必要とする場合**   開封確認などのメッセージ プロパティを、一部の受信者に対しては有効にし、他の受信者に対してはブロックする必要がある場合があります。元のメッセージとわずかに異なるプロパティを持つ新しいバージョンのメッセージの作成は、*分割*と呼ばれます。

  - **単一メッセージ内のエンベロープ受信者の数を制限する場合**   大規模な配布グループが展開される場合、受信者の展開処理によって数千にも及ぶ個別の受信者が生成される場合があります。Exchange では、数千のエンベロープ受信者を含むメッセージの単一コピーを作成する代わりに、エンベロープ受信者の数が制限された同じメッセージの複数のコピーが作成されます。

## 分割

受信者の解決では、次の条件が満たされる場合にメッセージが分割されます。

  - メッセージ エンベロープの **MAIL FROM:**  内のメッセージ送信者が更新される場合。たとえば、配布グループの *ReportToManagerEnabled* パラメーターの値が `$true` になっている場合です。

  - DSN、OOF メッセージ、取り消し状況レポートなどの自動応答メッセージを抑制する必要がある場合。

  - 代替受信者が展開される場合。

  - **Resent-From:**  ヘッダー フィールドをメッセージ ヘッダーに追加する必要がある場合。Resent ヘッダー フィールドは、メッセージがユーザーによって転送されたかどうかを判断するために使用できる情報ヘッダー フィールドです。Resent ヘッダー フィールドは、受信者にとってメッセージが元の送信者から直接送信されたように見えるようにするために使用されます。受信者は、メッセージ ヘッダーを参照して、メッセージを転送したのはだれかを確認することができます。Resent ヘッダー フィールドは RFC 2822 のセクション 3.6.6 で定義されています。

  - 配布グループの展開履歴を送信する必要がある場合。

## 受信者の展開の制御

展開される受信者の数が多すぎる場合、カテゴライザーはメッセージを複数のコピーに分割します。これは、メッセージ展開時のシステム リソースの使用を削減するために実行されます。メッセージ内のエンベロープ受信者の最大数は、アプリケーション構成ファイル `%ExchangeInstallPath%Bin\EdgeTransport.exe.config` の *ExpansionSizeLimit* キーによって制御されます。既定値は 1,000 です。


> [!NOTE]
> 運用環境の Exchange トランスポート サーバーでは、<EM>ExpansionSizeLimit</EM> キーの値を変更しないことをお勧めします。



ページのトップへ

## 受信者の解決の診断

受信者の解決のレポートおよび診断情報は、パフォーマンス カウンター、およびメッセージ追跡ログのエントリによって提供されます。これらのソースは、受信者の解決における問題を特定し、診断するのに役立ちます。

## 受信者の解決に関するパフォーマンス カウンター

次の表は、受信者の解決において使用可能なパフォーマンス カウンターを示しています。

### 受信者の解決に関するパフォーマンス カウンター

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>カウンター名</th>
<th>表示名</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AmbiguousRecipientsTotal</p></td>
<td><p>Ambiguous Recipients</p></td>
<td><p>これは、受信者の解決時に検出された、あいまいな受信者の合計数です。あいまいな受信者とは、一致する <strong>legacyExchangeDN</strong> Active Directory 属性、または一致する <strong>proxyAddresses</strong> Active Directory 属性を持つ、複数の異なる受信者です。</p></td>
</tr>
<tr class="even">
<td><p>AmbiguousSendersTotal</p></td>
<td><p>Ambiguous Senders</p></td>
<td><p>これは、受信者の解決時に検出された、あいまいな送信者の合計数です。あいまいな送信者とは、一致する <strong>legacyExchangeDN</strong> Active Directory 属性、または一致する <strong>proxyAddresses</strong> Active Directory 属性を持つ、複数の異なる送信者です。</p></td>
</tr>
<tr class="odd">
<td><p>FailedRecipientsTotal</p></td>
<td><p>Failed Recipients</p></td>
<td><p>これは、受信者の解決時に検出された、解決できない受信者の数です。</p></td>
</tr>
<tr class="even">
<td><p>LoopRecipientsTotal</p></td>
<td><p>Loop Recipients</p></td>
<td><p>これは、受信者ループが原因で受信者の解決に失敗した受信者の数です。</p></td>
</tr>
<tr class="odd">
<td><p>MessagesChippedTotal</p></td>
<td><p>Messages Chipped</p></td>
<td><p>これは、単一メッセージ内のエンベロープ受信者の数を制御するために、受信者の解決時に作成された同じメッセージのコピーの合計数です。Exchange では、この処理は<em>細分化 (チッピング)</em> と呼ばれます。</p></td>
</tr>
<tr class="even">
<td><p>MessagesCreatedTotal</p></td>
<td><p>Messages Created</p></td>
<td><p>これは、受信者の解決時に作成されたメッセージの数です。</p></td>
</tr>
<tr class="odd">
<td><p>MessagesRetriedTotal</p></td>
<td><p>Messages Retried</p></td>
<td><p>これは、受信者の解決時に再試行がスケジュールされたメッセージの数です。</p></td>
</tr>
<tr class="even">
<td><p>UnresolvedOrgRecipientsTotal</p></td>
<td><p>Unresolved Org Recipients</p></td>
<td><p>これは、受信者の解決時に検出された、権限のあるドメインからの解決されない受信者の数です。</p></td>
</tr>
<tr class="odd">
<td><p>UnresolvedOrgSendersTotal</p></td>
<td><p>Unresolved Org Senders</p></td>
<td><p>これは、受信者の解決時に検出された、権限のあるドメインからの解決されない送信者の数です。</p></td>
</tr>
</tbody>
</table>


## メッセージ追跡ログの受信者の解決イベント

次の表は、メッセージ追跡ログに書き込まれる受信者の解決イベントを示しています。

### メッセージ追跡ログの受信者の解決イベント

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>メッセージ追跡イベント</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EXPAND</p></td>
<td><p>このイベントは、配布グループが展開されたことを示します。</p></td>
</tr>
<tr class="even">
<td><p>REDIRECT</p></td>
<td><p>このイベントは、メールボックス受信者またはメールが有効なパブリック フォルダー受信者に送信されたメッセージが <em>ForwardingAddress</em> パラメーターの指定通りに代替受信者にリダイレクトされたことを示します。</p></td>
</tr>
<tr class="odd">
<td><p>RESOLVE</p></td>
<td><p>このイベントは、受信者の電子メール アドレスが、対応する Active Directory 受信者オブジェクトのプライマリ SMTP 電子メール アドレスに変更されたことを示します。</p></td>
</tr>
<tr class="even">
<td><p>TRANSFER</p></td>
<td><p>このイベントは、メッセージの分割または細分化 (チッピング) が発生したことを示します。</p></td>
</tr>
</tbody>
</table>


メッセージ追跡の詳細については、「[メッセージ追跡](message-tracking-exchange-2013-help.md)」を参照してください。

