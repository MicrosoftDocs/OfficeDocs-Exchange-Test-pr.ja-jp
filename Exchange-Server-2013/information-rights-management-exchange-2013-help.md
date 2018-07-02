---
title: 'Information Rights Management: Exchange 2013 Help'
TOCTitle: Information Rights Management
ms:assetid: 6ea3a695-3ddd-4d53-b3c6-90041f44ef64
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd638140(v=EXCHG.150)
ms:contentKeyID: 49896304
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Information Rights Management

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

インフォメーション ワーカーは、毎日、電子メールを使用して、財務レポートや財務データ、法的契約、社外秘の製品情報、売上レポートや売上見込み、競合他社の分析、研究や特許情報、顧客や従業員の情報などの機密性の高い情報を交換しています。人々はほとんどどこからでも自分の電子メールにアクセスできるようになったため、メールボックスは、機密性の高い情報を大量に含むリポジトリになりました。その結果、情報漏洩が組織にとって深刻な脅威になる可能性があります。情報漏洩を防止するために、Microsoft Exchange Server 2013 には、電子メール メッセージおよび添付ファイルをオンラインおよびオフラインで永続的に保護する Information Rights Management (IRM) 機能が搭載されています。

**目次**

情報漏洩について

情報漏洩に対する従来の解決策

Exchange 2013 での IRM

メッセージへの IRM による保護の適用

IRM による保護のシナリオ

IRM で保護されたメッセージの解読によるメッセージング ポリシーの適用

プレライセンス

IRM エージェント

IRM の要件

IRM の構成とテスト

権限管理コネクタで権利の管理を拡張

## 情報漏洩について

機密性の高い情報の漏洩は、組織にとって多大なコストがかかり、組織やその事業、従業員、顧客、およびパートナーに広範な影響を与える可能性があります。地域や業界の規制によって、特定の種類の情報の保存、転送、セキュリティ保護方法がますます管理されるようになっています。適用される規制の違反を回避するために、組織では、意図的、不注意、または偶然による情報の漏洩から自身を保護する必要があります。

次に、情報漏洩によって引き起こされる結果をいくつか示します。

  - **財務上の悪影響**   規模、業界、地域の規制によっては、情報漏洩によって、事業機会の損失が発生したり、裁判所または規制機関によって罰金や懲罰的損害賠償が課されたりすることで、財務上の悪影響を被る可能性があります。株式公開企業は、メディアの非難により時価総額を減らす危険性もあります。

  - **イメージと信頼性に対する悪影響**   情報漏洩によって、顧客を持つ組織のイメージと信頼性が損なわれる可能性があります。さらに、通信の性質によっては、漏洩された電子メール メッセージが、送信者や組織にバツの悪い思いをもたらす可能性もあります。

  - **競争上の優位性の損失**   情報漏洩による最も深刻な脅威の 1 つに、ビジネスにおける競争上の優位性の損失があります。戦略的計画の暴露、または吸収合併に関する情報の開示によって、売上や時価総額を減らす可能性もあります。他の脅威としては、研究情報、分析データ、その他の知的財産の損失などがあります。

情報漏洩について

## 情報漏洩に対する従来の解決策

情報漏洩に対する従来の解決策では、初期的なデータ アクセスを防ぐ効果が得られる場合もありますが、通常、継続的な保護は提供されません。次の表に、従来の解決策とその制限事項を示します。

### 従来の解決策

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>解決策</th>
<th>説明</th>
<th>制限事項</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>トランスポート層セキュリティ (TLS)</p></td>
<td><p>TLS は、暗号化によってネットワークを介した通信をセキュリティで保護するために使用されるインターネットの標準プロトコルです。メッセージング環境では、TLS を使用して、サーバー/サーバー間やサーバー/クライアント間の通信をセキュリティで保護します。</p>
<p>既定では、Exchange 2010 はすべての内部メッセージ転送に TLS を使用します。外部ホストとのセッションには、既定で便宜的な TLS も有効になります。Exchange では、そのセッションに対して最初に TLS 暗号化の使用を試みますが、送信先サーバーとの TLS 接続が確立できない場合、Exchange では SMTP を使用します。外部組織との相互 TLS を強制するように、ドメイン セキュリティを構成することもできます。</p></td>
<td><p>TLS は、2 つの SMTP ホスト間の SMTP セッションのみ保護します。つまり、TLS では移動している情報が保護されるだけで、メッセージ レベルでの保護や静止している情報の保護は提供されません。メッセージを別の方法で暗号化しない限り、送信者や受信者のメールボックス内のメッセージは未保護のままになります。組織外に送信される電子メールの場合、1 回目のホップにのみ TLS を要求できます。組織外のリモート SMTP ホストがメッセージを受信後に、暗号化されていないセッションを介して別の SMTP ホストにそのメッセージを中継できます。TLS はトランスポート層テクノロジであるため、受信者がメッセージに対して行う操作を制御することはできません。</p></td>
</tr>
<tr class="even">
<td><p>電子メールの暗号化</p></td>
<td><p>ユーザーは、S/MIME などのテクノロジを使用してメッセージを暗号化できます。</p></td>
<td><p>ユーザーはメッセージを暗号化するかどうかを決定します。公開キー基盤 (PKI) を展開するための追加コスト、およびユーザーに対する証明書の管理や秘密キーの保護に付随するオーバーヘッドが発生します。メッセージが解読されると、受信者がその情報に対してどのような操作を行っても制御できません。解読された情報は、コピー、印刷、または転送できます。既定では、保存された添付ファイルは保護されません。</p>
<p>S/MIME などのテクノロジを使用して暗号化されたメッセージは、組織ではアクセスできません。組織では、メッセージのコンテンツを検査できないため、メッセージ ポリシーの強制的な適用、メッセージでのウイルスや悪意のあるコンテンツのスキャン、またはコンテンツへのアクセスに必要な他の操作を行うことができません。</p></td>
</tr>
</tbody>
</table>


最後に、従来の解決策には、ほとんどの場合、統一されたメッセージング ポリシーを適用して情報漏洩を防止する強制ツールがありません。たとえば、ユーザーが、機密情報を含むメッセージを **\[社内機密\]** および **\[転送不可\]** のマークを付けて送信したとします。この場合、メッセージが受信者に配信されると、送信者または組織はこの情報を制御できなくなります。受信者はメッセージを意図的に、または不注意によって外部電子メール アカウントに転送できるため (自動転送ルールなどの機能を使用して)、組織が実質的に情報漏洩の危険を被る可能性があります。

情報漏洩について

## Exchange 2013 での IRM

Exchange 2013 では、IRM 機能を使用して、メッセージおよび添付ファイルを永続的に保護できます。IRM では、Windows Server 2008 以降の情報保護テクノロジである Active Directory Rights Management サービス (AD RMS) が使用されます。Exchange 2013 で IRM 機能を使用すると、受信者が電子メールに対して保有する権限を組織とユーザーが制御できるようになります。IRM はまた、メッセージの他の受信者への転送、メッセージや添付ファイルの印刷、コピーと貼り付けによるメッセージや添付ファイルのコンテンツの抽出などの受信者の操作を許可または制限するのに役立ちます。IRM による保護は、ユーザーが Microsoft Outlook や Microsoft OfficeOutlook Web App で適用したり、組織のメッセージング ポリシーに基づき、トランスポート保護ルールや Outlook の保護ルールを使用して適用したりできます。他の電子メール暗号化ソリューションとは異なり、IRM では、保護されたコンテンツを解読してポリシーへの準拠を徹底させることもできます。

AD RMS では、XrML (eXtensible rights Markup Language) ベースの証明書とライセンスを使用して、コンピューターとユーザーを認定し、コンテンツを保護します。ドキュメントやメッセージなどのコンテンツを AD RMS を使用して保護すると、認証されたユーザーがコンテンツに対して持つ権限を含む XrML ライセンスが添付されます。IRM で保護されたコンテンツにアクセスするには、AD RMS 対応アプリケーションで、AD RMS クラスターから認証されたユーザーの使用ライセンスを調達する必要があります。


> [!NOTE]
> Exchange 2013 では、プレライセンス エージェントが、使用ライセンスを組織の AD RMS クラスターを使用して保護されたメッセージに添付します。詳細については、このトピックで後述する「プレライセンス」を参照してください。



コンテンツの作成に使用するアプリケーションは、AD RMS を使用してコンテンツを永続的に保護できるように、RMS 対応である必要があります。Word、Excel、PowerPoint、Outlook などの Microsoft Office アプリケーションは、RMS 対応であるため、保護されたコンテンツを作成および使用できます。

IRM では、次の操作を行うことができます。

  - IRM で保護されたコンテンツの認証された受信者が、コンテンツの転送、変更、印刷、FAX、保存、カットアンドペーストをできないようにします。

  - サポートされている添付ファイルの形式をメッセージと同じレベルの保護で保護します。

  - IRM で保護されたメッセージと添付ファイルの有効期限をサポートし、指定された期間以降表示できないようにします。

  - Microsoft Windows の切り取りツールで IRM で保護されたコンテンツをコピーできないようにします。

ただし、IRM では、次の方法による情報のコピーを防止することはできません。

  - サードパーティ製の画面キャプチャ プログラム

  - カメラなどのイメージング デバイスによる、画面に表示された IRM で保護されたコンテンツの撮影

  - ユーザーによる情報の記憶または書き写し

AD RMS の詳細については、「[Active Directory Rights Management サービス](https://go.microsoft.com/fwlink/p/?linkid=129823)」を参照してください。

## AD RMS 権利ポリシー テンプレート

AD RMS では、XrML ベースの権利ポリシー テンプレートを使用して、互換性がある IRM 対応アプリケーションが一貫した保護ポリシーを適用できるようにします。Windows Server 2008 以降で、AD RMS サーバーはテンプレートの列挙および取得に使用できる Web サービスを公開します。Exchange 2013 には \[転送不可\] テンプレートが添付されます。\[転送不可\] テンプレートをメッセージに適用すると、メッセージにアドレスが指定された受信者のみがメッセージを解読できます。受信者は、メッセージを転送したり、メッセージの内容をコピーしたり、メッセージを印刷したりすることはできません。IRM による保護要件に合うように、組織内の AD RMS サーバー上に追加の RMS テンプレートを作成できます。

IRM による保護を適用するには、AD RMS 権利ポリシー テンプレートを適用します。ポリシー テンプレートを使用すると、受信者がメッセージに関して持つアクセス許可を制御できます。返信、全員へ返信、転送、メッセージからの情報の抽出、メッセージの保存、メッセージの印刷などの操作を制御するには、該当する権利ポリシー テンプレートをメッセージに適用します。

権利ポリシー テンプレートの詳細については、「[AD RMS ポリシー テンプレートの考慮事項](https://go.microsoft.com/fwlink/p/?linkid=179455)」を参照してください。

AD RMS 権利ポリシー テンプレートの作成方法の詳細については、「[ステップ バイ ステップ ガイド - Active Directory Rights Management サービス権利ポリシー テンプレートを作成および展開する](https://go.microsoft.com/fwlink/p/?linkid=136593)」を参照してください。

情報漏洩について

## メッセージへの IRM による保護の適用

Exchange 2010 では、IRM による保護を次の方法でメッセージに適用できます。

  - **Outlook ユーザーによる手動適用**   Outlook ユーザーは、利用可能な AD RMS 権利ポリシー テンプレートを使用して IRM でメッセージを保護できます。このプロセスは、Exchange ではなく Outlook の IRM 機能を使用します。ただし、Exchange を使用してメッセージにアクセスし、組織のメッセージング ポリシーを強制するための対処法 (トランスポート ルールの適用など) をとることができます。Outlook での IRM の使用方法の詳細については、「[メール メッセージでの IRM の使用方法](https://go.microsoft.com/fwlink/p/?linkid=166897)」をご覧ください。

  - **Outlook Web App ユーザーによる手動適用**   Outlook Web App で IRM を有効にすると、ユーザーは送信するメッセージを IRM で保護したり、受信する IRM で保護されたメッセージを表示したりできます。Exchange 2013 累積的な更新 1 (CU1)、 Outlook Web App ユーザーは IRM で保護された添付ファイルを Web 用のドキュメントの表示を使用しても表示できます。Outlook Web App の IRM の詳細については、「[Outlook Web App での Information Rights Management](information-rights-management-in-outlook-web-app-exchange-2013-help.md)」を参照してください。

  - **Windows Mobile および Exchange ActiveSync デバイス ユーザーによる手動適用**   Exchange 2010 の RTM (Release To Manufacturing) 版では、Windows Mobile デバイスのユーザーは、IRM で保護されたメッセージを表示および作成できます。この場合、ユーザーは、サポートされる Windows Mobile デバイスをコンピューターに接続し、それらのデバイスを IRM 用にアクティブ化する必要があります。Exchange 2010 SP1 では、Exchange ActiveSync デバイス (Windows Mobile デバイスを含む) のユーザーが IRM で保護されたメッセージの表示、返信、転送、および作成を行うことができるように、Microsoft Exchange ActiveSync で IRM を有効にできます。Exchange ActiveSync の IRM の詳細については、「[Exchange ActiveSync での Information Rights Management](information-rights-management-in-exchange-activesync-exchange-2013-help.md)」を参照してください。

  - **Outlook 2010 以降での自動適用**   Outlook の保護ルールを作成して、Outlook 2010 以降で自動的にメッセージを IRM で保護するようにできます。Outlook の保護ルールは Outlook 2010 クライアントに自動的に展開され、ユーザーがメッセージを作成する際、Outlook 2010 によって IRM による保護が適用されます。Outlook の保護ルールの詳細については、「[Outlook の保護ルール](outlook-protection-rules-exchange-2013-help.md)」を参照してください。

  - **メールボックス サーバーでの自動適用**   トランスポート保護ルールを作成して、Exchange 2013 メールボックス サーバーで自動的にメッセージを IRM で保護できます。トランスポート保護ルールの詳細については、「[トランスポート保護ルール](transport-protection-rules-exchange-2013-help.md)」を参照してください。
    

    > [!NOTE]
    > IRM による保護は、既に IRM で保護されたメッセージに再度適用されることはありません。たとえば、ユーザーが Outlook または Outlook Web App でメッセージを IRM で保護した場合、IRM による保護は、トランスポート保護ルールを使用してメッセージに適用されることはありません。



情報漏洩について

## IRM による保護のシナリオ

次の表に、IRM による保護のシナリオを示します。

### IRM による保護のシナリオ

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>IRM で保護されたメッセージの送信</th>
<th>サポート</th>
<th>必要条件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>社内の同じ Exchange 2013 展開内での送信</p></td>
<td><p>はい</p></td>
<td><p>要件については、後の「IRM の要件」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>社内の展開内における異なるフォレスト間での送信</p></td>
<td><p>はい</p></td>
<td><p>要件については、「<a href="https://go.microsoft.com/fwlink/p/?linkid=199009">複数のフォレスト間で Exchange Server 2010 と統合するための AD RMS の構成</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>社内の Exchange 2013 展開とクラウドベースの Exchange 組織間での送信</p></td>
<td><p>はい</p></td>
<td><ul>
<li><p>社内の AD RMS サーバーを使用します。</p></li>
<li><p>信頼された発行ドメインを社内の AD RMS サーバーからエクスポートします。</p></li>
<li><p>信頼された発行ドメインをクラウドベースの組織にインポートします。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>外部受信者への送信</p></td>
<td><p>いいえ</p></td>
<td><p>Exchange 2010 には、IRM で保護されたメッセージを、非フェデレーション組織内の外部受信者に送信するための解決策は含まれていません。AD RMS には、信頼ポリシーを使用した解決策があります。AD RMS クラスターと Microsoft アカウント (旧称: Windows Live ID) との間の信頼ポリシーを構成することができます。2 つの組織間で送信されたメッセージに関しては、Active Directory フェデレーション サービス (AD FS) を使用して 2 つの Active Directory フォレスト間のフェデレーション信頼を作成できます。詳細については、「<a href="https://go.microsoft.com/fwlink/p/?linkid=182909">AD RMS 信頼ポリシーとは</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>


情報漏洩について

## IRM で保護されたメッセージの解読によるメッセージング ポリシーの適用

メッセージング ポリシーを強制的に適用して規制に準拠するには、暗号化されたメッセージ コンテンツにアクセスできる必要があります。訴訟、規制に基づく監査、または内部的な調査による電子情報開示要件を満たすには、暗号化されたメッセージを検索できる必要もあります。これらのタスクを支援するために、Exchange 2013 には次の IRM 機能が搭載されています。

  - **トランスポート復号化**   メッセージング ポリシーを適用するには、トランスポート ルール エージェントなどのトランスポート エージェントがメッセージ コンテンツにアクセスできる必要があります。トランスポート復号化を使用すると、Exchange 2013 サーバーにインストールされているトランスポート エージェントがメッセージ コンテンツにアクセスできるようになります。詳細については、「[トランスポート復号化](transport-decryption-exchange-2013-help.md)」を参照してください。

  - **ジャーナル レポート復号化**   準拠や事業要件を満たすために、組織ではジャーナリングを使用してメッセージング コンテンツを保持できます。ジャーナリング エージェントは、ジャーナリング対象のメッセージのジャーナル レポートを作成し、レポート内のメッセージに関するメタデータを格納します。元のメッセージは、ジャーナル レポートに添付されます。ジャーナル レポート内のメッセージが IRM で保護されている場合、ジャーナル レポート復号化によってメッセージのクリア テキスト コピーがジャーナル レポートに添付されます。詳細については、「[ジャーナル レポート復号化](journal-report-decryption-exchange-2013-help.md)」を参照してください。

  - **Exchange Search 用の IRM 解読**   Exchange Search 用の IRM 解読では、Exchange Search は、IRM で保護されたメッセージのコンテンツにインデックスを作成できます。検出マネージャーがインプレースの電子情報開示検索を実行すると、検索結果にインデックスが作成された IRM で保護されたメッセージが返されます。詳細については、「[インプレース電子情報開示 (eDiscovery)](in-place-ediscovery-exchange-2013-help.md)」を参照してください。
    

    > [!NOTE]
    > Exchange 2010 SP1 以降では、"Discovery Management/検出の管理" 役割グループのメンバーは、探索検索によって返され、探索メールボックスに保存されている IRM で保護されたメッセージにアクセスできます。この機能を有効にするには、<A href="https://technet.microsoft.com/ja-jp/library/dd979792(v=exchg.150)">Set-IRMConfiguration</A> コマンドレットを <EM>EDiscoverySuperUserEnabled</EM> パラメーターと共に使用します。詳細については、「<A href="configure-irm-for-exchange-search-and-in-place-ediscovery-exchange-2013-help.md">Exchange 検索およびインプレース電子情報開示のための IRM の構成</A>」を参照してください。



これらの解読機能を有効にするには、Exchange サーバーがメッセージにアクセスできる必要があります。これを行うには、Exchange セットアップ プログラムによって作成されるシステム メールボックスである、フェデレーション メールボックスを AD RMS サーバーのスーパー ユーザー グループに追加します。詳細については、「[フェデレーション メールボックスを AD RMS のスーパー ユーザー グループに追加する](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)」を参照してください。

情報漏洩について

## プレライセンス

IRM で保護されたメッセージと添付ファイルを表示するために、Exchange 2013 では、プレライセンスを保護されたメッセージに自動的に添付します。この機能によって、クライアントは AD RMS サーバーに繰り返しトリップを行って使用ライセンスを取得する必要がなくなるうえ、IRM で保護されたメッセージと添付ファイルのオフライン表示が可能になります。プレライセンスでは、IRM で保護されたメッセージを Outlook Web App で表示することもできます。IRM 機能を有効にすると、プレライセンスが既定で有効になります。

情報漏洩について

## IRM エージェント

Exchange 2013 では、メールボックス サーバー上のトランスポート サービスのトランスポート エージェントを使用して、IRM 機能が有効にされます。IRM エージェントは、Exchange セットアップ プログラムによって、メールボックス サーバーにインストールされます。トランスポート エージェントの管理タスクを使用して、IRM エージェントを制御することはできません。


> [!NOTE]
> Exchange 2013 では、IRM エージェントはビルトイン エージェントです。ビルトイン エージェントは、<STRONG>Get-TransportAgent</STRONG> コマンドレットによって返されるエージェントの一覧には含まれていません。詳細については、「<A href="transport-agents-exchange-2013-help.md">トランスポート エージェント</A>」を参照してください。



次の表に、メールボックス サーバー上のトランスポート サービスに実装される IRM エージェントを示します。

### メールボックス サーバー上のトランスポート サービスにおける IRM エージェント

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>エージェント</th>
<th>イベント</th>
<th>機能</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RMS 復号化エージェント</p></td>
<td><p>OnEndOfData (SMTP) および OnSubmittedMessage</p></td>
<td><p>メッセージを解読して、トランスポート エージェントへのアクセスを許可します。</p></td>
</tr>
<tr class="even">
<td><p>トランスポート ルール エージェント</p></td>
<td><p>OnRoutedMessage</p></td>
<td><p>トランスポート保護ルールのルール条件に一致するメッセージに対して、RMS 暗号化エージェントによって IRM で保護するというフラグを設定します。</p></td>
</tr>
<tr class="odd">
<td><p>RMS 暗号化エージェント</p></td>
<td><p>OnRoutedMessage</p></td>
<td><p>トランスポート ルール エージェントによってフラグ設定されたメッセージに対して IRM による保護を適用し、トランスポートで解読されたメッセージを再度暗号化します。</p></td>
</tr>
<tr class="even">
<td><p>プレライセンス エージェント</p></td>
<td><p>OnRoutedMessage</p></td>
<td><p>IRM で保護されたメッセージにプレライセンスを添付します。</p></td>
</tr>
<tr class="odd">
<td><p>ジャーナル レポート復号化エージェント</p></td>
<td><p>OnCategorizedMessage</p></td>
<td><p>ジャーナル レポートに添付されている IRM で保護されたメッセージを解読し、元の暗号化されたメッセージと共にクリア テキスト バージョンを埋め込みます。</p></td>
</tr>
</tbody>
</table>


トランスポート エージェントの詳細については、「[トランスポート エージェント](transport-agents-exchange-2013-help.md)」を参照してください。

情報漏洩について

## IRM の要件

Exchange 2013 組織に IRM を実装するには、展開が次の表に記載された要件を満たしている必要があります。

### IRM の要件

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>サーバー</th>
<th>要件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AD RMS クラスター</p></td>
<td><ul>
<li><p><strong>オペレーティング システム</strong>   Windows Server 2012、Windows Server 2008 R2、または修正プログラム「<a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=973247">Active Directory Rights Management サービスの役割</a>」が適用された Windows Server 2008 SP2 が必要です。</p></li>
<li><p><strong>サービス接続ポイント</strong>   Exchange 2010 および AD RMS 対応アプリケーションは、Active Directory に登録されているサービス接続ポイントを使用して、AD RMS クラスターと URL を検出します。AD RMS では、AD RMS セットアップ プログラム内からサービス接続ポイントを登録できます。AD RMS のセットアップに使用されるアカウントが Enterprise Admins セキュリティ グループのメンバーでない場合、サービス接続ポイントの登録はセットアップ後に実行できます。AD RMS のサービス接続ポイントは、Active Directory フォレスト内に 1 つだけ存在します。</p></li>
<li><p><strong>アクセス許可</strong>   次の対象には、AD RMS サーバー証明パイプライン (AD RMS サーバー上の <code>ServerCertification.asmx</code> ファイル) に対する読み取りと実行のアクセス許可を割り当てる必要があります。</p>
<ul>
<li><p>Exchange サーバー グループまたは個々の Exchange サーバー</p></li>
<li><p>AD RMS サーバー上の AD RMS サービス グループ</p></li>
</ul>
<p>既定では、ServerCertification.asmx ファイルは、AD RMS サーバーの <code>\inetpub\wwwroot\_wmcs\certification\</code> フォルダー内にあります。詳細については、「<a href="https://go.microsoft.com/fwlink/p/?linkid=186951">AD RMS サーバー証明パイプラインにアクセス許可を設定する</a>」を参照してください。</p></li>
<li><p><strong>AD RMS スーパー ユーザー</strong>   トランスポート復号化、ジャーナル レポート復号化、Outlook Web App の IRM、および Exchange Search の IRM を有効にするには、Exchange 2013 セットアップ プログラムによって作成されるシステム メールボックスであるフェデレーション メールボックスを、AD RMS クラスターのスーパー ユーザー グループに追加する必要があります。詳細については、「<a href="add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md">フェデレーション メールボックスを AD RMS のスーパー ユーザー グループに追加する</a>」を参照してください。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange</p></td>
<td><ul>
<li><p>Exchange 2010 以降が必要です。</p></li>
<li><p>「<a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=973136">FIX: .NET Framework 2.0 SP2 ベースのアプリケーションが、非同期の ASP.NET Web サービス要求に対する長さゼロの応答を処理しようとすると、「値を NULL にすることはできません」という ArgumentNullException 例外エラー メッセージが表示される</a>」という修正プログラムが、Microsoft .NET Framework 2.0 SP2 には推奨されます。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook</p></td>
<td><ul>
<li><p>ユーザーは、Outlook でメッセージを IRM で保護できます。Outlook 2003 およびそれ以降では、メッセージを IRM で保護するための AD RMS テンプレートがサポートされます。</p></li>
<li><p>Outlook の保護ルールは、Exchange 2010 および Outlook 2010 の機能です。以前のバージョンの Outlook では、この機能はサポートされません。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync</p></td>
<td><ul>
<li><p>Exchange ActiveSync プロトコル Version 14.1 をサポートするデバイス (Windows Mobile デバイスを含む) は、Exchange ActiveSync で IRM をサポートできます。デバイスのモバイル電子メール アプリケーションでは、Exchange ActiveSync プロトコル Version 14.1 で定義されている <strong>RightsManagementInformation</strong> タグがサポートされる必要があります。Exchange 2013 では、Exchange ActiveSync の IRM を使用することで、サポートされるデバイスを所有するユーザーは、そのデバイスをコンピューターに接続して IRM 用にアクティブ化することなく、IRM で保護されたメッセージの表示、返信、転送、および作成を行うことができます。詳細については、「<a href="information-rights-management-in-exchange-activesync-exchange-2013-help.md">Exchange ActiveSync での Information Rights Management</a>」を参照してください。</p></li>
</ul></td>
</tr>
</tbody>
</table>



> [!NOTE]
> <EM>AD RMSクラスター</EM>とは、単一サーバーの展開を含めた、組織での AD RMS の展開に使用される用語です。AD RMS は Web サービスです。Windows Server フェールオーバー クラスターを設定する必要はありません。高可用性と負荷分散を実現するには、クラスター内に複数の AD RMS サーバーを展開して、ネットワーク負荷分散を使用できます。




> [!IMPORTANT]
> 運用環境では、同じサーバーへの AD RMS および Exchange のインストールはサポートされていません。



Exchange 2013 IRM 機能では、Microsoft Office ファイル形式がサポートされています。カスタム プロテクターを展開することで、IRM 保護を他のファイル形式に拡張できます。カスタム プロテクターの詳細については、[独立ソフトウェア ベンダー](https://go.microsoft.com/fwlink/p/?linkid=210336)の「情報保護と管理パートナー」を参照してください。

情報漏洩について

## IRM の構成とテスト

Exchange 2013 で IRM 機能を構成するには、Exchange 管理シェルを使用する必要があります。個々の IRM 機能を構成するには、[Set-IRMConfiguration](https://technet.microsoft.com/ja-jp/library/dd979792\(v=exchg.150\)) コマンドレットを使用します。内部メッセージ、トランスポート復号化、ジャーナル レポート復号化、Exchange Search、および Outlook Web App の IRM を有効または無効にできます。IRM 機能の構成の詳細については、「[Information Rights Management の手順](information-rights-management-procedures-exchange-2013-help.md)」を参照してください。

Exchange 2013 サーバーを設定すると、[Test-IRMConfiguration](https://technet.microsoft.com/ja-jp/library/dd979798\(v=exchg.150\)) コマンドレットを使用して IRM 展開のエンドツーエンド テストを実行できます。これらのテストは、IRM 機能を初期の IRM 構成直後および継続的に検証する場合に便利です。このコマンドレットは、次のテストを実行します。

  - Exchange 2013 組織の IRM 構成を検査する

  - AD RMS サーバーのバージョンや修正プログラムの情報を確認する

  - 権利アカウント証明書 (RAC) とクライアント ライセンサー証明書を取得することで、Exchange サーバーを RMS 用にアクティブにできるかどうかを確認する

  - AD RMS 権利ポリシー テンプレートを AD RMS サーバーから取得する

  - 指定された送信者が IRM で保護されたメッセージを送信できることを確認する

  - 指定された受信者のスーパー ユーザー使用ライセンスを取得する

  - 指定された受信者のプレライセンスを取得する

情報漏洩について

## 権限管理コネクタで権利の管理を拡張

Microsoft 権利管理コネクタ (RMS コネクタ) は、クラウドベースの Microsoft 権利管理サービスの導入によって、Exchange 2013 サーバーのデータ保護を拡張するオプションのアプリケーションです。RMS コネクタをインストールすると、情報の使用期間にわたって継続的なデータ保護を提供するだけでなく、これらのサービスはカスタマイズできるため、必要となる保護レベルを定義することができます。たとえば、特定のユーザーに電子メール メッセージのアクセスを制限または特定のメッセージについて表示のみの権限を設定できます。

RMS コネクタについての詳細およびインストール方法については、「[権利管理コネクタ](https://technet.microsoft.com/ja-jp/library/dn375964.aspx)」を参照してください。

