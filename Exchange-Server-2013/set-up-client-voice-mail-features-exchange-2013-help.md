---
title: 'クライアント ボイス メール機能をセットアップする: Exchange 2013 Help'
TOCTitle: クライアント ボイス メール機能をセットアップする
ms:assetid: 5e661cfd-d34e-4caa-91a5-967bbecb75eb
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ673529(v=EXCHG.150)
ms:contentKeyID: 50555790
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# クライアント ボイス メール機能をセットアップする

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2013-02-20_

このトピックでは、Exchange ユニファイド メッセージング (UM) が有効になっているユーザーが、自分のメールボックス内の電子メールとボイス メール メッセージにアクセスできるようにする、クライアント機能について説明します。これらの機能を使用すると、ユーザーはボイス メールと電子メールに簡単にアクセスし、ユーザー エクスペリエンス全体が向上します。

**目次**

ボイス メール クライアントのサポート

Outlook Voice Access

呼び出しの転送

ボイス メールのプレビュー

ファックスの受信

## ボイス メール クライアントのサポート

**Exchange ActiveSync クライアント**   Microsoft Exchange ActiveSync プロトコルは、インターネット対応のモバイル デバイスで使用されるモバイル クライアントを Exchange メールボックスに接続するために使用されます。ユーザーはモバイル デバイスを使用して、自分のメールボックスにアクセスして電子メール メッセージを表示する、予定表と連絡先情報を表示および変更する、ボイス メール メッセージを聞くなどの操作ができます。電子メール、ボイス メール、予定表アイテム、および連絡先情報を他のデバイスと同期することもできます。

**Outlook との統合**   Microsoft Outlook を使用すると、ユーザーは、Exchange メールボックスにアクセスして受信トレイ内の電子メール メッセージを表示する、予定表情報を表示および変更する、音声メッセージを聞くなどの操作ができます。これには、電子メール メッセージ内に埋め込まれている Microsoft Windows Media Player を使用します。サポートされている電子メール クライアントを使用すると、ユーザーは電話での再生機能などの追加機能を利用できるようになります。

**Outlook Web App との統合**   Microsoft Outlook Web App には、Outlook などの多機能電子メール クライアントに匹敵する一連の UM インターフェイスとツールが用意されています。Outlook Web App では、ユーザーは準拠する Web ブラウザーを使用して Exchange メールボックスにアクセスできます。Outlook と同様に、Outlook Web App では電子メール メッセージに Windows Media Player が埋め込まれているため、ユーザーは音声メッセージを聞くことができ、電話での再生などの他の機能にアクセスできます。

## Outlook Voice Access

Exchange UM では、UM が有効なユーザーが、UM ダイヤル プランで構成されている内部または外部の電話番号に呼び出しを行って、自分のメールボックスにアクセスしたり、Outlook Voice Access のメニュー システムを使用したりできます。UM が有効なユーザーは、このメニューを使用して、電子メールを読む、音声メッセージを聞く、Outlook 予定表を操作する、個人用連絡先にアクセスする、タスクを実行する (Outlook Voice Access PIN の構成やボイス メールの録音) などの操作ができます。詳細については、「[Outlook Voice Access の設定](setting-up-outlook-voice-access-exchange-2013-help.md)」を参照してください。

## 呼び出しの転送

UM が有効なユーザーは、Outlook または Outlook Web App を使用して、通話応答ルールを作成および構成できます。通話応答ルールを使用すると、ユーザーは着信呼び出しの処理方法を制御できます。このルールが着信呼び出しに適用される方法は、受信トレイ ルールが受信電子メール メッセージに適用される方法と似ていて、ユーザーのメールボックス内の他のボイス設定と共に保存されます。UM が有効なそれぞれのメールボックスに対して、最大 9 つの通話応答ルールを設定できます。これらのルールは受信トレイ ルールから独立し、ユーザーの受信トレイ ルールの格納域の制限を消費しません。詳細については、「[ボイス メール ユーザーの呼び出し転送を許可する](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/allow-voice-mail-users-to-forward-calls)」を参照してください。

## ボイス メールのプレビュー

ボイス メール プレビューは、UM ボイス メール システムからボイス メール メッセージを受信するユーザーが使用できる機能です。ボイス メールのプレビューでは、テキスト形式による録音出力により、ボイス メールのエクスペリエンスを強化しました。詳細については、「[ユーザーがボイス メールのトランスクリプトを表示できるようにする](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/allow-users-to-see-a-voice-mail-transcript)」を参照してください。

## ファックスの受信

UM は、UM が有効なユーザーの受信 FAX 呼び出しを専門の FAX パートナー ソリューションに転送します。この FAX パートナー ソリューションは、FAX 送信者と FAX 通話を確立し、ユーザーの代わりに FAX を受信します。UM が有効なユーザーが FAX メッセージを自分のメールボックスに受信する前に、次の手順を実行する必要があります。

  - *FaxEnabled* パラメーターを `$true` に設定して、ユーザーにリンクされている UM ダイヤル プラン上の着信 FAX を有効にします。

  - *Allowfax* パラメーターを `$true` に設定して、ユーザーにリンクされている UM ダイヤル プラン上の着信 FAX を有効にします。

  - *FaxEnabled* パラメーターを `$true` に設定して、ユーザーの着信 FAX を有効にします。

  - パートナー FAX サーバーの URI を着信 FAX を許可するように設定します。

  - メールボックス サーバーと FAX パートナー サーバー間の認証を構成します。

