---
title: 'ユーザーの音声呼び出しの音質の調査: Exchange Online Help'
TOCTitle: ユーザーの音声呼び出しの音質の調査
ms:assetid: 0c945886-3cfa-423e-9b46-0d6b1584a145
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ659059(v=EXCHG.150)
ms:contentKeyID: 50555728
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ユーザーの音声呼び出しの音質の調査

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) 呼び出しの音質に問題があるという報告をユーザーから受けた場合は、原因の究明にユーザー呼び出しのログ レポートを使用できます。


> [!NOTE]
> 呼び出しの音質には、このレポートの対象に含まれない要因が影響している場合もあります。たとえば、Exchange サーバーでメモリや CPU の負荷が高くなっていると、レポートには音質が最高と示されていても、ユーザーから音質の問題が報告される場合があります。



UM レポートに関連するその他のタスクについては、「[UM レポート手順](um-reports-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM 呼び出しデータと要約レポート コマンドレット」エントリ。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## EAC を使用して、UM が有効なユーザーの呼び出しログを取得する

1.  EAC で <strong>ユニファイド メッセージング</strong> \> <strong>その他のオプション</strong>![\[その他のオプション\] アイコン](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "[その他のオプション] アイコン") \> <strong>ユーザー呼び出しのログ</strong> へ移動します。

2.  <strong>ユーザーの選択</strong> をクリックし、データを表示するユーザーを選択します。

3.  レポートの特定の行の音質の詳細を表示するには、その行を選択してから <strong>音質の詳細</strong> をクリックします。次の情報が表示されます。
    
      - <strong>日付と時刻</strong>   呼び出しの日付と時刻です。選択したユーザーが Outlook Web App で設定したタイム ゾーンで表示されます。
    
      - <strong>ユーザー</strong>   選択したユーザーです。
    
      - <strong>UM ダイヤル プラン</strong>   呼び出しのダイヤル プランです。
    
      - <strong>UM IP ゲートウェイ</strong>   呼び出しに使用された UM IP ゲートウェイです。
    
      - <strong>Audio Codec</strong>   呼び出し中に使用されたオーディオ コーデックです。
    
      - <strong>NMOS</strong>   呼び出しの Network Mean Opinion Score (NMOS) です。NMOS は、呼び出しの音質を 1 から 5 までの数値で表します (5 が最高)。
        

        > [!NOTE]
        > 呼び出しの NMOS の最高値は、使用するオーディオ コーデックによって決まります。NMOS は、10 秒未満の非常に短い呼び出しでは評価されない可能性があります。

    
      - <strong>NMOS 低下</strong>   NMOS の、使用されているオーディオ コーデックの最高値との差です。たとえば、呼び出しの \[NMOS 低下\] の値が 1.2 で \[NMOS\] の値が 3.3 の場合、その呼び出しの NMOS の最高値は 4.5 (1.2 + 3.3) です。
    
      - <strong>Jitter</strong>   呼び出しのデータ パケットの到着時間の変動の平均値です。
    
      - <strong>パケット損失</strong>   選択した呼び出しのデータ パケット損失の割合の平均値です。パケット損失は、接続の信頼性の指標になります。
    
      - <strong>ラウンド トリップ</strong>   選択した呼び出しの音声のラウンド トリップ スコア (ミリ秒) の平均値です。ラウンド トリップ スコアでは接続の待機時間が測定されます。
    
      - <strong>バースト損失期間</strong>   選択した呼び出しのバースト損失中のパケット損失の平均時間です。

