---
title: '組織の Outlook 用アプリをインストールまたは削除する: Exchange Online Help'
TOCTitle: 組織の Outlook 用アプリをインストールまたは削除する
ms:assetid: 112f3ef7-9943-4a1e-8a42-e08e8e9f67f4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ943752(v=EXCHG.150)
ms:contentKeyID: 52057797
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 組織の Outlook 用アプリをインストールまたは削除する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

EAC またはシェルを使用して、組織の Outlook 用アドインをインストールまたは削除できます。


> [!NOTE]
> 既定では、組織でアドインをインストールすると、組織内のすべてのユーザーがそのアドインを使用できるようになります。インストール後に EAC かシェルを使用して、ユーザーに対してアドインをオプションまたは必須にし、そのアドインを有効にするか無効にするかを指定できます。アドインの既定の設定を変更する方法については、「<A href="manage-user-access-to-add-ins-for-outlook-exchange-online-help.md">Outlook 用アプリへのユーザー アクセスを管理する</A>」を参照してください。組織の特定のユーザーに対してアドインの利用を制限するには、シェルを使用する必要があります。詳細については、「<A href="manage-user-access-to-add-ins-for-outlook-exchange-online-help.md">Outlook 用アプリへのユーザー アクセスを管理する</A>」を参照してください。



その他の管理タスクについては、「[Outlook 用アプリ](add-ins-for-outlook-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の "Outlook 用アプリ"。

  - 組織にアドインをインストールして管理するために、管理者のアクセス許可を割り当てることができます。ユーザーが自分で使用するアドインをインストールして管理するために、ユーザーのアクセス許可を割り当てることもできます。詳細については、「[Outlook 用のアドインをインストールおよび管理できる管理者とユーザーを指定する](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md)」を参照してください。

  - 特定の地域では、メールボックス、または組織での Office ストアへのアクセスはサポートされていません。**Exchange 管理センター**の **\[組織\]** \> **\[アドイン\]** \> ![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") の下のオプションに **\[Office ストアから追加\]** が表示されない場合は、URL またはファイルの場所から Outlook 用アドインをインストールできる場合があります。詳細については、サービス プロバイダーにお問い合わせください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## Outlook 用アドインをインストールする

## EAC を使用してアドインを追加する

1.  EAC で、**\[組織\]** \> **\[アドイン\]** の順に移動します。

2.  **\[新規\]** ![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックし、アドインのインストール元の場所を選択します。
    
      - **\[Office ストアから追加\]**。インストールするアプリを Office ストアで選択し、**\[追加\]** をクリックします。Outlook Web App で動作するアプリは、**\[Office/SharePoint 用アドイン\]** の **\[Outlook\]** に表示されます。
        

        > [!NOTE]
        > 特定の地域では、メールボックス、または組織での Office ストアへのアクセスはサポートされていません。<STRONG>Exchange 管理センター</STRONG>の <STRONG>[組織]</STRONG> &gt; <STRONG>[アドイン]</STRONG> &gt; <IMG title="[追加] アイコン" alt="[追加] アイコン" src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif"> の下のオプションに <STRONG>[Office ストアから追加]</STRONG> が表示されない場合は、URL またはファイルの場所から Outlook 用アドインをインストールできる場合があります。詳細については、サービス プロバイダーにお問い合わせください。

    
      - **\[URL から追加\]**。インストールするアドイン マニフェスト ファイルの完全な URL を **\[URL\]** に入力します。
    
      - **\[ファイルから追加\]**。**\[参照\]** を選択し、インストールするアドイン マニフェスト ファイルの場所に移動します。

3.  \[**保存**\] をクリックします。

## シェルを使用してアドインを追加する

この例は、URL からアドインを追加する方法を示しています。

    New-App -OrganizationApp -Url <URL location for add-in manifest file>

この例は、ファイルからアドインを追加する方法を示しています。

    New-App -OrganizationApp -FileData <File location for add-in manifest file>


> [!TIP]
> シェルを使用して組織にアドインをインストールする場合、アドインのインストールと設定の構成を同時に実行できます。



構文とパラメーターについては、「[New-App](https://technet.microsoft.com/ja-jp/library/jj218722\(v=exchg.150\))」を参照してください。

## Outlook 用アドインを削除する

## EMC を使用してアドインを削除する

1.  EAC で、**\[組織\]** \> **\[アドイン\]** の順に移動します。

2.  リスト ビューで、削除するアプリを選択し、**\[削除\]**![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") をクリックします。

## シェルを使用してアドインを削除する

シェルを使用して、組織からアドインを削除できます。


> [!NOTE]
> 次のコマンドを実行し、組織にインストールされているすべての Outlook 用アドインの表示名とアプリケーション ID を参照します。



    Get-App -OrganizationApp |FL DisplayName,AppID

次のコマンドを実行し、カスタム アドイン "Finance Test Add-in" を組織から削除します。

    Remove-App -OrganizationApp -Identity <GUID for Finance Test Add-in>

構文とパラメーターについては、「[Remove-App](https://technet.microsoft.com/ja-jp/library/jj218709\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

組織にインストールされているアドインを確認するには、次の操作のいずれかを実行します。

  - EAC で **\[組織\]** \> **\[アドイン\]** の順に移動し、インストールされているアドインのリストを確認します。

  - シェルから `Get-App` を実行し、インストールされているアドインのリストを確認します。

