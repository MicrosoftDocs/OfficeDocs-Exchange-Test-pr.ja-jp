---
title: '組織の音声呼び出しの音質を調査する: Exchange Online Help'
TOCTitle: 組織の音声呼び出しの音質を調査する
ms:assetid: 8a87694b-1678-4a01-859f-5ad3b2c73db5
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ659069(v=EXCHG.150)
ms:contentKeyID: 50555814
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 組織の音声呼び出しの音質を調査する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

組織の ユニファイド メッセージング (UM) およびボイス メール メッセージの呼び出しの音質に問題がある場合は、呼び出しの統計レポートを使用すると原因の究明に役立ちます。


> [!NOTE]
> 呼び出しの音質には、このレポートの対象に含まれない要因が影響している場合もあります。たとえば、Exchange サーバーでメモリや CPU の負荷が高くなっていると、レポートには音質が最高と示されていても、ユーザーから音質の問題が報告される場合があります。



呼び出しの統計に関連する追加のタスクについては、「[UM レポート手順](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/run-voice-mail-call-reports/um-reports-procedures)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 3 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM 呼び出しデータと要約レポートのコマンドレット」エントリ。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## EAC を使用して組織の音質統計情報を取得する

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>その他のオプション</strong>![\[その他のオプション\] アイコン](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "[その他のオプション] アイコン") \> <strong>呼び出しの統計</strong> に移動します。

2.  レポートに含める呼び出しの統計を選択します。以下のオプションを選択すると、レポートが自動的に更新されます。
    
      - <strong>表示</strong>   表示する呼び出しの統計の種類を次の中から選択します。
        
          - <strong>毎日 (90 日間)</strong>   過去 90 日間のすべての呼び出しの詳細を表示する場合に選択します。
        
          - <strong>毎月 (12 か月)</strong>   過去 12 か月間の呼び出しの月ごとの概要を表示する場合に選択します。
        
          - <strong>すべて</strong>   UM による呼び出しの処理の開始以降に受信されたすべての呼び出しの統計を表示する場合に選択します。
    
      - <strong>UM ダイヤル プラン</strong>   レポートのデータを特定の UM ダイヤル プランの呼び出しのみに限定する場合にそのダイヤル プランを選択します。
    
      - <strong>UM IP ゲートウェイ</strong>   レポートのデータを特定の UM IP ゲートウェイの呼び出しのみに限定する場合に、その UM IP ゲートウェイを選択します。先に UM ダイヤル プランを選択した場合は、選択した UM ダイヤル プランに関連付けられている UM IP ゲートウェイのみが一覧に表示されます。

3.  レポートの特定の行の音質の詳細を表示するには、行を選択して <strong>音質の詳細</strong> をクリックします。次の情報を使用できます。
    
      - <strong>日付と時刻</strong>   呼び出しの統計が取得された UTC の日時です。
    
      - <strong>UM ダイヤル プラン</strong>   統計に含まれている呼び出しのダイヤル プランです。
    
      - <strong>UM IP ゲートウェイ</strong>   統計に含まれている呼び出しに応答した UM IP ゲートウェイです。
    
      - <strong>NMOS</strong>   呼び出しの Network Mean Opinion Score (NMOS) です。NMOS では、呼び出しの音質が 5 段階で評価されます (5 が最高)。
        

        > [!NOTE]
        > 呼び出しにおいて可能な最大の NMOS は、使用されているオーディオ コーデックによって異なります。10&nbsp;秒未満の短い呼び出しの場合は、NMOS を使用できない場合があります。

    
      - <strong>NMOS 低下</strong>   NMOS の、使用されているオーディオ コーデックで取得可能な最も高い値との差です。たとえば、呼び出しの \[NMOS 低下\] の値が 1.2 で \[NMOS\] の値が 3.3 の場合、その呼び出しの NMOS の上限は 4.5 (1.2 + 3.3) です。
    
      - <strong>ジッター</strong>   呼び出しのデータ パケットの到着時間の変動の平均値です。
    
      - <strong>パケット損失</strong>   選択した呼び出しのデータ パケット損失の割合の平均値です。パケット損失は、接続の信頼性の指標になります。
    
      - <strong>ラウンド トリップ</strong>   選択した呼び出しの音声のラウンド トリップ スコア (ミリ秒) の平均値です。ラウンド トリップ スコアでは接続の待機時間が測定されます。
    
      - <strong>バースト損失期間</strong>   選択した呼び出しのバースト損失中のパケット損失の平均時間です。
    
      - <strong>サンプル数</strong>   平均値を計算するためにサンプリングされた呼び出しの数です。

4.  特定の呼び出しに関する音質の指標の詳細については、「[ユーザーの音声呼び出しの音質の調査](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/run-voice-mail-call-reports/audio-quality-of-voice-calls-for-user)」を参照してください。

