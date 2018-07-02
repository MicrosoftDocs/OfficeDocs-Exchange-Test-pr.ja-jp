---
title: 'ドキュメント フィンガープリンティングを使用してフォーム データを保護する: Exchange Online Help'
TOCTitle: ドキュメント フィンガープリンティングを使用してフォーム データを保護する
ms:assetid: 110c839b-7693-42f6-aa5d-58ce64f4c357
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn635175(v=EXCHG.150)
ms:contentKeyID: 61204721
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ドキュメント フィンガープリンティングを使用してフォーム データを保護する

 

_**適用先:** Exchange Online, Exchange Server 2013_

組織でフォームを使用して機密情報を収集している場合は、ユーザーがそのようなフォームを電子メールで外部の連絡先に送ることで、セキュリティ リスクが生じる可能性があります。Exchange のデータ損失防止 (DLP) は、[ドキュメント フィンガープリンティング](overview-of-document-fingerprinting-in-exchange.md) を使用して機密情報を検出することによって、その情報の保護を支援します。ドキュメント フィンガープリンティングを使用するには、知的財産文書、政府機関フォーム、組織内で使用されているその他の標準フォームなどの空白のフォームをアップロードするだけです。その後で、生成されたドキュメント フィンガープリントを DLP ポリシーまたはトランスポート ルールに追加します。ここでは、使用方法について説明します。

> [!VIDEO https://www.microsoft.com/ja-jp/videoplayer/embed/df9d0f67-cf16-4beb-868b-c7149b260056]

## EAC を使用してドキュメント フィンガープリントを作成する

![強調表示された EAC 内のドキュメント フィンガープリントへのパス](images/Dn635175.e8562ea7-40ba-4feb-adde-2e81f029fcda(EXCHG.150).png "強調表示された EAC 内のドキュメント フィンガープリントへのパス")

1.  Exchange 管理センター (EAC) で、**\[コンプライアンス管理\]** \> **\[データ損失防止\]** に移動します。

2.  **\[ドキュメントの指紋の管理\]** をクリックします。

3.  ドキュメント フィンガープリントのページで、**\[新規\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックして、新しいドキュメント フィンガープリントを作成します。

4.  ドキュメント フィンガープリントの **\[名前\]** と **\[説明\]** を入力します (選択した名前が機密情報の種類の一覧に表示されます)。

5.  フォームをアップロードするには、**\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

6.  フォームを選択して、**\[開く\]** をクリックします (アップロードするファイルにテキストが含まれていること、そのファイルがパスワードで保護されていないこと、そのファイルの種類がトランスポート ルールでサポートされていることを確認します。サポートされているファイルの種類の一覧については、「[Office 365 で、メール フロー ルールを使用してメッセージの添付ファイルを検査する](https://technet.microsoft.com/ja-jp/library/jj919236\(v=exchg.150\))」を参照してください。そうでない場合、フィンガープリントを作成しようとしたときにエラーが表示されます)。このドキュメント フィンガープリントのドキュメント一覧に追加するすべてのファイルに対して、同じ操作を繰り返します。必要に応じて、後からこのドキュメント フィンガープリントに対してファイルを追加または削除することもできます。

7.  **\[保存\]** をクリックします。

これで、ドキュメント フィンガープリントが機密情報の種類の一部になったため、DLP ポリシーに追加したり、\[**メッセージに機密情報が含まれる**\] 条件を介してトランスポート ルールに追加したりできます。

![強調表示されている \[このルールを適用する条件\]](images/Dn635175.9355a513-a790-48eb-a61b-575ba2ecdfa6(EXCHG.150).png "強調表示されている [このルールを適用する条件]")

DLP ポリシーへのルールの追加方法については、「[DLP ポリシーの管理](manage-dlp-policies-exchange-2013-help.md)」の「DLP ポリシーを変更する」を参照してください。また、トランスポート ルールの変更方法については、「[機密情報ルールとトランスポート ルールの統合](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)」を参照してください。新しいポリシーを作成する場合は、「[テンプレートからの DLP ポリシーの作成](how-to-new-dlp-data-loss-prevention-policy-template.md)」を参照してください。

## シェルを使用してドキュメント フィンガープリントに基づいて分類ルール パッケージを作成する


> [!TIP]
> シェルでも分類ルール パッケージを作成または修正できますが、EAC でドキュメント フィンガープリントを作成した方が簡単な場合があります。シェルでこの手順を試す前に、EAC で試すことをお勧めします。



DLP は、分類ルール パッケージを使用して、メッセージ内の機密コンテンツを検出します。ドキュメント フィンガープリントに基づいて分類ルール パッケージを作成するには、**New-Fingerprint** コマンドレットと **New-DataClassification** コマンドレットを使用します。**New-Fingerprint** の結果はデータ分類ルールの外部に保存されないため、**New-Fingerprint** と **New-DataClassification** または **Set-Dataclassification** は、必ず同じ PowerShell セッション内で実行します。次の例では、C:\\My Documents\\Contoso Employee Template.docx ファイルに基づいて新しいドキュメント フィンガープリントを作成します。新しいフィンガープリントは変数として保存し、同じ PowerShell セッション内の **New-DataClassification** コマンドレットで使用できるようにします。

    $Employee_Template = Get-Content "C:\My Documents\Contoso Employee Template.docx" -Encoding byte
    $Employee_Fingerprint = New-Fingerprint -FileData $Employee_Template -Description "Contoso Employee Template"

ここで、C:\\My Documents\\Contoso Customer Information Form.docx ファイルのドキュメント フィンガープリントを使用する、"Contoso Employee Confidential" という名前の新しいデータ分類ルールを作成してみましょう。

    $Employee_Template = Get-Content "C:\My Documents\Contoso Customer Information Form.docx" -Encoding byte
    $Customer_Fingerprint = New-Fingerprint -FileData $Customer_Form -Description "Contoso Customer Information Form"
    New-DataClassification -Name "Contoso Customer Confidential" -Fingerprints $Customer_Fingerprint -Description "Message contains Contoso customer information." 

**Get-DataClassification** コマンドレットを使用してすべての DLP データ分類ルール パッケージを探すことができます。この例では、"Contoso Customer Confidential" がデータ分類ルール パッケージの一覧に含まれています。

最後に、"Contoso Customer Confidential" データ分類ルール パッケージを DLP ポリシーに追加します。

    New-TransportRule -Name "Notify :External Recipient Contoso confidential" -NotifySender NotifyOnly -Mode Enforce -SentToScope NotInOrganization -MessageContainsDataClassification @{Name=" Contoso Customer Confidential"}

これで、DLP エージェントが Contoso Customer Form.docx ドキュメント フィンガープリントと一致するドキュメントを検出するようになります。

構文とパラメーターの詳細については、「[New-Fingerprint](https://technet.microsoft.com/ja-jp/library/dn584142\(v=exchg.150\))」、「[New-DataClassification](https://technet.microsoft.com/ja-jp/library/dn584139\(v=exchg.150\))」、「[Set-DataClassification](https://technet.microsoft.com/ja-jp/library/dn584141\(v=exchg.150\))」、「[Get-DataClassification](https://technet.microsoft.com/ja-jp/library/jj215720\(v=exchg.150\))」を参照してください。

## 詳細情報

[ドキュメント フィンガープリンティング](overview-of-document-fingerprinting-in-exchange.md)

[DLP ポリシーの管理](manage-dlp-policies-exchange-2013-help.md)

[機密情報ルールとトランスポート ルールの統合](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

