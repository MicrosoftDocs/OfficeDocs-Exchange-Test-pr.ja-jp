﻿---
title: 'リモート ドメイン: Exchange 2013 Help'
TOCTitle: リモート ドメイン
ms:assetid: 10fb7d62-4d78-40a3-82db-d62bcd27ba42
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa996309(v=EXCHG.150)
ms:contentKeyID: 49895253
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# リモート ドメイン

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-07_

リモート ドメイン エントリを作成して、Microsoft Exchange Server 2013 組織と、Exchange 組織の外側にあるドメインとの間でメッセージを転送するための設定を定義できます。リモート ドメイン エントリを作成するときは、そのドメインに対して送信されるメッセージの種類を制御します。また、組織内のユーザーからリモート ドメインに送信されるメッセージのメッセージ形式ポリシーやそのメッセージに使用できる文字セットを適用することもできます。リモート ドメインの設定は、Exchange 組織のグローバル構成設定です。

リモート ドメイン設定は、メールボックス サーバー上のトランスポート サービスでの分類中にメッセージに適用されます。受信者の解決時に、受信者ドメインは構成済みのリモート ドメインと照合されます。リモート ドメインの構成で特定のメッセージの種類がそのドメイン内の受信者に送信されないようになっている場合、そのメッセージは削除されます。リモート ドメインに対して特定のメッセージ形式を指定すると、メッセージのヘッダーと内容は変更されます。これらの設定は、Exchange 組織で処理されるすべてのメッセージに適用されます。


> [!NOTE]
> メッセージの設定をユーザーごとに構成すると、このユーザーごとの設定が組織の構成より優先されます。



既定では、単一のリモート ドメイン エントリが存在します。ドメインのアドレス スペースは、アスタリスク (\*) として構成されています。これは、すべてのリモート ドメインを指します。追加のリモート ドメイン エントリを作成していない場合は、すべてのリモート ドメインのすべての受信者に送信されるすべてのメッセージに同じ設定が適用されます。

リモート ドメインの構成時には、特定の種類のメッセージがそのドメインに送信されないようにすることができます。これらのメッセージの種類には、不在メッセージ、自動返信メッセージ、配信不能レポート (NDR)、会議出席依頼の転送通知などがあります。複数のフォレスト環境の場合は、このような種類のメッセージをそれらのドメインに送信できるようにする必要があることもあります。ただし、スパムの発信元であるドメインを特定した場合は、このような種類のメッセージをそれらのリモート ドメインに送信できないようにする必要があります。

**目次**

メッセージ形式

自動返信設定

NDR 情報の制御

## メッセージ形式

リモート ドメインに送信される電子メール メッセージに使用するメッセージ形式や文字セットを指定することができます。これらの設定は、ドメイン内の送信者からリモート ドメインに送信される電子メールと、受信側の電子メール システムとの互換性を確保するために役立ちます。たとえば、リモート ドメインのメッセージング システムが Exchange であるとわかっている場合は、常に Exchange リッチ テキスト形式 (RTF) を使用するように指定できます。詳細については、「[コンテンツ変換](content-conversion-exchange-2013-help.md)」を参照してください。

## 自動返信設定

Exchange 2013 では、ユーザーが内部および外部の受信者に対してさまざまな自動返信を指定できます。さらに、組織で使用できる自動返信の種類は、使用中の Microsoft Outlook バージョンによって決まります。

Exchange 2013 では、次の 2 種類の自動返信があります。

  - <strong>\[外部\]</strong>Exchange 2013 および Exchange 2010 でサポートされます。Outlook 2010 または Office Outlook 2007 で設定できるか、Microsoft Office Outlook Web App を使用して設定できます。

  - <strong>\[内部\]</strong>Exchange 2013 および Exchange 2010 でサポートされます。Outlook 2010 または Outlook 2007 で設定できるか、Outlook Web App を使用して設定できます。

以下の表は、さまざまなクライアントとサーバーの組み合わせと、各シナリオで使用できる自動返信の種類を示します。

**自動返信に対するクライアントとサーバーのサポート**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>クライアント バージョン</th>
<th>Exchange のバージョン</th>
<th>サポートされる自動返信</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2010 またはOutlook 2007</p></td>
<td><p>Exchange 2013Exchange 2010Exchange 2007</p></td>
<td><p>内部、外部</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App</p></td>
<td><p>Exchange 2013Exchange 2010Exchange 2007</p></td>
<td><p>内部、外部</p></td>
</tr>
</tbody>
</table>


## NDR 情報の制御

最初に説明したように、NDR がリモート ドメインに送信されないようにできます。NDR がリモート ドメインに送信されるのをブロックすることにより、NDR メッセージ内に含まれている情報が組織から発信されないようにし、結果的に悪意を持つユーザーが組織に関して取得できる知識を制限できます。ただし、これによって、正当な送信者も NDR を受信できなくなり、混乱と生産性の低下が生じます。

Exchange 2013 では、リモート ドメイン宛の NDR のコンテンツを詳細に制御できます。Exchange 2013 では、診断情報を削除する一方で、リモート ドメインへの NDR の送信を許可できます。このため、Exchange 展開に関する情報が組織から発信されないようにすると同時に、NDR 通知を外部の送信者に送信できます。

この機能は、**Set-RemoteDomain** コマンドレットの *NDRDiagnosticInfoEnabled* パラメーターで制御されます。この設定はリモート ドメインごとに構成できるため、ニーズに基づいて設定を変えることができます。たとえば、既定のリモート ドメインの NDR 診断情報は削除するが、パートナーを表すリモート ドメインに対しては完全な NDR 診断情報を許可できます。

この新しい設定の詳細については、「[Set-RemoteDomain](https://technet.microsoft.com/ja-jp/library/aa997857\(v=exchg.150\))」を参照してください。
