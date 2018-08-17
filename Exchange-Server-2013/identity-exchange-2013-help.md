---
title: 'ID: Exchange 2013 Help'
TOCTitle: ID
ms:assetid: e90fae91-37e7-4fdc-9170-44f0dc965c66
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb125042(v=EXCHG.150)
ms:contentKeyID: 49129858
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# ID

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-04_

*Identity* パラメーターは、ほとんどのコマンドレットと共に使用できる特殊なパラメーターです。*Identity* パラメーターを使用すると、MicrosoftExchange Server 2013 の特定のオブジェクトを参照する一意の識別子にアクセスできます。この機能により、ユーザーは特定の Exchange 2013 オブジェクトに対する処理を実行できます。

次のセクションでは、Identity パラメーター、およびこのパラメーターの効果的な使用例について説明します。

Characteristics of the Identity parameter

Wildcard characters in Identity

Examples of the Identity parameter

## Identity パラメーターの特徴

Exchange 2013 のオブジェクトの主要な一意の識別子は常に GUID です。GUID は `63d64005-42c5-4f8f-b310-14f6cb125bf3` のような 128 ビットの識別子です。この GUID が繰り返して使用されることはないため、常に一意になります。しかし、このような GUID を頻繁に入力するのは煩雑です。このため、*Identity* パラメーターは、通常、他のパラメーターの値、または 1 つのオブジェクトの複数のパラメーターの値の組み合わせで構成されます。また、これらの値はオブジェクト セットの中で一意であることが保証されています。*Name* および *DistriguishedName* などの、これらの他のパラメーターの値は、指定またはシステムによる生成が可能です。使用する追加パラメーター (該当する場合) およびその作成方法は、参照するオブジェクトにより異なります。

*Identity* パラメーターは、位置パラメーターとも見なされます。パラメーター ラベルが指定されていない場合、コマンドレットの最初の引数が *Identity* パラメーターと見なされます。このため、コマンド入力時のキー操作を少なくすることができます。位置パラメーターの詳細については、「[パラメーター](https://technet.microsoft.com/ja-jp/library/bb124388\(v=exchg.150\))」を参照してください。

次の例では、受信コネクタの一意の *Name* パラメーター値を使用して、*Identity* パラメーターを使用する方法を示しています。また、この例は、*Identity* が位置パラメーターであるため、*Identity* パラメーター名を省略できる方法も示しています。

    Get-ReceiveConnector -Identity "From the Internet"
    Get-ReceiveConnector "From the Internet"

Exchange 2013 のすべてのオブジェクトと同様、受信コネクタは一意の GUID で参照することもできます。たとえば、`"From the Internet"` という名前の受信コネクタが GUID `63d64005-42c5-4f8f-b310-14f6cb125bf3` も割り当てられている場合、次のコマンドを使用して受信コネクタを取得することもできます。

    Get-ReceiveConnector 63d64005-42c5-4f8f-b310-14f6cb125bf3

ページのトップへ

## Identity のワイルドカード文字

**Get** コマンドレットの中には、コマンドレットの実行時に、ワイルドカード文字 (`*`) を *Identity* に発信する値の一部として受け付けられるものがあります。*Identity* パラメーターでワイルドカード文字を使用すると、名前の一部を指定してこれに一致するオブジェクトの一覧を取得できます。*Identity* 値の先頭または末尾にワイルドカード文字を入れることはできますが、文字列の途中にワイルドカード文字を入れることはできません。たとえば、`Get-Mailbox David*` および `Get-Mailbox *anders*` というコマンドは有効ですが、`Get-Mailbox Reb*ca` は有効なコマンドではありません。

**Get** コマンドレットによって、階層関係または親子関係で編成されている Exchange 2013 内のオブジェクトが取得される場合があります。この場合、自身の子オブジェクトも含む親オブジェクトのコレクションがある可能性があります。親子関係を持つオブジェクトには、`<parent>\<child>` の構文を持つ *Identity* が含まれている場合があります。

*Identity* パラメーターに `<parent>\<child>` の構文が含まれている場合、一部のコマンドレットでは、ワイルドカード文字 (\*) を使用して親または子の名前の全部または一部を置き換えられます。たとえば、すべての親オブジェクトで "Contoso" という名前の子オブジェクトをすべて検索する場合、`"*\Contoso"` という構文が使用できます。同様に、`"ServerA" ` という親オブジェクト以下にある、名前の一部に"Auth" が含まれている子オブジェクトをすべて検索する場合は、`"ServerA\Auth*"` という構文を使用できます。

すべてのコマンドではありませんが、一部のコマンドでは、コマンド実行時に Identity パラメーターの子の一部だけを指定できます。この操作を行う場合、コマンドレットはアクセス中の現在の親オブジェクトで既定となります。たとえば、"Contoso Receive Connector" という名前の受信コネクタが MBX1 と MBX2 に 2 個あるとします。MBX2 で `Get-ReceiveConnector "Contoso Receive Connector"` というコマンドを実行すると、MBX2 サーバー上の受信コネクタのみが返されます。

Identity パラメーターおよびワイルドカード文字の固有の動作は、実行中のコマンドレットに依存します。実行しているコマンドレットの詳細については、そのコマンドレットの機能固有のコンテンツを参照してください。

ページのトップへ

## Identity パラメーターの例

ここで説明した例は、Exchange 2013 組織の特定のオブジェクトを参照するために、*Identity* パラメーターがさまざまな一意の値を受け取ることができる方法を示しています。また、これらの例では、コマンド入力時に *Identity* パラメーター ラベルを省略して、キー操作数を減らす方法も示されています。

## DSN メッセージ

ここで説明する例は、Exchange 2013 組織で構成可能な配信状態通知 (DSN) メッセージを参照します。最初の例は、**Get-SystemMessage** コマンドレットを使用して、DSN 5.4.1 を取得する方法を示します。**Get-SystemMessage** コマンドレットでは、*Identity* パラメーターは 各 DSN メッセージ オブジェクトに構成された複数のデータで構成されます。これらの複数のデータには、DSN が記述されている言語、DSN がスコープの内部か外部か、および次の例のような DSN メッセージ コードが含まれます。

    Get-SystemMessage en\internal\5.4.1

また、Exchange 2013 のすべてのオブジェクトが GUID を持っているため、次の例のように GUID を使用して、この DSN メッセージを取得することもできます。

    Get-SystemMessage 82ca7bde-1c2d-4aa1-97e1-f298a6f10222

**SystemMessage** コマンドレットで使用される場合の *Identity* パラメーターの構成の詳細については、「[DSN メッセージ ID](dsn-message-identity-exchange-2013-help.md)」を参照してください。

## 管理役割エントリ

このセクションの例では、Exchange 2013 で管理役割を構成する管理役割のエントリを参照します。管理役割は、管理者およびエンド ユーザーに与えられるアクセス許可の制御に使用されます。管理役割のエントリは 2 つの部分から構成されます。関連付けられている管理役割とコマンドレット。Identity パラメーターも、同様に管理役割名およびコマンドレット名の両方で構成されます。たとえば、次は `Mail Recipients` 役割での **Set-Mailbox** コマンドレットの役割エントリです。

    Mail Recipients\Set-Mailbox

`Mail Recipients\Set-Mailbox` 役割エントリは、`Mail Recipients` 役割にいくつかあるエントリのうちの 1 つです。`Mail Recipients` 役割のすべての役割エントリを表示するには、次のコマンドを使用します。

    Get-ManagementRoleEntry "Mail Recipients\*"

"`Mailbox`" という文字列を含む `Mail Recipients` 役割のすべての役割エントリを表示するには、次のコマンドを使用します。

    Get-ManagementRoleEntry "Mail Recipients\*Mailbox*"

**Set-Mailbox** が役割エントリの 1 つとなっている管理役割をすべて表示するには、次のコマンドを使用します。

    Get-ManagementRoleEntry *\Set-Mailbox

役割エントリによって、ワイルドカード文字をさまざまな方法で使用し、Exchange 2013 を照会して必要な情報を入手できます。

管理役割の詳細については、「[管理の役割について](understanding-management-roles-exchange-2013-help.md)」を参照してください。

ページのトップへ

