---
title: 'Outlook 用アプリへのユーザー アクセスを管理する: Exchange Online Help'
TOCTitle: Outlook 用アプリへのユーザー アクセスを管理する
ms:assetid: e5833dec-a23a-439e-ac03-92671817bff8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ943757(v=EXCHG.150)
ms:contentKeyID: 52057869
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook 用アプリへのユーザー アクセスを管理する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

Exchange 管理センター (EAC) または Exchange PowerShell を使用して、Outlook 用アドインへのユーザー アクセスを管理できます。

  - EAC を使用して、ユーザー用の基本的なアドイン アクセス設定を組織レベルで管理できます。たとえば、ユーザーに対してアドインを有効/無効にするかどうかを構成できます。また、ユーザーにとってアドインを必須にするか、またはオプションにするかを指定できます。

  - Exchange 管理シェルまたは Exchange Online PowerShell では、EAC で管理できる設定とその他の設定を含め、すべての設定を管理できます。たとえば、組織内の特定のユーザーについてアプリの使用を制限できます。

その他の管理タスクについては、「[Outlook 用アプリ](add-ins-for-outlook-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - EAC の詳細については、「[Exchange 2013 の Exchange 管理者センター](exchange-admin-center-in-exchange-2013-exchange-2013-help.md)」または「[Exchange Online の Exchange 管理センター](https://technet.microsoft.com/ja-jp/library/jj200743\(v=exchg.150\))」を参照してください。

  - オンプレミスの Exchange 組織で Exchange 管理シェル を開く方法については、「[シェルを開く](https://technet.microsoft.com/ja-jp/library/dd638134\(v=exchg.150\))」を参照してください。 Windows PowerShell を使って Exchange Online に接続する方法については、「[Exchange Online PowerShell への接続](https://go.microsoft.com/fwlink/p/?linkid=396554)」を参照してください。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の "Outlook 用アドイン"。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## アドインが利用可能であるか、有効か、または無効かを指定する

## EAC を使用して、アドインが利用可能であるか、有効か、または無効かを指定できます

1.  EAC で、<strong>組織</strong> \> <strong>アドイン</strong> の順に移動します。

2.  リスト ビューで、設定を変更するアドインを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  ユーザーにアドインを使用させたくない場合は、<strong>組織内のユーザーがこのアドインを使用できるようにする</strong> チェックボックスをオフにして、<strong>保存</strong> をクリックします。

4.  ユーザーがアドインを使用できるようにする場合は、<strong>組織内のユーザーがこのアドインを使用できるようにする</strong> をオンにして、必要なオプションを選択します。
    
      - <strong>オプション、既定で有効</strong>: ユーザーがアドインをオフにできるようにする場合は、この設定を使用します。
    
      - <strong>オプション、既定で無効</strong>: ユーザーがアドインをオンにできるようにする場合は、この設定を使用します。
    
      - <strong>必須で、常に有効です。ユーザーはこのアドインを無効にできません</strong>: ユーザーがアドインをオフにできないようにする場合は、この設定を使用します。

5.  <strong>保存</strong> をクリックします。

## Exchange PowerShell を使用して、アドインが利用可能であるか、有効か、または無効かを指定する

まず次のコマンドを実行し、組織にインストールされているすべての Outlook 用アドインの表示名とアドイン ID を見つけます。

    Get-App -OrganizationApp | Format-List DisplayName,AppId

**AppId** 値は、アドインを一意に識別する GUID です (`fe93bfe1-7947-460a-a5e0-7a5906b51360` など)。アドインの設定を識別および変更するには、**AppId** 値を使用します。

アドインを無効にしてすべてのユーザーに対して非表示にするには、*\<AppId\>* を実際の **AppId** 値に置き換えて次のコマンドを実行します。

    Set-App -Identity <AppId> -OrganizationApp -Enabled $false

アドインを既定で有効にするが、ユーザーがこれをオフにできるようにするには、*\<AppId\>* 値を実際の **AppId** 値に置き換えて次のコマンドを実行します。

    Set-App -Identity <AppId> -OrganizationApp -Enabled $true -DefaultStateForUser Enabled

アドインを既定で無効にするが、ユーザーがこれをオンにできるようにするには、*\<AppId\>* 値を実際の **AppId** 値に置き換えて次のコマンドを実行します。

    Set-App -Identity <AppId> -OrganizationApp -Enabled $true -DefaultStateForUser Disabled

アドインをユーザーにとって必須にする場合は、*\<AppId\>* を実際の **AppId** 値に置き換えて次のコマンドを実行します。

    Set-App -Identity <AppId> -OrganizationApp -Enabled $true -DefaultStateForUser AlwaysEnabled

構文およびパラメーターの詳細については、「[Set-App](https://technet.microsoft.com/ja-jp/library/jj218630\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

アドインが正常に構成されたことを確認するには、次のいずれかの手順を実行します。

  - EAC で <strong>組織</strong> \> <strong>アドイン</strong> に移動し、<strong>ユーザーの既定値</strong> 列と <strong>提供先</strong> 列の値を確認します。

  - Exchange Online PowerShell で次のコマンドを実行し、**DefaultStateForUser** および **Enabled** プロパティの値を確認します。
    
        Get-App -OrganizationApp | Format-List DisplayName,AppId,Enabled,DefaultStateForUser

## Exchange PowerShell を使用してアドインの使用を特定のユーザーに限定する

アドインの使用を特定のユーザーに限定するには、EAC は使用できません。Exchange 管理シェルまたは Exchange Online PowerShell だけを使用できます。

この例では、架空の **AppId** 値 `ac83a9d5-5af2-446f-956a-c583adc94d5e` が設定されている LinkedIn アドインを、Marketing という名前の配布グループに限定します。
```
$a = Get-DistributionGroupMember Marketing
```
```
Set-App -Identity ac83a9d5-5af2-446f-956a-c583adc94d5e -OrganizationApp -ProvidedTo SpecificUsers -UserList $a.Identity -DefaultStateForUser Enabled
```

構文およびパラメーターの詳細については、「[Set-App](https://technet.microsoft.com/ja-jp/library/jj218630\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

アドインの使用を特定のユーザーに正常に限定できたことを確認するには、Exchange PowerShell で次のコマンドを実行し、**ProvidedTo** および **UserList** プロパティの値を確認します。

    Get-App -OrganizationApp | Format-List DisplayName,AppId,Enabled,DefaultStateForUser,ProvidedTo,UserList

