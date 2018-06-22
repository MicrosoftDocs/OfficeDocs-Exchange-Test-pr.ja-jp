---
title: 'Exchange ハイブリッド展開での IRM: Exchange 2013 Help'
TOCTitle: Exchange ハイブリッド展開での IRM
ms:assetid: ba6ec48b-8f79-4807-b74b-fd442bbbe82f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ659052(v=EXCHG.150)
ms:contentKeyID: 49894955
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange ハイブリッド展開での IRM

 

_<strong>適用先:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>トピックの最終更新日:</strong>2016-12-09_

**概要:** Exchange ハイブリッド環境での IRM の機能、および Exchange Online とオンプレミスの Exchange サーバー間で IRM を構成する方法。

Information Rights Management (IRM) は、電子メール メッセージと添付ファイルをオンラインおよびオフラインで永続的に保護し、機密性の高い情報の漏洩防止を支援します。オンプレミス組織の Exchange と、Office 365 for enterprises の Exchange Online の両方は共に、IRM をサポートしています。ただし、これらの 2 つの実装には違いがあり、Exchange Online 組織ユーザーが IRM を使用できるようにするには、組織内で IRM を構成する必要があります。

IRM は、Windows Server 2008 以降のコンポーネントである Active Directory Rights Management サービス (AD RMS) を使用します。AD RMS を使用すると、ユーザーは電子メールや添付ファイルなどの権利が保護されたコンテンツを作成し、そのコンテンツの使用方法と配布先を制御できます。ユーザーはコンテンツの使用方法を決定するテンプレートを指定できます。たとえば、ユーザーは電子メール メッセージを他の受信者に転送できないように指定したり、メッセージ内の情報をコピーできないように指定したりできます。

Exchange 2010 の IRM の詳細情報:[Information Rights Management について](https://technet.microsoft.com/ja-jp/library/dd638140\(v=exchg.141\).aspx)。

Exchange 2013 および Exchange 2016 の IRM の詳細については、「[Information Rights Management](https://technet.microsoft.com/ja-jp/library/dd638140\(v=exchg.150\))」を参照してください。

AD RMS の詳細については、「[Active Directory Rights Management サービスの概要](http://go.microsoft.com/fwlink/p/?linkid=215243)」を参照してください。

## Exchange On-premises と Exchange Online での IRM の相違点

オンプレミスの Exchange 組織で利用できる IRM 機能は、Exchange Online 組織で利用できる IRM 機能とは異なる場合があります。次の表は、IRM 機能の概要と各組織で利用できる機能を示しています。(これらの機能の詳細情報: [Information Rights Management](https://technet.microsoft.com/ja-jp/library/dd638140\(v=exchg.150\)))

### 利用できる IRM 機能

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>Exchange 2007 以前で使用可能</th>
<th>Exchange 2010</th>
<th>Exchange Online および Exchange 2013 以降で使用可能</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook での手動によるメッセージ保護</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App での手動によるメッセージ保護</p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p>Outlook での IRM で保護されたメッセージの表示</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App での IRM で保護されたメッセージの表示</p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p>IRM プレライセンス エージェント</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p>RMS ポリシー テンプレート</p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p>トランスポート復号化</p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p>ジャーナル レポート復号化</p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Search と検出の復号化</p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p>自動 Outlook 保護ルール</p></td>
<td><p>いいえ</p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p>自動トランスポート保護ルール</p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
</tr>
</tbody>
</table>


## ハイブリッド展開での IRM

Exchange では、Exchange サーバーをインストールしている Active Directory フォレスト内で AD RMS サーバーが使用されます。オンプレミス Exchange サーバーでは、オンプレミス AD RMS サーバーが使用されます。Exchange Online 組織では、Office 365 データセンター内で維持されている AD RMS サーバーが使用されます。各 Exchange 組織が使用する AD RMS 構成は、他のすべての AD RMS 展開から独立しています。

AD RMS 構成、したがって IRM 構成は、オンプレミスの Exchange 組織と Exchange Online 組織間で自動的にレプリケートされません。定義した AD RMS テンプレートは Exchange Online 組織に自動的にコピーされません。同じ AD RMS テンプレートを Exchange Online 組織で使用可能にする場合は、オンプレミスの組織からテンプレートを手動でエクスポートし、Office 365 組織に適用する必要があります。このトピックの後半の「ハイブリッド展開での IRM の構成」を参照してください。

## ユーザーの操作性

ユーザーに適用される IRM 構成は、ユーザーが使用するクライアントと、ユーザーのメールボックスの場所によって決まります。次の表は、ユーザーが使用する AD RMS サーバーを示しています。

### アクティブな AD RMS サーバー

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>クライアント</th>
<th>社内メールボックス</th>
<th>Exchange Online メールボックス</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook デスクトップ クライアント</p></td>
<td><p>社内 AD RMS</p></td>
<td><p>社内 AD RMS</p></td>
</tr>
<tr class="even">
<td><p>Web 上の Outlook</p></td>
<td><p>社内 AD RMS</p></td>
<td><p>Exchange Online AD RMS</p></td>
</tr>
<tr class="odd">
<td><p>ActiveSync デバイス</p></td>
<td><p>社内 AD RMS</p></td>
<td><p>Exchange Online AD RMS</p></td>
</tr>
</tbody>
</table>


社内組織と Exchange Online 組織で構成する AD RMS 構成によって、Outlook 2007 および Web 上の Outlook を使用するユーザーに対して異なる AD RMS テンプレートが表示される可能性があります。このため、社内組織と Exchange Online 組織の両方に同じテンプレートを適用することを強くお勧めします。

Outlook クライアント ユーザーのメールボックスが社内組織内にあるか、Exchange Online 組織内にあるかに関係なく、ユーザーが IRM をまったく同じように利用できるようにする必要があります。

Exchange オンプレミス サーバー上にメールボックスがある Web 上の Outlook ユーザーは、Internet Explorer 用 Rights Management アドインをインストールした後は、権利を保護されたメッセージを開くことしかできません。これらのメッセージに返信することや、権利を保護されたメッセージを新規に作成することはできません。

Web 上の Outlook メールボックスが Exchange Online 上にある ユーザーは、別のソフトウェアを追加することなく権利で保護されたメッセージを開くことができ、これらのメッセージに返信することも、権利で保護されたメッセージを新規に作成することもできます。

## サーバーの機能

社内 Exchange サーバーは、 ユーザーが権利で保護されたメッセージを開く際に資格情報を入力する必要がないように、AD RMS プレライセンス エージェントを使用してこれらのメッセージを解読します。社内 Exchange サーバーは社内 AD RMS サーバーに接続し、使用ポリシーと権利を確認し、メッセージを解読するための認証を要求します。

Exchange Online 組織には、Exchange Online AD RMS を使用するための追加の IRM 関連機能がいくつか備えられています。ジャーナル レポート復号化などのこれらの機能は、権利で保護されたメッセージのコンテンツを Exchange サービスから利用できるようにして、追加の処理を行えるようにします。たとえば、解読されたジャーナル メッセージのコンテンツを元の権利で保護されたメッセージと共に保存して、より容易に検索できるようにします。さらに、メッセージが情報の保護に関する組織のポリシーに確実に従うように、Outlook 保護ルールまたはトランスポート ルールのいずれかを使用して IRM テンプレートを自動的にメッセージに適用できます。

## ハイブリッド展開での IRM の構成

Exchange の IRM は、Exchange サーバーが存在する Active Directory フォレスト内に展開されている AD RMS を使用します。AD RMS 構成は社内組織と Exchange Online 組織間では自動的に同期されません。信頼された発行ドメイン (TPD) と呼ばれる AD RMS 構成は、手動で社内の AD RMS サーバーからエクスポートし、Exchange Online 組織にインポートする必要があります。TPD には、Exchange Online 組織が IRM を使用するために必要とするテンプレートなどの AD RMS 構成が含まれます。

詳細については、「[AD RMS の信頼された発行ドメインについての考慮事項](http://go.microsoft.com/fwlink/p/?linkid=215244)」を参照してください。

社内の AD RMS 構成を Exchange Online 組織に適用することに加え、社内ネットワークの外側にある Outlook と ActiveSync クライアントから AD RMS サーバーに接続できるようにする必要があります。これらのクライアントから、社内ネットワークの外側にある権利で保護されたメッセージにアクセスさせたい場合は、この設定を行う必要があります。

社内ネットワークの構成と TPD データのエクスポートが完了したら、TPD データをインポートし、IRM を有効にすることで Exchange Online 組織を構成する必要があります。


> [!NOTE]
> 社内 AD&nbsp;RMS 構成を変更したときは常に、Exchange Online 組織に新しい構成を手動で適用する必要があります。これを行うには、社内 AD&nbsp;RMS サーバーから TPD をエクスポートし、Exchange Online 組織にインポートします。



## Exchange ハイブリッド展開での IRM の構成方法

オンプレミスの Exchange 組織で IRM を使用し、Exchange Online ユーザーも IRM を使用できるようにするには、次の作業を行う必要があります。

1.  社内 Active Directory Rights Management Services (AD RMS) サーバーを構成します。

2.  Exchange Online 組織内の IRM を有効にします。

3.  インポート済みの AD RMS テンプレートを Exchange Online 組織内のユーザーに配布します。

## 社内 AD RMS サーバーの構成方法

ハイブリッド展開で IRM を構成するには、Windows PowerShell を使用して社内 AD RMS サーバーにアクセスする必要があります。詳細情報:「[Windows PowerShell を使用した AD RMS の管理](http://go.microsoft.com/fwlink/p/?linkid=214938)」

社内 AD RMS サーバーから信頼された発行ドメイン (TPD) のデータをエクスポートして、外部クライアント向けに AD RMS サーバーへのアクセスを構成します。

1.  社内組織から TPD データをエクスポートします。詳細情報:「[信頼された発行ドメインのエクスポート](http://go.microsoft.com/fwlink/p/?linkid=214942)」

2.  外部クライアントからの AD RMS サーバーへのアクセスを構成します。詳細情報:「[外部クラスター URL の追加](http://go.microsoft.com/fwlink/p/?linkid=214945)」

## Exchange Online 組織で IRM を有効にする方法

社内 AD RMS サーバーから TPD データをエクスポートしたら、Exchange Online 組織にデータをインポートして、IRM を有効にする必要があります。

1.  Exchange Online 組織で、TPD データをインポートします。
    
        Import-RMSTrustedPublishingDomain -FileData $( [Byte[]] (Get-Content -Encoding Byte -Path "<Path to exported TPD file>" -ReadCount 0))

2.  Exchange Online 組織で IRM を有効にします。
    
        Set-IRMConfiguration -InternalLicensingEnabled $True

## Exchange Online 組織で AD RMS テンプレートを配布する方法

Exchange Online 組織で IRM を有効にしたら、インポート済みの AD RMS テンプレートを配布する必要があります。AD RMS テンプレートを使用する Exchange Online ユーザーおよび機能は次のとおりです。

  - Web 上の Outlook ユーザー

  - Exchange ActiveSync ユーザー

  - トランスポート ルール

  - ジャーナル レポート復号化

  - Outlook 保護ルール

<!-- end list -->

1.  Exchange Online 組織で、AD RMS テンプレートの一覧を取得します。
    
        Get-RMSTemplate -Type All

2.  Exchange Online 組織内のユーザーと機能に AD RMS テンプレートを配布します。
    
        Set-RMSTemplate <template name> -Type Distributed
    

    > [!NOTE]
    > "転送不可" のAD RMS テンプレートは変更できません。



3.  配布する各 AD RMS テンプレートに対して、手順 2 を繰り返します。

## 設定が適用されたことを確認する方法

Web 上の Outlook ユーザーは、新規メッセージに AD RMS テンプレートを適用できる必要があります。Web 上の Outlook ユーザーと Exchange ActiveSync ユーザーは、AD RMS テンプレートが適用されているメッセージを読み取れる必要があります。さらに、**Get-RMSTemplate** コマンドレットを実行すると、社内組織からインポートされたすべての AD RMS テンプレートが一覧表示されます。

Exchange Online 組織で、次のコマンドを実行します。

    Get-RMSTemplate 

詳細情報: [Outlook Web App での Information Rights Management](https://technet.microsoft.com/ja-jp/library/dd876891\(v=exchg.150\))

