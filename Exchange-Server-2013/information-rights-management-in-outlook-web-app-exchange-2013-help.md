---
title: 'Outlook Web App での Information Rights Management: Exchange 2013 Help'
TOCTitle: Outlook Web App での Information Rights Management
ms:assetid: 60a49dab-17ac-4d2c-9b41-7d87250d6c00
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd876891(v=EXCHG.150)
ms:contentKeyID: 49896276
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Web App での Information Rights Management

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2016-12-09_

インフォメーション ワーカーが電子メールを使用して機密情報をやり取りする機会が増えています。この情報をセキュリティ保護するため、組織は Information Rights Management (IRM) を使用して、メッセージング コンテンツに強力な保護を適用できます。Microsoft Exchange Server 2010 より前では、IRM 保護の使用による効果は Outlook クライアントに限られていました。Exchange Server 2007 では、Microsoft Outlook Web Access ユーザーが IRM 保護されたコンテンツにアクセスできるようになるには、Microsoft Internet Explorer 用 Rights Management アドインをダウンロードする必要があります。

Exchange 2013 では Outlook Web App の IRM により、ユーザーは Exchange により提供される豊富な IRM 機能にアクセスして、メッセージング コンテンツに強力な IRM 保護を適用できます。

Outlook Web App では、次の IRM 機能があります。

  - **IRM 保護されたメッセージの送信**   以下の図のように、Outlook Web App ユーザーはアクセス許可ドロップダウン リストを使用して、メッセージに適用する権利ポリシー テンプレートを選択できます。これにより、Outlook Web App 内から IRM 保護されたメッセージを送信できます。メッセージは、クライアント アクセス サーバーによって IRM 保護されます。
    
    ![OWA から IRM 保護されているメッセージを送信](images/Dd876891.fa8cabb5-c049-46dc-8b29-9d9957dbfd3e(EXCHG.150).gif "OWA から IRM 保護されているメッセージを送信")  

  - **IRM 保護された添付ファイル**   ユーザーが Outlook Web App から IRM 保護されたメッセージを送信するとき、そのメッセージに添付されるあらゆる添付ファイルも同様の IRM 保護を受け、メッセージと同じ権利ポリシー テンプレートを使用して保護されます。Exchange 2013 では、Microsoft OfficeWord、Excel、と PowerPoint に関連付けられたファイル、および .xps ファイルと電子メール メッセージに IRM 保護が適用されます。添付ファイルがまだ IRM 保護されていない場合にのみ IRM 保護が適用されます。Active Directory Rights Management サービス (AD RMS) 権利ポリシー テンプレートの詳細については、「[Information Rights Management](information-rights-management-exchange-2013-help.md)」を参照してください。
    

    > [!NOTE]
    > Outlook Web App では、IRM はここの説明にあるサポートされる添付ファイルのみを保護します。サポートされないファイル形式を使用する添付ファイルは保護されません。Outlook Web App ユーザーがメッセージを保護する場合に、サポートされない種類のファイルを添付すると、サポートされるファイルのみが保護される旨を知らせる通知が表示されます。

    

    > [!IMPORTANT]
    > IRM 保護は、既に S/MIME を使用して署名、または暗号化されているメッセージには適用できません。IRM 保護を適用するには、S/MIME 署名または暗号化をメッセージから取り除く必要があります。同じことが IRM 保護されたメッセージにも当てはまります。ユーザーは S/MIME を使用して署名、または暗号化できません。



  - **IRM 保護されたメッセージの読み取り**   組織の AD RMS クラスターを使用して送信者によって保護されたメッセージは、Outlook Web App のプレビュー ウィンドウに表示されます。アドインを追加する必要はなく、コンピューターを AD RMS 展開に登録する必要はありません。ユーザーがメッセージを開いたりプレビュー ウィンドウで表示すると、プレライセンス エージェントによって追加された使用ライセンスを使用して、メッセージは暗号化が解除されます。暗号化の解除後は、メッセージはプレビュー ウィンドウに表示されます。プレライセンスが利用できない場合、Outlook Web App は AD RMS サーバーからプレライセンスを要求して、メッセージを表示します。Outlook Web App 内の添付ファイルの IRM 保護された添付ファイルを読み取るとき、WebReady ドキュメント表示は利用できません。
    

    > [!NOTE]
    > Outlook Web App 内の IRM は、Outlook およびその他の Office アプリケーションが行う Print Screen 機能を使用したスクリーン キャプチャーを防止できません。これは、AD RMS 権利ポリシー テンプレート内で指定されるとメッセージ コンテンツのコピーを防止する EXTRACT 権利に影響します。



  - **クロスブラウザー、複数プラットフォーム IRM のサポート**Outlook Web App 内の IRM は、クロスブラウザー、複数プラットフォームの IRM サポートを提供します。Outlook Web App 内の IRM は、Apple Macintosh と Linux オペレーティング システムを含む Exchange 2013 によりサポートされるすべてのブラウザーでサポートされます。サポートされるブラウザーとオペレーティング システムの詳細については、「[Outlook Web App をサポートしているブラウザー](https://go.microsoft.com/fwlink/p/?linkid=129362)」を参照してください。

  - **WebReady ドキュメント表示**Exchange 2013 では、ユーザーは WebReady ドキュメント表示を使用して、サポートされている IRM で保護された添付ファイルを表示できます。これにより、ユーザーは、関連付けられたアプリケーションを使用する添付ファイルをダウンロードせずに、サポートされている添付ファイルを表示できます。

IRM の管理に関連する管理タスクについては、「[Information Rights Management の手順](information-rights-management-procedures-exchange-2013-help.md)」をご覧ください。

## Outlook Web App で IRM を有効にする

Outlook Web App 内で IRM を有効にするには、AD RMS 内のスーパー ユーザー グループに Exchange 2013 セットアップによって作成されるシステム メールボックスであるフェデレーション メールボックスを追加する必要があります。詳細については、「[フェデレーション メールボックスを AD RMS のスーパー ユーザー グループに追加する](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)」を参照してください。これにより、Exchange 2013 サーバーは IRM で保存されたメッセージにアクセスできるようになります。

Outlook Web App 管理シェルで [Set-IRMConfiguration](https://technet.microsoft.com/ja-jp/library/dd979792\(v=exchg.150\)) コマンドレットを使用して、Exchange で IRM を有効にすることもできます。 これにより、Outlook Web App 組織の Exchange 2013 内の IRM が有効になります。Outlook Web App 仮想ディレクトリの Outlook Web App 内の IRM を無効、有効にできます。Outlook Web App 内の IRM は、次の細分レベルで制御することもできます。

  - **Per-Outlook Web App 仮想ディレクトリ**   Outlook Web App 仮想ディレクトリの Outlook Web App 内の IRM を有効または無効にするには、**Set-OWAVirtualDirectory** コマンドレットを使用して、*IRMEnabled* パラメーターを `$false` または `$true` (既定) に設定します。これで、Exchange 2013 クライアント アクセス サーバー上のある仮想ディレクトリを有効にしたまま、別のクライアント アクセス サーバー上の別の仮想ディレクトリの Outlook Web App 内の IRM を無効にできます。

  - **Per-Outlook Web App メールボックス ポリシー**   Outlook Web App メールボックス ポリシーの Outlook Web App 内の IRM を有効または無効にするには、**Set-OWAMailboxPolicy** コマンドレットを使用して、*IRMEnabled* パラメーターを `$false` または `$true` (既定) に設定します。これで、Outlook Web App 内の IRM を、ある 1 組のユーザーに対して有効し、別の 1 組のユーザーに対して無効にできます。これを行うには、それぞれの組に対して別の Outlook Web App メールボックス ポリシーを割り当てます。

詳細については、「[クライアント アクセス サーバーで Information Rights Management を有効または無効にする](enable-or-disable-information-rights-management-on-client-access-servers-exchange-2013-help.md)」を参照してください。

