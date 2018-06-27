---
title: 'スパム検疫メールボックスの構成: Exchange 2013 Help'
TOCTitle: スパム検疫メールボックスの構成
ms:assetid: 907d2f90-2a62-4d59-a4cf-945fef2e963f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb123746(v=EXCHG.150)
ms:contentKeyID: 49896365
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# スパム検疫メールボックスの構成

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2013-02-19_

コンテンツ フィルター エージェントによってスパムと判断されたメッセージは、スパム検疫メールボックスに転送することができます。SCL (Spam Confidence Level) による検疫のしきい値が有効である場合、隔離されるすべてのメッセージは配信不能レポート (NDR) としてラップされ、スパム検疫メールボックスとして指定した SMTP アドレスに送信されます。隔離されたメッセージを検証し、Microsoft Outlook の再送機能を使用して、意図された受信者に送信することもできます。

## 始める前に把握しておくべき情報

  - このタスクの予想所要時間:45 分。

  - 既定では、メールボックス サーバーのトランスポート サービスでスパム対策機能が有効になっていません。一般的には、Exchange 組織が受信メッセージの受信前にスパム対策フィルターを事前に設定しない場合に限り、スパム対策機能を有効にします。詳細については、「[メールボックス サーバーのスパム対策機能を有効にする](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)」を参照してください。

  - スパム検疫メールボックスの担当者は、個人的で機密性の高いメッセージを表示したり、Exchange 組織内のすべてのユーザーに代わってメールを送信したりすることができます。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 実行方法

## 手順 1: コンテンツ フィルターが有効になっていることを確認する

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[スパム対策とマルウェア対策のアクセス許可](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)」の「スパム対策機能」。

1.  コンテンツ フィルター エージェントが Exchange サーバーにインストールされ、有効になっていることを確認するには、次のコマンドを実行します。
    
        Get-TransportAgent "Content Filter Agent"

2.  コンテンツ フィルターが有効になっていることを確認するには、次のコマンドを実行します。
    
        Get-ContentFilterConfig | Format-List Enabled

詳細については、「[コンテンツ フィルターの管理](manage-content-filtering-exchange-2013-help.md)」を参照してください。

## 手順 2: スパム検疫専用のメールボックスを作成する

スパム検疫専用のメールボックスを作成するには、次の手順を実行します。

  - **専用の Exchange データベースを作成します**   スパム検疫メールボックス専用のデータベースを作成することをお勧めします。格納域の制限の上限に達するとメッセージが失われるため、スパム検疫メールボックスには大きなデータベースが必要です。詳細については、「[Exchange 2013 のメールボックス データベースの管理](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)」を参照してください。

  - **専用のメールボックスとユーザー アカウントを作成します**   スパム検疫メールボックス専用のメールボックスと Active Directory ユーザー アカウントを作成することをお勧めします。詳細については、「[ユーザー メールボックスを作成する](create-user-mailboxes-exchange-2013-help.md)」を参照してください。
    
    組織の準拠ポリシーとニーズに応じて、メッセージング レコード管理、メールボックスのクォータ、委任権限など、受信者ポリシーを適用することができます。詳細については、「[メッセージング レコード管理](messaging-records-management-exchange-2013-help.md)」を参照してください。
    

    > [!NOTE]
    > 隔離されたメッセージが格納域クォータにより拒否された場合、そのメッセージは失われます。隔離されたメッセージは NDR としてラップされるため、Exchange では隔離されたメッセージの NDR を生成しません。



  - **Outlook を構成します**   組織のニーズに応じて Outlook の代理人アクセス許可を構成する必要があります。さらに、**\[メッセージ\]** ビューに元の `Sender[#0x0069001E]`、`Recipient[#0x0E04001E]`、および `Bcc[#0x0E02001E]` フィールドを表示するように Outlook プロファイルを構成することをお勧めします。詳細については、「[検疫済みメッセージをスパム検疫メールボックスから解放する](release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md)」を参照してください。

## 手順 3: スパム検疫メールボックスを指定する

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[スパム対策とマルウェア対策のアクセス許可](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)」の「スパム対策機能」。

次のコマンドを実行します。

    Set-ContentFilterConfig -QuarantineMailbox <SmtpAddress>

この例では、スパム検疫のしきい値を超えるすべてのメッセージを spamQ@contoso.com に送信します。

    Set-ContentFilterConfig -QuarantineMailbox spamQ@contoso.com

## このステップの検証方法

指定したスパム検疫メールボックスを正常に取得したことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
        Get-ContentFilterConfig | Format-List QuarantineMailbox

2.  表示された値が構成した値であることを確認します。

## 手順 4: SCL による検疫のしきい値を構成する

SCL による検疫のしきい値は、スパムの可能性があるとして識別された特定のメッセージがスパム検疫メールボックスに配信されるしきい値です。SCL による検疫のしきい値は 0 から 9 の値に設定できます。0 はスパムである可能性が最も低く、9 はスパムである可能性が最も高いと見なされます。

組織の要件に応じて SCL しきい値を調整する方法と、受信者単位で SCL しきい値を調整する方法の詳細については、「[コンテンツ フィルターの管理](manage-content-filtering-exchange-2013-help.md)」を参照してください。

## 手順 5: スパム検疫メールボックスを管理する

スパム検疫メールボックスを管理するときは、以下のガイドラインに従います。

  - Outlook の再送機能を使用して元のメッセージを再送信し、スパム検疫メールボックスに送信されたアイテムを解放します。
    
    詳細については、「[検疫済みメッセージをスパム検疫メールボックスから解放する](release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md)」を参照してください。

  - スパム検疫メールボックスのサイズが適切な範囲内に維持されるように、スパム検疫メールボックスを監視します。電子メール メッセージの量は、多数の受信者、メッセージ数が増える自然な傾向、SCL 検疫アクションのしきい値のために変化する可能性があります。

  - スパム検疫メールボックスの誤検出を監視します。スパム検疫メールボックスに多数の誤検知が含まれる場合には、SCL 検疫のしきい値を調整します。誤検出のメッセージがスパム検疫メールボックスに配信されている理由を特定する方法の詳細については、「[スパム対策スタンプ](anti-spam-stamps-exchange-2013-help.md)」を参照してください。

  - 隔離されたメッセージをスパム検疫メールボックスから復元するには、同一の Outlook プロファイルを使用します。異なる Outlook プロファイルにアクセス許可を適用して行うメッセージの復元は、サポートされていません。スパム検疫メールボックスからメッセージを復元または解放するのに、異なる Outlook プロファイルを使用することはできません。


> [!IMPORTANT]
> スパムとして識別された NDR は、検疫される SCL レベルであっても削除されます。NDR はスパム検疫メールボックスに配信されません。このようなメッセージを追跡するには、エージェント ログまたはメッセージ追跡ログを使用します。詳細については、「<A href="anti-spam-agent-logging-exchange-2013-help.md">スパム対策エージェントのログ</A>」を参照してください。



## 手順 6: SCL による検疫のしきい値を調整する

SCL による検疫のしきい値を構成した後、設定を定期的に監視し、組織のニーズに応じて調整する必要があります。たとえば、多数の誤検出がフィルター処理されてスパム検疫メールボックスに入る場合は、SCL による検疫のしきい値を増やします。SCL による検疫のしきい値を調整する方法の詳細については、「[Spam Confidence Level のしきい値](spam-confidence-level-threshold-exchange-2013-help.md)」を参照してください。

