---
title: 'Exchange ハイブリッド展開のアクセス許可: Exchange 2013 Help'
TOCTitle: Exchange ハイブリッド展開のアクセス許可
ms:assetid: 58b46b2c-a6b2-424a-8fc2-0f1fe1ad8e18
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ906433(v=EXCHG.150)
ms:contentKeyID: 51406953
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange ハイブリッド展開のアクセス許可

 

_<strong>適用先:</strong>Exchange Server 2013, Exchange Server 2016_

_<strong>トピックの最終更新日:</strong>2018-05-02_

Office 365 組織の Exchange Online は Exchange Server に基づいており、オンプレミスの組織の場合と同様に、役割ベースのアクセス制御 (RBAC) を使用してアクセス許可を制御します。管理者には管理役割グループを使用してアクセス許可が付与され、エンド ユーザーには管理役割の割り当てポリシーを使用してアクセス許可が付与されます。

Exchange Online とオンプレミスの Exchange のアクセス許可については、「[アクセス許可](https://technet.microsoft.com/ja-jp/library/dd351175\(v=exchg.150\))」をご覧ください

## 管理者のアクセス許可

既定では、Office 365 テナントの作成に使用されたユーザーは、Exchange Online 組織の Organization Management 役割グループのメンバーになります。このユーザーは、組織レベルの設定の構成や Exchange Online の受信者の管理を含め、Exchange Online 組織全体を管理できます。

実行する必要がある管理機能に応じて、Exchange Online 組織に管理者を追加できます。たとえば、組織管理者と受信者管理者を追加したり、専門家ユーザーが法令遵守タスク (検出、カスタム アクセス許可の構成など) を実行できるようにしたりすることが可能です。Office 365 管理者の Exchange Online のすべてのアクセス許可管理は、Exchange 管理センター (EAC) またはリモート PowerShell を使用して Exchange Online 組織で実行する必要があります。


> [!IMPORTANT]
> 社内組織と Office&nbsp;365 組織間でのアクセス許可の転送はありません。社内組織で定義したアクセス許可は、Office&nbsp;365 の組織で再作成する必要があります。



詳細については、「[役割グループの管理](https://technet.microsoft.com/ja-jp/library/jj657480\(v=exchg.150\))」および「[役割グループのメンバーの管理](https://technet.microsoft.com/ja-jp/library/jj657492\(v=exchg.150\))」を参照してください。

## メールボックスのアクセス許可の委任

オンプレミスの Exchange の導入において、許可できるさまざまなその他のユーザーのメールボックスへのアクセスを許可します。ときに呼び出されます委任されたメールボックスのアクセス許可とその便利な管理アシスタントは、別のユーザーのメールボックスの一部を管理する必要があります。たとえば、経営幹部の予定表を管理します。Exchange ハイブリッド展開では、オンプレミスの Exchange 組織内にあるメールボックスとメールボックスを Office 365 にあるとの間のすべてではなく、いくつかのメールボックスへのアクセスの使用をサポートします。アクセス許可の詳細を次のセクションとは、サポートされていません。ハイブリッド メールボックス アクセス許可をサポートするために必要な追加の構成設置型の組織と Office 365 のメールボックスのアクセス許可を同期する方法です。

## ハイブリッド環境でサポートされるメールボックスのアクセス許可

以下のアクセス許可は、サポート**されています**。

  - **フル アクセス:** オンプレミスの Exchange サーバー上のメールボックスから Office 365 メールボックスへ、またはその逆への**フル アクセス**のアクセス許可を付与できます。たとえば、Office 365 メールボックスにはオンプレミスの共有メールボックスへの**フル アクセス**のアクセス許可を付与できます。ユーザーは Outlook デスクトップ クライアントを使用してメールボックスを開く必要があります。クロスプレミスのメールボックス アクセス許可は、Outlook on the web ではサポートされていません。
    

    > [!NOTE]
    > 初めて他の組織内のメールボックスにアクセスして、Outlook プロファイルに追加する際、ユーザーに対して追加の資格情報が求められる場合があります。



  - **代理人として送信:** オンプレミスの Exchange サーバー上のメールボックスから Office 365 メールボックスへ、またはその逆への**代理人として送信**のアクセス許可を付与できます。たとえば、Office 365 メールボックスにはオンプレミスの共有メールボックスへの**代理人として送信**のアクセス許可を付与できます。ユーザーは Outlook デスクトップ クライアントを使用してメールボックスを開く必要があります。クロスプレミスのメールボックス アクセス許可は、Outlook on the web ではサポートされていません。
    
    オンプレミスの Exchange サーバーと Exchange Online の間で、代理人として送信のアクセス許可を同期させるには、Azure Active Directory Connect サーバー上でいくつかの変更が必要です。詳細については、このトピックで後述する「Azure Active Directory Connect でハイブリッド メールボックス アクセス許可のサポートを有効にする」を参照してください。

  - **Folder permissions** Grants access to the contents of a particular folder.

  - **プライベートなアイテム**デリゲートを追加する場合は、個人の予定表アイテムを表示するフォルダーのアクセス許可を持つユーザーを許可するオプションを構成できます。


> [!NOTE]
> 2018年 2 月年の完全なアクセスをサポートして、クロス フォレストが展開されることにし、2018年 4 月で完了する必要の権利をフォルダーの代わりに送信する機能です。



次のアクセス許可や機能は、サポート**されていません**。

  - **Send-As** ユーザーがメールを送信する際、別のユーザーのメールボックスから送信されたように表示します。

  - **自動マッピング:** Outlook 起動時に、ユーザーに**フル アクセス**権限が付与されているすべてのメールボックスが自動的に開くようにします。

これらのアクセス許可を別のメールボックスから受け取るすべてのメールボックスは、付与する側のメールボックスと同時に移動する必要があります。1 つのメールボックスが複数のメールボックスからアクセス許可を受け取る場合、そのメールボックスと、そのメールボックスにアクセス許可を付与するすべてのメールボックスは、同時に移動する必要があります。

## オンプレミスの Exchange サーバーを構成して、ハイブリッド メールボックス アクセス許可をサポートする

インストールされている Exchange のバージョンによっては、ハイブリッド展開でフル アクセスおよび代理として送信のアクセス許可を有効にするため、追加で構成を変更する必要があります。次の表は、Office 365 とのハイブリッド展開で代理メールボックス アクセス許可をサポートする Exchange のバージョンと、必要な追加構成を示しています。ACL をサポートするよう Exchange 2013 および 2010 のサーバーとメールボックスを構成する手順については、「[ハイブリッド展開で委任されたメールボックスへのアクセス許可をサポートするように Exchange を構成する](configure-exchange-to-support-delegated-mailbox-permissions-in-a-hybrid-deployment-exchange-2013-help.md)」を参照してください。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange のバージョン</th>
<th>前提条件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2016</p></td>
<td><p>追加の構成は必要ありません。</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013</p></td>
<td><p>Exchange 2013 サーバーには以下が必要です。</p>
<ul>
<li><p>最新の累積的な更新プログラム (CU)、または直前の CU がインストールされていること。古い CU を実行している Exchange 2013 サーバーはサポートされていないため、ハイブリッド展開で代理メールボックス アクセス許可が機能しない可能性があります。</p></li>
<li><p>アクセス制御リスト (ACL) がメール オブジェクトにスタンプされ、Office 365 と同期できるよう Exchange 組織が構成されていること。</p></li>
<li><p>Exchange 2013 CU10 以前に Office 365 に移行されたメールボックスと関連付けられているオンプレミスのリモート メールボックスは、ACL をサポートするよう手動で構成する必要があります。Exchange 2013 CU10 以降を実行しているサーバー上に作成されたリモート メールボックスは、ACL を許可するよう Exchange の組織を設定した後、自動的に構成されます。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange 2010</p></td>
<td><p>Exchange 2010 SP3 サーバーには以下が必要です。</p>
<ul>
<li><p>最新の更新プログラムのロールアップ (RU)、または直前の RU がインストールされていること。古い RU を実行している Exchange 2010 SP3 サーバーはサポートされていないため、ハイブリッド展開で代理メールボックス アクセス許可が機能しない可能性があります。</p></li>
<li><p>Office 365 のメールボックスに関連付けられているオンプレミスのリモート メールボックスは、ACL をサポートするよう構成する必要があります。このことを、Office 365 のメールボックスと関連付けられているオンプレミスの各リモート メールボックスで実行する必要があります。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange 2007 以前</p></td>
<td><p>サポートされていません。</p></td>
</tr>
</tbody>
</table>


## Azure Active Directory Connect でハイブリッド メールボックス アクセス許可のサポートを有効にする

オンプレミスの Exchange サーバーを構成することに加え、Azure Active Directory Connect (AAD Connect) サーバーがハイブリッド メールボックス アクセス許可を同期するよう設定されているかどうか確認する必要があります。AAD Connect サーバーがこれらのアクセス許可をサポートできることを確認するため、次のように行う必要があります。

  - **アップグレード AAD の接続**AAD の接続が必要以上にアップグレードするバージョン 1.1.553.0 です。 AAD の接続の最新バージョンは、 [Microsoft Azure Active Directory 接続](http://go.microsoft.com/fwlink/p/?linkid=510956)からダウンロードできます。

  - **AAD Connect で Exchange ハイブリッドを有効にする:** ハイブリッド メールボックス アクセス許可 (具体的には、代理で送信のアクセス許可) を有効にする属性を同期するため、AAD Connect で **Exchange ハイブリッド展開**構成オプションが有効であることを確認する必要があります。AAD Connect インストール ウィザードを再度実行して構成を更新する方法については、「[Azure AD Connect 同期： インストール ウィザードの 2 回目の実行](https://docs.microsoft.com/en-us/azure/active-directory/connect/active-directory-aadconnectsync-installation-wizard)」を参照してください。

## オンプレミスと Office 365 組織の間でメールボックスのアクセス許可を同期する方法

## エンド ユーザーのアクセス許可

管理者のアクセス許可と同様に、Exchange Online 内のエンド ユーザーにもアクセス許可を付与できます。既定では、既定の役割の割り当てポリシーに従ってエンド ユーザーにアクセス許可が付与されます。このポリシーは Exchange Online の組織内のすべてのメールボックスに適用されます。既定で付与されているアクセス許可で十分な場合、何も変更する必要はありません。

エンド ユーザーのアクセス許可をカスタマイズする場合は、既存の既定の役割の割り当てポリシーを変更するか、新しい割り当てポリシーを作成することができます。複数の割り当てポリシーを作成する場合、メールボックスの異なるグループに異なるポリシーを割り当て、各グループの要件に応じてグループに付与するアクセス許可を制御できます。Exchange Online エンド ユーザーのすべてのアクセス許可の管理は、EAC またはリモート PowerShell を使用して Exchange Online 組織で実行する必要があります。

管理者のアクセス許可と同様に、エンド ユーザーのアクセス許可は、社内組織と Exchange Online の組織間で転送されません。社内組織で定義したアクセス許可は、Exchange Online の組織で再作成する必要があります。

詳細については、「[役割の割り当てポリシーの管理](https://technet.microsoft.com/ja-jp/library/jj657511\(v=exchg.150\))」および「[メールボックスの割り当てポリシーを変更する](https://technet.microsoft.com/ja-jp/library/dd638076\(v=exchg.150\))」を参照してください。

次の表に、Exchange Online の組織の既定の役割の割り当てポリシーによって付与されるアクセス許可を示します。

### 既定の役割の割り当てポリシーによるアクセス許可

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>管理役割</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MyTeamMailboxes</p></td>
<td><p><code>MyTeamMailboxes</code> 管理役割では、個々のユーザーがサイト メールボックスを作成してそれを Microsoft SharePoint サイトに接続できます。</p></td>
</tr>
<tr class="even">
<td><p>マイ マーケットプレース アプリ</p></td>
<td><p><code>My Marketplace Apps</code> 管理役割を使用すると、個々のユーザーが自身の Microsoft Office マーケットプレース アプリを表示または変更できます。</p></td>
</tr>
<tr class="odd">
<td><p>MyBaseOptions</p></td>
<td><p><code>MyBaseOptions</code> 管理役割を割り当てられた個々のユーザーは、自身のメールボックスの基本構成および関連付けられている設定を表示、変更することができます。</p></td>
</tr>
<tr class="even">
<td><p>MyContactInformation</p></td>
<td><p><code>MyContactInformation</code> 管理役割により、個々のユーザーは、住所と電話番号を含めた自分の連絡先情報を変更できます。</p></td>
</tr>
<tr class="odd">
<td><p>MyDistributionGroupMembership</p></td>
<td><p><code>MyDistributionGroupMembership</code> 管理役割を割り当てられた個々のユーザーは、組織の配布グループ内のメンバーシップを表示、変更することができます。ただし、これは該当の配布グループがグループ メンバーシップの操作を許可していることが前提条件になります。</p></td>
</tr>
<tr class="even">
<td><p>MyDistributionGroups</p></td>
<td><p><code>MyDistributionGroups</code> 管理役割により、個々のユーザーは配布グループを作成、変更、および表示することと、自らが所有する配布グループでメンバーを変更、表示、削除、および追加することができます。</p></td>
</tr>
<tr class="odd">
<td><p>MyMailSubscription</p></td>
<td><p><code>MyMailSubscription</code> 役割により、個々のユーザーは、メッセージ形式やプロトコルの既定値などの自分の電子メール サブスクリプション設定を表示および変更することができます。</p></td>
</tr>
<tr class="even">
<td><p>MyProfileInformation</p></td>
<td><p><code>MyProfileInformation</code> 管理役割は、個々のユーザーが自分の名前を変更できるようにします。</p></td>
</tr>
<tr class="odd">
<td><p>MyRetentionPolicies</p></td>
<td><p><code>MyRetentionPolicies</code> 管理役割を割り当てられた個々のユーザーは、保持タグを表示することも、保持タグの設定および既定値を表示し変更することもできます。</p></td>
</tr>
<tr class="even">
<td><p>MyTextMessaging</p></td>
<td><p><code>MyTextMessaging</code> 管理役割を割り当てられた個々のユーザーは、テキスト メッセージ設定を作成、表示、および変更できます。</p></td>
</tr>
<tr class="odd">
<td><p>MyVoiceMail</p></td>
<td><p><code>MyVoiceMail</code> 管理役割を割り当てられた個々のユーザーは、ボイス メール設定を表示、変更することができます。</p></td>
</tr>
<tr class="even">
<td><p>自分の ReadWriteMailbox アプリ</p></td>
<td><p><code>My ReadWriteMailbox Apps</code> 管理役割のユーザーは、ReadWriteMailbox のアクセス許可を持つアプリをインストールできます。</p></td>
</tr>
<tr class="odd">
<td><p>自分のカスタム アプリ</p></td>
<td><p><code>My Custom Apps</code> 管理役割のユーザーは、自分のカスタム アプリを表示して変更できます。</p></td>
</tr>
</tbody>
</table>

