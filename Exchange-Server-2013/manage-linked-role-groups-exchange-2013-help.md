---
title: 'リンクされた役割グループの管理: Exchange 2013 Help'
TOCTitle: リンクされた役割グループの管理
ms:assetid: e2a07395-90c2-4d62-b15d-ac3ff28fe786
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657502(v=EXCHG.150)
ms:contentKeyID: 49896526
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# リンクされた役割グループの管理

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-09_

リンクされた管理役割グループを使用すると、外部 Active Directory 内のユニバーサル セキュリティ グループ (USG) のメンバーがリソース Active Directory フォレスト内の Microsoft Exchange Server 2013 組織を管理できるようになります。外部フォレスト内の USG をリンクされた役割グループに関連付けることによって、その USG のメンバーに対して、リンクされた役割グループに割り当てられた管理役割で提供されるアクセス許可が付与されます。リンクされた役割グループの詳細については、「[管理役割グループについて](understanding-management-role-groups-exchange-2013-help.md)」を参照してください。

リンクされた役割グループを作成するには、**New-RoleGroup** コマンドレットおよび **Set-RoleGroup** コマンドレットを使用する必要があります。構文およびパラメーターの詳細については、以下のトピックを参照してください。

  - [New-RoleGroup](https://technet.microsoft.com/ja-jp/library/dd638181\(v=exchg.150\))

  - [Set-RoleGroup](https://technet.microsoft.com/ja-jp/library/dd638182\(v=exchg.150\))

役割グループに関連する追加の管理タスクについては、「[アクセス許可](permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 ～ 10 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「役割グループ」。

  - Exchange 管理センター (EAC) を使用して、リンクされた役割グループを作成または構成することはできません。 Exchange 管理シェルを使用する必要があります。

  - 少なくとも、リンクされた役割グループを構成するには、リンクされた役割グループが存在することになるリソース Active Directory フォレストとユーザーまたは USG が存在している外部 Active Directory フォレスト間に一方向の信頼が確立されている必要があります。リソース フォレストは外部フォレストを信頼する必要があります。

  - 外部 Active Directory フォレストに関する以下の情報を把握している必要があります。
    
      - **資格情報**   外部 Active Directory フォレストにアクセスできるユーザー名とパスワードを有する必要があります。この情報は、**New-RoleGroup** コマンドレットおよび **Set-RoleGroup** コマンドレットの *LinkedCredential* パラメーターで使用されます。
    
      - **ドメイン コントローラー**   外部 Active Directory フォレスト内の Active Directory ドメイン コントローラーの完全修飾ドメイン名 (FQDN) を有する必要があります。この情報は、**New-RoleGroup** コマンドレットおよび **Set-RoleGroup** コマンドレットの *LinkedDomainController* パラメーターで使用されます。
    
      - **外部 USG**   リンクされた役割グループに関連付けるメンバーを含む外部 Active Directory フォレスト内の USG の完全名を有する必要があります。 この情報は、**New-RoleGroup** コマンドレットおよび **Set-RoleGroup** コマンドレットの *LinkedForeignGroup* パラメーターで使用されます。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## リンクされた役割グループを作成する

## シェルを使用してスコープのないリンクされた役割グループを作成する

リンクされた役割グループを作成して管理役割をリンクされた役割グループに割り当てるには、次の手順を実行します。

1.  変数に外部 Active Directory フォレストの資格情報を格納します。
    
    ```powershell
    $ForeignCredential = Get-Credential
    ```

2.  以下の構文を使用して、リンクされた役割グループを作成します。
    
    ```powershell
        New-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -Roles <role1, role2, role3...>
    ```

3.  外部 Active Directory フォレストにあるコンピューター上で Active Directory ユーザーとコンピューターを使用して、メンバーを外部 USG に追加、または外部 USG から削除します。

この例では、次のことが行われます。

  - users.contoso.com 外部 Active Directory フォレストの資格情報を取得します。これらの資格情報を使用して、外部フォレストにある DC01.users.contoso.com ドメイン コントローラーに接続します。

  - Exchange 2013 がインストールされたリソース フォレスト内に "Compliance Role Group/準拠役割グループ" という名前のリンクされた役割グループを作成します。

  - 新しい役割グループを users.contoso.com 外部 Active Directory フォレスト内の "Compliance Administrators USG/準拠管理者 USG" にリンクします。

  - "Transport Rules/トランスポート ルール" および "Journaling /ジャーナリング" 管理役割をリンクされた新しい役割のグループに割り当てます。

<!-- end list -->

```powershell
$ForeignCredential = Get-Credential
```

```powershell
    New-RoleGroup "Compliance Role Group" -LinkedForeignGroup "Compliance Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles "Transport Rules", "Journaling"
```

## シェルを使用してカスタム管理スコープ付きのリンクされた役割グループを作成する

カスタム受領者管理スコープ、カスタム構成管理スコープ、または両方が付いているリンクされた役割グループを作成できます。リンクされた役割グループを作成してカスタム スコープ付きの管理の役割をそのグループに割り当てるには、次の手順を実行します。

1.  変数に外部 Active Directory フォレストの資格情報を格納します。
    
    ```powershell
    $ForeignCredential = Get-Credential
    ```

2.  以下の構文を使用して、リンクされた役割グループを作成します。
    
    ```powershell
        New-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -CustomConfigWriteScope <name of configuration scope> -CustomRecipientWriteScope <name of recipient scope> -LinkedCredential $ForeignCredential -Roles <role1, role2, role3...>
    ```
    
3.  外部 Active Directory フォレストにあるコンピューター上で Active Directory ユーザーとコンピューターを使用して、メンバーを外部 USG に追加、または外部 USG から削除します。

この例では、次のことが行われます。

  - users.contoso.com 外部 Active Directory フォレストの資格情報を取得します。これらの資格情報を使用して、外部フォレストにある DC01.users.contoso.com ドメイン コントローラーに接続します。

  - Exchange 2013 がインストールされたリソース フォレスト内に "Seattle Compliance Role Group/Seattle の準拠役割グループ" という名前のリンクされた役割グループを作成します。

  - 新しい役割グループを users.contoso.com 外部 Active Directory フォレスト内の "Seattle Compliance Administrators USG/Seattle の準拠管理者 USG" にリンクします。

  - "Transport Rules/トランスポート ルール" および "Journaling /ジャーナリング" 管理役割を "Seattle Recipients/Seattle 受信者" カスタム受信者スコープ付きのリンクされた新しい役割のグループに割り当てます。

<!-- end list -->

```powershell
$ForeignCredential = Get-Credential
```

```powershell
New-RoleGroup "Seattle Compliance Role Group" -LinkedForeignGroup "Seattle Compliance Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -CustomRecipientWriteScope "Seattle Recipients" -Roles "Transport Rules", "Journaling"
```

管理のスコープの詳細については、「[管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)」を参照してください。

## シェルを使用して OU スコープ付きのリンクされた役割グループを作成する

OU 受領者スコープを使用するリンクされている役割グループを作成できます。リンクされた役割グループを作成して OU スコープ付きの管理役割をそのグループに割り当てるには、次の手順を実行します。

1.  変数に外部 Active Directory フォレストの資格情報を格納します。
    
    ```powershell
    $ForeignCredential = Get-Credential
    ```

2.  以下の構文を使用して、リンクされた役割グループを作成します。
    
    ```powershell
    New-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -RecipientOrganizationalUnitScope <OU name> -Roles <role1, role2, role3...>
    ```

3.  外部 Active Directory フォレストにあるコンピューター上で Active Directory ユーザーとコンピューターを使用して、メンバーを外部 USG に追加、または外部 USG から削除します。

この例では、次のことが行われます。

  - users.contoso.com 外部 Active Directory フォレストの資格情報を取得します。これらの資格情報を使用して、外部フォレストにある DC01.users.contoso.com ドメイン コントローラーに接続します。

  - Exchange 2013 がインストールされたリソース フォレスト内に "Executives Compliance Role Group/エグゼクティブ準拠の役割グループ" という名前のリンクされた役割グループを作成します。

  - 新しい役割グループを users.contoso.com 外部 Active Directory フォレスト内のエグゼクティブ準拠管理者 USG にリンクします。

  - "Transport Rules/トランスポート ルール" および "Journaling /ジャーナリング" 管理役割を OU 受領者スコープ エグゼクティブ OU 付きのリンクされた新しい役割のグループに割り当てます。

<!-- end list -->

```powershell
$ForeignCredential = Get-Credential
```

```powershell
New-RoleGroup "Executives Compliance Role Group" -LinkedForeignGroup "Executives Compliance Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -RecipientOrganizationalUnitScope "Executives OU" -Roles "Transport Rules", "Journaling"
```

管理のスコープの詳細については、「[管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)」を参照してください。

## リンクされた役割グループの外部 USG を変更する

## シェルを使用してリンクされた役割グループの外部 USG を変更する

リンクされた役割グループに関連付けられた外部 USG を変更するには、次の手順を実行します。

1.  変数に外部 Active Directory フォレストの資格情報を格納します。
    
    ```powershell
    $ForeignCredential = Get-Credential
    ```

2.  次の構文を使用して、リンクされた既存の役割グループの外部 USG を変更します。
    
    ```powershell
    Set-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential 
    ```

この例では、次のことが行われます。

  - users.contoso.com 外部 Active Directory フォレストの資格情報を取得します。これらの資格情報を使用して、外部フォレストにある DC01.users.contoso.com ドメイン コントローラーに接続します。

  - 外部 USG に関連付けられている役割グループを、Compliance Role Group から Regulatory Compliance Officers に変更します。

<!-- end list -->

```powershell
$ForeignCredential = Get-Credential
```

```powershell
Set-RoleGroup "Compliance Role Group" -LinkedForeignGroup "Regulatory Compliance Officers" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential
```
