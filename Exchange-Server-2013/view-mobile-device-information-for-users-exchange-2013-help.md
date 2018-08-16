---
title: 'ユーザーのモバイル デバイス情報の表示: Exchange 2013 Help'
TOCTitle: ユーザーのモバイル デバイス情報の表示
ms:assetid: 4fd263c0-ad61-416c-bd68-339bf66605cf
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997974(v=EXCHG.150)
ms:contentKeyID: 49896244
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ユーザーのモバイル デバイス情報の表示

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-11-29_

ユーザーは複数のモバイル デバイスを MicrosoftExchange Server 2013 と同期するように構成できます。 EAC またはシェルを使用して、特定ユーザーに関連付けられたモバイル デバイスの一覧を表示できます。

モバイル デバイスに関連する追加の管理タスクについては、「[Exchange ActiveSync](exchange-activesync-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「モバイル デバイス メールボックス ポリシー」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## EAC を使用して、ユーザーのモバイル デバイス情報を表示するには

EAC はユーザーのメールボックスと現在同期しているモバイル デバイスの一覧を表示します。モバイル デバイスを、ファミリー、モデル、電話番号、またはステータス別に表示できます。

1.  EAC で、<strong>受信者</strong> \> <strong>メールボックス</strong> の順にクリックし、メールボックスを選択します。

2.  \[詳細\] ウィンドウで、スクロールして <strong>電話機能と音声機能</strong> を表示し、<strong>詳細の表示</strong> をクリックして <strong>モバイル デバイスの詳細</strong> 画面を表示します。

## シェルを使用して、ユーザーのモバイル デバイス情報を表示するには

Get-MobileDevice コマンドレットを使用すると、特定ユーザーのモバイル デバイスの一覧を表示できます。

1.  次のコマンドを実行します。
    
        Get-MobileDevice -Mailbox useralias

