---
title: 'ディレクトリ参照を有効または無効にする: Exchange Online Help'
TOCTitle: ディレクトリ参照を有効または無効にする
ms:assetid: c0768815-8578-4385-8d4c-7d1e40304cec
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee423557(v=EXCHG.150)
ms:contentKeyID: 52057514
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ディレクトリ参照を有効または無効にする

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

ディレクトリ参照を有効にすることで、発信者がユニファイド メッセージング (UM) の自動応答を呼び出した際に、電話のキーパッドを使用してディレクトリ内の名前を参照できるようになります。ただし、音声入力によるディレクトリの検索はできません。既定では、この設定は有効になっています。この設定を無効にすると、発信者はタッチトーンや音声コマンドを使用して特定の個人のディレクトリを検索できません。

UM 自動応答に関連する追加の管理タスクについては、「[UM 自動応答手順](um-auto-attendant-procedures-exchange-2013-help.md)」を参照してください。


> [!NOTE]
> Outlook Voice Access ユーザーは自動音声認識 (ASR) または音声入力を使ってディレクトリ内のユーザーを検索できません。使えるのは DTMF またはタッチトーン入力のみです。



## 始める前に把握しておくべき情報

  - 予想所要時間:1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM 自動応答」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM 自動応答が作成されていることを確認してください。詳細な手順については、「[UM 自動応答を作成する](create-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してディレクトリ参照を有効または無効にする

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページの **\[UM 自動応答\]** で、ディレクトリ参照を有効または無効にする UM 自動応答を選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[UM 自動応答\]** ページの **\[アドレス帳とオペレーター アクセス\]** にある **\[アドレス帳の検索のオプション\]** で、**\[ユーザーを名前やエイリアスで検索することを発信者に許可する\]** の横のチェック ボックスをオンにして発信者によるユーザーの検索を有効にします。発信者によるユーザーの検索を無効にするには、このチェック ボックスをオフにします。

4.  **\[保存\]** をクリックします。

## シェルを使用してディレクトリ ルックアップを有効または無効にする

この例では、`MyUMAutoAttendant` という UM 自動応答でディレクトリ参照を無効にします。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -NameLookupEnabled $false

