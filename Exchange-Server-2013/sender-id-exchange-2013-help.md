---
title: '送信者 ID: Exchange 2013 Help'
TOCTitle: 送信者 ID
ms:assetid: 0f628f83-df8c-43fb-bf49-7aaa9ec69ab1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa996295(v=EXCHG.150)
ms:contentKeyID: 49895245
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 送信者 ID

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2016-12-09_

Sender ID エージェントは、Microsoft Exchange Server 2013 で使用可能なスパム対策エージェントです。Sender ID エージェントは、RECEIVED SMTP ヘッダーおよび送信元システムの DNS サービスへのクエリに基づき、受信メッセージに対して実行すべき処理 (ある場合) を決定します。

Sender ID は、送信者とドメインの偽装に対処することを目的としています。この偽装は、よく、*スプーフィング*と呼ばれます。*偽装メール*は、メッセージの実際の送信者とは別の送信者から発信されたように見せるために送信者アドレスが変更された電子メール メッセージです。

スプーフィングされたメールには、通常、特定の組織から発信されたことになっている差出人アドレスが含まれています。以前はヘッダーの検証が行われていなかったため、SMTP セッションの差出人アドレス (MAIL FROM: ヘッダーなど) も、RFC 2822 メッセージ データの差出人アドレス (From: "Masato Kawai" masato@contoso.com など) も比較的簡単にスプーフィングすることが可能でした。

**目次**

Using Sender ID to combat spoofing

Updating your organization's Internet-facing DNS to support Sender ID

Specifying recipients and sender domains to exclude from Sender ID filtering

## Sender ID を使用したスプーフィング対策

Sender ID によって、スプーフィングが困難になります。Sender ID を有効にすると、各メッセージのメタデータ内に Sender ID の状態が格納されます。電子メール メッセージが受信されると、Exchange サーバーは送信者の DNS サーバーに対してクエリを実行し、メッセージの送信元の IP アドレスが、そのメッセージのヘッダーで指定されているドメイン向けにメッセージを送信することが認められているかどうかを確認します。認証されている送信側サーバーの IP アドレスは、PRA (Purported Responsible Address) と呼ばれます。

ドメイン管理者は、その DNS サーバー上の送信者ポリシー フレームワーク (SPF) レコードを発行します。SPF レコードは、承認済みの送信電子メール サーバーを識別します。場合は送信者の DNS サーバーで SPF レコードを構成すると、Exchange サーバーは SPF レコードを解析し、メッセージで指定されているドメインに代わって電子メールを送信するメッセージの受信元となる IP アドレスが承認されたかどうかを決定します。SPF レコードが含まれていて、SPF レコードを作成する方法の詳細については、[送信者 ID](https://go.microsoft.com/fwlink/p/?linkid=50977)を参照してください。

Exchange サーバーは、SPF レコードに基づいてメッセージのメタデータを Sender ID の状態で更新します。Exchange サーバーがメッセージ メタデータを更新した後は、通常どおりメッセージが配信されます。

## Sender ID の状態の値

Sender ID の評価処理によってメッセージの Sender ID の状態が生成されます。Sender ID の状態は、メッセージの SCL (Spam Confidence Level) レベルを評価するために使用されます。この状態は、以下に示すいずれかの値に設定されます。

  - **Pass   **IP アドレスと PRA (Purported Responsible Address) の両方が Sender ID の検証確認に合格しました。

  - **Neutral**   発行された Sender ID のデータだけでは判断できないことを示します。

  - **Soft fail**   PRA の IP アドレスは許可されていないセットに含まれている可能性があります。

  - **Fail   **IP アドレスが許可されていません。受信メールで PRA が見つからないか、送信ドメインが存在しません。

  - **None   **送信者の DNS 内に、公開されている SPF データが存在しません。

  - **TempError**   DNS サーバーが使用できないなど、一時的な DNS エラーが発生しました。

  - **PermError   **レコードの形式にエラーがあるなど、DNS レコードが無効です。

Sender ID の状態は、メッセージのメタデータに追加され、後で MAPI プロパティに変換されます。Microsoft Outlook の迷惑メール フィルターで SCL の値を生成するときにその MAPI プロパティが使用されます。

Outlook は、Sender ID の状態を表示しませんし、特定の Sender ID 値を持つメッセージに常に迷惑メールのフラグを設定するわけではありません。Outlook が Sender ID の状態の値を使用するのは、SCL 値を計算するときのみです。

Sender ID の状態を生成する 7 つのシナリオ以外に、Sender ID の評価処理で、差出人の IP アドレスがないものが見つかることがあります。差出人の IP アドレスがなければ、Sender ID の状態を設定できません。Sender ID の状態を設定できない場合、Exchange はメッセージの Sender ID の状態を含めずに、メッセージの処理を続行します。メッセージが破棄されたり拒否されたりすることはありません。このシナリオでは、Sender ID の状態は設定されず、アプリケーション イベントがログに出力されます。

メッセージに Sender ID の状態を表示する方法の詳細については、「[スパム対策スタンプ](anti-spam-stamps-exchange-2013-help.md)」を参照してください。

## スプーフィングされたメールと到達できない DNS サーバーを処理するための Sender ID のオプション

スプーフィングされたメールとして識別されたメッセージを Exchange サーバーで処理する方法と、DNS サーバーに到達できない場合に Exchange サーバーでメッセージを処理する方法も定義できます。スプーフィングされたメールと、DNS サーバーに到達できない状況に Exchange サーバーで対処する方法として、以下の処理を選択できます。

  - **Stamp the status**   このオプションは既定の処理です。組織へのすべての受信メッセージは、メッセージのメタデータ中に Sender ID の状態が設定されます。

  - **Reject**   このオプションはメッセージを拒否し、送信側サーバーに SMTP エラー応答を返します。SMTP エラー応答は 5*xx* レベルのプロトコル応答で、テキストは Sender ID の状態に対応しています。

  - **Delete**   このオプションは、送信側システムに通知せずにメッセージを削除します。実際には、Exchange サーバーは偽の OK SMTP コマンドを送信側サーバーに送信してからメッセージを削除します。送信側サーバーはメッセージが送信されたと見なすため、同じセッションでメッセージの送信を再試行しません。

Sender ID エージェントを構成する方法の詳細については、「[送信者 ID の管理](manage-sender-id-exchange-2013-help.md)」を参照してください。

ページのトップへ

## Sender ID をサポートするようにインターネットに直接接続された組織の DNS を更新する

Sender ID の効果は、特定の DNS データに依存しています。インターネットに直接接続された DNS サーバーを SPF レコードを使用して更新する組織が多くなるほど、Sender ID はスプーフィングされた電子メール メッセージをより効果的に識別できるようになります。

Sender ID インフラストラクチャをサポートするために、SPF レコードを作成し、パブリック DNS サーバーで SPF レコードをホストしている DNS のインターネットに接続するデータを更新する必要があります。作成し、SPF レコードを展開する方法の詳細については、[送信者 ID](https://go.microsoft.com/fwlink/p/?linkid=50977)を参照してください。

ページのトップへ

## Sender ID フィルターの対象外にする受信者および送信者ドメインを指定する

Sender ID フィルターから特定の受信者および送信者ドメインを除外できます。これを行うには、Exchange 管理シェルで **Set-SenderIdConfig** コマンドレットを使用して、受信者と送信者のドメインを指定します。詳細については、「[Set-SenderIdConfig](https://technet.microsoft.com/ja-jp/library/aa998859\(v=exchg.150\))」を参照してください。

ページのトップへ

