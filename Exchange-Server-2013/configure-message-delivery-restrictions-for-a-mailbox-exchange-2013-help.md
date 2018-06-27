---
title: 'メールボックスのメッセージの配信制限を構成する: Exchange Online Help'
TOCTitle: メールボックスのメッセージの配信制限を構成する
ms:assetid: c4b8b89f-3dbe-4cb8-8839-9a4e8067e00c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb397214(v=EXCHG.150)
ms:contentKeyID: 50555869
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックスのメッセージの配信制限を構成する

 

_**適用先:**Exchange Online, Exchange Server 2013_

EAC またはシェルを使用して、メッセージが個々の受信者に配信されるかどうかを制限できます。メッセージの配信制限は、組織内のユーザーに誰がメッセージを送信できるかを制御するのに役立ちます。たとえば、メールボックスを構成して、特定のユーザーによって送信されたメッセージを受け付けるか、または拒否できます。または、Exchange 組織のユーザーからのメッセージのみを受け付けることができます。

ここで説明するメッセージの配信制限は、すべての受信者の種類に適用されます。異なる受信者の種類の詳細については、「[受信者](recipients-exchange-2013-help.md)」を参照してください。

受信者に関連する追加の管理タスクについては、次のトピックを参照してください。

  - [ユーザー メールボックスの管理](manage-user-mailboxes-exchange-2013-help.md)

  - [配布グループの作成と管理](create-and-manage-distribution-groups-exchange-2013-help.md)

  - [動的配布グループの管理](manage-dynamic-distribution-groups-exchange-2013-help.md)

  - [メール ユーザーの管理](manage-mail-users-exchange-2013-help.md)

  - [メール連絡先の管理](manage-mail-contacts-exchange-2013-help.md)

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「受信者プロビジョニングのアクセス許可」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してメッセージの配信制限を構成する

1.  EAC で、**\[受信者\]** \> **\[メールボックス\]**に移動します。

2.  ユーザー メールボックスの一覧で、メッセージの配信制限を構成するメールボックスをクリックし、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  メールボックスのプロパティ ページで、**\[メールボックスの機能\]** をクリックします。

4.  **\[メッセージの配信制限\]** で **\[詳細の表示\]** をクリックして、次の配信制限を表示して変更します。
    
      - **\[受信を許可する送信者\]**   この受信者にメッセージを送信できる送信者を指定するには、このセクションを使用します。
        
          - **\[すべての送信者\]**   このオプションでは、受信者がすべての送信者からのメッセージを受け付けられるように指定します。これには、Exchange 組織内の送信者と外部の送信者の両方が含まれます。これは既定のオプションです。これに外部ユーザーが含まれるのは、**\[すべての送信者に認証を要求する\]** チェック ボックスをオフにした場合のみです。このチェック ボックスがオンの場合、外部ユーザーからのメッセージは拒否されます。
        
          - **\[指定した送信者からのメッセージのみ許可する\]**   このオプションでは、受信者が Exchange 組織内の指定した一連の送信者からのメッセージのみを受信できるように指定します。**\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックして、Exchange 組織内のすべての受信者の一覧を表示します。目的の受信者を選択して一覧に追加し、**\[OK\]** をクリックします。また、検索ボックスに名前を入力し、**\[検索\]**![\[検索\] アイコン](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "[検索] アイコン") をクリックすることで、特定の受信者を検索することもできます。
        
          - **\[すべての送信者に認証を要求する\]**   このオプションを使用すると、匿名ユーザーはこのユーザーにメッセージを送信できなくなります。これには、Exchange 組織外の外部ユーザーが含まれます。
    
      - **\[受信を拒否する送信者\]**   この受信者へのメッセージの送信をブロックするには、このセクションを使用します。
        
          - **\[拒否する送信者なし\]**   このオプションでは、メールボックスが Exchange 組織内のいずれの送信者からのメッセージも拒否しないように指定します。これは既定のオプションです。
        
          - **\[指次の一覧の送信者\]**   このオプションでは、メールボックスが Exchange 組織内の指定した一連の送信者からのメッセージを拒否するように指定します。**\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックして、Exchange 組織内のすべての受信者の一覧を表示します。目的の受信者を選択して一覧に追加し、**\[OK\]** をクリックします。また、検索ボックスに名前を入力し、**\[検索\]**![\[検索\] アイコン](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "[検索] アイコン") をクリックすることで、特定の受信者を検索することもできます。

5.  **\[OK\]** をクリックして **\[メッセージの配信制限\]** ページを閉じ、**\[保存\]** をクリックして変更を保存します。

## シェルを使用してメッセージ配信の制限を構成する

次の例では、シェルを使用してメールボックスのメッセージの配信制限を構成する方法を示します。その他の受信者の種類には、同じパラメーターと共に、対応する **Set-** コマンドレットを使用します。

この例では、ユーザー Lori Penor、Jeff Phillips、および配布グループ Legal Team 1 のメンバーからのメッセージのみを受け付けるように、Robin Wood のメールボックスを構成します。

    Set-Mailbox -Identity "Robin Wood" -AcceptMessagesOnlyFrom "Lori Penor","Jeff Phillips" -AcceptMessagesOnlyFromDLMembers "Legal Team 1"


> [!NOTE]
> 個別の送信者からのメッセージのみを受け付けるようにメールボックスを構成する場合は、<EM>AcceptMessagesOnlyFrom</EM> パラメーターを使用する必要があります。特定の配布グループのメンバーである送信者からのメッセージのみを受け付けるようにメールボックスを構成する場合は、<EM>AcceptMessagesOnlyFromDLMembers</EM> パラメーターを使用します。



この例では、Robin Wood のメールボックスによってメッセージが受け付けらるユーザーの一覧に、David Pelton という名前のユーザーを追加します。

    Set-Mailbox -Identity "Robin Wood" -AcceptMessagesOnlyFrom @{add="David Pelton"}

この例では、すべての送信者の認証を要求するように Robin Wood のメールボックスを構成します。これは、Exchange 組織の他のユーザーによって送信されたメッセージのみをメールボックスが受け付けることを意味します。

    Set-Mailbox -Identity "Robin Wood" -RequireSenderAuthenticationEnabled $true

この例では、ユーザー Joe Healy、Terry Adams、および配布グループ Legal Team 2 のメンバーからのメッセージを拒否するように、Robin Wood のメールボックスを構成します。

    Set-Mailbox -Identity "Robin Wood" -RejectMessagesFrom "Joe Healy","Terry Adams" -RejectMessagesFromDLMembers "Legal Team 2"

この例では、配布グループ Legal Team 3 のメンバーからのメッセージも拒否するように、Robin Wood のメールボックスを構成します。

    Set-Mailbox -Identity "Robin Wood" -RejectMessagesFromDLMembers @{add="Legal Team 3"}


> [!NOTE]
> 個別の送信者からのメッセージを拒否するようにメールボックスを構成する場合は、<EM>RejectMessagesFrom</EM> パラメーターを使用する必要があります。特定の配布グループのメンバーである送信者からのメッセージを拒否するようにメールボックスを構成する場合は、<EM>RejectMessagesFromDLMembers</EM> パラメーターを使用します。



異なる種類の受信者に対する配信制限の構成に関連する構文およびパラメーターの詳細については、次のトピックを参照してください。

  - [Set-DistributionGroup](https://technet.microsoft.com/ja-jp/library/bb124955\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/ja-jp/library/bb123796\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/ja-jp/library/aa995950\(v=exchg.150\))

  - [Set-MailUser](https://technet.microsoft.com/ja-jp/library/aa995971\(v=exchg.150\))

## 正常な動作を確認する方法

ユーザー メールボックスに対するメッセージの配信制限が正常に構成されたことを確認するには、次のいずれかを実行します。

1.  EAC で、**\[受信者\]** \> **\[メールボックス\]**に移動します。

2.  ユーザー メールボックスの一覧で、メッセージの配信制限を確認するメールボックスをクリックし、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  メールボックスのプロパティ ページで、**\[メールボックスの機能\]** をクリックします。

4.  **\[メッセージの配信制限\]** で **\[詳細の表示\]** をクリックして、メールボックスの配信制限を確認します。

または

シェルで、次のコマンドを実行します。

    Get-Mailbox <identity> | fl AcceptMessagesOnlyFrom,AcceptMessagesOnlyFromDLMembers,RejectMessagesFrom,RejectMessagesFromDLMembers,RequireSenderAuthenticationEnabled

