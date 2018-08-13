---
title: 'Outlook でのスパム対策スタンプの表示: Exchange 2013 Help'
TOCTitle: Outlook でのスパム対策スタンプの表示
ms:assetid: cddb5dbf-ad1e-471c-9fc8-28ddcf7ec1d0
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124595(v=EXCHG.150)
ms:contentKeyID: 49896482
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook でのスパム対策スタンプの表示

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-03_

Microsoft Outlook を使用して、Microsoft Exchange によって電子メール メッセージに適用されたスパム対策スタンプを表示できます。スパム対策スタンプは、スパムに関連する問題を診断するのに役立ちます。この機能は、インターネットからの受信メッセージをフィルタリングするためのスパム対策エージェントをメッセージが通過するとき、送信者固有の情報、パズル検証の結果、コンテンツ フィルターの結果などの診断メタデータ (スタンプ) を適用することによって、実行されます。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「Mailbox access (メールボックス アクセス)」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## Outlook 2010 または Outlook 2013 を使用してスパム対策スタンプを表示する

1.  クライアント コンピューターの Outlook 2010 または Outlook 2013 の **\[メール\]** ビューで、メッセージをダブルクリックして開きます。

2.  \[リボン\] の **\[タグ\]** セクションで **\[オプション\]** アイコンをクリックして、メッセージの **\[プロパティ\]** ダイアログ ボックスを表示します。

3.  次の例に示すように、**\[プロパティ\]** ダイアログ ボックスの **\[インターネット ヘッダー\]** セクションで、スクロール バーを使用してスパム対策スタンプを表示します。
    
        X-MS-Exchange-Organization-PCL:7
        X-MS-Exchange-Organization-SCL:6
        X-MS-Exchange-Organization-Antispam-Report: DV:3.1.3924.1409;SID:SenderIDStatus Fail;PCL:PhishingLevel SUSPICIOUS;CW:CustomList;PP:Presolved;TIME:TimeBasedFeatures

## Outlook 2007 を使用してスパム対策スタンプを表示する

1.  クライアント コンピューターの Outlook 2007 の **\[メール\]** ビューで、メッセージをダブルクリックして開きます。

2.  **\[メッセージ\]** タブの **\[オプション\]** グループで、**\[メッセージ オプション\]** をクリックします。

3.  次の例に示すように、**\[メッセージ オプション\]** ダイアログ ボックスの **\[インターネット ヘッダー\]** セクションで、スクロール バーを使用してスパム対策スタンプを表示します。
    
        X-MS-Exchange-Organization-PCL:7
        X-MS-Exchange-Organization-SCL:6
        X-MS-Exchange-Organization-Antispam-Report: DV:3.1.3924.1409;SID:SenderIDStatus Fail;PCL:PhishingLevel SUSPICIOUS;CW:CustomList;PP:Presolved;TIME:TimeBasedFeatures

