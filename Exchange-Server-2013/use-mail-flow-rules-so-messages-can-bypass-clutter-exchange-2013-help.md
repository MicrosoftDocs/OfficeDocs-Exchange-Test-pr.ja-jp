---
title: 'メッセージが低優先メール機能を迂回できるメール フロー ルールを使用する: Exchange Online Help'
TOCTitle: メッセージが低優先メール機能を迂回できるメール フロー ルールを使用する
ms:assetid: 58e413f0-aa27-4307-bffd-4df03090a15e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn896639(v=EXCHG.150)
ms:contentKeyID: 64141282
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メッセージが低優先メール機能を迂回できるメール フロー ルールを使用する

 

_**適用先:** Exchange Server 2013_

特定のメッセージを確実に受信するには、これらのメッセージが低優先メール機能フォルダーを迂回するための Exchange トランスポート ルールを作成できます。低優先メール機能の詳細については、「[Outlook Web App でクラッター機能を使って優先度の低いメッセージを並べ替える](https://go.microsoft.com/fwlink/p/?linkid=528411)」を参照してください。

トランスポート ルールに関連するその他の管理タスクについては、「[Exchange Online のメール フロー ルール (トランスポート ルール)](https://technet.microsoft.com/ja-jp/library/jj919238\(v=exchg.150\))」と「[New-TransportRule](https://technet.microsoft.com/ja-jp/library/bb125138\(v=exchg.150\))」の PowerShell のトピックを確認してください。初めて PowerShell を使用する場合は、以下のトピックを参照して、Powershell を使用する際に役立ててください。

  - [リモート PowerShell による Exchange への接続](https://technet.microsoft.com/ja-jp/library/jj984289\(v=exchg.150\))

  - [リモート シェルを使用した Exchange への接続](https://technet.microsoft.com/ja-jp/library/dd335083\(v=exchg.150\))

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「トランスポート ルール」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

## UI を使用して低優先メール機能フォルダーを迂回するトランスポート ルールを作成する

この例では、「Meeting」というタイトルのすべてのメッセージが低優先メール機能を迂回できるようにします。

1.  Exchange 管理センターで、<strong>メール フロー</strong>\><strong>ルール</strong> と移動します。![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックし、\[**新しいルールを作成する...**\] を選択します。

2.  新しいルールの作成後、\[**保存**\] をクリックしてルールを開始します。

![アートの例:件名に "meeting" が含まれる場合、低優先メールをバイパスする](images/Dn896639.75957aa4-4b2a-4142-92ff-07f8ccc64d82(EXCHG.150).png "アートの例:件名に \"meeting\" が含まれる場合、低優先メールをバイパスする")

## シェルを使用して低優先メール機能フォルダーを迂回するトランスポート ルールを作成する

この例では、「Meeting」というタイトルのすべてのメッセージが低優先メール機能を迂回できるようにします。

    New-TransportRule -Name <name_of_the_rule> -SubjectContainsWords "Meeting" -SetHeaderName "X-MS-Exchange-Organization-BypassClutter" -SetHeaderValue "true"


> [!IMPORTANT]
> この例では、"X-MS-Exchange-Organization-BypassClutter" と "true" のどちらも大文字小文字が区別されます。



構文およびパラメーターの詳細については、「[New-TransportRule](https://technet.microsoft.com/ja-jp/library/bb125138\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

電子メール メッセージのヘッダーを調べると、低優先メール トランスポート ルールの迂回によって電子メール メッセージが受信トレイに到着しているかどうかを確認できます。低優先メール迂回トランスポート ルールが適用されている組織内のメールボックスから、電子メール メッセージを取り出します。メッセージにスタンプされたヘッダーを調べると、**X-MS-Exchange-Organization-BypassClutter: true** というヘッダーが見つかります。これは、迂回が機能していることを意味します。ヘッダー情報を調べる方法については、「[電子メール メッセージのインターネット ヘッダー情報を表示する](https://go.microsoft.com/fwlink/p/?linkid=822530)」を参照してください。


> [!NOTE]
> 予定表アイテム (Meetings Accepted、Sent、Declined など) には、それらについて該当するヘッダーがありません。マイクロソフトでは、近日中に、これらの予定表アイテムに低優先メール機能を拡張するように作業を継続しています。


