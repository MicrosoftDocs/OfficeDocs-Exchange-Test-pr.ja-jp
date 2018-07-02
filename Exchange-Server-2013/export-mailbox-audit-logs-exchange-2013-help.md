---
title: 'メールボックス監査ログをエクスポートする: Exchange Online Help'
TOCTitle: メールボックス監査ログをエクスポートする
ms:assetid: b458a95a-3321-4647-8884-cf97f8e7186a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ150552(v=EXCHG.150)
ms:contentKeyID: 48269941
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックス監査ログをエクスポートする

 

_**適用先:** Exchange Online, Exchange Server 2013_

メールボックスでメールボックス監査が有効になっている場合、所有者以外のユーザーがそのメールボックスにアクセスするたびに、*メールボックス監査ログ*に情報が記録されます。各ログ エントリには、メールボックスにアクセスしたユーザーとアクセスの日時、所有者以外のユーザーが実行した操作、およびその操作が成功したかどうかの情報が含まれています。既定では、メールボックス監査ログのエントリは 90 日間保持されます。メールボックス監査ログを使用すると、所有者以外のユーザーがメールボックスにアクセスしたかどうかを確認できます。

メールボックス監査ログのエントリをエクスポートすると、エントリが XML ファイルに保存されて、指定した受信者に電子メール メッセージの添付ファイルとして送信されます。

**目次**

開始する前に

メールボックス監査ログの構成

メールボックス監査ログのエクスポート

メールボックス監査ログの表示

詳細情報

## 開始する前に

  - 各手順の推定完了時間:時間は変数です。Exchange Online では、メールボックス監査ログは、エクスポート後数日以内に送信されます。

  - Exchange Online では、このトピックの手順の多くを実行するために、リモート Windows PowerShell を使用する必要があります。詳しくは、「[リモート PowerShell による Exchange への接続](https://technet.microsoft.com/ja-jp/library/jj984289\(v=exchg.150\))」を参照してください。

  - このトピックの手順には、特定のアクセス許可が必要です。アクセス許可情報については、各手順を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## メールボックス監査ログの構成

メールボックス監査ログをエクスポートおよび表示する前に、監査する各メールボックスでメールボックス監査ログを有効にしておく必要があります。また、監査ログにアクセスするため、XML 添付ファイルがOutlook Web App を使用できるようMicrosoft Outlook Web App を構成する必要があります。

## 手順 1:メールボックス監査ログを有効にする

所有者以外のメールボックス アクセスのレポートを実行する各メールボックスでメールボックス監査ログを有効にする必要があります。メールボックスでメールボックス監査ログが有効になっていないと、メールボックス監査ログをエクスポートしても、何の結果も得られません。

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」トピックの「メールボックス監査ログ」エントリ。

1 つのメールボックスでメールボックス監査ログを有効にするには、Shell でコマンドを実行します。

    Set-Mailbox <Identity> -AuditEnabled $true

組織のすべてのユーザー メールボックスでメールボックス監査を有効にするには、次のコマンドを実行します。

    $UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}

    $UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}

## 手順 2:XML 添付ファイルを許可するように Outlook Web App を構成する

メールボックス監査ログをエクスポートすると、監査ログの XML ファイルが電子メール メッセージに添付されますが、Outlook Web App では、XML 添付ファイルは既定でブロックされます。エクスポートされた監査ログにアクセスするには、Microsoft Outlook を使用するか、Outlook Web App を構成して XML 添付ファイルを許可するようにする必要があります。

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「Outlook Web App メールボックス ポリシー」。

Outlook Web App で XML 添付ファイルを許可するには、以下の手順を実行します。Exchange Server 2013 では、値 `Default` を *Identity* パラメーターに使用します。

1.  次のコマンドを実行して、Outlook Web App で許可されるファイルの種類の一覧に XML を追加します。
    
        Set-OwaMailboxPolicy -Identity OwaMailboxPolicy-Default -AllowedFileTypes @{add='.xml'}

2.  次のコマンドを実行して、Outlook Web App でブロックされるファイルの種類の一覧から XML を削除します。
    
        Set-OwaMailboxPolicy -Identity OwaMailboxPolicy-Default -BlockedFileTypes @{remove='.xml'}

## 正常な動作を確認する方法

メールボックス監査ログが正常に構成されていることを確認するには、次の操作を行います。

1.  次のコマンドを実行してメールボックスに監査ログが構成されたことを確認します。
    
        Get-Mailbox | FL Name,AuditEnabled
    
    *AuditEnabled* プロパティの値を `True` にすると、監査ログが有効であることが確認されます。

2.  次のコマンドを実行して、Outlook Web App で XML 添付ファイルが許可されていることを確認します。
    
        Get-OwaMailboxPolicy | Select-Object -ExpandProperty AllowedFileTypes
    
    許可されたファイルの種類の一覧に `.xml` が含まれていることを確認します。

3.  次のコマンドを実行して、Outlook Web App でブロックされるファイルの一覧から XML 添付ファイルが削除されていることを確認します。
    
        Get-OwaMailboxPolicy | Select-Object -ExpandProperty BlockedFileTypes
    
    ブロックされるファイルの種類の一覧に `.xml` が含まれていないことを確認します。

ページのトップへ

## メールボックス監査ログのエクスポート

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[Exchange およびシェル インフラストラクチャのアクセス許可](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)」の「表示専用の管理者監査ログ」。

1.  Exchange 管理センター (EAC) で、**\[コンプライアンス管理\]** \> **\[監査\]** の順に選択します。

2.  **\[メールボックス監査ログのエクスポート\]** をクリックします。

3.  メールボックス監査ログのエントリをエクスポートするための検索条件を構成します。次の条件を指定できます。
    
      - **開始日と終了日**   エクスポートされるファイルに含めるエントリの日付の範囲を選択します。
    
      - **監査ログの検索対象のメールボックス**   監査ログ エントリを取得するメールボックスを選択します。
    
      - **所有者以外のアクセスの種類**   次のいずれかのオプションを選択して、エントリを取得する所有者以外のアクセスの種類を定義します。
        
          - **\[所有者以外すべて\]**   組織内の管理者および委任されたユーザーによるアクセスと、Exchange Online の Microsoft データセンターの管理者によるアクセスを検索します。
        
          - **\[外部ユーザー\]**   Microsoft データセンターの管理者によるアクセスを検索します。
        
          - **\[管理者と委任されたユーザー\]**   組織内の管理者と委任されたユーザーによるアクセスを検索します。
        
          - **\[管理者\]**   組織の管理者によるアクセスを検索します。
    
      - **受信者**   メールボックス監査ログの送信先のユーザーを選択します。

4.  **\[エクスポート\]** をクリックします。
    
    指定した検索条件に一致するエントリがメールボックス監査ログから取得され、SearchResult.xml というファイルに保存されて、指定した受信者に電子メール メッセージの添付ファイルとして送信されます。

## 正常な動作を確認する方法

メールボックス監査ログの送信先のメールボックスにサインインします。監査ログを正常にエクスポートできていれば、Exchange からメッセージが送信されます。Exchange Online では、このメッセージを受け取るまでに数日かかる場合があります。メールボックス監査ログ (SearchResult.xml という名前) は、このメッセージに添付されます。XML 添付ファイルが許可されるように Outlook Web App を正しく構成した場合は、添付の XML ファイルをダウンロードできます。

ページのトップへ

## メールボックス監査ログの表示

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[Exchange およびシェル インフラストラクチャのアクセス許可](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)」の「表示専用の管理者監査ログ」。

SearchResult.xml ファイルを保存して表示するには、以下のようにします。

1.  メールボックス監査ログの送信先のメールボックスにサインインします。

2.  \[受信トレイ\] で、Microsoft Exchange から送信された、XML 添付ファイルを含むメッセージを開きます。この電子メール メッセージの本文には検索条件が含まれています。

3.  添付ファイルをクリックして、XML ファイルのダウンロードを選択します。

4.  Microsoft Excel で SearchResult.xml を開きます。

ページのトップへ

## 詳細情報

  - **メールボックス監査ログのエントリ** 次の例は、SearchResult.xml ファイルに含まれるメールボックス監査ログからのエントリを示しています。各エントリは **\<Event\>** XML タグで始まり、**\</Event\>** XML タグで終了します。このエントリは、2010 年 4 月 30 日に管理者が David のメールボックスの \[回復可能なアイテム\] フォルダーから "**Notification of litigation hold**" という件名のメッセージを削除したことを示しています。
    
        <Event MailboxGuid="6d4fbdae-e3ae-4530-8d0b-f62a14687939" 
          Owner="PPLNSL-dom\david50001-1363917750" 
          LastAccessed="2010-04-30T11:01:55.140625-07:00" 
          Operation="HardDelete" 
          OperationResult="Succeeded" 
          LogonType="Admin"
         FolderId="0000000073098C3277988F4CB882F5B82EBF64610100A7C317F68C24304BBD18ABE1F185E79B00000026BD4F0000"
          FolderPathName="\Recoverable Items\Deletions"
          ClientInfoString="Client=OWA;Action=ViaProxy" 
          ClientIPAddress="10.196.241.168" 
          InternalLogonType="Owner"
          MailboxOwnerUPN="david@contoso.com"
          MailboxOwnerSid="S-1-5-21-290112810-296651436-1966561949-1151" 
          CrossMailboxOperation="false" 
          LogonUserDN="Administrator"
          LogonUserSid="S-1-5-21-290112810-296651436-1966561949-1149">
          <SourceItems>
           <ItemId="0000000073098C3277988F4CB882F5B82EBF64610700A7C317F68C24304BBD18ABE1F185E79B00000026BD4F0000A7C317F68C24304BBD18ABE1F185E79B00000026BD540"
            Subject="Notification of litigation hold"
            FolderPathName="\Recoverable Items\Deletions" /> 
          </SourceItems>
        </Event>

  - **メールボックス監査ログの有用なフィールド** メールボックス監査ログの有用なフィールドの説明を示します。これらのフィールドは、メールボックスの所有者以外のアクセスの各インスタンスに関する特定の情報を確認するのに役立ちます。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>フィールド</th>
    <th>説明</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Owner</strong></p></td>
    <td><p>所有者以外のユーザーがアクセスしたメールボックスの所有者。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>LastAccessed</strong></p></td>
    <td><p>メールボックスへのアクセス日時。</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Operation</strong></p></td>
    <td><p>所有者以外のユーザーが実行した操作。詳細については、「<a href="https://technet.microsoft.com/ja-jp/library/jj156300(v=exchg.150)">所有者以外のメールボックス アクセスのレポートの実行の詳細情報</a>」の「メールボックス監査ログに記録される内容」を参照してください。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OperationResult</strong></p></td>
    <td><p>所有者以外のユーザーが実行した操作が成功したか失敗したか。</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>LogonType</strong></p></td>
    <td><p>所有者以外のアクセスの種類。これには、管理者、代理人、および外部があります。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>FolderPathName</strong></p></td>
    <td><p>所有者以外のユーザーによる影響を受けたメッセージを格納しているフォルダーの名前。</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>ClientInfoString</strong></p></td>
    <td><p>所有者以外のユーザーがメールボックスにアクセスするために使用したメール クライアントに関する情報。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ClientIPAddress</strong></p></td>
    <td><p>所有者以外のユーザーがメールボックスにアクセスするために使用したコンピューターの IP アドレス。</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>InternalLogonType</strong></p></td>
    <td><p>所有者以外のユーザーがこのメールボックスにアクセスするために使用したアカウントのログオンの種類。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>MailboxOwnerUPN</strong></p></td>
    <td><p>メールボックスの所有者の電子メール アドレス。</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>LogonUserDN</strong></p></td>
    <td><p>所有者以外のユーザーの表示名。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Subject</strong></p></td>
    <td><p>所有者以外のユーザーによる影響を受けた電子メール メッセージの件名。</p></td>
    </tr>
    </tbody>
    </table>
    
    ページのトップへ

