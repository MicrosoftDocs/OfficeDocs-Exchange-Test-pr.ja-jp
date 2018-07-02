---
title: 'アドレス一覧を作成する: Exchange 2013 Help'
TOCTitle: アドレス一覧を作成する
ms:assetid: e86ba1b7-c41c-4050-bc29-13996cf53c59
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb125036(v=EXCHG.150)
ms:contentKeyID: 49896534
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.NewAddressListWizardForm.AddressListIntroductionPage
ms.translationtype: MT
---

# アドレス一覧を作成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-12_

アドレス一覧は、受信者およびその他の Active Directory オブジェクトの集合です。それぞれのアドレス一覧には、ユーザー、連絡先、グループ、パブリック フォルダー、会議、その他のリソースなど、1 つ以上の種類のオブジェクトを含めることができます。アドレス一覧には、特定のユーザー グループのために、メールが有効なオブジェクトを Active Directory 内で分割する機能もあります。

アドレス一覧に関連する他の管理タスクについては、「[アドレス一覧の手順](address-list-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[電子メール アドレスおよびアドレス帳のアクセス許可](email-address-and-address-book-permissions-exchange-2013-help.md)」の「アドレス一覧」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EAC を使用してアドレス一覧を作成する

1.  **\[組織\]** \> **\[アドレス一覧\]** に移動し、**\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  **\[アドレス一覧\]** で、名前を入力し、一覧に含める送信者の種類を指定します。

3.  既定では Exchange が、組織のすべてのメンバーを含むアドレス リストを作成します。一意のカスタム アドレス一覧を作成するには、**\[ルールを追加する\]** をクリックします。
    

    > [!IMPORTANT]
    > ルールを追加しない場合は、既定のアドレス一覧のいずれかと重複するアドレス一覧を作成します。



4.  一覧で、フィルター オプション (たとえば、**\[カスタム属性 1\]**) を選択します。

5.  **\[単語または語句の指定\]** にフィルター処理する単語または語句を入力し、**\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックし、**\[OK\]** をクリックします。
    
    手順 4 を繰り返して、複数の語句または単語を続けて追加できます。フィルターは、Boolean **OR** ステートメントです。たとえば、アドレス一覧をカスタム属性 1 が **Oregon**、**Idaho**、または **Washington** と等しいユーザーに適用するフィルターを作成できます。

6.  (省略可能) **\[ルールを追加する\]** を再度クリックして、追加のフィルターを追加します。追加のフィルターでは、ブール値 **And** ステートメントが作成されます。さらにフィルターを追加するほど、アドレス一覧が適用されるユーザーの数が少なくなります。

7.  **\[アドレス一覧内の受信者をプレビューします\]** をクリックして、アドレス一覧が適用される受信者を表示します。

8.  **\[保存\]** をクリックします。

9.  更新するまで、アドレス一覧は適用されないことを示す警告が表示されます。組織の規模およびアドレス一覧に追加したフィルターに応じて、一部のアドレス一覧には、数千から数万の受信者が含まれる可能性があります。アドレス一覧の更新はリソースに影響を及ぼす可能性があるため、ピーク時以外の時間帯にアドレスを更新することをお勧めします。
    
    アドレス一覧の更新の詳細については、「[アドレス一覧を更新する](update-an-address-list-exchange-2013-help.md)」を参照してください。

## シェルを使用してアドレス一覧を作成する

この例では、*RecipientFilter* パラメーターを使用してアドレス一覧 MyAddressList を作成し、メールボックス ユーザーであり、`StateOrProvince` が `Washington` または `Oregon` に設定されている受信者を含めます。

    New-AddressList -Name MyAddressList -RecipientFilter {((RecipientType -eq 'UserMailbox') -and ((StateOrProvince -eq 'Washington') -or (StateOrProvince -eq 'Oregon')))}

この例では、組み込みのコンテナーを使用して、親コンテナー All Rooms に子アドレス一覧 Building 34 Meeting Rooms を作成します。

    New-AddressList -Name "Building 34 Meeting Rooms" -Container "\All Rooms" -IncludedRecipients Resources -ConditionalCustomAttribute1 "Building 34"

構文およびパラメーターの詳細については、「[New-AddressList](https://technet.microsoft.com/ja-jp/library/aa996912\(v=exchg.150\))」を参照してください。

