---
title: '受信者のアクセス許可を管理する: Exchange Online Help'
TOCTitle: 受信者のアクセス許可を管理する
ms:assetid: 749cdfe3-496b-453f-96eb-20a0bf28fd52
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ919240(v=EXCHG.150)
ms:contentKeyID: 51407465
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 受信者のアクセス許可を管理する

 

_**適用先:** Exchange Online, Exchange Server 2013_

EAC またはシェルを使用して、ユーザーまたはグループ (*代理人*と呼ばれます) にアクセス許可を割り当てることができます。これによりユーザーまたはグループは、他のメールボックスからのメッセージを開いたり、送信したりできるようになります。アクセス許可はユーザー メールボックス、リンクされたメールボックス、リソース メールボックス、および共有メールボックスに割り当てることができます。また、アクセス許可は、配布グループ、動的配布グループ、およびメールが有効なセキュリティ グループに割り当てることで、そのグループの代理人がメッセージを送信できるようになります。代理人に次のアクセス許可を割り当てると、メールボックスまたはグループの代わりにメールボックスにアクセスしたり、メッセージを送信したりできます。

  - <strong>フル アクセス</strong>   このアクセス許可によって、代理人がユーザーのメールボックスを開き、メールボックスのコンテンツにアクセスできるようになります。ただし、\[フル アクセス\] のアクセス許可を割り当てても、代理人はそのメールボックスからメールを送信することはできません。メールを送信するには、代理人に \[差出人を指定して送信する\] または \[代理人として送信する\] アクセス許可を割り当てる必要があります。
    
    \[フル アクセス\] アクセス許可は、グループのアクセス許可を構成する場合は使用できません。

  - <strong>差出人を指定して送信する</strong>   このアクセス許可により、代理人はメールボックスを使用してメッセージを送信できます。このアクセス許可が代理人に割り当てられると、代理人がこのメールボックスから送信するすべてのメッセージは、メールボックスの所有者から送信されたかのように表示されます。ただし、このアクセス許可は、代表者がユーザーのメールボックスにサインインすることは許可していません。メールボックスを開くことができるのはユーザーのみです。このアクセス許可がグループに割り当てられると、代理人によって送信されたメッセージはそのグループから送信されたかのように表示されます。

  - <strong>代理人として送信する</strong>   このアクセス許可も、代理人がそのメールボックスを使用してメッセージを送信することを許可します。このアクセス許可が代理人に割り当てられると、代理人によって送信されたすべてのメッセージの <strong>送信元</strong> アドレスに、そのメッセージがメールボックスの所有者の代理として、代理人から送信されたことが示されるようになります。


> [!NOTE]
> アドレス一覧では非表示のメールボックスにアクセスするために [フル アクセス]、[メールボックス所有者として送信する]、または [代理人として送信する] のアクセス許可を割り当てる場合、代理人はそのメールボックスを開いたり、メッセージを送信したりすることができません。



## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:2 分。

  - このトピックの手順には、特定のアクセス許可が必要です。アクセス許可情報については、各手順を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## アクセス許可をメールボックスに割り当てる

前述のとおり、代理人に、ユーザー メールボックス、リンクされたメールボックス、リソース メールボックス、および共有メールボックスのアクセス許可を割り当てることができます。また、シェルを使用すると、代理人に探索メールボックスにアクセスするアクセス許可を割り当てることができます。

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「受信者プロビジョニングのアクセス許可」セクションの「アクセス許可と委任」。

## EAC を使用してアクセス許可を割り当てる

次の手順では、ユーザー メールボックスのアクセス許可を割り当てる方法を示します。リソース メールボックスまたは共有メールボックスにアクセス許可を割り当てるのと同様の手順で、EAC の <strong>リソース</strong> または <strong>共有</strong> ページに移動し、アクセス許可を割り当てるメールボックスを選択します。

1.  EAC で、<strong>受信者</strong> \> <strong>\[メールボックス\]</strong>に移動します。

2.  メールボックスの一覧で、アクセス許可を割り当てるメールボックスをクリックし、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  メールボックスのプロパティ ページで、<strong>メールボックスの委任</strong> をクリックします。

4.  アクセス許可を代理人に割り当てるには、該当のアクセス許可の下にある <strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックして、アクセス許可を割り当てることができる Exchange 組織内のすべての受信者が一覧表示されるページを表示します。目的の受信者を選択して一覧に追加し、<strong>OK</strong> をクリックします。また、検索ボックスに名前を入力し、<strong>検索</strong>![\[検索\] アイコン](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "[検索] アイコン") をクリックすることで、特定の受信者を検索することもできます。
    
    受信者のアクセス許可を削除するには、該当のアクセス許可の下にある受信者を選択し、<strong>削除</strong>![\[削除\] アイコン](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[削除] アイコン") をクリックします。

5.  <strong>保存</strong> をクリックして変更を保存します。

## EAC を使用してアクセス許可を一括で割り当てる

アクセス許可の一括割り当てを行うには、次の手順に従います。

1.  EAC で、<strong>受信者</strong> \> <strong>\[メールボックス\]</strong>に移動します。

2.  アクセス許可を割り当てるメールボックスを選びます。

3.  右のウィンドウで <strong>その他のオプション</strong> をクリックまたはタップし、<strong>メールボックスの委任</strong> で <strong>追加</strong> を選びます。

4.  <strong>委任を一括で追加する</strong> ページで、該当のアクセス許可の下にある <strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックまたはタップして、そのアクセス許可を割り当てることができる Exchange 組織内のすべての受信者が一覧表示されるページを表示します。目的の受信者を選び、一覧に追加して、<strong>OK</strong> をクリックします。
    
    受信者のアクセス許可を削除するには、該当のアクセス許可の下にある受信者を選び、<strong>削除</strong>![\[削除\] アイコン](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[削除] アイコン") をクリックします。

## 他のユーザーのメールボックスからメールを送信するユーザーのアクセス許可を割り当てるには、EAC を使用してください。

別のユーザーのメールボックスからメールを送信するユーザーのアクセス許可を割り当てる方法を次に示します。

1.  EAC で、<strong>受信者</strong> \> <strong>\[メールボックス\]</strong>に移動します。

2.  メールボックスの一覧で、送信のアクセス許可を割り当てるメールボックスをクリックし、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  メールボックスのプロパティ ページで、<strong>メールボックスの委任</strong> をクリックします。

4.  アクセス許可を委任する場合は、<strong>メールボックス所有者として送信する</strong> または <strong>代理人として送信する</strong> から <strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックして、Exchange 組織でアクセス許可の割り当てが可能なすべての受信者を一覧できるページを表示します。目的の受信者を選択して一覧に追加し、<strong>OK</strong> をクリックします。また、検索ボックスに名前を入力し、<strong>検索</strong>![\[検索\] アイコン](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "[検索] アイコン") をクリックすることで、特定の受信者を検索することもできます。
    
    <strong>送信</strong> アクセス許可により代理人はこのメールボックスからメールを送信することができます。
    
    <strong>代理送信</strong> アクセス許可により代理人はこのメールボックスの代理としてメールを送信することができます。代理人が送信したメッセージの \[**差出人**\] は、メッセージがメールボックスの所有者に代わって代理人によって送信されたことが示されます。
    

    > [!NOTE]
    > さらにメールボックスの内容を開いて表示する必要がある場合は、[<STRONG>フル アクセス</STRONG>] のアクセス許可をユーザーに割り当てる必要があります。



5.  <strong>保存</strong> をクリックして変更を保存します。

## グループからのメールを送信するユーザーのアクセス許可を割り当てるには、EAC を使用してください。

グループからのメールを送信するユーザーのアクセス許可を割り当てる方法を次に示します。

1.  EAC で、<strong>受信者</strong> \> <strong>グループ</strong> に移動します。

2.  グループの一覧で、送信のアクセス許可を割り当てるグループをクリックし、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  グループのプロパティ ページで、<strong>グループの委任</strong> をクリックします。

4.  アクセス許可を委任する場合は、<strong>メールボックス所有者として送信する</strong> または <strong>代理人として送信する</strong> から <strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックして、Exchange 組織でアクセス許可の割り当てが可能なすべての受信者を一覧できるページを表示します。目的の受信者を選択して一覧に追加し、<strong>OK</strong> をクリックします。また、検索ボックスに名前を入力し、<strong>検索</strong>![\[検索\] アイコン](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "[検索] アイコン") をクリックすることで、特定の受信者を検索することもできます。
    
    <strong>送信</strong> アクセス許可により代理人はこのグループからメールを送信することができます。
    
    <strong>代理送信</strong> アクセス許可により代理人はこのグループの代理としてメールを送信することができます。代理人が送信したメッセージの \[**差出人**\] は、メッセージがグループに代わって代理人によって送信されたことが示されます。

5.  <strong>保存</strong> をクリックして変更を保存します。

## EAC を使用して、フル アクセスのアクセス許可を割り当てる

次の手順では、ユーザーのメールボックスにフル アクセスのアクセス許可を割り当てる方法を示します。

1.  EAC で、<strong>受信者</strong> \> <strong>\[メールボックス\]</strong>に移動します。

2.  メールボックスの一覧で、フル アクセスのアクセス許可を割り当てるメールボックスをクリックし、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  メールボックスのプロパティ ページで、<strong>メールボックスの委任</strong> をクリックします。

4.  アクセス許可を代理人に割り当てるには、<strong>フル アクセス</strong> のアクセス許可の下にある <strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックして、アクセス許可を割り当てることができる Exchange 組織内のすべての受信者が一覧表示されるページを表示します。目的の受信者を選択して一覧に追加し、<strong>OK</strong> をクリックします。また、検索ボックスに名前を入力し、<strong>検索</strong>![\[検索\] アイコン](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "[検索] アイコン") をクリックすることで、特定の受信者を検索することもできます。
    
    <strong>フル アクセス</strong>   このアクセス許可によって、代理人がユーザーのメールボックスを開き、メールボックスのコンテンツにアクセスできるようになります。
    

    > [!NOTE]
    > ただし、[<STRONG>フル アクセス</STRONG>] のアクセス許可を割り当てても、代理人はそのメールボックスからメールを送信することはできません。メールを送信するには、代理人に [<STRONG>送信</STRONG>] または [<STRONG>代理送信</STRONG>] のアクセス許可を割り当てる必要があります。



5.  <strong>保存</strong> をクリックして変更を保存します。

## シェルを使用してアクセス許可を割り当てる

次のセクションでは、シェルを使用してメールボックスの \[フル アクセス\]、\[差出人を指定して送信する\]、および \[代理人として送信する\] アクセス許可を管理する方法を示します。

## \[フル アクセス\] アクセス許可を管理する

次の例は、**Add-MailboxPermission** および **Remove-MailboxPermission** コマンドレットを使用して、\[フル アクセス\] アクセス許可を管理する方法を示しています。

この例では、代理人 "Raymond Sam" に "Terry Adams" のメールボックスの \[フル アクセス\] アクセス許可を割り当てます。

    Add-MailboxPermission -Identity "Terry Adams" -User raymonds -AccessRights FullAccess -InheritanceType all

この例では、"Esther Valle" に、組織の既定の探索検索メールボックスの \[フル アクセス\] アクセス許可を割り当てます。

    Add-MailboxPermission -Identity "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -User estherv -AccessRights FullAccess -InheritanceType all

この例では、ヘルプデスク配布グループのメンバーに、"Helpdesk Tickets" 共有メールボックスの \[フル アクセス\] アクセス許可を割り当てます。

    Add-MailboxPermission "HelpdeskTickets" -User helpdesk -AccessRights FullAccess -InheritanceType all

この例では、"Ayla Kol" のメールボックスに対する \[フル アクセス\] アクセス許可を "Jim Hance" から削除します。

    Remove-MailboxPermission -Identity ayla -User "Jim Hance" -AccessRights FullAccess -Inheritance

構文およびパラメーターの詳細については、以下のトピックを参照してください。

  - [Add-MailboxPermission](https://technet.microsoft.com/ja-jp/library/bb124097\(v=exchg.150\))

  - [Remove-MailboxPermission](https://technet.microsoft.com/ja-jp/library/bb125153\(v=exchg.150\))

## \[差出人を指定して送信する\] アクセス許可を管理する

次の例は、Exchange Server 2013 および Exchange Online で \[差出人を指定して送信する\] アクセス許可を管理する方法を示しています。Exchange 2013 では、**Add-ADPermission** および **Remove-ADPermission** コマンドレットを、Exchange Online では、**Add-RecipientPermission** および **Remove-RecipientPermission** コマンドレットを使用する必要があります。どちらの場合も、*Identity* パラメーターを使用して、\[差出人を指定して送信する\] アクセス許可を追加または削除するメールボックスの名前を指定し、*User* または *Trustee* パラメーターで \[差出人を指定して送信する\] アクセス許可を割り当てる、または割り当てを解除する代理人 (たとえば、ユーザーまたはグループ) を指定します。


> [!TIP]
> <STRONG>Get-Recipient</STRONG> コマンドレットを使用して、メールボックスおよび代理人の <EM>Name</EM> プロパティを取得します。これらの値を使用して、[差出人を指定して送信する] アクセス許可を割り当てます。



## Exchange Server 2013

この例では、共有メールボックス "Helpdesk Support Team" の \[差出人を指定して送信する\] アクセス許可を、ヘルプデスク グループに割り当てます。

    Add-ADPermission -Identity helpdesksupport -User helpdeskgroup -ExtendedRights "Send As"

この例では、"James Alvord" のメールボックスに対する \[差出人を指定して送信する\] アクセス許可を、ユーザー "Pilar Pinilla" から削除します。

    Remove-ADPermission -Identity "James Alvord" -User pilarp -ExtendedRights "Send As"

構文およびパラメーターの詳細については、「」を参照してください。

  - [Add-ADPermission](https://technet.microsoft.com/ja-jp/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/ja-jp/library/aa996048\(v=exchg.150\))

## Exchange Online

この例では、"Contoso Printer Support" という共有メールボックスの \[差出人を指定して送信する\] アクセス許可を、プリンター サポート グループに割り当てます。

    Add-RecipientPermission -Identity "Contoso Printer Support" -Trustee "Printer Support" -AccessRights SendAs

この例では、メールボックス "Yan Li" に対する \[差出人を指定して送信する\] アクセス許可を、ユーザー "Karen Toh" から削除します。

    Remove-RecipientPermission -Identity "Yan Li" -Trustee "Karen Toh" -ExtendedRights SendAs

構文およびパラメーターの詳細については、「」を参照してください。

  - [Add-RecipientPermission](https://technet.microsoft.com/ja-jp/library/ff935839\(v=exchg.150\))

  - [Remove-RecipientPermission](https://technet.microsoft.com/ja-jp/library/ff945794\(v=exchg.150\))

## \[代理人として送信する\] アクセス許可を管理する

次の例は、**Set-Mailbox** コマンドレットを使用して \[代理人として送信する\] アクセス許可を管理する方法を示しています。

この例では、代理人 "Holly Holt" に、メールボックス "Sean Chai" の \[代理人として送信する\] アクセス許可を割り当てます。

    Set-Mailbox -Identity seanc@contoso.com -GrantSendOnBehalfTo hollyh

この例では、"Temporary Executive Assistants" グループに割り当てられた、共有メールボックス "Contoso Executives" の \[代理人として送信する\] アクセス許可を削除します。

    Set-Mailbox "Contoso Executives" -GrantSendOnBehalfTo @{remove="tempassistants@contoso.com"}

構文およびパラメーターの詳細については、「[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

メールボックスまたは共有メールボックスにアクセス許可を正常に割り当てたことを確認するには、次のいずれかを実行します。

  - EACで:
    
    1.  <strong>受信者</strong> \> <strong>\[メールボックス\]</strong> または <strong>共有</strong> の順に移動してメールボックスをクリックし、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。
    
    2.  メールボックスのプロパティ ページで、<strong>メールボックスの委任</strong> をクリックします。
    
    3.  受信者にアクセス許可を割り当てた場合、該当するアクセス許可の下にユーザーまたはグループが一覧表示されていることを確認します。アクセス許可を削除した場合、該当するアクセス許可の下にその受信者が一覧表示されていないことを確認します。

または

  - シェルでは、管理するアクセス許可に応じて、次のコマンドのいずれかを実行します。
    
      - **フル アクセス**
        
            Get-MailboxPermission -Identity <mailbox>
        
        特定の代理人にメールボックスの \[フル アクセス\] アクセス許可が割り当てられたかどうかを確認するには、次のコマンドを実行します。
        
            Get-MailboxPermission -Identity <mailbox> -User <delegate>
    
      - **送信者**
        
        Exchange Server 2013 で、次のコマンドを実行します。
        
            Get-ADPermission -Identity <name of mailbox> -User <delegate>
        
        Exchange Online で、次のコマンドを実行します。
        
            Get-RecipientPermission -Identity <mailbox> -Trustee <delegate>
    
      - **代理人として送信する**
        
            Get-Mailbox -Identity <mailbox> | FL GrantSendOnBehalfTo

## アクセス許可をグループに割り当てる

前述のように、\[差出人を指定して送信する\] および \[代理人として送信する\] アクセス許可を、配布グループ、動的配布グループ、およびメールが有効なセキュリティ グループに割り当てると、代理人がそのグループとして、またはグループの代わりにメッセージを送信できるようになります。

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「受信者プロビジョニングのアクセス許可」セクションの「配布グループ」および「動的配布グループ」。

## EAC を使用してアクセス許可を割り当てる

1.  EAC で、<strong>受信者</strong> \> <strong>グループ</strong> に移動します。

2.  グループの一覧で、アクセス許可を割り当てるグループをクリックし、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  グループのプロパティ ページで、<strong>グループの委任</strong> をクリックします。

4.  アクセス許可を代理人に割り当てるには、適切なアクセス許可の下にある <strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックすると、アクセス許可を割り当てることができる、Exchange 組織内のすべての受信者の一覧を示すページが表示されます。目的の受信者を選択して一覧に追加し、<strong>OK</strong> をクリックします。また、検索ボックスに名前を入力し、<strong>検索</strong>![\[検索\] アイコン](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "[検索] アイコン") をクリックすることで、特定の受信者を検索することもできます。
    
    受信者のアクセス許可を削除するには、該当のアクセス許可の下にある受信者を選択し、<strong>削除</strong>![\[削除\] アイコン](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[削除] アイコン") をクリックします。

5.  <strong>保存</strong> をクリックして変更を保存します。

## シェルを使用してアクセス許可を割り当てる

次のセクションでは、シェルを使用してグループの \[差出人を指定して送信する\] および \[代理人として送信する\] アクセス許可を管理する方法を示します。

## \[差出人を指定して送信する\] アクセス許可を管理する

次の例は、Exchange Server 2013 および Exchange Online でグループの \[差出人を指定して送信する\] アクセス許可を管理する方法を示しています。Exchange 2013 では、**Add-ADPermission** および **Remove-ADPermission** コマンドレットを使用する必要があります。Exchange Online では、**Add-RecipientPermission** および **Remove-RecipientPermission** コマンドレットを使用する必要があります。どちらの場合も、*Identity* パラメーターを使用して、\[差出人を指定して送信する\] アクセス許可を追加または削除するグループの名前を指定し、*User* または *Trustee* パラメーターで \[差出人を指定して送信する\] アクセス許可を割り当てる、または割り当てを解除する代理人 (たとえば、ユーザーまたはグループ) を指定します。


> [!TIP]
> <STRONG>Get-Recipient</STRONG> コマンドレットを使用して、グループおよび代理人の <EM>Name</EM> プロパティを取得します。これらの値を使用して、[差出人を指定して送信する] アクセス許可を割り当てます。



## Exchange Server 2013

この例では、"Contoso Sales Info" というグループに、セールス管理者グループの \[差出人を指定して送信する\] アクセス許可を割り当てます。これにより、セールス管理者グループのメンバーは、"Contoso Sales Information" グループとしてメッセージを送信できるようになります。

    Add-ADPermission -Identity "Contoso Sales Info" -User "Sales Admins" -ExtendedRights "Send As"

この例では、"Corporate IT Admins" グループの \[差出人を指定して送信する\] アクセス許可を、ユーザー "Alan Shen" から削除します。

    Remove-ADPermission -Identity "Corporate IT Admins" -User contoso\alans -ExtendedRights "Send As"

構文およびパラメーターの詳細については、「」を参照してください。

  - [Add-ADPermission](https://technet.microsoft.com/ja-jp/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/ja-jp/library/aa996048\(v=exchg.150\))

## Exchange Online

この例では、"Contoso Admins" グループに、"Emergency Broadcast Messages" という動的配布グループの \[差出人を指定して送信する\] アクセス許可を割り当てます。

    Add-RecipientPermission -Identity emergencybroadcast@contoso.com -Trustee "Contoso Admins" -AccessRights SendAs

この例では、"Printer Resources" セキュリティ グループの \[差出人を指定して送信する\] アクセス許可を、ユーザー "Walter Harp" から削除します。

    Remove-RecipientPermission -Identity "Printer Resources" -Trustee walterh@contoso.com ExtendedRights SendAs

構文およびパラメーターの詳細については、「」を参照してください。

  - [Add-RecipientPermission](https://technet.microsoft.com/ja-jp/library/ff935839\(v=exchg.150\))

  - [Remove-RecipientPermission](https://technet.microsoft.com/ja-jp/library/ff945794\(v=exchg.150\))

## \[代理人として送信する\] アクセス許可を管理する

次の例は、**Set-DistributionGroup** および **Set-DynamicDistributionGroup** コマンドレットを使用して、グループの \[代理人として送信する\] アクセス許可を管理する方法を示しています。

この例では、"Printer Support" 配布グループの \[代理人として送信する\] アクセス許可を、代理人 "Sara Davis" に割り当てます。

    Set-DistributionGroup -Identity printersupport@contoso.com -GrantSendOnBehalfTo sarad

この例では、"All Employees" 動的配布グループの \[代理人として送信する\] アクセス許可を、代理人 "Administrator" に割り当てます。

    Set-DynamicDistributionGroup -Identity "All Employees" -GrantSendOnBehalfTo administrator

この例では、管理者に割り当てられた "All Employees" 動的配布グループの \[代理人として送信する\] アクセス許可を削除します。

    Set-DynamicDistributionGroup "All Employees" -GrantSendOnBehalfTo @{remove="administrator"}

構文およびパラメーターの詳細については、「」を参照してください。

  - [Set-DistributionGroup](https://technet.microsoft.com/ja-jp/library/bb124955\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/ja-jp/library/bb123796\(v=exchg.150\))

## 正常な動作を確認する方法

アクセス権限がグループに正常に割り当てられたことを確認するには、次の手順を実行します。

  - EACで:
    
    1.  <strong>受信者</strong> \> <strong>グループ</strong> の順に移動してグループをクリックし、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。
    
    2.  グループのプロパティ ページで、<strong>グループの委任</strong> をクリックします。
    
    3.  受信者にアクセス許可を割り当てた場合、該当するアクセス許可の下にユーザーまたはグループが一覧表示されていることを確認します。アクセス許可を削除した場合、該当するアクセス許可の下にその受信者が一覧表示されていないことを確認します。

または

  - シェルでは、管理するアクセス許可に応じて、次のコマンドのいずれかを実行します。
    
      - **送信者**
        
        Exchange Server 2013 で、次のコマンドを実行します。
        
            Get-ADPermission -Identity <name of group> -User <delegate>
        
        Exchange Online で、次のコマンドを実行します。
        
            Get-RecipientPermission -Identity <group> -Trustee <delegate>
    
      - **代理人として送信する**
        
            Get-DistributionGroup -Identity <group> | FL GrantSendOnBehalfTo
        
        または
        
            Get-DynamicDistributionGroup -Identity <group> | FL GrantSendOnBehalfTo

