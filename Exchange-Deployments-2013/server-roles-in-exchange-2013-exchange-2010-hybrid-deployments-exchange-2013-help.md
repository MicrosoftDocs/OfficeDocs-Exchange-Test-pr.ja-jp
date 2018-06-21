---
title: 'Exchange 2013/Exchange 2010 ハイブリッド展開でのサーバーの役割: Exchange 2013 Help'
TOCTitle: Exchange 2013/Exchange 2010 ハイブリッド展開でのサーバーの役割
ms:assetid: 7d774948-94f9-4405-af2b-0c67c0405c0f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn393966(v=EXCHG.150)
ms:contentKeyID: 59635070
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013/Exchange 2010 ハイブリッド展開でのサーバーの役割

このトピックは処理中です。  

_<strong>適用先:</strong>Exchange Online, Exchange Server, Exchange Server 2013_

_<strong>トピックの最終更新日:</strong>2017-02-16_

Exchange 2010 組織でハイブリッド展開を構成する場合、既存の Exchange 2010 組織に、クライアント アクセス サーバーとメールボックス サーバーの役割を備えた Exchange 2013 サーバーを少なくとも 1 台設置する必要があります。Exchange 2013 クライアント アクセス サーバーとメールボックス サーバーは、既存の Exchange 2010 社内組織と Exchange Online 組織との間で通信を調整します。この通信には、社内組織と Exchange Online 組織間のメッセージ トランスポート機能およびメッセージング機能が使用されます。

ハイブリッド展開機能の信頼性と可用性を向上させために、社内組織に複数の Exchange 2013 サーバーを設置することを強くお勧めします。

## ハイブリッド展開におけるサーバーの役割

ここでは、ハイブリッド展開における Exchange 2013 サーバーの役割について簡単に概説します。

  - **クライアント アクセス サーバーの役割**   Exchange 2013 クライアント アクセス サーバーの役割は、組織内の Exchange 2010 クライアント アクセス サーバーが一般的に提供する機能と同じ機能を数多く提供するほか、ハイブリッド展開をサポートして Exchange 2010 と共存するために必要な機能を追加で提供します。さらに、クライアント アクセス サーバーは、Exchange Online 組織から社内組織に送信されるセキュリティで保護されたすべてのメール メッセージを処理するほか、ハイブリッド展開におけるトランスポート ルールの処理、ポリシーのジャーナリング、およびメールボックス サーバーへのメッセージ配信も行います。専用受信コネクタはクライアント アクセス サーバー上で構成され、セキュリティ保護されたハイブリッド メール トランスポートがサポートされます。Outlook クライアント アクセス、Outlook Web App、および Outlook Anywhere などのすべてのクライアント接続は、クライアント アクセス サーバーの役割を介します。空き情報の共有など、社内組織と Exchange Online 組織間の組織上の関係機能も、クライアント アクセス サーバーの役割によって処理されます。
    
    詳細については、「[クライアント アクセス サーバー](https://technet.microsoft.com/ja-jp/library/dd298114\(v=exchg.150\))」を参照してください。

  - **メールボックス サーバーの役割**   Exchange 2013 メールボックス サーバーの役割は、社内組織から Exchange Online 組織へ送信された、セキュリティで保護された電子メール メッセージを処理することです。一般的ではありませんが、社内受信者メールボックスをホストし、社内クライアント アクセス サーバーを経由してプロキシで Exchange Online 組織と通信することもできます。専用送信コネクタは既定ではメールボックス サーバーの役割で構成され、セキュリティ保護されたハイブリッド メール トランスポートがサポートされます。
    
    詳細については、「[メールボックス サーバー](https://technet.microsoft.com/ja-jp/library/jj150491\(v=exchg.150\))」を参照してください。

必要なハイブリッド展開構成に応じて、Exchange 2013 サーバーに、片方または両方のサーバーの役割をインストールする必要があります。

  - **単一の Exchange サーバー**   社内組織に単一の Exchange サーバーをインストールする場合は、単一のサーバーにクライアント アクセス サーバーとメールボックス サーバーの両方の役割をインストールする必要があります。

  - **複数の Exchange サーバー**   社内組織に複数の Exchange サーバーをインストールする場合は、社内組織内にある別々のサーバーにサーバーの役割をインストールできます。たとえば、メールボックスの役割とクライアント アクセスの役割がインストールされている 1 台の Exchange 2013 サーバーを設置するとともに、クライアント アクセス サーバーの役割のみがインストールされている別の Exchange サーバーを設置することもできます。ただし、ベスト プラクティスであり推奨されるサーバーの構成は、社内組織に展開されている*各* Exchange 2013 サーバーにクライアント アクセス サーバーとメールボックス サーバーの両方の役割をインストールする構成です。

Exchange 容量プランニングの詳細については、「[容量計画での複数のサーバーの役割の構成について](https://go.microsoft.com/fwlink/?linkid=266576)」を参照してください。

## ハイブリッドの展開での Exchange サーバーの機能

Exchange サーバーは、ハイブリッド展開の社内組織にとって重要な機能をいくつか提供します。

  - **フェデレーション**   Exchange 2013 サーバーおよび Exchange 2010 サーバーにより、Microsoft Federation Gateway との間の社内組織のフェデレーションの信頼を作成することができます。Microsoft Federation Gateway は、社内組織と Office 365 テナント組織間の信頼ブローカーとして機能する、マイクロソフトが無償で提供するクラウドベースのサービスです。フェデレーションは、社内組織と Exchange Online 組織の間に組織上の関係を作成するうえで必須です。
    
    詳細については、「[フェデレーション](https://technet.microsoft.com/ja-jp/library/dd335047\(v=exchg.150\))」を参照してください。

  - **組織上の関係**   クライアント アクセス サーバーの役割がインストールされている Exchange 2013 サーバーにより、社内組織と Exchange Online 組織間の組織上の関係を作成できます。組織上の関係は、ハイブリッド展開においてその他の多くのサービス (予定表の空き時間情報の共有、メッセージ追跡、社内組織と Exchange Online 組織間でのメールボックスの移動など) に必要です。
    
    詳細については、「[共有](https://technet.microsoft.com/ja-jp/library/dd638083\(v=exchg.150\))」を参照してください。

  - **メッセージ トランスポート**   クライアント アクセス サーバーとメールボックス サーバーの役割がインストールされている Exchange 2013 サーバーは、ハイブリッド展開でのメッセージ トランスポートを処理します。送信/受信コネクタを使用して、外部の受信メッセージ用の接続エンドポイントとして機能し、さらに送信メッセージをインターネットおよび Exchange Online 組織に配信します。
    
    詳細については、「[Exchange 2013/Exchange 2010 ハイブリッド展開でのトランスポート オプション](transport-options-in-exchange-2013-exchange-2010-hybrid-deployments-exchange-2013-help.md)」を参照してください。

  - **メッセージ トランスポート セキュリティ**   クライアント アクセス サーバーとメールボックス サーバーの役割がインストールされている Exchange 2013 サーバーは、Exchange 2013 のドメイン セキュリティ機能を使用して、社内組織と Exchange Online 組織間のメッセージ通信のセキュリティ保護を支援します。メッセージ通信に対して相互トランスポート層セキュリティ認証および暗号化を使用することによって、セキュリティを強化できます。
    
    詳細については、「[ドメイン セキュリティについて](https://go.microsoft.com/fwlink/p/?linkid=266581)」を参照してください。

  - **Outlook Web App**   クライアント アクセス サーバーの役割がインストールされている Exchange 2013 サーバーは、社内メールボックスと Exchange Online メールボックスへの外部接続用の単一の URL エンドポイントの構成を支援します。社内メールボックスの場合、クライアント アクセス サーバーは、Outlook Web App 要求を処理するように構成されます。Exchange Online 組織メールボックスの場合、クライアント アクセス サーバーは、Outlook Web App エンドポイントへのリンクを Exchange Online 組織に自動的に表示するように構成されます。
    
    詳細については、「[Outlook Web App](https://technet.microsoft.com/ja-jp/library/jj657718\(v=exchg.150\))」を参照してください。

## Exchange サーバー トポロジ

ハイブリッド展開をサポートするために、別の Exchange 2013 サーバーを追加する場合、Exchange サーバーは、他の Exchange サーバーが既存の Exchange 2010 組織に展開されるのと同じ様に展開されます。社内の既存の Exchange 2010 組織をハイブリッド展開用に構成するためには、特別な Exchange サーバー トポロジは必要ありません。ただし、Exchange 2010 Service Pack 3 (SP3) を Exchange 2010 サーバーにインストールする必要があります。また、Office 365 での互換性と完全なハイブリッド機能を確保するため、Exchange 2013 累積更新プログラム 1 (CU1) をインストールすることも必要です。

次の表に、ハイブリッド展開を構成した後のサービスにおける変更点の概要を示します。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>サービス</th>
<th>ハイブリッド展開前</th>
<th>ハイブリッド展開後</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>メッセージ トランスポート (受信および送信)</p></td>
<td><p>Exchange 2010 クライアント アクセス サーバー</p></td>
<td><p>Office 365 に含まれる Exchange 2013 クライアント アクセス サーバーまたは Exchange Online Protection (EOP)</p></td>
<td><p>ドメインの MX (メール エクスチェンジャー) レコードは、変更されないか、または EOP をポイントするように更新されます。</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App パブリック URL</p></td>
<td><p>Exchange 2010 クライアント アクセス サーバー</p></td>
<td><p>Exchange 2013 クライアント アクセス サーバー</p></td>
<td><p>Exchange 2013 クライアント アクセス サーバーは、社内メールボックス サーバーから Exchange 2010 クライアント アクセス サーバーへの Outlook Web App 要求をプロキシ化します。Exchange Online でホストされているメールボックス宛ての Outlook Web App 要求には、Exchange Online Outlook Web App URL へのリンクが添付されます。</p></td>
</tr>
</tbody>
</table>


## Exchange サーバー ソフトウェア

Exchange 2013 CU1 以上は、ハイブリッド構成ウィザードを使用したハイブリッド展開機能を有効にします。追加の Exchange 2013 サーバーをインストールする際は、任意の Exchange 2013 CU1 以上のメディアを使用できます。

Exchange 2013 の最新バージョンをダウンロードする方法の詳細については、「[Exchange 2016 用の更新プログラム](https://technet.microsoft.com/library/jj907309)」を参照してください。


> [!IMPORTANT]
> ハイブリッド展開を Exchange 2013 または 2010 および Office 365 と共に構成する場合、ハイブリッド サーバーのライセンスを取得する必要があります。ハイブリッド展開を構成するために使用する無償の Exchange Server プロダクト キーを入手するには、<A href="https://aka.ms/hybridkey">Hybrid Edition プロダクト キー ツール</A> を使用します。


