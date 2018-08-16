---
title: 'ユーザーのボイス メール呼び出しの確認: Exchange Online Help'
TOCTitle: ユーザーのボイス メール呼び出しの確認
ms:assetid: 95768fe3-3ae2-43bd-9cbf-18c3b85c4592
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ659070(v=EXCHG.150)
ms:contentKeyID: 50555822
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ユーザーのボイス メール呼び出しの確認

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユーザー呼び出しのログを使用すると、特定のユニファイド メッセージング (UM) ユーザーについて次の情報を表示できます。

  - ユーザーの過去 90 日間の UM 呼び出しの詳細。

  - 各呼び出しの音質。音質の指標は、呼び出しの種類や長さなど、複数の要因に依存するため、すべての呼び出しで利用できるとは限りません。

## UM が有効なユーザーの呼び出しログを取得する方法

1.  Exchange 管理センター (EAC) で、<strong>ユニファイド メッセージング</strong> \> <strong>その他のオプション</strong>![\[その他のオプション\] アイコン](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "[その他のオプション] アイコン") \> <strong>ユーザー呼び出しのログ</strong> に移動します。

2.  <strong>ユーザーの選択</strong> をクリックし、データを表示するユーザーを選択します。

3.  レポートの特定の行の音質の詳細を表示するには、行を選択して <strong>音質の詳細</strong> をクリックします。音質の情報の詳細については、「[ユーザーの音声呼び出しの音質の調査](investigate-the-audio-quality-of-voice-calls-for-a-user-exchange-2013-help.md)」を参照してください。

4.  レポートをクリップボードにコピーするには、<strong>すべての行をクリップボードにコピーします。</strong> をクリックします。

## UM ユーザーの呼び出しログの情報

ユーザーの呼び出しログには、各呼び出しについて次の情報が含まれています。

  - <strong>日付と時刻</strong>   呼び出しの日付と時刻です。選択したユーザーが Microsoft Outlook Web App で設定したタイム ゾーンで表示されます。

  - <strong>期間</strong> 呼び出しの期間です。次の形式で表示されます (MM は分、SS は秒)。MM:SS。

  - <strong>呼び出しの種類</strong>   呼び出しの種類です。
    
      - <strong>Call Answering (呼び出し応答)</strong>   呼び出しが応答されずにメールボックス サーバーに転送され、発信者が音声メッセージを残しました。
    
      - <strong>Call Answering Missed Call (呼び出し応答の不在着信)</strong>   呼び出しが応答されずにメールボックス サーバーに転送され、発信者が音声メッセージを残しませんでした。
    
      - <strong>サブスクライバー アクセス</strong>   サブスクライバー アクセス番号に対する呼び出しが行われました。発信者がサインインし、内線番号とパスワードにより UM に認証され、電子メール、予定表、および音声メッセージに電話を介してアクセスしました。
    
      - <strong>自動応答</strong>   UM 自動応答が呼び出しに応答しました。これは、発信者が組織の代表番号をダイヤルした呼び出しであるのが一般的です。
    
      - <strong>FAX</strong>   FAX トーンが検出された呼び出しが受信されました。FAX パートナーが構成されている場合、このコールはパートナーに送信されました。
    
      - <strong>PlayonPhone (電話での再生)</strong>   ユーザーが Microsoft Outlook Web App または Outlook で音声メッセージの \[電話での再生\] ボタンをクリックしたために、UM によって呼び出しが行われました。
    
      - <strong>FindMe (自分を検索する)</strong>   呼び出し応答ルールの \[自分を検索する\] ルールの結果として、UM によって発信呼び出しが行われました。
    
      - <strong>認証されていないパイロット番号</strong>   Outlook Voice Access 番号に対する呼び出しが行われました。発信者はサインインせず、認証されませんでした。
    
      - <strong>案内応答の録音</strong>   ユーザーの個人用の案内応答を録音するために UM によって呼び出しが行われました。
    
      - <strong>なし</strong>   呼び出しが行われましたが、種類は定義されませんでした。

  - <strong>呼び出し元の番号</strong> 発信者の電話便号または SIP アドレスです。

  - <strong>呼び出された番号</strong> 呼び出しの指定された受信者の電話番号または SIP アドレス (Microsoft Office Communications Server 2007 R2 または Microsoft Lync Server のユーザーなど、SIP ダイヤル プランのユーザーの場合) です。

  - <strong>UM IP ゲートウェイ</strong> 呼び出しに応答した UM IP ゲートウェイです。

  - <strong>音質</strong> 呼び出しの全体的な音質です。音質の詳細を表示するには、行を選択して <strong>音質の詳細</strong> をクリックします。

