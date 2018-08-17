---
title: '組織の関係を作成する: Exchange 2013 Help'
TOCTitle: 組織の関係を作成する
ms:assetid: 5ea61b96-c8ca-44fc-b8b5-ca4341af36a6
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657451(v=EXCHG.150)
ms:contentKeyID: 49896274
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 組織の関係を作成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-07_

外部ビジネス パートナーと予定表の情報を共有するには、組織上の関係を設定します。組織上の関係は、2 つの Exchange 2013 フェデレーション組織間、または 1 つの Exchange 2013 フェデレーション組織と複数の Exchange 2010 フェデレーション組織との間で構成できます。社内の Exchange 組織と Office 365 の組織との間にも、組織上の関係を設定できます。


> [!IMPORTANT]
> 組織の関係の作成は、Exchange 組織でフェデレーション共有を設定するためのいくつかの手順のうちの 1 つで、社内 Exchange 組織に対するフェデレーション信頼の構成を必要とします。



フェデレーション共有の詳細については、「[共有](sharing-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 15 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。 「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」トピックの「予定表と共有のアクセス許可」セクション。

  - 社内の Exchange 組織に対するアクティブなフェデレーション信頼を構成する必要があります。詳細については、「[フェデレーション信頼の構成](configure-a-federation-trust-exchange-2013-help.md)」を参照してください。

  - 組織上の関係で構成する外部組織には、Azure AD 認証システムとのフェデレーション信頼も確立されている必要があります。組織の関係を構成する場合は、外部 Exchange 組織用のプライマリ フェデレーション ドメインを使用します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

## 必要な作業

## EAC を使用して組織の関係を作成する

1.  社内組織の Exchange 2013 サーバーで、<strong>組織</strong> \> <strong>共有</strong> に移動します。

2.  <strong>組織の共有</strong> で、<strong>新規作成</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

3.  <strong>組織上の関係の新規作成</strong> の <strong>関係の名前</strong> ボックスに、組織上の関係のわかりやすい名前を入力します。

4.  <strong>共有するドメイン</strong> ボックスに、予定表の表示を許可する社内の Office 365 または Exchange 組織のフェデレーション ドメインまたはフェデレーション サブドメインを入力します。外部組織の複数のドメインを入力する必要がある場合は、ドメインをコンマで区切ります。たとえば、**contoso.com、service.contoso.com** のようにします。

5.  リストしたドメインとの予定表の共有を有効にするには、<strong>予定表の空き時間情報の共有を有効にする</strong> チェック ボックスをオンにします。予定表の空き時間情報の共有レベルを設定し、予定表の空き時間情報を共有できるユーザーを設定します。
    
    空き時間情報のアクセス レベルを設定するには、次のいずれかを選択します。
    
      - <strong>時刻のみを指定して予定表の空き時間情報にアクセス</strong>
    
      - <strong>予定表の空き時間情報のうち、空き時間、件名、場所情報へのアクセス</strong>
    
    予定表の空き時間情報を共有する内部ユーザーを設定するには、次のいずれかを選択します。
    
      - **組織内の全員**
    
      - <strong>指定したセキュリティ グループ</strong>
        
        セキュリティ グループを指定するには <strong>参照</strong> をクリックします。

6.  <strong>保存</strong> をクリックして組織上の関係を作成します。

## シェルを使用して組織の関係を作成する

この例では、次の条件で Contoso, Ltd との組織の関係を作成します。

  - 組織の関係は、contoso.com、northamerica.contoso.com、および europe.contoso.com で有効です。

  - 空き時間情報のアクセスが有効です。

  - 要求側の組織は、接続先の組織から空き時間、件名、場所情報を受け取ります。

<!-- end list -->

    New-OrganizationRelationship -Name "Contoso" -DomainNames "contoso.com","northamerica.contoso.com","europe.contoso.com" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel LimitedDetails

この例では、**Get-FederationInformation** コマンドレットで指定したドメイン名を使用して、外部 Exchange 組織 Contoso.com から構成情報の自動検出を試行します。この方法を使用して組織の関係を作成する場合は、**Set-FederatedOrganizationIdentifier** コマンドレットを使用して組織 ID を作成していることを最初に確認する必要があります。

    Get-FederationInformation -DomainName Contoso.com | New-OrganizationRelationship -Name "Contoso" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel -LimitedDetails

構文およびパラメーターの詳細については、「[Get-FederationInformation](https://technet.microsoft.com/ja-jp/library/dd351221\(v=exchg.150\))」と「[New-OrganizationRelationship](https://technet.microsoft.com/ja-jp/library/ee332357\(v=exchg.150\))」を参照してください。

この例では、Fourth Coffee との組織の関係を作成します。この例では、外部 Exchange 組織との接続設定が提供されています。次の条件が適用されます。

  - 組織の関係は、ドメイン fourthcoffee.com、Fourth Coffee のフェデレーション ドメインで確立されます。

  - Exchange Web サービス アプリケーションの URL は mail.fourthcoffee.com です。

  - 自動検出 URL は https://mail.fourthcoffee.com/autodiscover/autodiscover.svc/wssecurity です。

  - 空き時間情報のアクセスが有効です。

  - 要求側の組織は、空き時間のみを含む空き時間情報を受け取ります。

<!-- end list -->

    New-OrganizationRelationship -Name "Fourth Coffee" -DomainNames "fourthcoffee.com" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel -AvailabilityOnly -TargetAutodiscoverEpr "https://mail.fourthcoffee.com/autodiscover/autodiscover.svc/wssecurity" -TargetApplicationUri "mail.fourthcoffee.com"

構文およびパラメーターの詳細については、「[New-OrganizationRelationship](https://technet.microsoft.com/ja-jp/library/ee332357\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

組織の関係が想定どおりに作成されたことは、まず、**組織の関係の新規作成**ウィザードが正常に完了したことで判断できます。

組織の関係が正常に作成されたことをさらに確認するには、次のシェル コマンドを実行して組織の関係の情報を確認します。

    Get-OrganizationRelationship | format-list


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。


