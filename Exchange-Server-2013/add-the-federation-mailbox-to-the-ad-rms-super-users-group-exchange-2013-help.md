---
title: 'フェデレーション メールボックスを AD RMS のスーパー ユーザー グループに追加する: Exchange 2013 Help'
TOCTitle: フェデレーション メールボックスを AD RMS のスーパー ユーザー グループに追加する
ms:assetid: 44618df9-54f0-4474-a450-dcba48a02901
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee424431(v=EXCHG.150)
ms:contentKeyID: 49896222
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# フェデレーション メールボックスを AD RMS のスーパー ユーザー グループに追加する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

以下の Microsoft Exchange Server 2013 Information Rights Management (IRM) 機能を有効にするには、フェデレーション メールボックス (Exchange 2013 セットアップで作成されるシステム メールボックス) を、組織の [Active Directory Rights Management サービス (AD RMS)](https://technet.microsoft.com/ja-jp/library/hh831364.aspx) クラスターのスーパー ユーザー グループに追加する必要があります。

  - Microsoft Office Outlook Web App の IRM

  - Exchange ActiveSync の IRM

  - 仕訳帳レポート復号化

  - トランスポート復号化

メールが有効な配布グループは、AD RMS のスーパー ユーザー グループとして構成できます。配布グループのメンバーが AD RMS クラスターからライセンスを要求した場合、そのメンバーには所有者使用ライセンスが付与されます。これによって、そのクラスターで発行された RMS で保護されたコンテンツをすべて解読することができます。既存の配布グループを使用するか、配布グループを作成して AD RMS のスーパー ユーザー グループとして構成するかに無関係に、配布グループをこの目的専用のものにし、適切な設定を構成して、メンバーシップの変更を承認、監査、および監視することをお勧めします。


> [!NOTE]
> AD RMS 内にスーパー ユーザー グループを構成すると、グループのメンバーは IRM で保護されたコンテンツを復号できるようになります。グループのメンバーシップを制御および管理するための適切な措置を行って、監査を有効にしてメンバーシップの変更を追跡することをお勧めします。また、グループ ポリシーを使用してグループを制限されたグループとして構成することで、グループ メンバーシップへの不必要な変更を制限できます。詳細については、「<A href="https://technet.microsoft.com/ja-jp/library/cc756802(v=ws.10).aspx">制限されたグループ ポリシーの設定</A>」を参照してください。



IRM に関連する追加の管理タスクについては、「[Information Rights Management の手順](information-rights-management-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 15 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「配布グループ」。

  - AD RMS クラスターが Active Directory フォレストに展開されている必要があります。

  - AD RMS クラスター上で既にスーパー ユーザー グループが構成されている場合、配布グループのメンバーシップに対する変更では、AD RMS クラスターでの更新に最大 24 時間かかる可能性があります。これは、クラスターのグループ メンバーシップをキャッシュする結果です。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 実行方法

## 手順 1: シェルを使用して、フェデレーション メールボックスを配布グループに追加する

配布グループが、AD RMS クラスターのスーパー ユーザー グループとして作成され構成されている場合、Exchange 2013 フェデレーション メールボックスをそのグループのメンバーとして追加できます。スーパー ユーザー グループが構成されていない場合は、配布グループを作成してフェデレーション メールボックスをメンバーとして追加する必要があります。

1.  AD RMS スーパー ユーザー グループとして使用する専用の配布グループを作成します。詳細については、「[配布グループの作成と管理](https://docs.microsoft.com/ja-jp/exchange/recipients-in-exchange-online/manage-distribution-groups/manage-distribution-groups)」を参照してください。

2.  **FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042** というユーザーを新しい配布グループに追加します。フェデレーション メールボックスはシステム メールボックスなので、EAC には表示されません。このメールボックスを配布グループに追加するには、シェルから [Add-DistributionGroupMember](https://technet.microsoft.com/ja-jp/library/bb124340\(v=exchg.150\)) コマンドレットを使用する必要があります。
    
    この例では、フェデレーション メールボックスを ADRMSSuperUsers 配布グループに追加します。
    
    ```powershell
    Add-DistributionGroupMember ADRMSSuperUsers -Member FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042
    ```

構文およびパラメーターの詳細については、「[Add-DistributionGroupMember](https://technet.microsoft.com/ja-jp/library/bb124340\(v=exchg.150\))」を参照してください。

## 手順 2: AD RMS を使用してスーパー ユーザー グループを設定する

AD RMS クラスターで次の手順を実行します。この手順を実行するために使用するアカウントは、AD RMS サーバーの AD RMS Enterprise Administrators ローカル グループのメンバーである必要があります。

1.  Active Directory Rights Management サービス コンソールを開き、AD RMS クラスターを展開します。

2.  コンソール ツリーで、<strong>セキュリティ ポリシー</strong> を展開し、<strong>スーパー ユーザー</strong> をクリックします。

3.  操作ウィンドウで、<strong>スーパー ユーザーを有効にする</strong> をクリックします。

4.  結果ウィンドウで、<strong>スーパー ユーザー グループの変更</strong> をクリックし、<strong>スーパー ユーザー</strong> プロパティ シートを開きます。

5.  <strong>スーパー ユーザー グループ</strong> ボックスに、前の手順で作成した配布グループの電子メール アドレスを入力し、<strong>参照</strong> をクリックして、配布グループを選択します。

## 正常な動作を確認する方法

フェデレーション メールボックスを新規の、または既存の配布グループに追加した後で、[Get-DistributionGroupMember](https://technet.microsoft.com/ja-jp/library/aa996367\(v=exchg.150\)) コマンドレットを使用してグループのメンバーシップを確認します。

配布グループ メンバーシップの確認方法の例については、「**Get-DistributionGroupMember**」の「[Examples](https://technet.microsoft.com/ja-jp/aa996367\(exchg.150\)#examples)」を参照してください。

AD RMS を使用してスーパー ユーザー グループを設定したら、次の方法でスーパー ユーザー グループが正しく構成されていることを確認できます。さらに、[Test-IRMConfiguration](https://technet.microsoft.com/ja-jp/library/dd979798\(v=exchg.150\)) コマンドレットを使用して IRM 機能を確認できます。

  - AD RMS コンソールを使用して、適切なグループがスーパー ユーザー グループとして構成されたことを確認します。

  - AD RMS サーバー上で次の PowerShell コマンドを実行して、スーパー ユーザー グループを取得します。
    

    > [!IMPORTANT]
    > ADRMSAdmin PowerShell モジュールは、Windows Server 2008 R2 以降で利用できます。

    ```powershell
    Import-Module ADRMSAdmin
    New-PSDrive -Name MyRmsAdmin -PsProvider AdRmsAdmin -Root https://localhost 
    Get-ItemProperty -Path MyRmsAdmin:\SecurityPolicy\SuperUser
    ```

