﻿---
title: 'ピックアップ ディレクトリと再生ディレクトリ: Exchange 2013 Help'
TOCTitle: ピックアップ ディレクトリと再生ディレクトリ
ms:assetid: ae191700-953f-411c-906f-dc90feec3d5a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124230(v=EXCHG.150)
ms:contentKeyID: 49896415
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ピックアップ ディレクトリと再生ディレクトリ

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

既定では、ピックアップ ディレクトリおよび再生ディレクトリは各 Microsoft Exchange Server 2013 メールボックス サーバーまたはエッジ トランスポート サーバーに存在します。正しい形式の電子メール メッセージ ファイルをピックアップ ディレクトリまたは再生ディレクトリにコピーすると、そのメッセージ ファイルが配信のために送信されます。ピックアップ ディレクトリは、管理者がメール フローのテストに使用したり、独自のメッセージを作成して送信したりする必要があるアプリケーションが使用します。再生ディレクトリは、外部ゲートウェイ サーバーからメッセージを受信し、管理者が Exchange サーバーのキューからエクスポートするメッセージを再送信するのにも使用できます。

**目次**

電子メール メッセージ ファイルの詳細

ピックアップ ディレクトリおよび再生ディレクトリのメッセージ処理方法

ピックアップ ディレクトリのメッセージ ファイルの要件

ピックアップ ディレクトリのメッセージ ヘッダーの変更

再生ディレクトリのメッセージ ファイルの要件

再生ディレクトリのメッセージ ヘッダーの変更

ピックアップディレクトリおよび再生ディレクトリのメッセージ処理の失敗

ピックアップ ディレクトリおよび再生ディレクトリに関するセキュリティ上の考慮事項

ピックアップ ディレクトリおよび再生ディレクトリに対するアクセス許可

## 電子メール メッセージ ファイルの詳細

標準的な SMTP 電子メール メッセージは、*メッセージ エンベロープ*とメッセージのコンテンツで構成されます。メッセージ エンベロープには、メッセージの転送と配信に必要な情報が含まれます。メッセージのコンテンツには、総称して "*メッセージ ヘッダー*" と呼ばれるメッセージ ヘッダー フィールドと、メッセージ本文があります。メッセージ エンベロープは RFC 2821 で定義され、メッセージ ヘッダーは RFC 2822 で定義されます。

送信者が電子メール メッセージを作成し、配信のために送信した段階でメッセージに含まれるのは、SMTP 標準に準拠するために必要な基本的な情報 (送信者、受信者、メッセージの作成日時、省略可能な件名、省略可能なメッセージ本文など) です。この情報は、メッセージ自体 (定義上はメッセージ ヘッダー) に含まれます。

送信者のメッセージング サーバーは、メッセージ ヘッダーで見つかった送信者と受信者の情報を使用してメッセージのメッセージ エンベロープを生成し、受信者のメッセージング サーバーに配信するためにメッセージをインターネットに送信します。メッセージ エンベロープはメッセージ送信プロセスによって生成されるものであり、実際にはメッセージの一部ではないため、受信者がメッセージ エンベロープを目にすることはありません。

メッセージの送信に関与する各サーバーによって、メッセージの配信におけるサーバーの役割に関連するメッセージ ヘッダー フィールドや、その他のアプリケーション固有のメッセージ ヘッダー フィールドがメッセージ ヘッダーに挿入される場合もあります。受信者が電子メール クライアントを使用してメッセージを開くと、メッセージ ヘッダーの情報のうち、送信者、受信者、件名などの比較的関連性の高い情報が、メッセージ本文と共に表示されます。

ページのトップへ

## ピックアップ ディレクトリおよび再生ディレクトリのメッセージ処理方法

Exchange 2013 では、ピックアップ ディレクトリの既定の場所は `%ExchangeInstallPath%TransportRoles\Pickup` です。再生ディレクトリの既定の場所は `%ExchangeInstallPath%TransportRoles\Replay` です。適切な書式が設定され、ピックアップ ディレクトリまたは再生ディレクトリにコピーされた .eml メッセージ ファイルは、次の手順で送信用に処理されます。

1.  ピックアップ ディレクトリおよび再生ディレクトリでは新しいメッセージ ファイルの有無が 5 秒ごとに確認されます。このポーリング間隔は変更できません。メッセージ ファイルの処理速度は、**Set-TransportService** コマンドレットの *PickupDirectoryMaxMessagesPerMinute* パラメーターを使用して調整することができます。このパラメーターは、ピックアップ ディレクトリと再生ディレクトリに影響します。既定値は 1 分あたり 100 メッセージです。開くことのできないファイルはピックアップ ディレクトリに残り、次のポーリング時に再評価されます。

2.  ピックアップ ディレクトリのメッセージ ファイルに適用される制限 (最大ヘッダー サイズ、受信者の最大数など) が確認されます。既定では、最大ヘッダー サイズは 64 KB、受信者の最大数は 100 です。**Set-TransportService** コマンドレットを使用して、これらの制限を変更できます。これらの設定は、ピックアップ ディレクトリだけに影響します。

3.  ファイル名が *\<filename\>*.eml から *\<filename\>*.tmp に変更されます。*\<filename\>*.tmp ファイルが既に存在する場合は、*\<filename\>\<datetime\>*.tmp に変更されます。ファイル名の変更に失敗した場合はイベント ログにエラーが生成されて、ピックアップ プロセスは次のファイルに進みます。

4.  .tmp ファイルが電子メール メッセージに正しく変換されると, .tmp ファイルに対して **delete on close** コマンドが発行されます。.tmp ファイルはピックアップ ディレクトリに残っているように見えますが、そのファイルを開くことはできません。

5.  メッセージが配信用のキューに登録されたら、**close** コマンドが発行され, .tmp ファイルはピックアップ ディレクトリから削除されます。削除に失敗した場合は、イベント ログにエラーが生成されます。ピックアップ ディレクトリに .tmp ファイルが残っている状態で Microsoft Exchange トランスポート サービスが再起動されると、すべての .tmp ファイルの名前が .eml ファイルに変更されて再処理されます。この場合は、メッセージ転送が重複する可能性があります。

ページのトップへ

## ピックアップ ディレクトリのメッセージ ファイルの要件

ピックアップ ディレクトリにコピーされたメッセージ ファイルが正しく配信されるためには、ファイルが次の要件を満たしている必要があります。

  - メッセージ ファイルは、基本的な SMTP メッセージ形式に準拠するテキスト ファイルである必要があります。MIME メッセージ ヘッダー フィールドとコンテンツがサポートされます。

  - メッセージ ファイルのファイル名には, .eml 拡張子が付いている必要があります。

  - メッセージ ヘッダーの `Sender` または `From` メッセージ ヘッダー フィールドには、電子メール アドレスが少なくとも 1 つ存在する必要があります。`Sender` と `From` の両方のフィールドに 1 つの電子メール アドレスが存在する場合は、`From` フィールドの電子メール アドレスがメッセージの発信者としてメッセージ エンベロープで使用されます。

  - `Sender` フィールドに存在できる電子メール アドレスは 1 つだけです。複数の電子メール アドレスは許可されません。`Sender` フィールドに存在する電子メール アドレスが 1 つだけの場合、`From` フィールドは任意です。

  - `From` フィールドでは複数の電子メール アドレスが許可されますが、`Sender` フィールドにも電子メール アドレスが 1 つ存在する必要があります。その `Sender` フィールドのアドレスが、メッセージの発信者としてメッセージ エンベロープで使用されます。

  - `To`、`Cc`、または `Bcc` のいずれかのフィールドに、電子メール アドレスが少なくとも 1 つ存在する必要があります。

  - メッセージ ヘッダーとメッセージ本文の間に空白行が存在する必要があります。

この例では、ピックアップ ディレクトリで受け入れ可能な形式を使用しているテキスト メッセージを示します。

  ```XML
  To: mary@contoso.com
  From: bob@fabrikam.com
  Subject: Message subject
    
  This is the body of the message.
  ```

ピックアップ ディレクトリのメッセージ ファイルでは、MIME コンテンツもサポートされています。MIME では、7 ビットの ASCII テキストでは表現できない言語、HTML、その他のマルチメディア コンテンツなど、広範なメッセージのコンテンツが定義されています。MIME の詳細な説明とその要件に関しては、ここでは扱いません。この例では、ピックアップ ディレクトリで受け入れ可能な形式を使用している単純な MIME メッセージを示します。

  ```XML
  To: mary@contoso.com
  From: bob@fabrikam.com
  Subject: Message subject
  MIME-Version: 1.0
  Content-Type: text/html; charset="iso-8859-1"
  Content-Transfer-Encoding: 7bit
    
  <HTML><BODY>
  <TABLE>
  <TR><TD>cell 1</TD><TD>cell 2</TD></TR>
  <TR><TD>cell 3</TD><TD>cell 4</TD></TR>
  </TABLE>

  </BODY></HTML>
```

ページのトップへ

## ピックアップ ディレクトリのメッセージ ヘッダーの変更

ピックアップ ディレクトリでは、次のメッセージ ヘッダー フィールドがメッセージ ヘッダーからすべて削除されます。

  - `Received`

  - `Resent-*`

  - `Bcc`
    

    > [!NOTE]
    > メッセージ ヘッダーの省略可能な <CODE>Bcc</CODE> メッセージ ヘッダー フィールドで見つかった電子メール アドレスはすべて正しく処理されます。<CODE>Bcc</CODE> の受信者は、不可視のメッセージ エンベロープ受信者に昇格された後、ID 保護のためにメッセージ ヘッダーから削除されます。メッセージに <CODE>Bcc</CODE> 受信者しか指定されていない場合は、メッセージ ヘッダーの <CODE>To</CODE> フィールドに <STRONG>Undisclosed Recipients</STRONG> という値が追加されます。



ピックアップ ディレクトリでは、メッセージ送信プロセスの一環として、独自の `Received` ヘッダー フィールドがメッセージに追加されます。`Received` ヘッダー フィールドは次の形式で適用されます。

  ```XML
  Received: from localhost by Pickup with Microsoft SMTP Server id <ExchangeServerVersion><datetime>
  ```

ピックアップ ディレクトリでは、次のメッセージ ヘッダー フィールドが存在しない場合または正しくない場合に、次のような変更が加えられます。

  - **Message-Id**   `Message-Id` フィールドが欠落しているか空白である場合、ピックアップ ディレクトリでは *\<GUID\>*@*\< 既定のドメイン\>* という形式を使用して、Message-Id フィールドが追加されます。

  - **Date**   `Date` フィールドが存在しない場合または正しくない場合は、ピックアップ ディレクトリによるメッセージ処理の日時が追加されます。

ページのトップへ

## 再生ディレクトリのメッセージ ファイルの要件

再生ディレクトリは、エクスポートされた Exchange メッセージの再送信とメッセージの外部ゲートウェイ サーバーからの受信に使用されます。これらのメッセージは、再生ディレクトリ用にあらかじめ書式設定されています。管理者や他のアプリケーションが再生ディレクトリを使用することにより、新しいメッセージ ファイルを作成して送信する必要はほとんどありません。新しいメッセージ ファイルを作成して送信するには、ピックアップ ディレクトリを使用します。

再生ディレクトリ メッセージは *X-Header* を最大限に活用します。X-Header は、メッセージ ヘッダーに含まれている、ユーザー定義の非公式なメッセージ ヘッダー フィールドです。X-Header は RFC 2822 で具体的に記述されているわけではありませんが、"X-" で始まる未定義のメッセージ ヘッダー フィールドの使用は、メッセージに非公式なメッセージ ヘッダー フィールドを追加する方法として受け入れられています。再生ディレクトリ内のメッセージ ファイルで使用される Exchange 固有の X-Header によって、通常はメッセージ エンベロープ内に存在する配信情報を実際に設定できます。この機能は、再生ディレクトリを使用して、別の Exchange サーバーからエクスポートされたメッセージを処理するときに、元のメッセージ情報を保持するために必要になります。

再生ディレクトリにコピーされたメッセージ ファイルが正しく配信されるためには、ファイルが次の要件を満たしている必要があります。

  - メッセージ ファイルは、基本的な SMTP メッセージ形式に準拠するテキスト ファイルである必要があります。MIME メッセージ ヘッダー フィールドとコンテンツがサポートされます。

  - メッセージ ファイルのファイル名には, .eml 拡張子が付いている必要があります。

  - X-Header は、すべての通常のヘッダー フィールドの前に付いている必要があります。

  - ヘッダー フィールドとメッセージ本文の間に空白行が存在する必要があります。

次に示す X-Header は、再生ディレクトリ内にあるメッセージの必須のフィールドです。

  - **X-Sender**   この X-Header は、標準の SMTP メッセージ内の `From` メッセージ ヘッダー フィールド要件に替わります。1 つの電子メール アドレスを含む 1 つの `X-Sender` フィールドが存在する必要があります。`From` メッセージ ヘッダー フィールドがある場合、再生ディレクトリはこれを無視します。ただし、受信者の電子メール クライアントには、メッセージの送信者として `From` メッセージ ヘッダー フィールドの値が表示されます。次の例で示すように、他のパラメーターは通常、`X-Sender` フィールドに存在します。
    
    ```XML
    X-Sender: <bob@fabrikam.com> BODY=7bit RET=HDRS ENVID=12345ABCD auth=<someAuth>
    ```
    

    > [!NOTE]
    > これらのパラメーターは、通常は送信側サーバーによって生成されるメッセージ エンベロープ値です。エクスポートされたメッセージ ファイルには、これに似たパラメーターが含まれることがあります。<BR><CODE>RET</CODE> には、メッセージを配信できない場合、送信者にメッセージ全体を戻すか、ヘッダーのみを戻すかを指定します。<CODE>RET</CODE> に指定できる値は、<CODE>HDRS</CODE> または <CODE>FULL</CODE> です。<CODE> ENVID</CODE> は、メッセージ エンベロープの識別子です。<CODE>BODY</CODE> には、メッセージのテキスト エンコーディングを指定します。<CODE>auth</CODE> には、RFC 2554 に定義されている認証機構をメッセージング サーバーに対して指定します。



  - **X-Receiver**   この X-Header は、標準の SMTP メッセージ内の `To` メッセージ ヘッダー フィールド要件に替わります。1 つの電子メール アドレスを含む 1 つ以上の `X-Receiver` フィールドが存在する必要があります。複数の受信者がいる場合は、複数の `X-Receiver` フィールドを含めることができます。`To` メッセージ ヘッダー フィールドがある場合、再生ディレクトリはこれを無視します。ただし、受信者の電子メール クライアントには、メッセージの受信者として `To` メッセージ ヘッダー フィールドの値が表示されます。次の例で示すように、他の省略可能なパラメーターが、`X-Receiver` フィールドに存在することがあります。
    
      ```XML
      X-Receiver: <mary@contoso.com> NOTIFY=NEVER ORcpt=mary@contoso.com
      ```
    

    > [!NOTE]
    > これらのパラメーターは、通常は送信側サーバーによって生成されるメッセージ エンベロープ値です。エクスポートされたメッセージ ファイルを開くと、このようなパラメーターを見かけることがあります。これらのパラメーターは、RFC 1891 に記述されている配信状態通知 (DSN) メッセージに関連するものです。<BR><CODE>NOTIFY</CODE> は、<CODE>NEVER</CODE>、<CODE>DELAY</CODE>、<CODE>FAILURE</CODE> いずれかの値を取ることができます。<CODE>ORcpt</CODE> は、メッセージの元の受信者を保持します。



次に示す X-Header は、再生ディレクトリ内のメッセージ ファイル用のフィールドです。これらは省略可能です。

  - **X-CreatedBy**   ヘッダー ファイアウォール機能に対して使用されます。この X-Header が存在する場合、このフィールドを空白にすることはできません。`X-CreatedBy` フィールドが存在しない場合は、**Unspecified** という値を使用してこのフィールドが追加されます。通常、このフィールドの値は **MSExchange15** ですが、 **Notes** など、送信コネクタで設定されている、SMTP 以外の種類のアドレス スペースを含めることもできます。

  - **X-EndOfInjectedXHeaders**   存在しているすべての X-Header のサイズ (バイト単位) です。この X-Header は、通常のメッセージ ヘッダー フィールドが始まる直前の X-Header フィールドを示すマーカーとして使用されることがあります。

  - **X-ExtendedMessageProps**   メッセージの拡張メッセージ プロパティです。

  - **X-HeloDomain**   最初の SMTP プロトコル通信中に表示される HELO/EHLO ドメイン文字列です。

  - **X-Source** **MessageSourceName** 列の下でキュー ビューアーによって使用されます。この X-Header の値が指定されない場合、 **Replay** という値が使用されます。X-Header のその他の可能な値は、**Smtp Receive Connector** および **Smtp Send Connector**です。

  - **X-SourceIPAddress**   送信側サーバーの IP アドレスです。IP アドレスが指定されない場合、このフィールドは `0.0.0.0` になります。

この例では、再生ディレクトリで受け入れ可能な形式を使用しているテキスト メッセージを示します。

  ```XML
  X-Receiver: <mary@contoso.com> NOTIFY=NEVER ORcpt=mary@contoso.com
  X-Sender: <bob@fabrikam.com> BODY=7bit ENVID=12345AB auth=<someAuth>
  Subject: Optional message subject
    
  This is the body of the message.
  ```

再生ディレクトリ メッセージ ファイルでは MIME コンテンツもサポートされます。MIME では、7 ビットの ASCII テキストでは表現できない言語、HTML、その他のマルチメディア コンテンツなど、広範なメッセージのコンテンツが定義されています。MIME の詳細な説明とその要件に関しては、ここでは扱いません。この例では、再生ディレクトリで受け入れ可能な形式を使用している単純な MIME メッセージを示します。

  ```XML
  X-Receiver: <mary@contoso.com> NOTIFY=NEVER ORcpt=mary@contoso.com
  X-Sender: <bob@fabrikam.com> BODY=7bit ENVID=12345ABCD auth=<someAuth>
  To: mary@contoso.com
  From: bob@fabrikam.com
  Subject: Optional message subject
  MIME-Version: 1.0
  Content-Type: text/html; charset="iso-8859-1"
  Content-Transfer-Encoding: 7bit
   
  <HTML><BODY>
  <TABLE>
  <TR><TD>cell 1</TD><TD>cell 2</TD></TR>
  <TR><TD>cell 3</TD><TD>cell 4</TD></TR>
  </TABLE>

  </BODY></HTML>
  ```

ページのトップへ

## 再生ディレクトリのメッセージ ヘッダーの変更

再生ディレクトリでは、メッセージ ファイルから `Bcc` メッセージ ヘッダー フィールドが削除されます。

再生ディレクトリでは、メッセージ送信プロセスの中で、独自の `Received` メッセージ ヘッダー フィールドがメッセージに追加されます。Received メッセージ ヘッダー フィールドは次の形式で適用されます。

  ```XML
  Received: from <ReceivingServerName> by Replay with <ExchangeServerVersion><DateTime>
  ```

再生ディレクトリでは、メッセージ ヘッダー内の次のメッセージ ヘッダー フィールドが変更されます。

  - **Message-Id**   このメッセージ ヘッダー フィールドが欠落しているか空白である場合、再生ディレクトリでは *\<GUID\>*@*\<既定のドメイン\>* という形式を使用して、Message-Id フィールドが追加されます。

  - **Date**   このメッセージ ヘッダー フィールドが欠落しているか形式に誤りがある場合、再生ディレクトリでは、再生ディレクトリによるメッセージの処理日時を使用して Date メッセージ ヘッダー フィールドが追加されます。

ページのトップへ

## ピックアップディレクトリおよび再生ディレクトリのメッセージ処理の失敗

ピックアップ ディレクトリまたは再生ディレクトリにコピーされたメッセージ ファイルを配信のためにキューに入れる処理が正しく行われない場合があります。発生する可能性があるメッセージ送信エラーには、次のカテゴリがあります。

  - **配信エラー**   有効な送信者を持つ正しい形式のメッセージ ファイルを、ピックアップ ディレクトリで配信のために正しく送信できない場合は、配信不能レポート (NDR) が生成されます。内容の形式が正しくない場合や、ピックアップ ディレクトリ メッセージ制限に違反している場合も、NDRとなる場合があります。メッセージ処理の間に NDR が生成されると、元のメッセージ ファイルが NDR メッセージに添付され、ピックアップ ディレクトリまたは再生ディレクトリからそのメッセージ ファイルが削除されます。
    

    > [!NOTE]
    > トランスポート パイプラインに送信された正しい形式のメッセージが、その後の配信エラーによって、NDR と共に送信者に返される場合もあります。この種のエラーは、メッセージング サーバーの障害やメッセージの配信パスでのルーティング エラーなど、ピックアップ ディレクトリまたは再生ディレクトリとは無関係の送信の問題によって発生します。



  - **不正メール** *不正メール*に分類されるメッセージは、重大な問題があるためにピックアップ ディレクトリまたは再生ディレクトリで配信のために送信することができないメッセージです。また、メッセージの形式は正しいが受信者が有効ではなく、送信者も有効ではないために NDR メッセージを送信できない場合も、不正メールになります。
    
    不正メールと判別されたメッセージ ファイルは、名前が *\<filename\>*.eml から *\<filename\>*.bad に変更されて、ピックアップ ディレクトリまたは再生ディレクトリに残ります。*\<filename\>*.bad ファイルが既に存在する場合、ファイル名は *\<filename\>\<datetime\>*.bad に変更されます。ピックアップ ディレクトリまたは再生ディレクトリに不正メールが存在する場合は、イベント ログにエラーが生成されます。ただし、同じ不正メール メッセージに対して繰り返し生成されることはありません。
    

    > [!NOTE]
    > メッセージ ファイルは常に、別の場所で作成と保存を行ってから、配信のためにピックアップ ディレクトリにコピーするようにしてください。ピックアップ ディレクトリでは、5&nbsp;秒ごとに新しいメッセージのポーリングが行われます。このため、ピックアップ ディレクトリ自体でメッセージ ファイルの作成と保存を行うと、メッセージの作成が完了する前にメッセージ ファイルがピックアップ ディレクトリによって処理されてしまう可能性があります。



ページのトップへ

## ピックアップ ディレクトリおよび再生ディレクトリに関するセキュリティ上の考慮事項

次の一覧は、ピックアップ ディレクトリと再生ディレクトリに共通するセキュリティ上の問題です。

  - 受信コネクタで構成されているセキュリティ チェック (スパム対策、マルウェア対策、送信者フィルター、受信者フィルターの動作など) は、ピックアップ ディレクトリや再生ディレクトリを通じて送信されるメッセージに対しては実行されません。

  - 侵害されたピックアップ ディレクトリや再生ディレクトリが第三者中継として機能する可能性があります。これにより、別のサーバーを使って実際のメッセージの送信元を隠すことで、メッセージを再送信または *中継* することができます。

次の一覧は、再生ディレクトリに当てはまるセキュリティ上のさらなる問題です。

  - 再生ディレクトリで使用される X-Header を使用すると、メッセージ エンベロープを手動で作成することができます。`X-Sender` および `X-Receiver` フィールドの情報は、電子メール クライアントで表示される `To` または `From` メッセージ ヘッダー フィールドとはまったく異なる場合があります。このような送信者やドメインのなりすましは、多くの場合、*スプーフィング*と呼ばれます。*なりすましメール*は、メッセージの実際の送信者とは別の送信者から発信されたように見せるために送信者アドレスが変更された電子メール メッセージです。

  - `X-CreatedBy` フィールドの値が **MSExchange15** である場合、送信先は信頼できると見なされ、ヘッダー ファイアウォールは適用されません。*Header firewall* は、信頼できる Exchange サーバー間で転送されるメッセージ内の X-Header を保存したり、Exchange 組織外部の信頼できない送信先に転送されるメッセージから、情報漏洩の可能性がある X-Header を削除したりするための Exchange の手段です。これらの X-Header は、権限のある Exchange サーバー間の SCL (Spam Confidence Level)、メッセージの署名、暗号化などの Exchange 情報を共有するために使用されることがあります。権限のない送信元にこの情報が漏れると、セキュリティ上のリスクを抱える可能性があります。ヘッダー ファイアウォールの詳細については、["ヘッダー ファイアウォールについて"](https://go.microsoft.com/fwlink/?linkid=268394)を参照してください。

再生ディレクトリに関連するセキュリティ リスクが多いので、再生ディレクトリに適用するセキュリティを強化する必要があります。メッセージの作成や送信を行う必要があるユーザーやアプリケーションに対しては、ピックアップ ディレクトリへのアクセスのみを許可し、再生ディレクトリへのアクセスは許可しないようにしてください。

すべてのメールボックス サーバーとエッジ トランスポート サーバーでは、既定で、ピックアップ ディレクトリと再生ディレクトリの両方が有効になっています。組織の特定のメールボックス サーバーまたはエッジ トランスポート サーバーでピックアップ ディレクトリまたは再生ディレクトリが必要ない場合は、そのサーバーのピックアップ ディレクトリまたは再生ディレクトリのパスを `$null` に設定することで無効にしてもかまいません。詳細については、「[ピックアップ ディレクトリと再生ディレクトリの構成](configure-the-pickup-directory-and-the-replay-directory-exchange-2013-help.md)」を参照してください。

ページのトップへ

## ピックアップ ディレクトリおよび再生ディレクトリに対するアクセス許可

ピックアップ ディレクトリおよび再生ディレクトリには次のアクセス許可が必要です。

  - 管理者: フル コントロール

  - システム :フル コントロール

  - Network Service: サブフォルダーとファイルの読み取り、書き込み、および削除

既定では、Microsoft Exchange トランスポート サービスは、ネットワーク サービス ユーザー アカウントのセキュリティ資格情報を使用してピックアップ ディレクトリおよび再生ディレクトリの場所とアクセス許可を管理します。ネットワーク サービス アカウントには, .eml ファイルを開いて名前を .tmp に変更して削除したり、メッセージが不正メールとして分類された場合に名前を .bad に変更したりするために、ピックアップ ディレクトリに対してこれらのアクセス許可が必要になります。

ピックアップ ディレクトリおよび再生ディレクトリの場所は、**Set-TransportService** コマンドレットの *PickupDirectoryPath* および *ReplayDirectoryPath* パラメーターを使用して移動することができます。ピックアップ ディレクトリの場所を正しく変更できるかどうかは、新しいディレクトリの場所でネットワーク サービス アカウントに付与されている権利と、新しいディレクトリが既に存在しているかどうかによって決まります。ディレクトリが存在しておらず、ネットワーク サービス アカウントが変更先の場所でフォルダーを作成してアクセス許可を適用するために必要な権利を持っている場合、ディレクトリが新規作成され、適切なアクセス許可が適用されます。新しいディレクトリが既に存在している場合は、既存のフォルダーのアクセス許可は確認されません。**Set-TransportService** コマンドレットで *PickupDirectoryPath* または *ReplayDirectoryPath* パラメーターを使用してディレクトリを移動する場合は、新しいディレクトリが存在し、正しいアクセス許可が適用されていることを常に確認してください。

ページのトップへ
