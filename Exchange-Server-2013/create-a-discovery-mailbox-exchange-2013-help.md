---
title: '探索メールボックスの作成: Exchange Online Help'
TOCTitle: 探索メールボックスの作成
ms:assetid: bc20285d-35e2-4e49-9bd3-38abf96114ba
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd638177(v=EXCHG.150)
ms:contentKeyID: 49896443
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 探索メールボックスの作成

 

_**適用先:** Exchange Online, Exchange Server 2013_

Microsoft Exchange Server 2013 セットアップでは、既定で証拠開示用メールボックスが作成されます。Exchange Online においても、証拠開示用メールボックスが既定で作成されます。証拠開示用メールボックスは、Exchange 管理センター (EAC) 内の [インプレース電子情報開示 (eDiscovery)](in-place-ediscovery-exchange-2013-help.md) 検索用の対象メールボックスとして使用されます。必要に応じて、追加の証拠開示用メールボックスを作成できます。新しい証拠開示用メールボックスを作成したら、その証拠開示用メールボックスにコピーされる電子情報開示検索結果へのアクセスを可能にするため、該当するユーザーにフルアクセスのアクセス許可を割り当てる必要があります。


> [!NOTE]
> 探索マネージャーが電子情報開示の検索結果を探索メールボックスにコピーした後、メールボックスには機密情報が含まれる可能性があります。探索メールボックスへのアクセスを制御し、権限のあるユーザーしかアクセスできないようにします。



詳細については、「[Discovery mailboxes](in-place-ediscovery-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 3 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「探索メールボックスの作成」。

  - 探索メールボックスには、50 ギガバイト (GB) のメールボックス記憶域クォータがあります。この記憶域クォータを増やすことはできません。

  - 探索メールボックスを作成したり、それにアクセスするためのアクセス許可を割り当てたりするために EAC を使用することはできません。シェルを使用する必要があります。Office 365 で、Exchange Online 組織に接続したリモート PowerShell を使用します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## (オプション) 手順 1: リモート PowerShell による Exchange への接続

Exchange Online 組織または Office 365 組織がある場合はこの手順のみを実行する必要があります。Exchange Server 2013 組織がある場合は、次の手順に進み、Exchange 管理シェル でコマンドを実行します。

1.  ローカル コンピューターで、Windows PowerShell を開き、次のコマンドを実行します。
    
        $UserCredential = Get-Credential
    
    **\[Windows PowerShell 資格情報の要求\]** ダイアログ ボックスで、Office 365 のグローバル管理者アカウントのユーザー名とパスワードを入力し、**\[OK\]** をクリックします。

2.  次のコマンドを実行します。
    
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection

3.  次のコマンドを実行します。
    
        Import-PSSession $Session

4.  Exchange Online 組織に接続されたことを検証するために、次のコマンドを実行して、組織内のすべてのメールボックスのリストを取得します。
    
        Get-Mailbox

詳細については、または Exchange Online 組織への接続に関する問題がある場合は、「[リモート PowerShell による Exchange への接続](https://go.microsoft.com/fwlink/p/?linkid=517283)」を参照してください。

## 手順 2: 探索メールボックスの作成

この例では、探索メールボックス SearchResults を作成します。

    New-Mailbox -Name SearchResults -Discovery 

構文およびパラメーターの詳細については、「[New-Mailbox](https://technet.microsoft.com/ja-jp/library/aa997663\(v=exchg.150\))」を参照してください。

Exchange 組織内のすべての探索メールボックスのリストを表示するには、以下のコマンドを実行します。

    Get-Mailbox -Resultsize unlimited -Filter {RecipientTypeDetails -eq "DiscoveryMailbox"}

構文およびパラメーターの詳細については、「[Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\))」を参照してください。

## 手順 3: 探索メールボックスへの許可を割り当てる

作成した証拠開示用メールボックスを開くために必要なアクセス許可をユーザーまたはグループに明示的に割り当てる必要があります。以下の構文を使用して、証拠開示用メールボックスを開いたり検索結果を表示したりするためのアクセス許可をユーザーまたはグループに割り当てることができます。

    Add-MailboxPermission <Name of the discovery mailbox> -User <Name of user or group> -AccessRights FullAccess -InheritanceType all

たとえば、以下のコマンドは、Litigation Managers グループにフルアクセスのアクセス許可を割り当てて、このグループのメンバーが Fabrikam Litigation 探索メールボックスを開くことができるようにします。

    Add-MailboxPermission "Fabrikam Litigation" -User "Litigation Managers" -AccessRights FullAccess -InheritanceType all

構文およびパラメーターの詳細については、「[Add-MailboxPermission](https://technet.microsoft.com/ja-jp/library/bb124097\(v=exchg.150\))」を参照してください。

## 詳細情報

  - 既定では、既定の探索検索メールボックスのフル アクセスのアクセス許可を付与されているのは、Discovery Management 役割グループのメンバーだけです。作成した探索メールボックスを Discovery Management 役割グループのメンバーが開くことができるようにするには、そのグループにフル アクセスのアクセス許可を明示的に付与する必要があります。

  - 探索メールボックスは、Exchange アドレス一覧に表示されますが、ユーザーがそこに電子メールを送信することはできません。探索メールボックスへの電子メールの配信は、配信制限によって禁止されています。これにより、探索メールボックスにコピーされた検索結果の整合性が維持されます。

  - 探索メールボックスは、他の目的に使用することや別の種類のメールボックスに変換することはできません。

  - 探索メールボックスは、他の種類のメールボックスと同様に削除できます。

