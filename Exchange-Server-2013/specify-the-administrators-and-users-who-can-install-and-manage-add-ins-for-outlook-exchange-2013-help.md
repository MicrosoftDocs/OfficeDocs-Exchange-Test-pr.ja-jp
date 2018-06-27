---
title: 'Outlook 用のアドインをインストールおよび管理できる管理者とユーザーを指定する: Exchange 2013 Help'
TOCTitle: Outlook 用のアドインをインストールおよび管理できる管理者とユーザーを指定する
ms:assetid: 7ee4302d-b8bb-40a0-9810-10d3a0271bcb
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ943754(v=EXCHG.150)
ms:contentKeyID: 52057843
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook 用のアドインをインストールおよび管理できる管理者とユーザーを指定する

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:**2017-02-08_

組織のどの管理者に、Outlook 用のアドインをインストールして管理するアクセス許可を持たせるかを指定できます。また、組織のどのユーザーに、自分で使用するアドインをインストールして管理するアクセス許可を持たせるかを指定することもできます。

これは、アドインに固有の管理役割を割り当てるか、または削除するかで行います。使用できる組み込みの役割は、5 つあります。

管理者の役割

  - **組織マーケットプレース アプリ**   管理者が組織のために Office ストアのアドインをインストールし、管理できます。

  - **組織カスタム アプリ**   管理者が組織のためにカスタム アドインをインストールし、管理できます。

ユーザーの役割

  - **マイ マーケットプレース アプリ**   ユーザーが自分で使用するために Office ストア アドインをインストールし、管理できます。

  - **マイ カスタム アプリ**   ユーザーが自分で使用するためのカスタム アドインをインストールし、管理できます。

  - **自分の ReadWriteMailbox アプリ**   ユーザーがマニフェストで ReadWriteMailbox のアクセス許可レベルを要求するアドインをインストールし、管理できます。

既定では、**組織の管理**の役割グループを持っている管理者はすべて、上記の管理者の役割の両方が有効になっています。また、既定では、エンド ユーザーには上記のユーザーの役割が有効になっています。

これらの役割の詳細については、 ["Org Marketplace Apps/組織マーケットプレイス アプリ" 役割](org-marketplace-apps-role-exchange-2013-help.md)、 ["Org Custom Apps/組織のカスタム アプリ" 役割](org-custom-apps-role-exchange-2013-help.md)、 ["My Marketplace Apps/マイ マーケットプレイス アプリ" 役割](my-marketplace-apps-role-exchange-2013-help.md)、 ["My Custom Apps/自分のカスタム アプリ" 役割](my-custom-apps-role-exchange-2013-help.md)、および[自分の ReadWriteMailbox アプリの役割](my-readwritemailbox-apps-role-exchange-2013-help.md)を参照してください。

アドインの詳細については、「[Outlook 用アプリ](add-ins-for-outlook-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - このコマンドレットを実行する際には、あらかじめアクセス許可を割り当てる必要があります。このトピックにはこのコマンドレットのすべてのパラメーターが示されていますが、割り当てられているアクセス許可に含まれていない一部のパラメーターにはアクセスできません。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「役割の割り当て」。

  - 特定の地域では、メールボックス、または組織での Office ストアへのアクセスはサポートされていません。**Exchange 管理センター**の **\[組織\]** \> **\[アドイン\]** \> ![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") の下のオプションに **\[Office ストアから追加\]** が表示されない場合は、URL またはファイルの場所から Outlook 用アドインをインストールできる場合があります。詳細については、サービス プロバイダーにお問い合わせください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## 組織のためにアドインをインストールして管理するのに必要なアクセス許可を管理者に割り当てる

## EAC を使用して管理者にアクセス許可を割り当てる

EAC を使用して、組織のために Office ストアのアドインをインストールして管理するのに必要なアクセス許可を管理者に割り当てることができます。この手順の詳細については、「[役割グループの管理](manage-role-groups-exchange-2013-help.md)」をご覧ください。

## 自分で使用するアドインをインストールして管理するのに必要なアクセス許可をユーザーに割り当てる

## EAC を使用してユーザーにアクセス許可を割り当てる

EAC を使用して、自分で使用するカスタム アドインを表示して変更するのに必要なアクセス許可をユーザーに割り当てることができます。この手順の詳細については、「[役割グループの管理](manage-role-groups-exchange-2013-help.md)」をご覧ください。

## 正常な動作を確認する方法

ユーザーにアクセス許可を正常に割り当てたことを確認するには、`Get-ManagementRoleAssignment -Role <Role Name> -GetEffectiveUsers` の形式を使用してシェル コマンドを実行します。ここで `Role Name` には、アクセス許可を割り当てたことを確認する役割が入ります。

この例は、組織のために Office ストアのアドインをインストールするのに必要なアクセス許可を割り当てた対象を確認する方法を示しています。

1.  `Get-ManagementRoleAssignment -Role "Org Marketplace Apps" -GetEffectiveUsers` を実行します。

2.  結果の **\[有効なユーザー\]** 列のエントリを確認します。

構文およびパラメーターの詳細については、「[Get-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd351024\(v=exchg.150\))」を参照してください。

