---
title: 'メールボックスにおけるスパム対策設定の構成: Exchange 2013 Help'
TOCTitle: メールボックスにおけるスパム対策設定の構成
ms:assetid: 868d7fd8-e817-46ba-9b67-edf2f50b9494
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb123559(v=EXCHG.150)
ms:contentKeyID: 49896344
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックスにおけるスパム対策設定の構成

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-11-17_

個々のメールボックスで、Exchange 組織の他のメールボックスに適用されるスパム対策設定とは異なる特定のスパム対策設定を構成できます。メールボックス上でスパム対策設定を構成すると、その設定が対応する組織全体のコンテンツ フィルターや組織構成のスパム対策設定よりも優先されます。


> [!NOTE]
> 2016 年 11 月 1 日に Microsoft は、Exchange と Outlook の SmartScreen フィルターのスパム定義の更新を停止しました。既存の SmartScreen スパム定義はそのままですが、その効果は時間とともに低下する可能性があります。詳しくは、「<A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Outlook と Exchange での SmartScreen サポートの廃止</A>」をご覧ください。



## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[スパム対策とマルウェア対策のアクセス許可](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)」の「スパム対策機能」および「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「スパム対策」。

  - 既定では、メールボックス サーバーのトランスポート サービスでスパム対策機能が有効になっていません。一般的には、Exchange 組織が受信メッセージの受信前にスパム対策フィルターを事前に設定しない場合に限り、スパム対策機能を有効にします。詳細については、「[メールボックス サーバーのスパム対策機能を有効にする](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)」を参照してください。

  - この手順を実行するには、シェルを使用する必要があります。

  - 迷惑メール フォルダーの SCL しきい値は、SCL による削除、拒否、および検疫の値と異なる動作をします。詳細については、「[Spam Confidence Level のしきい値](spam-confidence-level-threshold-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用して 1 つのメールボックスのスパム対策機能を構成する

1 つのメールボックスのスパム対策設定を構成するには、以下の構文を使用します。

    Set-Mailbox <MailboxIdentity> -AntispamBypassEnabled <$true | $false> -RequireSenderAuthenticationEnabled <$true | $false> -SCLDeleteEnabled <$true | $false | $null> -SCLDeleteThreshold <0-9 | $null> -SCLJunkEnabled <$true | $false | $null > -SCLJunkThreshold <0-9 | $null> -SCLQuarantineEnabled <$true | $false | $null > -SCLQuarantineThreshold <0-9 | $null> -SCLRejectEnabled <$true | $false | $null > -SCLRejectThreshold <0-9 | $null>

この例では、Jeff Phillips という名前のユーザーのメールボックスを構成して、すべてのスパム対策フィルターをバイパスし、迷惑メール フォルダーの SCL しきい値が 5 以上のメッセージを Microsoft Outlook 内のそのユーザーの迷惑メール フォルダーに配信するようにします。

    Set-Mailbox "Jeff Phillips" -AntispamBypassEnabled $true -SCLJunkEnabled $true -SCLJunkThreshold 4

## 正常な動作を確認する方法

1 つのメールボックス上でスパム対策機能が正常に構成されたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
        Get-Mailbox <MailboxIdentity> | Format-List SCL*,Bypass*,*SenderAuth*

2.  表示された値が構成した値であることを確認します。

## シェルを使用して複数のメールボックスのスパム対策機能を構成する

複数のメールボックスのすべてのスパム対策設定を構成するには、以下の構文を使用します。

    Get-Mailbox [<Filter>]| Set-Mailbox <Anti-Spam Settings>

この例では、Contoso.com ドメインの Users コンテナーにあるすべてのメールボックスで、SCL による検疫のしきい値 7 を有効にします。

    Get-Mailbox -OrganizationalUnit Contoso.com/Users | Set-Mailbox -SCLQuarantineEnabled $true -SCLQuarantineThreshold 7

## 正常な動作を確認する方法

複数のメールボックス上でスパム対策機能が正常に構成されたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
        Get-Mailbox [<Filter>] | Format-List Name,SCL*,*SenderAuth*

2.  表示された値が構成した値であることを確認します。

## シェルを使用して組織内のすべてのメールボックスに迷惑メールのしきい値を構成する

次のコマンドを実行します。

    Set-OrganizationConfig -SCLJunkThreshold <Integer>

この例では、組織の迷惑メールのしきい値を 5 に設定します。

    Set-OrganizationConfig -SCLJunkThreshold 5

## 正常な動作を確認する方法

組織内のすべてのメールボックスに迷惑メールのしきい値が正常に構成されたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
        Get-OrganizationConfig | Format-List SCLJunkThreshold

2.  表示された値が構成した値であることを確認します。

