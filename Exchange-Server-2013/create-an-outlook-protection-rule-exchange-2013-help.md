---
title: 'Outlook 保護ルールを作成する: Exchange 2013 Help'
TOCTitle: Outlook 保護ルールを作成する
ms:assetid: da64750d-faaf-44de-ad8c-888eba7fbdbf
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd638196(v=EXCHG.150)
ms:contentKeyID: 49896507
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook 保護ルールを作成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

Microsoft Outlook 保護ルールを使用すると、メッセージの送信前に Outlook 2010 の Active Directory Rights Management Services (AD RMS) テンプレートを適用することによって、Information Rights Management (IRM) でメッセージを保護できます。

IRM に関連する追加の管理タスクについては、「[Information Rights Management の手順](information-rights-management-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 推定完了時間: 1 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「権限での保護」。

  - Microsoft Exchange Server 2013 を実行しているサーバーと同じ Active Directory フォレストにおいて、[AD RMS](https://technet.microsoft.com/ja-jp/library/hh831364.aspx) サーバーが展開されている必要があります。

  - IRM で保護されたメッセージに対して Outlook 保護ルールを構成する場合は、トランスポート解読を有効にして、トランスポート ルール エージェントなどのトランスポート エージェントがメッセージの解読およびメッセージへのアクセスを行えるようにしてください。ジャーナルを使用する場合は、ジャーナル レポートの解読も有効にして、ジャーナル エージェントがジャーナル レポートのメッセージの暗号化されていないコピーを保存できるようにする必要があります。詳細については、「[ジャーナル レポート復号化](journal-report-decryption-exchange-2013-help.md)」を参照してください。

  - Exchange 管理センター (EAC) を使用して Outlook 保護ルールを作成することはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用して Outlook 保護ルールを作成する

この例では、Project Contoso という Outlook 保護ルールを作成します。このルールによって、ContosoPMs という配布グループに対して送信されるメッセージが、Business Critical という AD RMS テンプレートで保護されます。

    New-OutlookProtectionRule -Name "Project Contoso" -SentTo "DL-ContosoPMs@contoso.com" -ApplyRightsProtectionTemplate "Business Critical"


> [!NOTE]
> Outlook 保護ルールに対して <CODE>SentTo</CODE> の述語を使用し、配布グループを指定した場合は、IRM 保護された [宛先] フィールド、[Cc] フィールド、または [Bcc] フィールドで、その配布グループが宛先になっているメッセージのみが送信されます。IRM 保護は、配布グループの個々のメンバー宛のメッセージには適用されません。



`FromDepartment` 述語および `SentToScope` 述語を使用して、指定の部署のユーザーからのメッセージまたは指定のスコープ宛のメッセージ (内部メッセージの場合は `InOrganization`、すべての受信者の場合は `All`) に対して IRM 保護を適用することもできます。

構文およびパラメーターの詳細については、「[New-OutlookProtectionRule](https://technet.microsoft.com/ja-jp/library/dd298182\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

Outlook 保護ルールが正常に作成されたことを確認するには、次の手順を実行します。

  - [Get-OutlookProtectionRule](https://technet.microsoft.com/ja-jp/library/dd298004\(v=exchg.150\)) コマンドレットを実行して、ルールが作成されていることを確認し、ルールのプロパティを表示します。Outlook 保護ルールを取得する方法の例については、「**Get-OutlookProtectionRule**」の「[Examples](https://technet.microsoft.com/ja-jp/dd298004\(exchg.150\)#examples)」を参照してください。

  - Outlook 2010 を使用して、ルールの条件を満たすテスト メッセージを作成し、クライアント上でルールがトリガーされることを確認します。
    

    > [!NOTE]
    > Outlook で Outlook 保護ルールが使用可能になるためには、しばらく時間がかかる場合があります。


