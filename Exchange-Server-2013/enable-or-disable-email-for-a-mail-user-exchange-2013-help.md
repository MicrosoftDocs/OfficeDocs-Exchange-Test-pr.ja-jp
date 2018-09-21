---
title: 'メール ユーザーの電子メールを有効または無効にする: Exchange 2013 Help'
TOCTitle: メール ユーザーの電子メールを有効または無効にする
ms:assetid: 1e2571d4-ff84-4fda-bb1d-825e96e1bd26
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa996598(v=EXCHG.150)
ms:contentKeyID: 50555743
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メール ユーザーの電子メールを有効または無効にする

 

_**適用先:** Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:** 2012-11-14_

Exchange 組織内で既存のメール ユーザーの電子メールを無効にすることができます。特定のメール ユーザーの電子メールを無効にすると、Exchange と組織のアドレス帳からメール ユーザーが削除されます。メール ユーザーが配布グループのメンバーになっている場合、削除されたユーザーは配布グループ宛に送信されたメールを受信しません。また、Exchange の属性は Active Directory のユーザー オブジェクトから削除されます。ただし、ユーザー オブジェクトと Exchange 以外の属性 (連絡先や組織情報など) は Active Directory 内に残ります。

メール ユーザーの電子メールを無効にした後で、ユーザーのメールを再度有効にするには、シェルで **Enable-MailUser** コマンドレットを使用します。このコマンドレットを使用すると、任意の Active Directory ユーザーのメールを有効にすることもできます。


> [!NOTE]
> メール ユーザー (<EM>メールが有効なユーザー</EM>ともいう) は、メールボックスを持つ組織内のユーザーとは異なります。主な違いは、メール ユーザーが外部電子メール アドレスを持つ Exchange 組織外のユーザーを表す点です。メール ユーザーは組織内のメールボックスを持っていません。組織内のメールボックスを持つユーザーとメール ユーザーとの違いについて詳しくは、「<A href="recipients-exchange-2013-help.md">受信者</A>」を参照してください。



メール ユーザーに関連する追加の管理タスクについては、「[メール ユーザーの管理](https://docs.microsoft.com/ja-jp/exchange/recipients-in-exchange-online/manage-mail-users)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「メール ユーザー」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## メール ユーザーの電子メールの無効化

前述のように、メール ユーザーの電子メールを無効にすると、Exchange の属性は対応する Active Directory メール ユーザー オブジェクトから削除されますが、ユーザーは残ります。EAC ではメール ユーザーがメール ユーザー一覧から削除されますが、\[Active Directory ユーザーとコンピューター\] を使用するか、シェルで **Get-MailUser** コマンドレットと **Set-Set-MailUser** コマンドレットを使用すると、対応する Active Directory 連絡先オブジェクトの表示と管理を行うことができます。

## EAC を使用してメール ユーザーの電子メールを無効にする

1.  EAC で、<strong>受信者</strong> \> <strong>連絡先</strong> に移動します。

2.  連絡先の一覧で、電子メールを無効にするメール ユーザーをクリックします。

3.  <strong>詳細</strong> ![\[その他のオプション\] アイコン](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "[その他のオプション] アイコン") クリックして、<strong>無効にする</strong> をクリックします。

4.  選択したメール ユーザーを無効にするかどうかを確認する警告が表示されます。<strong>はい</strong> をクリックしてメール ユーザーを無効にします。

メール ユーザーが連絡先リストから削除されます。

## シェルを使用してメール ユーザーの電子メールを無効にする

この例では、メール ユーザー Yan Li の電子メールを無効にします。

```powershell
Disable-MailUser -Identity "Yan Li"
```

構文およびパラメーターの詳細については、「[Disable-MailUser](https://technet.microsoft.com/ja-jp/library/aa998578\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

メール ユーザーの電子メールが正常に無効化されたことを確認するには、次の手順を実行します。

1.  EAC で、<strong>受信者</strong> \> <strong>連絡先</strong> の順に移動して、メール ユーザーが表示されなくなっていることを確認します。

2.  Active Directory ユーザーとコンピューターで、ユーザーを右クリックし、<strong>プロパティ</strong> をクリックします。<strong>全般</strong> タブで、<strong>電子メール</strong> ボックスが空欄になっていることに注意してください。これにより、メール ユーザーのメールが有効でないことを確認します。

3.  シェルで、次のコマンドを実行します。
    
    ```powershell
Get-MailUser
```
    
    このコマンドレットはメールが有効なユーザーのみを返すため、電子メールを無効にしたメール ユーザーは結果として返されません。

4.  シェルで、次のコマンドを実行します。
    
    ```powershell
Get-User
```
    
    このコマンドレットはすべての Active Directory ユーザー オブジェクトを返すため、電子メールを無効にしたメール ユーザーが結果として返されます。

## シェルを使用してユーザーのメールを有効にする

**Enable-MailUser** コマンドレットを使用すると、既存の Active Directory ユーザーをメールが有効な状態にすることができます。単一ユーザーのメールを有効にすることも、CSV ファイルを使用して複数ユーザーのメールを有効にすることもできます。

## シェルを使用して単一ユーザーのメールを有効にする

この例では、ユーザー Sanjay Shah のメールを有効にします。外部の電子メール アドレスを指定する必要があります。

```powershell
Enable-MailUser -Identity "Sanjay Shah" -ExternalEmailAddress renev@tailspintoys.com
```

## シェルと CSV ファイルを使用して複数ユーザーのメールの有効にする

複数のユーザーのメールをまとめて有効にする場合は、最初にメールが有効でないユーザーのリストを CSV (コンマ区切り) ファイルにエクスポートし、次にメモ帳などのテキスト エディターまたは Microsoft Excel などのスプレッドシート アプリケーションを使用して、外部の電子メール アドレスを CSV ファイルに追加します。次に、シェル コマンドで更新した CSV ファイルを使用して、CSV ファイルに記載されたユーザーのメールを有効にします。

1.  次のコマンドを実行すると、メールが有効でない既存のユーザーまたは組織内のメールボックスを持っていない既存のユーザーの一覧が管理者のデスクトップ上の UsersToMailEnable.csv というファイルにエクスポートされます。
    
        Get-User | Where { $_.RecipientType -eq "User" } | Out-File "C:\Users\Administrator\Desktop\UsersToMailEnable.csv"
    
    この結果, .csv ファイルは次のようになります。
    
        Name            RecipientType
        ----            -------------
        Guest           User
        krbtgt          User
        RMS_SERVICE     User
        David Pelton    User
        Kim Akers       User
        Janet Schorr    User
        Jeffrey Zang    User
        Spencer Low     User
        Toni Poe        User
        ...

2.  この CSV ファイルを次のように変更します。
    
      - メールを有効にしないユーザーを CSV ファイルから削除します。前の例の場合、最初の 3 つのエントリを削除します。これらは既定のシステム アカウントです。
    
      - **RecipientType** 列と `User` のすべてのインスタンスを削除します。
    
      - ファイルに **EmailAddress** という列見出しを追加し、各ユーザーの電子メール アドレスを追加します。各ユーザーの名前と外部メール アドレスはコンマで区切る必要があります。
    
    更新した CSV ファイルは次のようになります。
    
        Name,EmailAddress
        David Pelton,davidp@contoso.com
        Kim Akers,kakers@tailspintoys.com
        Janet Schorr,janet.schorr@adatum.com
        Jeffrey Zang,jzang@tailspintoys.com
        Spencer Low,spencerl@fouthcoffee.com
        Toni Poe,tonip@contoso.com
        ...

3.  次のコマンドを実行して、CSV ファイルのデータを使用し、ファイルに記載されたユーザーのメールを有効にします。
    
        Import-CSV "C:\Users\Administrator\Desktop\UsersToMailEnable.csv" | ForEach-Object {Enable-MailUser -Identity $_.Name -ExternalEmailAddress $_.EmailAddress}
    
    コマンドの結果には、新しくメールを有効にしたユーザーに関する情報が表示されます。

## 正常な動作を確認する方法

Active Directory ユーザーのメールが正常に有効化されたことを確認するには、次のいずれかの手順を実行します。

  - EAC で、<strong>受信者</strong> \> <strong>連絡先</strong> に移動します。新しいメール ユーザーが連絡先リストに表示されます。<strong>連絡先の種類</strong> で、種類は <strong>メール ユーザー</strong> と表示されます。
    

    > [!NOTE]
    > 新しいメール ユーザーを表示するのに、<STRONG>[最新の情報に更新]</STRONG><IMG title="[最新の情報に更新] アイコン" alt="[最新の情報に更新] アイコン" src="images/Dn624163.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif"> のクリックが必要になる場合があります。



  - シェルで、次のコマンドを実行して新しいメール ユーザーの情報を表示します。
    
    ```powershell
Get-MailUser | Format-Table Name,RecipientTypeDetails,ExternalEmailAddress
```

