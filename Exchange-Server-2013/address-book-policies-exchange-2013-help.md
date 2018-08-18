---
title: 'アドレス帳ポリシー: Exchange Online Help'
TOCTitle: アドレス帳ポリシー
ms:assetid: d0a916a1-e3ed-49ae-b116-a559be0dcce6
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Hh529948(v=EXCHG.150)
ms:contentKeyID: 49896487
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# アドレス帳ポリシー

 

_**適用先:** Exchange Online, Exchange Server 2013_

グローバル アドレス一覧を特定のグループに分割して、Outlook および Outlook Web App でカスタマイズされた GAL を作成する方法について説明します。

グローバル アドレス一覧 (GAL) セグメンテーション (*GAL セグメンテーション*とも呼ばれる) は、管理者がユーザーを特定のグループに分割し、組織の GAL をカスタマイズ表示するためのプロセスです。アドレス帳ポリシー (ABP) では、ユーザーを特定のグループに分割し、組織のグローバル アドレス一覧 (GAL) をカスタマイズ表示することができます。ABP の作成時には、GAL、オフライン アドレス帳 (OAB)、会議室一覧、1 つ以上のアドレス一覧をポリシーに割り当てます。次に ABP をメールボックス ユーザーに割り当て、カスタマイズされた GAL にメールボックス ユーザーが Outlook と Outlook Web App でアクセスできるようにします。目標は、複数の GAL を必要とする社内組織で GAL セグメンテーションを完成するメカニズムを単純にすることです。


> [!NOTE]
> ABP は、各ユーザー グループの GAL およびアドレス一覧を最適化するためのものであり、ユーザー同士の表示や組織内の他のユーザーとの通信を困難にするものではありません。ABP は、法的な分離ではなく、ディレクトリの観点によるユーザーの仮想的な分離のみを行います。



**目次**

ABP の仕組み

ABP の例

Entourage、Outlook for Mac、および ABP

## ABP の仕組み

ABP には次の一覧が含まれます。

  - 1 つの GAL

  - 1 つの OAB

  - 1 つの会議室一覧 (予約目的)

  - 1 つまたは複数のアドレス一覧

次の図では、アドレス帳ポリシー A は、組織内のさまざまなアドレス オブジェクトのサブセット (図の下半分) から構成されています。結果的に、ABP の範囲は、ポリシーに含まれる GAL (この例では GAL1) の範囲と等しくなります。ABP が作成され、ユーザーに割り当てられると、ABP のアドレス オブジェクトは、ユーザーが閲覧できる範囲のオブジェクトになります。

![アドレス帳ポリシーの概要](images/Hh529948.68084064-7319-431b-be3b-0cce761258b1(EXCHG.150).gif "アドレス帳ポリシーの概要")

次の方法で ABP を個々のメールボックス ユーザーに割り当てることができます。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>新規/既存メールボックス</th>
<th>シェル</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>新規作成</p></td>
<td><p><em>AddressBookPolicy</em> パラメーターを指定した <a href="https://technet.microsoft.com/ja-jp/library/aa997663(v=exchg.150)">New-Mailbox</a> コマンドレット</p></td>
</tr>
<tr class="even">
<td><p>既存</p></td>
<td><p><em>AddressBookPolicy</em> パラメーターを指定した <a href="https://technet.microsoft.com/ja-jp/library/bb123981(v=exchg.150)">Set-Mailbox</a> コマンドレット</p>
<p></p></td>
</tr>
</tbody>
</table>


ABP が有効になるのは、ユーザーのクライアント アプリケーションが Exchange 2013 のクライアント アクセス サーバーに接続したときです。ABP を変更した場合は、ユーザーがクライアントを再起動または再接続するまで、または Exchange 2013 メールボックス サーバー上の RPC クライアント アクセス サーバーを再起動するまで、更新した ABP は有効になりません。

## アドレス帳ポリシー ルーティング エージェント

ABP を使用していない Exchange 組織の場合、Outlook または Outlook Web App で電子メールを作成し、同じ Exchange 組織内の別の受信者に送信すると、次のことが起こります。

1.  電子メール アドレスが解決されます。たとえば、<strong>宛先</strong> フィールドに「<strong>kweku@contoso.com</strong>」と入力すると、その SMTP 電子メール アドレスがユーザーの表示名 **Kweku Ako-Adjei** に解決されます。

2.  他のユーザーの連絡先カードを表示できます。名前が解決されると、ユーザー名をダブルクリックすることで、ユーザーのオフィスや電話番号などの連絡先情報を表示できます。

ABP を使用しており、個別の仮想組織内のユーザーにお互いの個人情報の可能性がある内容を表示したくない場合は、アドレス帳ポリシー ルーティング エージェントをオンにします。ABP ルーティング エージェントは、組織内で受信者がどのように解決されるかを制御するトランスポート エージェントです。ABP ルーティング エージェントがインストールおよび構成されると、異なる GAL を割り当てられたユーザーは外部受信者として表示されるようになり、この場合、外部受信者の連絡先カードは表示できません。

Exchange Online で ABP ルーティング エージェントを有効にする方法の詳細については、「[アドレス帳ポリシー ルーティング \[オンライン\] を有効にする](https://technet.microsoft.com/ja-jp/library/jj891095\(v=exchg.150\))」を参照してください。

Exchange Server で ABP ルーティング エージェントを有効にする方法については、「[アドレス帳ポリシー ルーティング エージェントをインストールおよび構成する](install-and-configure-the-address-book-policy-routing-agent-exchange-2013-help.md)」を参照してください。

## ABP の例

次の図では、Fabrikam 社と Tailspin Toys 社が同じ Exchange 組織と同じ CEO を共有しています。CEO は、両社に共通する唯一の従業員です。

![2 つの企業に一人の CEO](images/Hh529948.c87a5654-d456-4688-acb2-0be15ba1cda6(EXCHG.150).gif "2 つの企業に一人の CEO")

この構成には、3 つの ABP が含まれています。

  - 1 つには、Fabrikam 社の従業員と CEO が含まれています。

  - 1 つには、Tailspin Toys 社の従業員と CEO が含まれています。

  - 1 つには、CEO のみが含まれています。

ABP は、次のルールに従います。

  - Tailspin Toys 社のユーザーは、GAL を参照する際に Tailspin Toys 社の従業員および CEO のみを表示できる。

  - Fabrikam 社のユーザーは、GAL を参照する際に Fabrikam 社の従業員および CEO のみを表示できる。

  - CEO は、GAL を参照する際に Fabrikam 社および Tailspin Toys 社のすべての従業員を表示できる。

  - CEO のグループ メンバーを閲覧するユーザーは、そのユーザーの会社に属するグループのみを表示できる。また、これらのユーザーには、他の会社に存在するグループは表示されない。

## Entourage、Outlook for Mac、および ABP

ABP は、企業内ネットワークに接続する Entourage ユーザーや Outlook for Mac ユーザーには機能しません。企業内ネットワークでは、Entourage と Outlook for Mac クライアントは、グローバル カタログ サーバーに直接接続し、クライアント アクセス サーバーを使用せずに Active Directory に直接照会します。ただし、インターネット経由で接続する Outlook for Mac 2011 クライアントは、OAB または Exchange Web サービス (EWS) を使用できます。そのため、これらのクライアントは、割り当てられた ABP に基づいて GAL を検索できます。Outlook for Mac 2011 の管理の詳細については、[「Outlook for Mac 2011 の計画」](https://go.microsoft.com/fwlink/p/?linkid=231878)を参照してください。

## 詳細情報

[シナリオ: アドレス帳ポリシーの展開](scenario-deploying-address-book-policies-exchange-2013-help.md)

[アドレス帳ポリシーに関連する手順](https://technet.microsoft.com/ja-jp/library/jj891096\(v=exchg.150\)) (Exchange Online)

