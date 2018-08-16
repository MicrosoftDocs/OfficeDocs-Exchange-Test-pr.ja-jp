---
title: 'メール連絡先の電子メールを有効または無効にする: Exchange 2013 Help'
TOCTitle: メール連絡先の電子メールを有効または無効にする
ms:assetid: ca47441f-1aa4-4958-aba5-18d51e59837e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124552(v=EXCHG.150)
ms:contentKeyID: 50555873
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メール連絡先の電子メールを有効または無効にする

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-12-05_

Exchange 組織内の既存のメール連絡先における電子メールを無効にできます。メール連絡先の電子メールを無効にすると、そのメール連絡先は Exchange および組織のアドレス帳から削除されます。メール連絡先が配布グループのメンバーである場合、連絡先はそのグループに送信されたメールを受信しなくなります。また、Exchange 属性は Active Directory のメールが有効な連絡先オブジェクトから削除されますが、連絡先とその Exchange 以外の属性 (連絡先および組織の情報など) は Active Directory に保持されます。

メール連絡先の電子メールを無効にした後には、シェルで **Enable-MailContact** コマンドレットを使用して、連絡先のメールを再度有効にできます。また、このコマンドレットを使用して、任意の Active Directory の連絡先のメールを有効にできます。

メール連絡先に関連する追加の管理タスクについては、「[メール連絡先の管理](manage-mail-contacts-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「メール連絡先」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## メール連絡先の電子メールを無効にする

前述のように、メール連絡先の電子メールを無効にすると、Exchange 属性は対応する Active Directory 連絡先オブジェクトから削除されますが、連絡先は保持されます。メール連絡先は EAC のメール連絡先の一覧から削除されますが、\[Active Directory ユーザーとコンピューター\] を使用するか、またはシェルで **Get-Contact** コマンドレットおよび **Set-Contact** コマンドレットを使用して、対応する Active Directory 連絡先オブジェクトを表示および管理できます。

## EAC を使用してメール連絡先の電子メールを無効にする

1.  EAC で、<strong>受信者</strong> \> <strong>連絡先</strong> に移動します。

2.  連絡先の一覧で、電子メールを無効にするメール連絡先をクリックします。

3.  <strong>その他</strong> ![\[その他のオプション\] アイコン](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "[その他のオプション] アイコン") をクリックし、<strong>無効にする</strong> をクリックします。

4.  選択したメール連絡先を無効にするかどうかを確認する警告が表示されます。<strong>はい</strong> をクリックして無効にします。

メール連絡先が連絡先の一覧から削除されます。

## シェルを使用してメール連絡先の電子メールを無効にする

この例では、メール連絡先 Neil Black の電子メールを無効にします。

    Disable-MailContact -Identity "Neil Black"

構文およびパラメーターの詳細については、「[Disable-MailContact](https://technet.microsoft.com/ja-jp/library/aa997465\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

メール連絡先の電子メールが正常に無効化されたことを確認するには、次のいずれかを実行します。

1.  EAC で、<strong>受信者</strong> \> <strong>連絡先</strong> に移動し、メール連絡先が一覧に表示されていないことを確認します。

2.  \[Active Directory ユーザーとコンピューター\] で、連絡先を右クリックし、<strong>プロパティ</strong> をクリックします。<strong>全般</strong> タブで、<strong>電子メール</strong> ボックスが空白になっていることに注意してください。これにより、連絡先のメールが有効ではないことが確認されます。

3.  シェルで、次のコマンドを実行します。
    
        Get-MailContact
    
    このコマンドレットはメールが有効な連絡先のみを返すため、電子メールを無効にした連絡先は結果に返されません。

4.  シェルで、次のコマンドを実行します。
    
        Get-Contact
    
    このコマンドレットはすべての Active Directory 連絡先オブジェクトを返すため、電子メールを無効にした連絡先が結果に返されます。

## シェルを使用して連絡先のメールを有効にする

**Enable-MailContact** コマンドレットを使用して、既存の Active Directory 連絡先のメールを有効にできます。1 つの連絡先のメールを有効にするか、または CSV ファイルを使用して複数の連絡先のメールを有効にできます。

## シェルを使用して 1 つの連絡先のメールを有効にする

この例では、連絡先 Rene Valdes のメールを有効にします。外部の電子メール アドレスを指定する必要があります。

    Enable-MailContact -Identity "Rene Valdes" -ExternalEmailAddress renev@tailspintoys.com

## シェルと CSV ファイルを使用して複数の連絡先のメールを有効にする

連絡先のメールを一括で有効にする際には、最初に、メールが有効ではない連絡先の一覧を CSV (コンマ区切り値) ファイルにエクスポートし、テキスト エディター (メモ帳など) や表計算アプリケーション (Microsoft Excel など) を使用して、外部の電子メールアドレスを CSV ファイルに追加します。次に、更新した CSV ファイルをシェル コマンドで使用して、CSV ファイルの一覧に含まれている連絡先のメールを有効にします。

1.  次のコマンドを実行して、メールが有効ではない既存の連絡先の一覧を管理者のデスクトップ上の Contacts.csv という名前のファイルにエクスポートします。
    
        Get-Contact | Where { $_.RecipientType -eq "Contact" } | Out-File "C:\Users\Administrator\Desktop\Contacts.csv"
    
    結果として得られるファイルは、次のようなファイルになります。
    
        Name
        Walter Harp
        James Alvord
        Rainer Witt
        Susan Burk
        Ian Tien
        ...

2.  <strong>EmailAddress</strong> という名前の列見出しを追加し、ファイルの各連絡先の電子メール アドレスを追加します。各連絡先の名前および外部電子メール アドレスは、コンマで区切る必要があります。更新した CSV ファイルは、次のファイルのようになっている必要があります。
    
        Name,EmailAddress
        James Alvord,james@contoso.com
        Susan Burk,sburk@tailspintoys.com
        Walter Harp,wharp@tailspintoys.com
        Ian Tien,iant@tailspintoys.com
        Rainer Witt,rainerw@fourthcoffee.com
        ...

3.  次のコマンドを実行して、ファイルの一覧に含まれている連絡先のメールを CSV ファイルのデータを使用して有効にします。
    
        Import-CSV C:\Users\Administrator\Desktop\Contacts.csv | ForEach-Object {Enable-MailContact -Identity $_.Name -ExternalEmailAddress $_.EmailAddress}
    
    コマンドの結果には、メールを有効にした新しい連絡先に関する情報が表示されます。

## 正常な動作を確認する方法

Active Directory 連絡先のメールが正常に有効化されたことを確認するには、次のいずれかを実行します。

  - EAC で、<strong>受信者</strong> \> <strong>連絡先</strong> に移動します。新しいメール連絡先が連絡先の一覧に表示されます。<strong>連絡先の種類</strong> の種類は、<strong>メール連絡先</strong> と表示されます。
    

    > [!NOTE]
    > 新しいメール連絡先を表示するために、<STRONG>[最新の情報に更新]</STRONG><IMG title="[最新の情報に更新] アイコン" alt="[最新の情報に更新] アイコン" src="images/Dn624163.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif"> のクリックが必要な場合があります。



  - シェルで次のコマンドを実行して、新しいメール連絡先の情報を表示します。
    
        Get-MailContact | Format-Table Name,RecipientTypeDetails,ExternalEmailAddress

