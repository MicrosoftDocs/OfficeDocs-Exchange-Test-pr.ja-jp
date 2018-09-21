---
title: '共有ポリシーの作成: Exchange 2013 Help'
TOCTitle: 共有ポリシーの作成
ms:assetid: cae8cab0-6265-448b-8add-5202cdb20678
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657494(v=EXCHG.150)
ms:contentKeyID: 49896478
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 共有ポリシーの作成

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-07_

共有ポリシーを使用して、Exchange 組織内のユーザーが組織外のユーザーと予定表情報を共有する方法を制御できます。共有ポリシーにより、さまざまな種類の外部ユーザーとユーザー指定の特定ユーザー間の予定表情報の共有が行えます。外部フェデレーション組織 (Office 365 や別の社内 Exchange 組織など)、外部の非フェデレーション組織、およびインターネットへのアクセスが可能な個人との予定表情報の共有がサポートされます。特定の共有ポリシーをユーザーに適用するには、「[メールボックスに共有ポリシーを適用する](apply-a-sharing-policy-to-mailboxes-exchange-2013-help.md)」を参照してください。


> [!IMPORTANT]
> 共有ポリシーの作成は、Exchange 組織内でフェデレーション共有を設定する際の、複数の手順の 1 つです。他のフェデレーション Exchange 組織と予定表情報を共有するには、その前にオンプレミスの Exchange 組織用に Azure Active Directory 認証システムとのフェデレーション信頼を設定する必要があります。フェデレーション信頼は、インターネット共有ポリシーには必要ありません。



フェデレーション共有の詳細については、「[共有](sharing-exchange-2013-help.md)」を参照してください。

フェデレーションに関連する追加の管理タスクについては、「[フェデレーションの手順](federation-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 15 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。 「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」トピックの「予定表と共有のアクセス許可」セクション。

  - Exchange フェデレーション組織間の共有ポリシーでは、以下の要件を満たしている必要があります。
    
      - Exchange 2013 クライアント アクセス サーバーが、各 Exchange 組織内に存在している。共有ポリシーは、1 つの組織が Exchange 2013 クライアント アクセス サーバーを保持し、もう 1 つの組織が Exchange 2010 SP3 以降のクライアント アクセス サーバーを保持する Exchange 組織間でもサポートされます。
    
      - 各 Exchange 組織で、Azure AD 認証システムとのフェデレーション信頼が作成されている。詳細については、「[フェデレーション信頼の構成](configure-a-federation-trust-exchange-2013-help.md)」を参照してください。
    
      - 各 Exchange 組織で、フェデレーション組織 ID が構成されている。ユーザーの電子メール アドレスの生成に使用するドメインが組織 ID に追加されている。
    
      - ユーザー メールボックスが、各 Exchange 組織内の Exchange 2013 メールボックス サーバー上または Exchange 2010 メールボックス サーバー上に配置されている。
    
      - Outlook 2010 以降および Outlook Web App のユーザーのみが、共有への招待を作成できる。

  - Exchange 非フェデレーション組織または個人との共有ポリシーでは、以下の要件を満たしている必要があります。
    
      - Exchange 2013 クライアント アクセス サーバーが、ユーザーの予定表情報を共有する Exchange 組織内に存在する。
    
      - ユーザー メールボックスが、ユーザーの予定表情報を共有する Exchange 組織内の Exchange 2013 メールボックス サーバー上に配置されている。
    
      - Exchange 2013 クライアント アクセス サーバーにおいて、Outlook Web App アクセスが有効になっている必要がある。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

## 必要な作業

## EAC を使用して共有ポリシーを作成する

1.  <strong>組織</strong> \> <strong>共有</strong> に移動します。

2.  リスト ビューの <strong>個別共有</strong> で、<strong>新規作成</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

3.  <strong>共有ポリシーの新規作成</strong> で、<strong>ポリシー名</strong> ボックスに共有ポリシーのフレンドリ名を入力します。

4.  <strong>追加</strong> ![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックして、共有ポリシーの共有ルールを指定します。

5.  <strong>共有ルール</strong> で、次のいずれかのオプションを選択して、共有するドメインを指定します。
    
      - <strong>すべてのドメインと共有</strong>
    
      - <strong>特定のドメインと共有</strong>

6.  <strong>特定のドメインと共有</strong> を選択した場合は、共有するドメインの名前を入力します。この共有ポリシーに複数のドメインを入力する必要がある場合は、最初のドメインの設定を保存してから、共有ルールを編集してさらにドメインを追加します。

7.  ポリシーに対して強制する予定表の共有レベルを定義するには、<strong>予定表フォルダーを共有する</strong> チェック ボックスをオンにし、次のいずれかのオプションを選択します。
    
      - <strong>時刻のみを指定して予定表の空き時間情報にアクセス</strong>
    
      - <strong>時間、件名、場所を含む予定表の空き時間情報</strong>
    
      - <strong>時刻、件名、場所、役職などの予定表のすべての予定情報</strong>

8.  共有ポリシーのルールを設定するには、<strong>\[保存\]</strong>をクリックします。

9.  この共有ポリシーを Exchange 組織におけるユーザーの既定の共有ポリシーにする場合は、<strong>このポリシーを既定の共有ポリシーにする</strong> チェック ボックスをオンにします。

10. 共有ポリシーを作成するには、<strong>保存</strong> をクリックします。

## EAC を使用してすべてのユーザーが予定表の完全な詳細情報を共有できるようにする

既定の共有ポリシーを編集すると、組織内のすべてのユーザーが、組織外のユーザーと予定表の完全な詳細情報を共有することができます。

1.  <strong>組織</strong> \> <strong>共有</strong> に移動します。

2.  リスト ビューの <strong>個別共有</strong> で <strong>既定の共有ポリシー</strong> を選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>共有ポリシー</strong> ダイアログ ボックスで、<strong>すべてのドメインと共有</strong> を選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

4.  <strong>共有ルール</strong> ダイアログ ボックスで、<strong>共有する情報を指定します</strong> の <strong>時刻、件名、場所、役職などの予定表のすべての予定情報</strong> を選択し、<strong>保存</strong> をクリックします。

5.  <strong>共有ポリシー</strong> ダイアログ ボックスで、<strong>保存</strong> をクリックして共有ポリシーのルールを設定します。

## シェルを使用して共有ポリシーを作成する

  - この例では、外部フェデレーション ドメイン contoso.com に対して、共有ポリシー Contoso を作成します。このポリシーを使用すると、contoso.com ドメイン内のユーザーは、ユーザーの詳細な予定表の空き時間情報を確認できます。既定では、この設定は有効になっています。
    
    ```powershell
New-SharingPolicy -Name "Contoso" -Domains contoso.com: CalendarSharingFreeBusyDetail
```

  - この例では、2 つの異なるフェデレーション ドメイン (contoso.com および woodgrovebank.com) に対して、ドメインごとに異なる共有アクションを構成した共有ポリシー ContosoWoodgrove を作成します。このポリシーは無効になっています。
    
        New-SharingPolicy -Name "ContosoWoodgrove" -Domains 'contoso.com: CalendarSharingFreeBusySimple', 'woodgrovebank.com: CalendarSharingFreeBusyDetail -Enabled $false

  - この例では、クライアント アクセス サーバー CAS01 およびメールボックス サーバー MAIL01 を持つ Exchange 組織に対して、限定的な予定表の空き時間情報を提供する共有アクションを構成した共有ポリシー Anonymous を作成します。このポリシーでは、Exchange 組織内のユーザーはリンクを送信して、インターネットへのアクセスが可能なユーザーが予定表の空き時間情報を表示できるよう招待できます。このポリシーは有効になっています。
    
    1.  MAIL01 の Web プロキシ URL を設定します。
        
        ```powershell
Set-ExchangeServer -Identity "Mail01" -InternetWebProxy "<Webproxy URL>"
```
    
    2.  CAS01 で仮想ディレクトリの発行を有効にします。
        
            Set-OwaVirtualDirectory -Identity "CAS01" -ExternalURL "<URL for CAS01>" -CalendarPublishingEnabled $true
    
    3.  共有ポリシー Anonymous を作成し、限定的な予定表情報の共有を構成します。
        
            New-SharingPolicy -Name "Anonymous" -Domains 'Anonymous: CalendarSharingFreeBusySimple' -Enabled $true

構文およびパラメーターの詳細については、以下のトピックを参照してください。

  - [New-SharingPolicy](https://technet.microsoft.com/ja-jp/library/dd298186\(v=exchg.150\))

  - [Set-ExchangeServer](https://technet.microsoft.com/ja-jp/library/bb123716\(v=exchg.150\))

  - [Set-OwaVirtualDirectory](https://technet.microsoft.com/ja-jp/library/bb123515\(v=exchg.150\))

## 正常な動作を確認する方法

共有ポリシーが正常に作成されたことを確認するには、次のシェル コマンドを実行して共有ポリシーの情報を確認します。

```powershell
Get-SharingPolicy <policy name> | format-list
```


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。


