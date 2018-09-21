---
title: '購読済みのエッジ トランスポート サーバーを介してインターネット メール フローを構成する: Exchange 2013 Help'
TOCTitle: 購読済みのエッジ トランスポート サーバーを介してインターネット メール フローを構成する
ms:assetid: d12ea770-99ce-4ab4-a373-96f2554641fa
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb738158(v=EXCHG.150)
ms:contentKeyID: 61180564
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 購読済みのエッジ トランスポート サーバーを介してインターネット メール フローを構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-08_

エッジ トランスポート サーバー経由のインターネット メールを確立するには、Active Directory サイトに対してエッジ トランスポート サーバーを購読します。この方法により、インターネット メール フローに必要な次の 2 つの送信コネクタが自動的に作成されます。

  - すべてのインターネット ドメインに送信電子メールを送信するように構成されている送信コネクタ

  - エッジ トランスポート サーバーから Exchange 2013 メールボックス サーバーに受信電子メールを送信するように構成されている送信コネクタ

エッジ トランスポート サーバーを Active Directory サイトに対して購読しない場合は、メールボックス サーバーとエッジ トランスポート サーバーとの間のメール フローの確立に必要な送信コネクタを手動で作成できます。詳細については、「[EdgeSync を使用せずにエッジ トランスポート サーバー経由のインターネット メール フローを構成する](configure-internet-mail-flow-through-an-edge-transport-server-without-using-edgesync-exchange-2013-help.md)」を参照してください。しかし、可能な場合は常に、Active Directory サイトに対してエッジ トランスポート サーバーを購読することをお勧めします。

## 開始する前に

  - 予想所要時間 : 20 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」トピックの「EdgeSync」と「エッジ トランスポート サーバー」。

  - 組織に対してエッジ トランスポート サーバーを購読する前に、まず Exchange 組織用に権限のあるドメインと電子メール アドレス ポリシーを構成する必要があります。

  - Exchange 組織から境界ネットワークを分離するファイアウォールによりセキュリティで保護された LDAP ポート 50636/TCP を有効にします。エッジ トランスポート サーバーは、購読済みの Active Directory サイト内のすべての Exchange 2013 メールボックス サーバーと通信できる必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 購読済みのエッジ トランスポート サーバーを介してインターネット メール フローを構成する

1.  エッジ トランスポート サーバーで、次の構文を使用してエッジ サブスクリプション ファイルを作成します。
    
        New-EdgeSubscription -FileName <FileName>.xml [-Force]
    
    次の例では、C:\\My Documents フォルダーに EdgeSubscriptionInfo.xml という名前のエッジ サブスクリプション ファイルを作成します。*Force* パラメーターは、無効になるコマンドを確認するプロンプトと、エッジ トランスポート サーバー上の構成データが上書きされることに対する警告が表示されないようにします。
    
    ```powershell
New-EdgeSubscription -FileName "C:\My Documents\EdgeSubscriptionInfo.xml" -Force
```

2.  作成したエッジ サブスクリプション ファイルを、エッジ トランスポート サーバーの購読先の Active Directory サイト内のメールボックス サーバーにコピーします。

3.  メールボックス サーバーで、エッジ サブスクリプション ファイルをインポートするには、次の構文を使用します。
    
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "<FileName>.xml" -Encoding Byte -ReadCount 0)) -Site <SiteName>
    
    この例では、D:\\Data フォルダーから EdgeSubscriptionInfo.xml という名前のエッジ サブスクリプション ファイルをインポートし、"Default-First-Site-Name" という名前の Active Directory サイトに対してエッジ トランスポート サーバーを購読します。
    
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "D:\Data\EdgeSubscriptionInfo.xml" -Encoding Byte -ReadCount 0)) -Site "Default-First-Site-Name"
    

    > [!NOTE]
    > <EM>CreateInternetSendConnector</EM> パラメーターか <EM>CreateInboundSendConnector</EM> パラメーターを使って、必要な送信コネクタの一方または両方が自動的に作成されないようにすることができます。詳細については、「<A href="edge-subscriptions-exchange-2013-help.md">エッジ サブスクリプション</A>」を参照してください。



4.  メールボックス サーバーで、次のコマンドを実行して、最初の EdgeSync 同期を開始します。
    
    ```powershell
Start-EdgeSynchronization
```

5.  終了後に、エッジ サブスクリプション ファイルをエッジ トランスポート サーバーとメールボックス サーバーの両方から削除することをお勧めします。エッジ サブスクリプション ファイルには、LDAP 通信プロセス中に使用する資格情報に関する情報が含まれています。

