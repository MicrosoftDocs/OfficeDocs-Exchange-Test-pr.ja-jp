---
title: 'モバイル デバイス: Exchange 2013 Help'
TOCTitle: モバイル デバイス
ms:assetid: 93a949e7-b3ef-43ea-ae0c-6698826fc8d2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb232129(v=EXCHG.150)
ms:contentKeyID: 49896377
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# モバイル デバイス

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2012-09-24_

MicrosoftExchange ActiveSync に対応するモバイル デバイスを使用すると、ユーザーはいつでも、どこからでも自分の Microsoft Exchange メールボックス データのほぼすべてにアクセスできます。 多種多様な携帯電話およびモバイル デバイスが Exchange ActiveSync に対応しています。 これらには、Windows Phone、Nokia 携帯電話、Android フォンおよびタブレット、Apple iPhone、iPod、iPad があります。

電話と電話以外のモバイル デバイスで Exchange ActiveSync をサポートしていますが、ほとんどの Exchange ActiveSync ドキュメントでは、*モバイル デバイス*という用語を使用します。 説明中の機能が SMS メッセージ通知などのセルラー型電話信号を必要としない限り、モバイル デバイスという用語は携帯電話とタブレットのような他のモバイル デバイスの両方を意味するものとします。

## Exchange ActiveSync

Exchange ActiveSync は、電子メール メッセージ、スケジュール データ、連絡先、およびタスクへの、ワイヤレスでのモバイル アクセスを可能にする通信プロトコルです。Exchange ActiveSync は Windows Phone、および Exchange ActiveSync に対応するサードパーティ製電話で利用できます。

Exchange ActiveSync は、ダイレクト プッシュ テクノロジを提供します。 ダイレクト プッシュは、モバイル デバイスとサーバーの間で確立および維持されている暗号化された HTTPS 接続を使用して、新しい電子メール メッセージやその他の Exchange データを電話にプッシュします。

MicrosoftExchange Server 2013 でダイレクト プッシュを使用するには、ダイレクト プッシュをサポートするように設計されているモバイル デバイスが必要です。

## Exchange ActiveSync の機能

Exchange ActiveSync は、モバイル デバイスでセキュリティ ポリシーを適用できるようにするさまざまな機能へのアクセスを提供します。 Exchange 2013 を使用することで、複数のモバイル デバイス メールボックス ポリシーを構成でき、どのモバイル デバイスが Exchange サーバーと同期できるのかを制御できます。Exchange ActiveSync を使用すると、モバイル デバイスが紛失または盗難にあった場合に、モバイル デバイスからすべてのデータを完全消去するリモート デバイス ワイプ コマンドを送信できます。また、ユーザーは、Outlook Web App からリモート デバイス ワイプを開始することもできます。

Exchange ActiveSync を使用すると、回復パスワードを生成できます。 この回復パスワードはモバイル デバイスに保存され、ユーザーが自分のパスワードを忘れたときに使用されます。 ユーザーは、デバイス パスワード (PIN) を生成するときに回復パスワードを生成します。 この回復パスワードを使用して、モバイル デバイスのロックを解除できます。 この回復パスワードを使用したら、ユーザーは直ちに新しい PIN を作成する必要があります。

## POP3 と IMAP4

モバイル デバイスで Exchange ActiveSync がサポートされていないか、Exchange ActiveSync によって提供される充実した機能セットが不要である場合は、POP3 または IMAP4 を使用してモバイル デバイスで電子メールにアクセスできます。 POP3 および IMAP4 によるメールボックスへのアクセスの詳細については、「[Exchange Server 2013 での POP3 と IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)」を参照してください。

