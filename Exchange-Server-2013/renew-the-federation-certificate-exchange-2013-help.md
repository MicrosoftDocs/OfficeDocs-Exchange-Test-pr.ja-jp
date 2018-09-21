---
title: 'フェデレーション証明書を更新する: Exchange 2013 Help'
TOCTitle: フェデレーション証明書を更新する
ms:assetid: 0f390713-3058-44d0-9c07-3c982616e790
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Mt779252(v=EXCHG.150)
ms:contentKeyID: 74429164
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# フェデレーション証明書を更新する

 

_**トピックの最終更新日:** 2017-02-28_

このトピックでは、フェデレーション信頼で使用した自己署名入りのフェデレーション証明書の更新の方法を説明します。

  - フェデレーション証明書の有効期限が切れていないければ、「作業中のフェデレーション証明書の更新」のセクションの手順に従ってください。

  - フェデレーション証明書が既に有効期限切れの場合は、「有効期限切れのフェデレーション証明書の置き換え」のセクションの手順に従ってください。

フェデレーション信頼とフェデレーションについての詳細は、「[フェデレーション](federation-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 10 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[Exchange およびシェル インフラストラクチャのアクセス許可](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)」のトピックの「フェデレーションと証明書」の項目。

  - このトピックの手順では Exchange 管理シェル を使います。オンプレミスの Exchange 組織で Exchange 管理シェル を開く方法については、「[シェルを開く](https://technet.microsoft.com/ja-jp/library/dd638134\(v=exchg.150\))」を参照してください。

  - 既存のフェデレーション証明書の有効期限が切れているかどうかを確かめるには、Exchange 管理シェル で次のコマンドを実行します。
    
        Get-ExchangeCertificate -Thumbprint (Get-FederationTrust).OrgCertificate.Thumbprint | Format-Table -Auto Thumbprint,NotAfter

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!WARNING]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 作業中のフェデレーション証明書の更新

フェデレーション証明書の有効期限が切れていない場合は、新しいフェデレーションの証明書で既存のフェデレーション信頼を更新できます。

## 手順 1:新しいフェデレーション証明書を作成する

Exchange 管理シェル で次のコマンドを実行して、新しいフェデレーション証明書を作成します。

    $SKI = [System.Guid]::NewGuid().ToString("N"); New-ExchangeCertificate -DomainName 'Federation' -FriendlyName "Exchange Delegation Federation" -Services Federation -SubjectKeyIdentifier $SKI -PrivateKeyExportable $true

構文およびパラメーターの詳細については、「[New-ExchangeCertificate](https://technet.microsoft.com/ja-jp/library/aa998327\(v=exchg.150\))」を参照してください。

コマンド出力には、新しい証明書の拇印値が含まれます。この値は、残りの手順で必要になり、次のようにして Exchange 管理シェル ウィンドウから直接コピーすることができます。

1.  Exchange 管理シェル ウィンドウの任意の場所で右クリックし、表示されるダイアログ ボックスで <strong>マーク</strong> を選択します。

2.  拇印値を選択し、Enter キーを押します。

このトピックのその他の手順で、このフェデレーション証明書の拇印値 (`6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73`) を使用します。実際の証明書の拇印値は異なります。

## 手順 2:新しい証明書をフェデレーション証明書として構成する

Exchange 管理シェル を使って、新しい証明書をフェデレーション証明書として構成するには、次の構文を使用します。

    Set-FederationTrust -Identity "Microsoft Federation Gateway" -Thumbprint <Thumbprint> -RefreshMetaData

この例では、手順 1 の証明書の拇印値 `6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73` を使用します。

    Set-FederationTrust -Identity "Microsoft Federation Gateway" -Thumbprint 6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73 -RefreshMetaData

構文およびパラメーターの詳細については、「[Set-FederationTrust](https://technet.microsoft.com/ja-jp/library/dd298034\(v=exchg.150\))」を参照してください。

**メモ**:コマンド出力には、DNS でドメイン所有権証明 TXT レコードを更新する必要があるという警告が含まれています。これは、次の手順で行います。

## 手順 3:外部の DNS で、フェデレーションのドメイン所有権証明 TXT レコードを更新します。

ドメイン所有権証明 TXT レコードはアクティブ化 (手順 5) の際にのみチェックされるため、この段階では安全にこの手順を実行できます。ただし、TXT レコードを更新した後、次の手順を続行する前に、更新した TXT レコードが伝達されるまで待つ (その時間は DNS レコードの TTL (time to live) の値に応じる) 必要があります。

1.  Exchange 管理シェル で次のコマンドを実行して、必要な TXT レコードに必要な値を調べます。
    
    ```powershell
Get-FederatedDomainProof -DomainName <Domain> | Format-List Thumbprint,Proof
```
    
    たとえば、フェデレーション ドメインが contoso.edu であれば次のコマンドを実行します。
    
    ```powershell
Get-FederatedDomainProof -DomainName contoso.com | Format-List Thumbprint,Proof
```
    
    コマンド出力は次のようになります。
    
    `Thumbprint : <new certificate thumbprint>` (例: `6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73`)
    
    `Proof      : <new hash text>` (例: `znMfbkgSbOQSsWFdsW+gm3to0nZSdE3zbcPPHGVAqdgsLFGsCPuLHiyVbKoPmgyZKX90NH2g1PbCZH0YTQF6oA==`)
    
    `Thumbprint : <old certificate thumbprint>` (例: `CC9BC204BB4DC60D06FC1F10F3C373DC785DA2A5`)
    
    `Proof      : <old hash text>` (例: `m4gZX7OLr9iOWYJMVjEklQpoSkPb5hSbcFjD7Q3/vsqmdJ2Z+HcSt7j5pzBKFmEW2s27JYr3xsK2POzAI/8Ffw==`)
    
    コマンド出力は 2 つのドメイン所有権証明レコードの情報を返すことに注意してください。1 つは新しい証明書、もう 1 つは置き換えようとしている現在の証明書です。どちらの証明書の情報なのかは、拇印値とハッシュ テキスト値 (外部 (パブリック) DNS の現在のドメイン所有権証明 TXT レコードで構成されている) によって見分けることができます。

2.  外部 DNS で、フェデレーションのドメイン所有権証明 TXT レコードを更新します。DNS プロバイダーによって手順は異なりますが、現在の TXT レコードを編集して、現在のハッシュ テキスト値を新しいハッシュ テキスト値に置き換えることができます。詳細については、「[Office 365 の外部ドメイン ネーム システム レコード](https://go.microsoft.com/fwlink/p/?linkid=265522)」の Exchange Online のセクションを参照してください。

## 手順 4:新しいフェデレーション証明書がすべての Exchange サーバーに配布されているか確認します。

Exchange は新しいフェデレーション証明書を自動的にすべてのサーバーに配布しますが、次に進む前に配布の確認をする必要があります。

Exchange 管理シェル を使って、新しいフェデレーション証明書の配布を確認するために、次のコマンドを実行します。

    $Servers = Get-ExchangeServer; $Servers | foreach {Get-ExchangeCertificate -Server $_ | Where {$_.Services -match 'Federation'}} | Format-List Identity,Thumbprint,Services,Subject

**メモ**:Exchange 2010 では **Test-FederationCertificate** コマンドレット出力に、サーバー名が含まれます。Exchange 2013 以降でのこのコマンドレット出力には、サーバー名は含まれません。

## 手順 5:新しいフェデレーション証明書をアクティブ化する

Exchange 管理シェル で新しいフェデレーション証明書をアクティブ化するために次のコマンドを実行します。

```powershell
Set-FederationTrust -Identity "Microsoft Federation Gateway" -PublishFederationCertificate
```

構文およびパラメーターの詳細については、「[Set-FederationTrust](https://technet.microsoft.com/ja-jp/library/dd298034\(v=exchg.150\))」を参照してください。

**メモ**:コマンド出力には、DNS でドメイン所有権証明 TXT レコードを更新する必要があるという警告が含まれています (これは手順 3 で既に実行済みです)。

## 正常な動作を確認する方法

既存のフェデレーション信頼が新しいフェデレーション証明書で正常に更新されたかを確かめるためには、以下の手順に従います。

  - Exchange 管理シェル で、次のコマンドを実行して、新しい証明書が使用されていることを確認します。
    
        Get-FederationTrust | Format-List *priv*
    
      - **OrgPrivCertificate** プロパティには、新しいフェデレーション証明書の拇印を含める必要があります。
    
      - **OrgPrevPrivCertificate** プロパティには、古い (置き換え済みの) フェデレーション証明書の拇印を含める必要があります。

  - Exchange 管理シェル で、*\<user's email address\>* を組織のユーザーの電子メールアドレスに置き換え、次のコマンドを実行して、フェデレーション信頼が機能していることを確認します。
    
    ```powershell
Test-FederationTrust -UserIdentity <user's email address>
```

## 有効期限切れのフェデレーション証明書の置き換え

フェデレーション証明書の有効期限が既に切れている場合は、フェデレーション信頼からすべてのフェデレーション ドメインを削除し、フェデレーション信頼を削除して作成し直す必要があります。

1.  複数のフェデレーション ドメインを使っている場合は、プライマリ共有ドメインを識別しておいて、このドメインは最後に削除する必要があります。Exchange 管理シェル を使ってプライマリ共有ドメインとすべてのフェデレーション ドメインを識別するには、次のコマンドを実行します。
    
    ```powershell
Get-FederatedOrganizationIdentifier | Format-List AccountNamespace,Domains
```
    
    **AccountNamespace** プロパティの値には、`FYDIBOHF25SPDLT<primary shared domain>` 形式のプライマリ共有ドメインが含まれます。たとえば、値 `FYDIBOHF25SPDLT.contoso.com` では contoso.com がプライマリ共有ドメインです。

2.  Exchange 管理シェル で次のコマンドを実行して、プライマリ共有ドメインではない各フェデレーション ドメインを削除します。
    
    ```powershell
Remove-FederatedDomain -DomainName <domain> -Force
```

3.  プライマリ共有ドメイン以外のすべてのフェデレーション ドメインを削除した後で、Exchange 管理シェル で次のコマンドを実行してプライマリ共有ドメインを削除します。
    
    ```powershell
Remove-FederatedDomain -DomainName <domain> -Force
```

4.  Exchange 管理シェル で次のコマンドを実行してフェデレーション信頼を削除します。
    
    ```powershell
Remove-FederationTrust "Microsoft Federation Gateway"
```

5.  フェデレーション信頼の再作成手順については、「[フェデレーションの信頼の作成](https://technet.microsoft.com/ja-jp/library/dd335198\(v=exchg.150\))」を参照ください。

