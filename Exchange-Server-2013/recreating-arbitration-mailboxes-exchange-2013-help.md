---
title: 'Recreating arbitration mailboxes: Exchange 2013 Help'
TOCTitle: Recreating arbitration mailboxes
ms:assetid: bb6b8524-aaee-4be8-a04e-e61cd2ab3465
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Mt829264(v=EXCHG.150)
ms:contentKeyID: 74518109
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Recreating arbitration mailboxes

 

_**トピックの最終更新日:** 2018-01-17_

**概要**:Exchange 2013 の調停メールボックスについての説明と、再作成の方法。

Exchange 2013 には、*調停メールボックス*と呼ばれる 5 つのシステム メールボックスが付属しています。調停メールボックスは、さまざまな種類のシステム データを格納し、メッセージングの承認ワークフローを管理するために使用します。以下に、各調停メールボックスの種類とその役割の一覧を表示します。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>調停メールボックス名</th>
<th>表示名</th>
<th>永続的な機能</th>
<th>機能</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042</p></td>
<td><p>Microsoft Exchange フェデレーション メールボックス</p></td>
<td><p>{}</p></td>
<td><p>このメールボックスは、異なる Exchange 組織間のフェデレーションを維持するために使用されるデータを格納します。これに含まれるのは、Rights Management サービス、 クロスプレミス メール フローの監視プローブと応答、 通知、 オンライン アーカイブ、メッセージング レコード管理、クロスプレミスの空き時間情報です。</p></td>
</tr>
<tr class="even">
<td><p>SystemMailbox{1f05a927-9350-4efe-a823-5529c2d64109}</p></td>
<td><p>Microsoft Exchange 承認アシスタント</p></td>
<td><p>{}</p></td>
<td><p>このメールボックスは、受信者のモデレートとグループの自動承認依頼のために Exchange 承認フレームワークによりプロビジョニングされます。</p></td>
</tr>
<tr class="odd">
<td><p>Migration.8f3e7716-2011-43e4-96b1-aba62d229136</p></td>
<td><p>Microsoft Exchange の移行</p></td>
<td><p>{OrganizationCapabilityManagement}</p></td>
<td><p>バッチでメールボックスを移動するときに使用する Exchange 移行サービスのデータを格納します。</p></td>
</tr>
<tr class="even">
<td><p>SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}</p></td>
<td><p>Microsoft Exchange</p></td>
<td><p>{OrganizationCapabilityUMDataStorage}</p></td>
<td><p>検出システム メールボックス。</p>
<p>指定された選択条件と一致するメッセージを検索するために、法令遵守責任者が使用する電子情報開示機能によりプロビジョニングされます。このメールボックスは、UM コンソールの出席ファイルや他の情報を格納するために、ユニファイド メッセージングでも使用されます。</p></td>
</tr>
<tr class="odd">
<td><p>SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}</p></td>
<td><p>Microsoft Exchange</p></td>
<td><p>{OrganizationCapabilityUMGrammarReady, OrganizationCapabilityPstProvider, OrganizationCapabilityMessageTracking, OrganizationCapabilityMailRouting, OrganizationCapabilityClientExtensions, OrganizationCapabilityGMGen, OrganizationCapabilityOABGen, OrganizationCapabilityUMGrammar}</p></td>
<td><p>これは組織メールボックスと呼ばれます。オフライン アドレス帳 (OAB) を作成するために使用されます。地理的に離れたサイト間を含む、組織内での OAB 生成の負荷を分散するため、追加の組織メールボックスを作成できます。</p></td>
</tr>
</tbody>
</table>


1 つ以上の調停メールボックスを再作成する必要があるなら、次の手順を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間: プロシージャごとに 10 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「受信者プロビジョニングのアクセス許可」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

## Exchange 管理シェル を使用して調停メールボックスを再作成する

次の手順に従って、特定の種類の調停メールボックスを再作成します。


> [!NOTE]
> 以下のセクションの手順はすべて、Exchange のインストール メディアを展開したのと同じディレクトリから実行してください。



## Microsoft Exchange フェデレーション メールボックスを再作成する

調停メールボックス FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042 を再作成するには:

1.  いずれかの調停メールボックスが見つからない場合には、次のコマンドを実行します。
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

2.  Exchange 管理シェル で、次を実行します。
    
        Enable-Mailbox -Arbitration -Identity "FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042"

## Microsoft Exchange 承認アシスタント メールボックスを再作成する

調停メールボックス SystemMailbox{1f05a927-9350-4efe-a823-5529c2d64109} を再作成するには:

1.  いずれかの調停メールボックスが見つからない場合には、次のコマンドを実行します。
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

2.  Exchange 管理シェル で、次を実行します。
    
        Get-User | Where-Object {$_.Name -like "SystemMailbox{1f05a927-7709-4e35-9dbe-d0f608fb781a}"} | Enable-Mailbox -Arbitration

## Microsoft Exchange 移行メールボックスを再作成する

調停メールボックス Migration.8f3e7716-2011-43e4-96b1-aba62d229136 を再作成するには:

1.  いずれかの調停メールボックスが見つからない場合には、次のコマンドを実行します。
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

2.  Exchange 管理シェル で、次を実行します。
    
        Enable-Mailbox -Arbitration -Identity "Migration.8f3e7716-2011-43e4-96b1-aba62d229136"

3.  Exchange 管理シェル で、次のコマンドを実行して、永続的な機能 (msExchCapabilityIdentifiers) を設定します。
    
        Set-Mailbox "Migration.8f3e7716-2011-43e4-96b1-aba62d229136" -Arbitration -Management:$True -Force

## Microsoft Exchange 検出システム メールボックスを再作成する

調停メールボックス SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9} を再作成するには:

1.  次のコマンドを実行します。
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

## OAB 用の Microsoft Exchange 組織メールボックスを再作成する

調停メールボックス SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c} を再作成するには:

1.  いずれかの調停メールボックスが見つからない場合には、次のコマンドを実行します。
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

2.  Exchange 管理シェル で、次を実行します。
    
        Enable-Mailbox -Arbitration -Identity "SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}"

3.  Exchange 管理シェル で、次のコマンドを実行して、永続的な機能 (msExchCapabilityIdentifiers) を設定します。
    
        Get-Mailbox "SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}" -Arbitration | Set-Mailbox -Arbitration -UMGrammar:$True -OABGen:$True -GMGen:$True -ClientExtensions:$True -MessageTracking:$True -PstProvider:$True -MaxSendSize 1GB -Force

完了後、コマンド `$OABMBX = Get-Mailbox "SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}" -Arbitration (Get-ADUser $OABMBX.SamAccountName -Properties *).msExchCapabilityIdentifiers` を実行すると、46、47、51 が見つからないと表示されます。次のコマンドを実行して、すべての機能を再び追加します。

    Set-ADUser $OABMBX.SamAccountName -Add @{"msExchCapabilityIdentifiers"="40","42","43","44","47","51","52","46"}

## 動作確認の方法

調停メールボックスが正常に再作成されたことを確認するには、**Get-Mailbox** コマンドレットを *Arbitration* スイッチ付きで使用してシステム メールボックスを取得します。

    Get-Mailbox -Arbitration | Format-Table Name, DisplayName

コマンドの結果を表示して、上記の表の名前または表示名により、適切なシステム メールボックスが再作成されていることを確認します。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。


