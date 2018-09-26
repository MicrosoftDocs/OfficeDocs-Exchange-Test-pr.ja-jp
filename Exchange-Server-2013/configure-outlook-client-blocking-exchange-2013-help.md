---
title: 'Outlook クライアントのブロックを構成する: Exchange 2013 Help'
TOCTitle: Outlook クライアントのブロックを構成する
ms:assetid: 3a579c83-8bc7-4adc-a25c-8eb6eed7220c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd335207(v=EXCHG.150)
ms:contentKeyID: 51407519
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook クライアントのブロックを構成する

 

_**適用先:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

Exchange Server 2013 では、メッセージング レコード管理 (MRM) の保持ポリシーまたは管理フォルダーを使用できます。Microsoft Outlook 2010 およびそれ以降を実行しているユーザーのみが、保持ポリシーのすべてのクライアント機能にアクセスできます。ただし、保持ポリシーは、ユーザーが使用している Outlook クライアント バージョンとは関係なく、管理フォルダー アシスタントによってメールボックス サーバーに適用されます。古い Outlook クライアントは、これらの MRM 機能を公開しません。たとえば、Outlook 2007 は保持ポリシーをサポートしないため、ユーザーはアイテムまたはフォルダーに個人タグを適用できません。

古いバージョンの Outlook を実行しているユーザーが Exchange メールボックスにアクセスできないようにすることができます。また、メールボックス単位またはクライアント アクセス サーバー単位でアクセスをブロックすることもできます。

MRM に関連するその他の管理タスクについては、「[メッセージング レコード管理の手順](messaging-records-management-procedures-exchange-2013-help.md)」を参照してください。

## 各クライアント アプリケーションおよびバージョンで使用できる MRM 機能

次の表に、さまざまなクライアント アプリケーションおよびバージョンで使用できる MRM 機能の一覧を示します。

### MRM 機能

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>クライアント アプリケーション</th>
<th>使用可能な MRM クライアントの機能</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013 およびOutlook 2010</p></td>
<td><p>すべて</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2007</p></td>
<td><p>管理フォルダー</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2003 およびそれ以前</p></td>
<td><p>非サポート</p></td>
</tr>
<tr class="even">
<td><p>その他の電子メール クライアント ソフトウェア</p></td>
<td><p>なし</p></td>
</tr>
</tbody>
</table>


次の表に、Outlook のバージョン番号を示します。

### Outlook のバージョン

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Outlook のバージョン</th>
<th>バージョン番号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013</p></td>
<td><p>15</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2010</p></td>
<td><p>14</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p>12</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2003</p></td>
<td><p>11</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2002</p></td>
<td><p>10</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2000</p></td>
<td><p>9</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 98</p></td>
<td><p>8.5</p></td>
</tr>
<tr class="even">
<td><p>Outlook 97</p></td>
<td><p>8</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> 変更を加える前に、修正プログラムおよびサービス パックのリリースがクライアントのバージョン文字列に影響を与える場合があることに注意してください。サーバー側の Exchange コンポーネントも MAPI を使用してログオンする必要があるため、クライアント アクセスを制限する場合は、注意が必要です。クライアント バージョンをコンポーネント名 (SMTP や OLE DB など) として報告するコンポーネントもあれば、Exchange のビルド番号 (6.0.4712.0 など) として報告するコンポーネントもあります。このため、6.&lt;<EM>x</EM>.<EM>x</EM>.&gt; で始まるバージョン番号を持つクライアントを制限することは避けてください。たとえば、MAPI アクセスを完全に防ぐには、<STRONG>0.0.0-6.5535.65535.65535</STRONG> を指定する代わりに、2 つの範囲を指定してサーバー コンポーネントがログオンできるようにします。たとえば、次のように指定します。<STRONG>0.0.0-5.9.9; 7.0.0-</STRONG>.



これらの手順を実行した後、ユーザーがメールボックスへのアクセスをブロックされると、次の警告メッセージが表示されることに注意してください。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Exchange サーバー管理者が、使用しているバージョンの Outlook をブロックしています。詳細については管理者に問い合わせてください。</p></td>
</tr>
</tbody>
</table>


Outlook より前のバージョンの Outlook 2010 を実行している電子メール クライアントでは MRM 機能がサポートされないことを通知する警告を省略するには、シェルで **New-Mailbox**、**Enable-Mailbox**、および **Set-Mailbox** の各コマンドレットの *ManagedFolderMailboxPolicyAllowed* パラメーターを使用できます。*ManagedFolderMailboxPolicy* パラメーターを使用してメールボックスに管理フォルダー メールボックス ポリシーを割り当てる場合、*ManagedFolderMailboxPolicyAllowed* パラメーターを使用しないと、既定で警告が表示されます。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分。

  - Exchange 管理センター (EAC) を使用してこれらの手順を実行することはできません。シェルを使用する必要があります。

  - このトピックの手順には、特定のアクセス許可が必要です。アクセス許可情報については、各手順を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## 必要な作業

## メールボックス単位で Outlook バージョンをブロックする

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「ユーザー メールボックス」。

この例では、11.8010.8036 以前のすべての Outlook バージョンをブロックします。

```powershell
Set-CASMailbox -Identity adam@contoso.com -MAPIBlockOutlookVersions "-11.8010.8036"
```

この例では、Outlook のバージョンでブロックされているメールボックスへのアクセスを復元します。

```powershell
Set-CASMailbox -Identity adam@contoso.com -MAPIBlockOutlookVersions $null
```

構文およびパラメーターの詳細については、「[Set-CASMailbox](https://technet.microsoft.com/ja-jp/library/bb125264\(v=exchg.150\))」を参照してください。

## クライアント アクセス サーバーの Outlook バージョンをブロックする

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「RPC クライアント アクセス設定」。

この例では、バージョン 12.0.0 より前の Outlook クライアントが Exchange 2010 またはそれ以降のクライアント アクセス サーバー上のメールボックスにアクセスできないようブロックします。


> [!IMPORTANT]
> <EM>BlockedClientVersions</EM> パラメーターで使用されている値は例です。適切なクライアント ソフトウェアのバージョンは、<CODE>%ExchangeInstallPath%Logging\RPC Client Access</CODE> にある RPC クライアント アクセスのログ ファイルを解析することによって判断できます。



  ```powershell
  Set-RpcClientAccess -Server CAS01 -BlockedClientVersions "0.0.0-5.65535.65535;7.0.0;8.02.4-11.65535.65535"
  ```

構文およびパラメーター定義の詳細については、「[Set-RpcClientAccess](https://technet.microsoft.com/ja-jp/library/dd351072\(v=exchg.150\))」を参照してください。

