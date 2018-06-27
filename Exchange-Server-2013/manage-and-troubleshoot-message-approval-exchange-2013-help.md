---
title: 'メッセージ承認の管理とトラブルシューティング: Exchange Online Help'
TOCTitle: メッセージ承認の管理とトラブルシューティング
ms:assetid: 860df43f-a05b-4da3-83f1-68d3123a923d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd298110(v=EXCHG.150)
ms:contentKeyID: 52057826
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メッセージ承認の管理とトラブルシューティング

 

_**適用先:**Exchange Server 2013_

調停メールボックスを削除しようとしたときに次のエラーが発生することがあります。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>調停メールボックス &lt;<em>メールボックス</em>&gt; は現在、メンバーシップ制限またはモデレートが有効になっている既存の受信者に対する承認ワークフローに使用されているため削除できません。この調停メールボックスを削除する前に、当該受信者の承認機能を無効にするか、または当該受信者に別の調停メールボックスを指定する必要があります。</p></td>
</tr>
</tbody>
</table>


調停メールボックスは、モデレートされた受信者および配布グループのメンバーシップ承認の承認ワークフローを処理するために使用できます。PowerShell を使用して、調停メールボックスを使用するように構成されているすべての受信者を特定します。受信者の特定後に、受信者が別の調停メールボックスを使用するように構成するか、または受信者のモデレートを無効にできます。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「調停」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

## 手順 1:シェルを使用して、削除しようとしている調停メールボックスを使用するすべての受信者を特定する

次のコマンドを実行します。

    $AM = Get-Mailbox "<arbitration mailbox>" -Arbitration
    $AMDN = $AM.DistinguishedName
    Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq $AMDN}

たとえば、Arbitration Mailbox01 という調停メールボックスを使用するすべての受信者を特定するには、次のコマンドを実行します。

    $AM = Get-Mailbox "Arbitration Mailbox01" -Arbitration
    $AMDN = $AM.DistinguishedName
    Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq $AMDN}


> [!NOTE]
> 調停メールボックスは、識別名 (DN) を使用して指定されます。調停メールボックスの DN がわかっている場合は、次のコマンドを実行できます。。<CODE>Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq &lt;DN&gt;}</CODE>.



## 手順 2:シェルを使用して、別の調停メールボックスを指定するか、または受信者のモデレートを無効にする

モデレート受信者が、削除しようとしている調停メールボックスを使用しないようにするには、別の調停メールボックスを指定するか、または受信者のモデレートを無効にできます。

受信者に別の調停メールボックスを指定する場合は、次のコマンドを実行します。

    Set-<RecipientType> <Identity> -ArbitrationMailbox <different arbitration mailbox>

たとえば、メンバーシップの承認のために、All Employees という配布グループが Arbitration Mailbox02 という調停メールボックスを使用するように構成し直すには、次のコマンドを実行します。

    Set-DistributionGroup "All Employees" -ArbitrationMailbox "Arbitration Mailbox02"

受信者のモデレートを無効にする場合は、次のコマンドを実行します。

    Set-<RecipientType> <Identity> -ModerationEanbled $false

たとえば、Human Resources というメールボックスのモデレートを無効にするには、次のコマンドを実行します。

    Set-Mailbox "Human Resources" -ModerationEanbled $false

## 正常な動作を確認する方法

使用中というエラー メッセージが表示されることなく調停メールボックスを削除できれば、この手順は正常に完了しています。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

