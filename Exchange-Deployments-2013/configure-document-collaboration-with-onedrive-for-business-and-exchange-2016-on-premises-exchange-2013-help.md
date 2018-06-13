---
title: 'OneDrive for Business と Exchange 2016 (オンプレミス) を使用して最新の添付ファイルを構成する: Exchange 2013 Help'
TOCTitle: OneDrive for Business と Exchange 2016 (オンプレミス) を使用して最新の添付ファイルを構成する
ms:assetid: 799518aa-7cfe-4708-92ee-98057ff168f5
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Mt589761(v=EXCHG.150)
ms:contentKeyID: 70318052
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# OneDrive for Business と Exchange 2016 (オンプレミス) を使用して最新の添付ファイルを構成する

 

_**適用先:**Exchange Server 2016_

_**トピックの最終更新日:**2016-12-09_

**概要**:オンプレミスの Exchange Server 2016 ユーザーに、ハイブリッド構成における OneDrive for Business と SharePoint Online のドキュメント コラボレーションを活用できるようにする方法。

Office 365 では、新しい添付オプションが利用可能になっています。Exchange 2016 では、このオプションは*ドキュメントのコラボレーション*と呼ばれ、オンプレミスのユーザーが OneDrive for Business に保存されている添付ファイルを Outlook on the web クライアントに直接統合することができます。


> [!NOTE]
> Exchange Server 2016 リリース以降、Outlook Web App は Outlook on the web と呼ばれます。



従来、ユーザーはファイルをメッセージに添付して、他のユーザーに送信していました。受信者がそれぞれ、そのファイルのコピーに変更を加えると、いずれかの時点で最終的にはその変更をすべてマージする必要がありました。また、これらの添付ファイルはそれぞれ、各ユーザーのメールボックスの記憶域スペースを消費します。ドキュメントのコラボレーションでは、ユーザーは OneDrive for Business アカウントに保存されているファイルへのリンクを挿入することによって、追加の記憶域スペースを必要とせず、複数のユーザーが同じソースの場所でそのファイルを編集できます。

ドキュメントのコラボレーション用に Exchange 2016 環境が正しく構成されていないと、Outlook on the web ユーザーの既定の添付ファイルのダイアログは、次のようになります。

![従来の \[添付ファイル\] ダイアログ](images/Mt589761.f8c74d70-42f9-48c6-b263-ce6cef8591a8(EXCHG.150).png "従来の [添付ファイル] ダイアログ")

次の手順で環境を構成すると、Outlook on the web の添付ファイル ダイアログは次のようになります。

![最新の添付ファイルが有効になっている \[添付ファイル\] ダイアログ](images/Mt589761.89eeae65-ce3a-4c47-b57e-db734a1de95b(EXCHG.150).png "最新の添付ファイルが有効になっている [添付ファイル] ダイアログ")

オンプレミスのメール ボックスのある組織内のユーザー、および Office 365 の OneDrive for Business アカウントのあるユーザーは、最新の添付ファイル メソッドを使用して、OneDrive for Business に保存されているドキュメントを複数の受信者と共有することができます。受信者の場所 (オンラインやオンプレミス) はどこでもかまいません。

ハイブリッド展開の詳細については、「[Exchange Server のハイブリッド展開](exchange-server-hybrid-deployments-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間: 15 分

  - 「[Exchange Server のハイブリッド展開](exchange-server-hybrid-deployments-exchange-2013-help.md)」を参照し、ハイブリッド展開の構成によって影響を受ける領域を必ず確認しておいてください。

  - 「[ハイブリッド展開の前提条件](hybrid-deployment-prerequisites-exchange-2013-help.md)」に示されたすべてのハイブリッド展開要件を確認し、満たしておく必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](https://technet.microsoft.com/ja-jp/library/jj150484\(v=exchg.150\))」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## ハイブリッド環境でのドキュメントのコラボレーションを有効にする Exchange 2016 の構成

次の前提条件の手順を完了していることを確認し、ドキュメントのコラボレーションを有効にする手順を実行します。

**前提条件**

  - [ハイブリッド構成ウィザード](hybrid-configuration-wizard-exchange-2013-help.md) (HCW) を使用して Exchange ハイブリッド環境を構成します。

  - Exchange 2016 をオンプレミスの組織にインストールしておく必要があります。Exchange 2016 は Exchange の以前のバージョンと共存できますが、ドキュメントのコラボレーションは Exchange 2016 サーバーのメールボックス以外では機能しません。

  - 同期するすべてのユーザーについて、認証サーバーをインストールする必要があります。認証サーバーを検索するには、[Get-AuthServer](https://technet.microsoft.com/ja-jp/library/jj218613\(v=exchg.150\)) コマンドレットを使用できます。Exchange 2016 サーバーから HCW を使用して、必要な OAuth を設定することをお勧めします。
    

    > [!IMPORTANT]
    > Exchange 2016 と Office 365 の間で OAuth を正しく設定する必要があります。詳細については、「<A href="https://technet.microsoft.com/ja-jp/library/dn594521(v=exchg.150)">Exchange と Exchange Online 組織の間の OAuth 認証の構成</A>」を参照してください。



  - ユーザーには、適切なライセンスが必要です。OneDrive for Business アカウントのユーザーは、SharePoint Online または OneDrive for Business のライセンスを取得する必要があります。ユーザーのライセンスは、Office 365 ポータルでユーザーを選択し、**\[編集\]** ボタンをクリックすると検証できます。
    

    > [!NOTE]
    > 詳細については、「<A href="https://support.office.com/ja-jp/article/office-365-%e3%81%ae-onedrive-for-business-%e2%80%93-%e7%ae%a1%e7%90%86%e3%83%98%e3%83%ab%e3%83%97-3e21f8f0-e0a1-43be-aa3e-8c0236bf11bb?omkt=ja-jp%26ui=ja-jp%26rs=ja-jp%26ad=jp">Office 365 の OneDrive for Business – 管理ヘルプ</A>」を参照してください。



次の手順を実行します。

1.  既定の Outlook on the web メールボックス ポリシーを設定し、OneDrive for Business ホスト URL が設定されるようにします。
    

    > [!NOTE]
    > Office 365 SharePoint Online テナント管理に進み、OneDrive for Business ホスト URL を取得します。たとえば、https://contoso-my.sharepoint.com は Contoso の Office365 テナントでの個人用サイトのホストの URL です。<BR>Exchange 2016 に付属の Outlook on the web メールボックス ポリシーは「既定」と呼ばれますが、既定のポリシーに設定するか、メールボックスに直接割り当てなければ、自動的にメールボックスには適用されません。

    
    次の例を基本として、Exchange 管理シェル を使用して、既定の Outlook on the web メールボックス ポリシーに内部または外部の個人用サイトの URL を設定します。
    
        Set-OwaMailboxPolicy Default -InternalSPMySiteHostURL https://Contoso-my.sharepoint.com -ExternalSPMySiteHostURL https://Contoso-my.sharepoint.com

2.  次に、設定したポリシーを既定のポリシーとしてすべてのメールボックスに適用されるようにするか、そのポリシーを個々のユーザーに割り当てます。
    
    そのポリシーを既定の Outlook on the web メールボックス ポリシーにするには、Exchange 管理シェル で次のコマンドを入力します。
    
        Set-OwaMailboxPolicy Default -IsDefault 
    
    そのポリシーを個々のメールボックスに割り当てるには、Exchange 管理シェル で次のコマンドを入力します。
    
        Set-CASMailbox <user mailbox> -OwaMailboxPolicy Default

3.  (省略可能) それぞれの Exchange 2016 サーバーで、設定作業をすぐに開始できる **OWAApplicationPool** を再起動します。このコマンドを実行しない場合、Exchange 2016 サーバーで更新したメールボックス ポリシーが適用されるまで数分かかります。Exchange 管理シェル で次を実行します。
    
        Restart-WebAppPool MSExchangeOWAAppPool

設定したら、Outlook on the web ユーザーは、メッセージに適用できる添付ファイルの種類を、従来のものか最新のものにするか選択できるようになります。

![\[OneDrive と共有\] または \[添付ファイルとして共有\] が含まれる \[添付ファイル\] オプション ダイアログ](images/Mt589761.7d2f27c2-3638-479a-a577-029ac61e7d95(EXCHG.150).png "[OneDrive と共有] または [添付ファイルとして共有] が含まれる [添付ファイル] オプション ダイアログ")

