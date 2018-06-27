---
title: 'Exchange 2013 からの DLP 機密情報の種類のエクスポート: Exchange Online Help'
TOCTitle: Exchange からの DLP 機密情報の種類のエクスポート
ms:assetid: 8f02fbc2-dd1c-4276-be1a-517a43fe39b2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn479225(v=EXCHG.150)
ms:contentKeyID: 59634979
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 からの DLP 機密情報の種類のエクスポート

 

_**適用先:**Exchange Online, Exchange Server 2013_

ポリシーをエクスポートし、それらを XML ファイルとして保存し、その XML ファイルを変更すれば、Exchange 管理センター (EAC) または Exchange 管理シェル コマンドレットを使用せずに、DLP ポリシー内の詳細を表示または変更できます。通常は、XML ファイルをその後 Exchange にインポートし直します。これにより、Exchange に依存せずにポリシーを編集することができます。ただし、正しく動作させるには、ポリシーが特定の書式要件 (XML スキーマとも呼ばれる) を満たしている必要があります。

DLP に関連する追加の管理タスクについては、「[DLP ポリシーの管理](manage-dlp-policies-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間: 15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「データ損失防止 (DLP)」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

EAC は、DLP ポリシーまたはテンプレートを外部ファイルにエクスポートする手段を提供していません。このタスクを実行するには、Exchange 管理シェル を使用します。

## Exchange 管理シェル を使用して DLP 機密情報の種類をエクスポートする

この例では、すべての DLP 機密情報タイプとその属性を XML ファイル (C:\\My Documents\\exportedInformationTypes.xml) にエクスポートします。現在の DLP 機密情報タイプ コレクションのバックアップ コピーを作成することをお勧めします。これを実行する 1 つの方法として、エクスポートしてからすぐにコピーし、その同じ XML ファイルの名前を変更する方法が挙げられます。

1.  Exchange 管理シェル を開きます。

2.  **Get-ClassificationRuleCollection** と入力すると、組織の機密情報の種類が画面に表示されます。独自の機密情報の種類を作成していない場合は、"Microsoft Rule Package" というラベルが付いた、組み込まれた既定の機密情報のタイプ コレクションのみが表示されます。

3.  **$ruleCollections = Get-ClassificationRuleCollection** と入力して、機密情報の種類を変数内に保存します。

4.  **Set-Content -path "C:\\My Documents\\exportedRules.xml" -Encoding Byte -Value $ruleCollections.SerializedClassificationRuleCollection**..と入力して、すべてのデータを含む書式化された XML ファイルを作成します。

これで、必要に応じて XML ファイルを編集し、ポリシーを調整することができます。組み込まれている機密情報の種類をカスタマイズする方法の詳細については、「[組み込みの DLP 機密情報の種類をカスタマイズする](customize-the-built-in-dlp-sensitive-information-types-exchange-2013-help.md)」を参照してください。ポリシーを Exchange にインポートし直す方法の詳細については、「[ファイルからカスタムの DLP ポリシー テンプレートをインポートする](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)」を参照してください。

## 詳細情報

[Exchange での機密情報の種類の検索基準：](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

[組み込みの DLP 機密情報の種類をカスタマイズする](customize-the-built-in-dlp-sensitive-information-types-exchange-2013-help.md)

[ファイルからカスタムの DLP ポリシー テンプレートをインポートする](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

