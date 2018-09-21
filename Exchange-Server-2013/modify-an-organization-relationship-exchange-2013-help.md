---
title: '組織の関係の変更: Exchange 2013 Help'
TOCTitle: 組織の関係の変更
ms:assetid: 3713ef83-f01a-41bb-b127-62ca242dd7a4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ673055(v=EXCHG.150)
ms:contentKeyID: 49896198
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 組織の関係の変更

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-01-01_

組織上の関係を使用すれば、Exchange 組織のユーザーは、Office 365 組織や別の社内 Exchange 組織と予定表の空き時間情報を共有できます。名前の変更、予定表共有の一時的な無効化、アクセス レベルの変更、予定表を共有するセキュリティ グループの変更など、組織上の関係の設定を変更する必要がある場合があります。

予定表を他の組織と共有するには、その前に、クラウドとの認証関係 (「フェデレーション」とも言う) をセットアップして、最小ソフトウェア要件を満たす必要があります。フェデレーション共有の詳細については、「[共有](sharing-exchange-2013-help.md)」を参照してください。

フェデレーションに関連する追加の管理タスクについては、「[フェデレーションの手順](federation-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間: 15 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。 「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「*Calendar and Sharing Permissions*」。

  - 社内 Exchange 組織に対するアクティブなフェデレーション信頼を構成する必要があります。

  - 組織上の関係で構成する外部組織には、Azure AD 認証システムとのフェデレーション信頼も確立されている必要があります。

  - このトピック内の手順では、Contoso という名前の組織上の関係に変更を加えます。例では次の方法を示します。
    
      - service.contoso.com という名前のドメインを外部組織に追加する。
    
      - 組織上の関係の空き時間情報共有を無効にする。
    
      - *Calendar free/busy information with time, subject, and location* から *Calendar free/busy information with time only* に空き時間情報のアクセス レベルを変更する。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

## 必要な作業

## EAC を使用して組織上の関係にドメインを追加する

1.  社内組織の Exchange 2013 サーバーで、<strong>組織</strong> \> <strong>共有</strong> に移動します。

2.  リスト ビューの <strong>組織の共有</strong> で組織上の関係 Contoso を選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>組織上の関係</strong> が <strong>全般</strong> になっている場合は、組織上の関係の <strong>名前</strong> が変更されません。

4.  <strong>共有するドメイン</strong> ボックスで、**service.contoso.com** ドメインを入力してから、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

5.  <strong>保存</strong> をクリックして組織上の関係を更新します。

## EAC を使用して組織上の関係のための空き時間情報の共有を無効にする

1.  <strong>組織</strong> \> <strong>共有</strong> に移動します。

2.  リスト ビューの <strong>組織の共有</strong> で組織上の関係 Contoso を選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>組織上の関係</strong> で、<strong>共有</strong> をクリックします。

4.  <strong>時刻のみを指定して予定表の空き時間情報にアクセス</strong> を選択します。

5.  <strong>保存</strong> をクリックして組織上の関係を更新します。

## EAC を使用して組織上の関係のための空き時間情報のアクセス レベルを変更する

1.  <strong>組織</strong> \> <strong>共有</strong> に移動します。

2.  リスト ビューの <strong>組織の共有</strong> で組織上の関係 Contoso を選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>組織上の関係</strong> で、<strong>共有</strong> をクリックします。

4.  <strong>時刻のみを指定して予定表の空き時間情報にアクセス</strong> を選択します。

5.  <strong>保存</strong> をクリックして組織上の関係を更新します。

## シェルを使用して組織上の関係を変更する

  - この例では、組織上の関係 Contoso にドメイン名 service.contoso.com を追加します。
    
        $domains = (Get-OrganizationRelationship Contoso).DomainNames
        $domains += 'service.contoso.com'
        Set-OrganizationRelationship -Identity Contoso -DomainNames $domains

  - この例では、組織上の関係 Contoso を無効にします。
    
    ```powershell
Set-OrganizationRelationship -Identity Contoso -Enabled $false
```

  - この例では、組織の関係 WoodgroveBank で予定表の空き時間情報アクセスを有効にして、アクセス レベルを `AvailabilityOnly` (時間だけの予定表の空き時間情報) に設定します。
    
        Set-OrganizationRelationship -Identity Contoso -FreeBusyAccessEnabled $true -FreeBusyAccessLevel AvailabilityOnly

構文およびパラメーターの詳細については、「[Get-OrganizationRelationship](https://technet.microsoft.com/ja-jp/library/ee332343\(v=exchg.150\))」と「[Set-OrganizationRelationship](https://technet.microsoft.com/ja-jp/library/ee332326\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

組織上の関係の更新が成功したかどうかを確認するには、以下のシェル コマンドを実行して組織上の関係情報を確認します。

```powershell
Get-OrganizationRelationship | format-list
```


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。


