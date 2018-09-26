---
title: 'UM の証明書を作成する: Exchange 2013 Help'
TOCTitle: UM の証明書を作成する
ms:assetid: 66807ee7-3d3f-482d-a3ac-d4e9baca3271
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn205141(v=EXCHG.150)
ms:contentKeyID: 54652971
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM の証明書を作成する

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2013-04-29_

EAC の Exchange 証明書の新規作成ウィザードまたはシェルを使用して、自己署名証明書、または、内部公開キー基盤 (PKI) 証明書に対する証明書要求を作成できます。ユニファイド メッセージング (UM) では、Microsoft Exchange ユニファイド メッセージング サービスと Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスの両方にこれらの証明書のいずれかを使用できます。両方のサービスに対して同じ証明書を使用することも、サービスごとに別々の証明書を使用することもできます。UM サービス用のサード パーティ商用証明書を購入してインポートすることもできます。UM 用の自己署名証明書を使用している場合は、クライアント アクセス サーバーとメールボックス サーバーの名前をサブジェクトの別名 (SAN) に含める必要があります。

既定では、Exchange Server 2013 をインストールすると、**Microsoft Exchange Server Auth Certificate** と **Microsoft Exchange** という 2 つの自己署名証明書が作成されます。**Microsoft Exchange** 自己署名証明書は UM によるデータの暗号化に使用できますが、この証明書を UM サービスと UM 呼び出しルーター サービスに割り当てる必要があります。証明書をユニファイド メッセージング サービスに割り当てた後、その証明書を VoIP ゲートウェイ、IP PBX、または SIP 対応 PBX にコピーしたり、インポートしたりできます。ただし、既定の自己署名証明書を使用する代わりに、ユニファイド メッセージング専用の別の証明書を作成しなければならない場合があります。


> [!NOTE]
> UM と Microsoft Lync Server が統合されている場合は自己署名証明書を使用できません。



ユニファイド メッセージング用の証明書の管理に関連したその他の管理タスクについては、「[UM の証明書の展開手順](deploying-certificates-for-um-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。 「[Exchange およびシェル インフラストラクチャのアクセス許可](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)」の「証明書管理」と「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM サービス」。コンピューター上のローカルな Administrators グループのメンバーであるアカウントを使用してログオンする必要もあります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して UM に対する証明書要求を作成する

1.  EAC で、<strong>サーバー</strong> \> <strong>証明書</strong> の順に選択してから、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  <strong>Exchange 証明書の新規作成</strong> ページで、<strong>証明機関発行の証明書の要求を作成する</strong> を選択してから、<strong>次へ</strong> をクリックします。

3.  証明書のフレンドリ名を入力してから、<strong>次へ</strong> をクリックします。

4.  ワイルドカード証明書が必要ない場合は、<strong>次へ</strong> をクリックします。ワイルドカード証明書が必要な場合は、<strong>Request a wildcard certificate. A wildcard certificate can be used to secure all sub-domains under your root domain with a single certificate</strong> を選択して、ルート ドメインの名前を入力してから、<strong>次へ</strong> をクリックします。

5.  <strong>Store certificate request on this server</strong> で、<strong>参照</strong> をクリックしてファイルの保存場所に移動します。証明書要求は Exchange 組織内の任意のクライアント アクセス サーバーまたはメールボックス サーバーに保存できます。場所を選択して、<strong>OK</strong> をクリックしてから、<strong>次へ</strong> をクリックします。

6.  ワイルドカード証明書を要求した場合は、手順 9 に進みます。

7.  ワイルドカード証明書を要求していない場合は、証明書に含めるドメインを指定する必要があります。ドメインを編集する場合は、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックしてから、<strong>次へ</strong> をクリックします。

8.  <strong>Based on your selections, the following domains will be included in your certificate. You can add additional domains here, or make changes</strong> では、<strong>ドメイン</strong> に列挙されたドメインの名前を追加、編集、削除、または確認できます。その後で、<strong>次へ</strong> をクリックします。

9.  <strong>Specify information about your organization. This is required by the certification authority</strong> で、以下を入力します。
    
      - **組織名**
    
      - **部署名**
    
      - **市区町村**
    
      - **都道府県**
    
      - <strong>国/地域名</strong>   このオプションでは、ドロップダウン リストを使用して国または地域を選択します。

10. <strong>Save the certificate request to the following file</strong> で、証明書ファイルの名前を入力してから、<strong>完了</strong> をクリックします。

## シェルを使用して UM に対する証明書要求を作成する

この例では、フレンドリ名が `CertUM` で `MyMailboxServer` という名前のメールボックス サーバーに対する新しい Exchange 証明書要求を作成します。

```powershell
    New-ExchangeCertificate -FriendlyName 'CertUM' -GenerateRequest -PrivateKeyExportable $true -KeySize '2048' -DomainName '*.northwindtraders.com' -SubjectName 'C=US,S=wa,L=redmond,O=northwindtraders,OU=servers,CN= northwindtraders.com' -Server 'MyMailboxServer'
```

## EAC を使用して UM 用の自己署名証明書を作成する

1.  EAC で、<strong>サーバー</strong> \> <strong>証明書</strong> の順に選択してから、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  <strong>Exchange 証明書の新規作成</strong> ページで、<strong>自己署名証明書を作成する</strong> を選択してから、<strong>次へ</strong> を選択します。

3.  証明書のフレンドリ名を入力してから、<strong>次へ</strong> を選択します。

4.  <strong>追加</strong> ![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックしてこの証明書を適用する Exchange サーバーを選択してから、<strong>次へ</strong> を選択します。

5.  証明書に含めるドメインを指定してから、<strong>次へ</strong> を選択します。サービス用のドメインを追加する場合は、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

6.  追加したドメインが正しいことを確認してから、<strong>完了</strong> を選択します。


> [!IMPORTANT]
> EAC を使用して自己署名証明書を作成した場合は、証明書に対してサービスを有効にするように要求されません。証明書が作成されたら、EAC またはシェルの <STRONG>Enable-ExchangeCertificate</STRONG> コマンドレットを使用して、Exchange サービスを有効にすることができます。UM サービスに証明書を割り当てる方法については、「<A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">UM および UM 呼び出しルーター サービスへの証明書の割り当て</A>」を参照してください。



## シェルを使用して UM 用の自己署名証明書を作成する

この例では、フレンドリ名が `UMCert` で `MyMailboxServer` という名前のメールボックス サーバーに対する新しい Exchange 自己署名証明書を作成します。

```powershell
    New-ExchangeCertificate -Services 'UM, UMCallRouter' -DomainName '*.northwindtraders.com' -FriendlyName 'UMSelfSigned' -SubjectName 'C=US,S=WA,L=Redmond,O=Northwindtraders,OU=Servers,CN= Northwindtraders.com' -PrivateKeyExportable $true
```

> [!TIP]
> <EM>Services</EM> パラメーターを使用して有効にするサービスを指定した場合は、それらのサービスを割り当てるように要求されます。この例では、UM サービスと UM 呼び出しルーター サービスに対して証明書を有効にするように要求されます。サービスの証明書を有効にする方法については、「<A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">UM および UM 呼び出しルーター サービスへの証明書の割り当て</A>」を参照してください。


