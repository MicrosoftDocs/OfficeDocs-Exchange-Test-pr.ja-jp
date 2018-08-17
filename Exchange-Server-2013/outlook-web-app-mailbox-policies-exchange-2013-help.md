---
title: 'Outlook Web App メールボックス ポリシー: Exchange Online Help'
TOCTitle: Outlook Web App メールボックス ポリシー
ms:assetid: 213b8b7a-1c29-49ee-8c98-d0364ddf4f9d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd335142(v=EXCHG.150)
ms:contentKeyID: 49895288
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Web App メールボックス ポリシー

 

_**適用先:** Exchange Online, Exchange Server 2013_

Outlook Web App の機能に対するアクセスを管理する組織レベルのポリシーは、MicrosoftOutlook Web App メールボックス ポリシーで作成します。

**目次**

Outlook Web App メールボックス ポリシー

Outlook Web App メールボックス ポリシーの作成または削除

Outlook Web App メールボックス ポリシーの構成

Outlook Web App メールボックス ポリシーの適用

## Outlook Web App メールボックス ポリシー

Exchange 2013 で、複数の Outlook Web App メールボックス ポリシーを作成し、それらのポリシーを個々のメールボックスに適用することができます。Outlook Web App メールボックス ポリシーをメールボックスに適用すると、ポリシーが仮想ディレクトリの設定より優先されます。

Outlook Web App 機能は、Outlook Web App 仮想ディレクトリを構成して管理することもできます。 仮想ディレクトリ設定は、メールボックス ポリシーが適用されていないメールボックスに使用します。

## Outlook Web App メールボックス ポリシーの作成または削除

Exchange をインストールすると、既定の Outlook Web App メールボックス ポリシーが自動的に生成されます。 既定では、すべてのオプションが既定の Outlook Web App メールボックス ポリシーで有効になっています。組織のニーズに応じて Outlook Web App メールボックス ポリシーを必要な数だけ作成できます。


> [!NOTE]
> 既定の Outlook Web App メールボックス ポリシーは、どのメールボックスにも自動的に適用されることはありません。



メールボックス ポリシーの作成や削除に関しては、「[Outlook Web App のメールボックス ポリシーの作成](create-an-outlook-web-app-mailbox-policy-exchange-2013-help.md)」と「[Exchange から Outlook Web App のメールボックス ポリシーを削除する](remove-an-outlook-web-app-mailbox-policy-from-exchange-exchange-2013-help.md)」を参照してください。

## Outlook Web App メールボックス ポリシーの構成

既定の Outlook Web App メールボックス ポリシーのオプションは、既定ですべて有効になります。 Outlook Web App メールボックス ポリシーの構成の詳細については、「[Outlook Web App メールボックス ポリシーのプロパティの表示または構成](view-or-configure-outlook-web-app-mailbox-policy-properties-exchange-2013-help.md)」を参照してください。

## Outlook Web App メールボックス ポリシーの適用

Outlook Web App メールボックス ポリシーは、メールボックスに 1 つだけ適用することができます。

メールボックスに適用される Outlook Web App メールボックス ポリシーがない場合、仮想ディレクトリで定義した設定が適用されます。

Outlook Web App メールボックス ポリシーは、既存のメールボックスを変更する場合は Exchange 管理センター (EAC) で、またメールボックス ポリシーを適用する場合はシェルと [Set-CASMailbox](https://technet.microsoft.com/ja-jp/library/bb125264\(v=exchg.150\)) コマンドレットでメールボックスに適用できます。詳細については、「[Outlook Web App のメールボックス ポリシーをメールボックスで適用または削除する](apply-or-remove-an-outlook-web-app-mailbox-policy-on-a-mailbox-exchange-2013-help.md)」を参照してください。

