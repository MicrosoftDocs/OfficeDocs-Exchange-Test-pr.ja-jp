---
title: '管理の役割について: Exchange 2013 Help'
TOCTitle: 管理の役割について
ms:assetid: 887b0a64-84b1-4b8c-9547-e456ea6f5dbd
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd298116(v=EXCHG.150)
ms:contentKeyID: 49896347
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理の役割について

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-07_

管理役割は、Microsoft Exchange Server 2013 で使用される役割ベースのアクセス制御 (RBAC) というアクセス許可モデルに属する概念です。役割は、メールボックスや、トランスポート ルール、受信者などの Exchange 2013 コンポーネントの構成の表示や変更アクセスを提供するために組み合わされるコマンドレットの論理的なグループとして機能します。管理役割をさらに組み合わせて、機能領域と受信者構成の管理を可能にする、管理役割グループおよび管理役割割り当てポリシーと呼ばれるより大きなグループにすることができます。役割グループと役割割り当てポリシーは、管理者とエンド ユーザーそれぞれにアクセス許可を割り当てます。管理役割グループと管理役割の割り当ての詳細については、「[役割ベースのアクセス制御について](understanding-role-based-access-control-exchange-2013-help.md)」を参照してください。


> [!NOTE]
> ここでは、RBAC の高度な機能について説明します。基本的な Exchange 2013 アクセス許可を管理する場合 (Exchange 管理センター (EAC) を使用して役割グループ間のメンバーの追加と削除、役割グループの作成と変更、役割割り当てポリシーの作成と変更を行う場合など) は、「<A href="permissions-exchange-2013-help.md">アクセス許可</A>」を参照してください。



**目次**

組み込みの管理役割

スコープ外の最上位レベルの管理役割

カスタムの管理役割

管理役割の階層

管理役割エントリ

スコープ外の最上位レベルの役割エントリ

管理の役割の種類

詳細情報

管理役割スコープと管理役割の割り当ては、管理役割を操作するための重要なコンポーネントです。これらのコンポーネントの詳細については、以下のトピックを参照してください。

  - [管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)

  - [管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)

管理役割に関連する管理タスクについては、「[アクセス許可](permissions-exchange-2013-help.md)」を参照してください。

## 組み込みの管理役割

Exchange 2013 には、組織の管理に使用できる組み込みの管理役割が多数備えられています。各役割には、ユーザーが特定の Exchange コンポーネントを管理するために必要なコマンドレットとパラメーターが含まれています。組み込みの管理役割の例をいくつか次に示します。

  - **メール受信者**   管理者にメールボックス、連絡先、およびメール ユーザーの管理を許可します。

  - **Transport Rules/トランスポート ルール**   役割を割り当てられた管理者または専門家ユーザーが、トランスポート ルール機能を管理できるようにします。

  - **Distribution Groups/配布グループ**   役割を割り当てられた管理者または専門家ユーザーが、配布グループと配布グループ メンバーを管理できるようにします。

  - **MyPersonalInformation**   エンド ユーザーに個人用の自宅電話番号および Web サイト アドレスの変更を許可します。

Exchange 2013 に備えられている管理役割の完全な一覧については、「[組み込みの管理役割](built-in-management-roles-exchange-2013-help.md)」を参照してください。

Exchange 2013 に備えられている組み込みの役割を使用し、この組み込みの役割をさまざまな方法で組み合わせて、ビジネスに合ったアクセス許可モデルを作成できます。たとえば、役割グループのメンバーに受信者およびパブリック フォルダーを管理させる場合は、"Mail Recipients/メール受信者" 役割と "Public Folders/パブリック フォルダー" 役割の両方を、該当する役割グループに割り当てます。多くの場合、役割グループまたは役割の割り当てポリシーに役割を割り当てます。アクセス許可を詳細なレベルで制御する必要がある場合は、直接ユーザーに管理役割を割り当てることもできますが、アクセス許可モデルを簡素化するには、ユーザーに役割の割り当てを直接行うよりも、役割グループや役割割り当てポリシーを使用することをお勧めします。


> [!NOTE]
> エンド ユーザー管理役割は、役割割り当てポリシーにしか割り当てることができません。



組み込みの管理役割は変更できません。ただし、組み込みの管理役割を基に管理役割を作成し、この新しい役割を、役割グループや役割割り当てポリシーに割り当てることができます。さらに自分のニーズに合わせて、新しい管理役割を変更できます。こうした作業は高度なタスクであり、実行する必要性が生じるのはごく稀です。

組み込みの Exchange 役割を基にしたカスタムの役割の作成の詳細については、このトピックで後述する「カスタムの管理役割」を参照してください。

管理役割を有効にするには、管理役割を割り当てる必要があります。多くの場合、役割グループと役割の割り当てポリシーに管理役割を割り当てます。状況によっては、直接ユーザーに役割を割り当てる場合もありますが、これは、高度なタスクになり、実行する必要性が生じるのは稀です。

管理役割の割り当ての詳細については、以下のトピックを参照してください。

  - [役割グループの管理](manage-role-groups-exchange-2013-help.md)

  - [役割の割り当てポリシーの管理](manage-role-assignment-policies-exchange-2013-help.md)

  - [ユーザーまたは USG に役割を追加する](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

管理役割の割り当ての詳細については、「[管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)」を参照してください。

ページのトップへ

## スコープ外の最上位レベルの管理役割

スコープ外の最上位レベルの管理役割は、特殊なタイプの管理役割で、RBAC を使用してカスタム スクリプトおよび Exchange 以外のコマンドレットへのアクセスをユーザーに許可することができます。正規の管理役割は、Exchange コマンドレットのみへのアクセスを提供します。Exchange サーバーで実行する Exchange 以外のコマンドレットへのアクセスを提供する必要がある場合、またはユーザーが実行可能なスクリプトを発行する必要がある場合は、スコープ外の役割にこれらのコマンドレットを追加する必要があります。これらのコマンドレットが最上位レベルの役割と呼ばれるのは、親の役割から派生させずにスコープ外の役割を作成した場合に、その作成した役割には親がなく、その役割は Exchange 2013 に備えられた組み込みの管理役割のピアになるためです。スコープ外の最上位レベルの役割エントリを作成するように指示するには、**New-ManagementRole** コマンドレットに *UnscopedTopLevel* スイッチを指定して使用する必要があります。

スコープ外の役割は、正規の管理役割とは異なり特定の対象にスコープを制限できないことから、このように名付けられています。スコープ外の役割は、常に組織規模です。つまり、スコープ外の役割を割り当てた担当者が、Exchange 2013 組織内のあらゆるオブジェクトを変更できるということです。このような理由から、スコープ外の役割を介して使用可能になったスクリプトおよびコマンドレットの場合は、徹底的にテストして何が変更されるかを把握したり、スコープ外の役割を慎重に割り当てるなど、細心の注意が求められます。

スコープ外の役割は、役割グループや、管理役割、ユーザー、ユニバーサル セキュリティ グループ (USG) などの役割の被割り当て者に割り当てることができます。ただし、スコープ外の役割は、管理役割割り当てポリシーには割り当てることができません。

Exchange コマンドレットは、スコープ外の役割にある管理役割エントリとして追加することはできませんが、役割エントリとして追加したスクリプトに含めることができます。このようにすると、ユーザーに割り当てることができる Exchange タスクを実行するカスタムのスクリプトを作成します。これは、ユーザーの管理レベルを超える高いアクセス許可が必要なタスクをユーザーが実行する必要がある場合や、新しい管理役割または役割グループの作成が難しい場合に有効です。この特定の機能を実行するスクリプトを作成し、そのスクリプトをスコープ外の役割に追加して、そのスコープ外の役割をユーザーに割り当てることができます。その後、ユーザーがスクリプトによって提供された特定の機能のみを実行できるようになります。

スコープ外の役割に追加する役割エントリも、スコープ外の最上位レベルの役割エントリとして指定する必要があります。スコープ外の最上位レベルの役割エントリの詳細については、後述する「スコープ外の最上位レベルの役割エントリ」を参照してください。

組織の管理 役割グループには、既定で、スコープ外の役割グループを作成または管理するためのアクセス許可がありません。これは、スコープ外の役割グループが誤って作成または変更されることを防止するためです。組織の管理 役割グループは、"Unscoped Role Management/スコープ外役割管理" 管理役割を役割グループ自身およびその他の役割の被割り当て者に委任できます。スコープ外の最上位レベルの管理役割の作成方法の詳細については、「[対象範囲外の役割を作成する](create-an-unscoped-role-exchange-2013-help.md)」を参照してください。

ページのトップへ

## カスタムの管理役割

組み込みの管理役割がユーザーのニーズを満たさない場合は、組み込みの Exchange 役割を基にカスタムの管理役割を作成できます。カスタムの管理役割を作成すると、新しい子の役割は、親の役割のすべての管理役割エントリを継承します。その後、カスタムの管理役割に維持する必要がある管理役割エントリを選択し、不要なエントリはすべて削除できます。

カスタムの役割は、新しい役割の作成に使用した役割の子になります。親の役割に存在する、新しい子の役割の管理役割エントリのみを使用できます。詳細については、後述する以下のセクションを参照してください。

  - 管理役割の階層

  - 管理役割エントリ

カスタムの管理役割を作成するには複数のステップが必要になり、これは高度なタスクで実行する必要が生じるのは稀です。カスタムの管理役割を作成する場合は、既存の組み込みの管理役割の 1 つに、必要なアクセス許可が備えられていないことを事前に確認してください。組み込みの管理役割の詳細、またはカスタムの管理役割の作成については、以下のトピックを参照してください。

  - [組み込みの管理役割](built-in-management-roles-exchange-2013-help.md)

  - [高度な権限](advanced-permissions-exchange-2013-help.md)

管理役割を作成する方法の詳細については、「[役割を作成する](create-a-role-exchange-2013-help.md)」を参照してください。

ページのトップへ

## 管理役割の階層

管理役割は親と子の階層内に存在します。既定で Exchange 2013 に備えられている組み込みの管理役割は、階層の最上位に位置付けられます。役割を作成すると、親の役割のコピーが作成されます。新しい役割は、コピー元の役割の子になります。その後、新しい役割は、割り当て対象の管理者またはユーザーのニーズに合わせてカスタマイズできます。

カスタマイズされた役割を使用して、役割を作成できます。カスタマイズされた既存の役割から新しい役割を作成した場合、カスタマイズされた既存の役割は、その親の役割の子であり続けると共に、新しい役割の親にもなります。役割がコピーされると、その都度新しい子の役割には直上の親の役割に存在する役割エントリのみが含まれます。

各管理役割には、変更できない役割の種類が与えられます。役割の種類は、役割に使用する基本のコンテキストを定義します。役割の種類は、子の役割の作成時に親の役割からコピーされます。

**管理役割の階層**

![RBAC 管理役割階層図](images/Dd298116.6851c829-ca8f-40e7-a67c-cc9e85c33953(EXCHG.150).gif "RBAC 管理役割階層図")

上の図に、いくつかの管理役割の階層関係を示します。"Mail Recipients/メール受信者" 役割と "Help Desk/ヘルプ デスク" 役割は、組み込みの役割です。これらの役割から派生するすべての子の役割は、各組み込み役割の役割の種類を継承します。たとえば、"Mail Recipients/メール受信者" 役割から直接または間接に派生するすべての子の役割は、`MailRecipients` の役割の種類を継承します。

"Seattle Recipient Administrators/Seattle の受信者管理者" カスタム役割は、組み込みの "Mail Recipients/メール受信者" 役割の子ですが、"Seattle Sales Recipient Administrators/Seattle の営業受信者管理者" カスタム役割と "Seattle Legal Recipient Administrators/Seattle のリーガル受信者の管理者" カスタム役割の親でもあります。"Seattle Recipient Administrators/Seattle の受信者管理者" カスタム役割には、"Mail Recipients/メール受信者" 役割で利用可能なコマンドレットの一部のみが含まれます。"Seattle Recipient Administrators/Seattle の受信者管理者" カスタム役割の子の役割には、その役割にも存在するコマンドレットしか含めることができません。たとえば、"Mail Recipients/メール受信者" 役割には存在するが、"Seattle Recipient Administrators/Seattle の受信者管理者" カスタム役割には存在しないコマンドレットは、"Seattle Sales Recipient Administrators/Seattle の営業受信者管理者" のカスタム役割に追加することはできません。

すべてのカスタム役割は、前に説明した役割と同じパターンに従います。管理役割に対するコマンドレットへのアクセスの制御方法の詳細については、このトピックで次に説明する「管理役割エントリ」を参照してください。

ページのトップへ

## 管理役割エントリ

すべての管理役割は、カスタムの Exchange 役割であってもスコープ外の役割であっても、少なくとも 1 つの管理役割エントリを持つ必要があります。エントリは、1 つのコマンドレットとそのパラメーター、スクリプト、または (必要であれば) 特殊なアクセス許可で構成されます。コマンドレットまたはスクリプトが管理役割のエントリとして存在しない場合、そのコマンドレットまたはスクリプトにはその管理役割を介してアクセスできません。同様に、パラメーターがエントリに存在しない場合、そのコマンドレットまたはスクリプトのパラメーターにはその管理役割を介してアクセスできません。

Exchange 2013 では、組み込みの Exchange 管理の最上位レベルの役割に基づいた役割エントリ、およびスコープ外の最上位レベルの管理役割に基づいた役割エントリを管理できます。組み込みの Exchange 最上位レベルの役割に基づいた役割には、Exchange 2013 コマンドレットである役割エントリしか含めることができません。カスタム スクリプトまたは Exchange 以外のコマンドレットを追加してユーザーが使用できるようにするには、それらをスコープ外の役割エントリとしてスコープ外の最上位レベルに追加する必要があります。スコープ外の役割エントリの詳細については、このトピックで後述する「スコープ外の最上位レベルの役割エントリ」を参照してください。

役割エントリが Exchange コマンドレットベースの役割エントリであるか、スコープ外の役割エントリであるかに関係なく、すべての役割エントリは以下のセクションで説明する原則と同じ原則に従います。

役割エントリの管理の詳細については、「[管理役割と役割エントリ](management-roles-and-role-entries-exchange-2013-help.md)」を参照してください。

## 親と子の管理役割の関係

前述したとおり、コマンドレットとそのパラメーターを含めた管理役割エントリは、エントリを子の役割に追加するために直上の親の役割に存在する必要があります。たとえば、親の役割に **New-Mailbox** のエントリがない場合は、そのコマンドレットを子の役割に割り当てることができません。さらに、**Set-Mailbox** は親の役割に存在するが *Database* パラメーターはそのエントリから削除されていた場合は、**Set-Mailbox** コマンドレットの *Database* パラメーターはその子の役割のエントリに追加できません。

管理役割エントリが親の役割に存在しない場合は、子の役割には追加できません。また役割は特定の役割の種類に基づいています。これらの理由から、カスタマイズした役割を作成する際は、コピー対象となる親の役割を慎重に選択してください。

ページのトップへ

## 管理役割エントリ名

管理役割エントリ名は、それらが関連付けられている管理役割と、コマンドレットまたはスクリプトの名前を組み合わせたものです。役割名と、コマンドレットまたはスクリプトは、円記号 (\\) で区切られます。たとえば、"Mail Recipients/メール受信者" 役割の **Set-Mailbox** コマンドレットの役割エントリ名は、`Mail Recipients\Set-Mailbox` です。役割エントリの名前にスペースが含まれる場合は、名前全体を二重引用符 (") で囲む必要があります。

入力した内容と一致するすべての役割エントリを返すためには、役割エントリ名内にワイルドカード文字 (\*) を使用できます。ワイルドカード文字は、円記号のどちらの側でも使用できます。以下の表に、役割エントリ名でのワイルドカード文字の使用方法についてのいくつかのバリエーションを示します。

**管理役割エントリ名にワイルドカード文字を使用する場合**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>使用例</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>*\*</code></p></td>
<td><p>すべての役割のすべての役割エントリの一覧を返します。</p></td>
</tr>
<tr class="even">
<td><p><code>*\Set-Mailbox</code></p></td>
<td><p><strong>Set-Mailbox</strong> コマンドレットを含むすべての役割エントリの一覧を返します。</p></td>
</tr>
<tr class="odd">
<td><p><code>Mail Recipients\*</code></p></td>
<td><p>&quot;Mail Recipients/メール受信者&quot; 役割のすべての役割エントリの一覧を返します。</p></td>
</tr>
<tr class="even">
<td><p><code>Mail Recipients\*Mailbox</code></p></td>
<td><p>&quot;Mail Recipients/メール受信者&quot; 役割の役割エントリのうち、Mailbox で終わるコマンドレットを含むすべてのエントリの一覧を返します。</p></td>
</tr>
<tr class="odd">
<td><p><code>My*\*Group*</code></p></td>
<td><p>My で始まるすべての役割の役割エントリのうち、コマンドレット名に文字列 Group を含むすべてのエントリの一覧を返します。</p></td>
</tr>
</tbody>
</table>


## スコープ外の最上位レベルの役割エントリ

カスタムのスクリプトまたは Exchange 以外のコマンドレットに基づいて役割を作成するには、スコープ外の最上位レベルの役割エントリをスコープ外の最上位レベルの管理役割と共に使用します。各スコープ外の役割エントリは、1 つのカスタムのスクリプトまたは Exchange 以外のコマンドレットに関連付けられます。スコープ外の役割にスコープ外の役割エントリを作成するように指定するには、**Add-ManagementRoleEntry** コマンドレットで *UnscopedTopLevel* パラメーターを指定する必要があります。

スコープ外の役割エントリを追加する場合は、スクリプトまたは Exchange 以外のコマンドレットで使用可能なすべてのパラメーターを指定する必要があります。Exchange は、役割エントリの追加時に指定したパラメーターの検証を試みます。スコープ外の役割に割り当てられているユーザーは、役割エントリの作成時に役割エントリに追加されたパラメーターのみを使用できます。スクリプトまたは Exchange 以外のコマンドレットにパラメーターを追加する場合やパラメーター名を変更する場合は、手動で役割エントリを更新する必要があります。Exchange は、スコープ外の役割エントリの既存のパラメーターが変更されたかどうかをチェックしません。スクリプト内で役割エントリのパラメーターが変更されており、そのパラメーターを使用しようとすると、コマンドの実行に失敗します。

スコープ外の役割エントリに追加するスクリプトは、管理者およびユーザーが Exchange 2013 管理シェルを使用して接続するすべてのサーバーの Exchange スクリプト ディレクトリに保存する必要があります。スコープ外の役割エントリを追加するために、使用しているサーバーの Exchange 2013 スクリプト ディレクトリに存在していないスクリプトに基づいたスコープ外の役割エントリを追加しようとすると、エラーが発生します。Exchange 2013 スクリプト ディレクトリの既定のインストール場所は、C:\\Program Files\\Microsoft\\Exchange Server\\V15\\RemoteScripts です。

スコープ外の役割エントリに追加する Exchange 以外のコマンドレットは、管理者およびユーザーがシェルを使用して接続してコマンドレットを使用するすべての Exchange 2013 サーバーにインストールする必要があります。スコープ外の役割エントリを追加するために、使用している Exchange サーバーにインストールしていない Exchange 2013 以外のコマンドレットに基づいたスコープ外の役割エントリを追加しようとすると、エラーが発生します。Exchange 以外のコマンドレットを追加する場合は、Windows 以外のコマンドレットを含む Exchange PowerShell スナップイン名を指定する必要があります。

スコープ外の管理役割エントリの追加方法の詳細については、「[役割エントリを役割に追加する](add-a-role-entry-to-a-role-exchange-2013-help.md)」を参照してください。

ページのトップへ

## 管理の役割の種類

管理役割の種類は、すべての管理役割の基礎になります。種類は、指定した役割の種類のすべての管理役割で定義された暗黙的なスコープを定義し、関連する役割の論理グループとしても機能します。親の組み込みの管理役割から派生したすべての管理役割には、同じ役割の種類があります。この関係を示した図については、このトピックの前述の管理役割の階層図を参照してください。管理役割の種類は、役割の種類に関連付けられた役割に追加可能なコマンドレットとそのパラメーターの最大セットも表します。

管理役割の種類は、次のカテゴリに分類されます。

  - **管理者または専門家**   管理者または専門家の役割の種類に関連付けられた役割は、Exchange 組織に広範な影響を与えます。この役割の種類を持つ役割では、サーバーまたは受信者の管理、組織の構成、法令遵守管理、監査などのタスクを実行できます。

  - **ユーザーフォーカス**   ユーザーフォーカスの役割の種類に関連付けられた役割は、個々のユーザーと密接に関連する一定範囲の影響を与えます。この役割の種類を持つ役割では、ユーザー プロファイル構成と自己管理、ユーザー独自の配布グループの管理などのタスクを実行できます。
    
    ユーザーフォーカスの役割の種類および種類名に関連付けられた役割名は、My で始まります。

  - **スペシャリティ**   スペシャリティの役割の種類に関連付けられた役割は、管理者またはユーザーフォーカスの役割の種類以外のタスクを実行できます。この役割の種類の役割では、アプリケーションに対する偽装、Exchange 以外のコマンドレットまたはスクリプトの使用などのタスクを実行できます。

以下の表に、Exchange 2013 の管理者の管理役割の種類のすべての一覧を示し、役割の種類によって許可される構成が、Exchange 組織全体に適用されるのか、個々のサーバーにのみ適用されるのかを示します。各役割の説明、役割を割り当てられたことによって恩恵を受ける可能性のある人間、およびその他の情報などの、これらの役割の種類に関連付けられた各管理役割の詳細については、「[組み込みの管理役割](built-in-management-roles-exchange-2013-help.md)」を参照してください。

**管理者の役割の種類**


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>管理の役割の種類</th>
<th>組み込みの管理役割</th>
<th>説明</th>
<th>組織またはサーバー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>ActiveDirectoryPermissions</code></p></td>
<td><p><a href="active-directory-permissions-role-exchange-2013-help.md">&quot;Active Directory Permissions/Active Directory アクセス許可&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内の Active Directory アクセス許可を構成できるようになる役割に関連付けられます。Active Directory アクセス許可またはアクセス制御リスト (ACL) を使用する一部の機能には、トランスポートの受信コネクタと送信コネクタ、メールボックスに対する送信者アクセス許可と代理送信アクセス許可などがあります。</p>

> [!NOTE]
> Active Directory オブジェクトに直接設定するアクセス許可が RBAC を介して強制されない場合があります。


</td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>AddressLists</code></p></td>
<td><p><a href="address-lists-role-exchange-2013-help.md">&quot;Address Lists/アドレス一覧&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者に組織内のアドレス一覧、グローバル アドレス一覧 (GAL)、およびオフライン アドレス一覧の管理を許可する役割に関連付けられています。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>ApplicationImpersonation</code></p></td>
<td><p><a href="applicationimpersonation-role-exchange-2013-help.md">ApplicationImpersonation 役割</a></p></td>
<td><p>この役割の種類は、組織内のユーザーに偽装したアプリケーションにそのユーザーのタスクの代行を許可する役割に関連付けられています。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>ArchiveApplication</code></p></td>
<td><p><a href="archiveapplication-role-exchange-2013-help.md">ArchiveApplication 役割</a></p></td>
<td><p>この役割の種類は、パートナー アプリケーションに組織内のユーザー メールボックスのアイテムのアーカイブを許可する役割に関連付けられています。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>AuditLogs</code></p></td>
<td><p><a href="audit-logs-role-exchange-2013-help.md">&quot;Audit Logs/監査ログ&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者に組織内の監査ログ構成の構成を許可する役割に関連付けられています。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>CmdletExtensionAgents</code></p></td>
<td><p><a href="cmdlet-extension-agents-role-exchange-2013-help.md">&quot;Cmdlet Extension Agents/コマンドレット拡張エージェント&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内のコマンドレット拡張エージェントを管理できるようになる役割に関連付けられます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>DataLossPrevention</code></p></td>
<td><p><a href="data-loss-prevention-role-exchange-2013-help.md">&quot;Data Loss Prevention/データ損失防止&quot; 役割</a></p></td>
<td><p>この役割の種類は、組織内のデータ損失防止 (DLP) ポリシーとこれらのポリシー内のルールを作成および管理する役割に関連付けられています。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>DatabaseAvailabilityGroups</code></p></td>
<td><p><a href="database-availability-groups-role-exchange-2013-help.md">&quot;Database Availability Groups/データベース可用性グループ&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者に組織内のデータベース可用性グループ (DAG) の管理を許可する役割に関連付けられています。この役割を直接的または間接的に割り当てられている管理者は、組織内の高可用性構成の責任を負う、最高レベルの管理者です。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>DatabaseCopies</code></p></td>
<td><p><a href="database-copies-role-exchange-2013-help.md">&quot;Database Copies/データベース コピー&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が個々のサーバーのデータベース コピーを管理できるようになる役割に関連付けられます。</p></td>
<td><p>サーバー</p></td>
</tr>
<tr class="even">
<td><p><code>Databases</code></p></td>
<td><p><a href="databases-role-exchange-2013-help.md">&quot;Databases/データベース&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が個々のサーバーのメールボックス データベースを作成、管理、マウント、マウント解除できるようになる役割に関連付けられます。</p></td>
<td><p>サーバー</p></td>
</tr>
<tr class="odd">
<td><p><code>DisasterRecovery</code></p></td>
<td><p><a href="disaster-recovery-role-exchange-2013-help.md">&quot;Disaster Recovery/障害回復&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者に組織内のメールボックスとメールボックス データベースの復元、メールボックス データベースの作成、およびデータベース可用性グループのデータセンター切り替えと切り戻しの実行を許可する役割に関連付けられています。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>DistributionGroups</code></p></td>
<td><p><a href="distribution-groups-role-exchange-2013-help.md">&quot;Distribution Groups/配布グループ&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内の配布グループと配布グループ メンバーを作成および管理できるようになる役割に関連付けられます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>EdgeSubscriptions</code></p></td>
<td><p><a href="edge-subscriptions-role-exchange-2013-help.md">&quot;Edge Subscriptions/エッジ サブスクリプション&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内の Exchange 2010 エッジ トランスポート サーバーと Exchange 2013 メールボックス サーバー間のエッジ同期およびサブスクリプション構成を管理できるようになる役割に関連付けられます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>EmailAddressPolicies</code></p></td>
<td><p><a href="e-mail-address-policies-role-exchange-2013-help.md">&quot;E-Mail Address Policies/電子メール アドレス ポリシー&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内の電子メール アドレス ポリシーを管理できるようになる役割に関連付けられます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>ExchangeConnectors</code></p></td>
<td><p><a href="exchange-connectors-role-exchange-2013-help.md">&quot;Exchange Connectors/Exchange コネクタ&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が配信エージェント コネクタを作成、変更、表示、削除できるようになる役割に関連付けられます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>ExchangeServerCertificates</code></p></td>
<td><p><a href="exchange-server-certificates-role-exchange-2013-help.md">&quot;Exchange Server Certificates/Exchange Server 証明書&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が個々のサーバーの Exchange サーバー証明書を作成、インポート、エクスポート、管理できるようになる役割に関連付けられます。</p></td>
<td><p>サーバー</p></td>
</tr>
<tr class="odd">
<td><p><code>ExchangeServers</code></p></td>
<td><p><a href="exchange-servers-role-exchange-2013-help.md">Exchange Servers 役割</a></p></td>
<td><p>この役割の種類は、管理者が個々のサーバーの Exchange サーバー構成を管理できるようになる役割に関連付けられます。</p></td>
<td><p>サーバー</p></td>
</tr>
<tr class="even">
<td><p><code>ExchangeVirtualDirectories</code></p></td>
<td><p><a href="exchange-virtual-directories-role-exchange-2013-help.md">&quot;Exchange Virtual Directories/Exchange 仮想ディレクトリ&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が各サーバーの Outlook Web App、Microsoft ActiveSync、オフライン アドレス帳 (OAB)、自動検出、Windows PowerShell、Exchange 管理センターの仮想ディレクトリを管理できるようになる役割に関連付けられます。</p></td>
<td><p>サーバー</p></td>
</tr>
<tr class="odd">
<td><p><code>FederatedSharing</code></p></td>
<td><p><a href="federated-sharing-role-exchange-2013-help.md">&quot;Federated Sharing/フェデレーションの共有&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内のフォレスト間と組織間の共有を管理できるようになる役割に関連付けられます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>InformationRightsManagement</code></p></td>
<td><p><a href="information-rights-management-role-exchange-2013-help.md">Information Rights Management 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内の Exchange の Information Rights Management (IRM) を管理できるようになる役割に関連付けられます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>Journaling</code></p></td>
<td><p><a href="journaling-role-exchange-2013-help.md">&quot;Journaling/ジャーナリング&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内のジャーナリング構成を構成できるようになる役割に関連付けられます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>LegalHold</code></p></td>
<td><p><a href="legal-hold-role-exchange-2013-help.md">&quot;Legal Hold/法的情報保留&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織の訴訟目的にメールボックス内のデータを保持するかどうかを設定できるようになる役割に関連付けられます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>MailboxImportExport</code></p></td>
<td><p><a href="mailbox-import-export-role-exchange-2013-help.md">&quot;Mailbox Import Export/メールボックスのインポートとエクスポート&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者にメールボックス内容のインポート/エクスポート、メールボックスの不要な内容の削除を許可する役割に関連付けられています。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>MailboxSearch</code></p></td>
<td><p><a href="mailbox-search-role-exchange-2013-help.md">&quot;Mailbox Search/メールボックス検索&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内の 1 つ以上のメールボックスの内容を検索できるようになる役割に関連付けられます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>MailboxSearchApplication</code></p></td>
<td><p><a href="mailboxsearchapplication-role-exchange-2013-help.md">MailboxSearchApplication 役割</a></p></td>
<td><p>この役割の種類は、パートナー アプリケーションに組織内のメールボックスの法的情報保留ステータスの設定および表示を許可する役割に関連付けられています。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>MailEnabledPublicFolders</code></p></td>
<td><p><a href="mail-enabled-public-folders-role-exchange-2013-help.md">&quot;Mail Enabled Public Folders/メールが有効なパブリック フォルダー&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が個々のパブリック フォルダーを組織内でメールが有効なパブリック フォルダーにするか、メールが無効なパブリック フォルダーにするかを設定できるようになる役割に関連付けられます。</p>
<p>この役割の種類では、パブリック フォルダーの電子メール プロパティのみを管理できます。パブリック フォルダーのプロパティのうち、電子メール プロパティ以外のものを管理することはできません。パブリック フォルダーのプロパティのうち電子メール以外のプロパティを管理するには、<code>PublicFolders</code> 役割の種類に関連付けられている役割が自分に割り当てられている必要があります。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>MailRecipientCreation</code></p></td>
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">&quot;メール受信者の作成&quot; 役割</a></p>
<p></p></td>
<td><p>この役割の種類は、管理者が組織内のメールボックス、メール ユーザー、メール連絡先、配布グループ、および動的配布グループを作成できるようになる役割に関連付けられます。この役割の種類に関連付けられている役割は、<code>MailRecipients</code> 役割の種類に関連付けられている役割と組み合わせて、受信者の作成と管理を有効にできます。</p>
<p>この役割の種類では、パブリック フォルダーのメールを有効にすることはできません。パブリック フォルダーのメールを有効にするには、<code>MailEnabledPublicFolders</code> の役割の種類に関連付けられている役割を割り当てられる必要があります。</p>
<p>組織がアクセス許可モデルを維持していて、受信者管理を実行するグループと受信者の作成を実行するグループが異なる場合は、受信者の作成を実行するグループに <code>MailRecipientCreation</code> 役割を割り当て、受信者管理を実行するグループに <code>MailRecipients</code> 役割を割り当ててください。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>MailRecipients</code></p></td>
<td><p><a href="mail-recipients-role-exchange-2013-help.md">&quot;Mail Recipient/メール受信者&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内の既存のメールボックス、メール ユーザー、メール連絡先、配布グループ、および動的配布グループを管理できるようになる役割に関連付けられます。この役割の種類に関連付けられている役割は、これらの受信者を作成できませんが、<code>MailRecipientCreation</code> 役割の種類に関連付けられている役割と組み合わせて、受信者の作成と管理を有効にできます。</p>
<p>この役割の種類では、メールが有効なパブリック フォルダーまたは配布グループを管理できません。メールが有効なパブリック フォルダーを管理するには、<code>MailEnabledPublicFolders</code> の役割の種類に関連付けられている役割を割り当てられる必要があります。配布グループを管理するには、<code>DistributionGroups</code> 役割の種類に関連付けられている役割を割り当てられる必要があります。</p>
<p>組織がアクセス許可モデルを維持していて、受信者管理を実行するグループと受信者の作成を実行するグループが異なる場合は、受信者の作成を実行するグループに <code>MailRecipientCreation</code> 役割を割り当て、受信者管理を実行するグループに <code>MailRecipients</code> 役割を割り当ててください。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>MailTips</code></p></td>
<td><p><a href="mail-tips-role-exchange-2013-help.md">&quot;Mail Tips/メール ヒント&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者に組織内のメール ヒントの管理を許可する役割に関連付けられています。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>MessageTracking</code></p></td>
<td><p><a href="message-tracking-role-exchange-2013-help.md">&quot;Message Tracking/メッセージ追跡&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内のメッセージを追跡できるようになる役割に関連付けられます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>Migration</code></p></td>
<td><p><a href="migration-role-exchange-2013-help.md">&quot;Migration/移行&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者がメールボックスとメールボックスの内容をサーバー内またはサーバー外へ移行できるようになる役割に関連付けられます。</p></td>
<td><p>サーバー</p></td>
</tr>
<tr class="even">
<td><p><code>Monitoring</code></p></td>
<td><p><a href="monitoring-role-exchange-2013-help.md">&quot;Monitoring/監視&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内の Microsoft Exchange サービスとコンポーネントの可用性を監視できるようになる役割に関連付けられます。管理者以外にも、この役割の種類に関連付けられている役割は、Exchange サーバーの状態情報を収集するために監視アプリケーションによって使用されるサービス アカウントと共に使用できます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>MoveMailboxes</code></p></td>
<td><p><a href="move-mailboxes-role-exchange-2013-help.md">&quot;Move Mailboxes/メールボックスの移動&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内のサーバー間、およびローカル組織と別の組織内のサーバー間でメールボックスを移動できるようになる役割に関連付けられます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>OfficeExtensionApplication</code></p></td>
<td><p><a href="officeextensionapplication-role-exchange-2013-help.md">OfficeExtensionApplication 役割</a></p></td>
<td><p>この役割の種類は、Microsoft Office 拡張アプリケーションに組織内のユーザー メールボックスへのアクセスを許可する役割に関連付けられています。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>OrgCustomApps</code></p></td>
<td><p><a href="org-custom-apps-role-exchange-2013-help.md">&quot;Org Custom Apps/組織のカスタム アプリ&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内のカスタム アプリケーションを表示および変更できるようになる役割に関連付けられます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>OrgMarketplaceApps</code></p></td>
<td><p><a href="org-marketplace-apps-role-exchange-2013-help.md">&quot;Org Marketplace Apps/組織マーケットプレイス アプリ&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内のマーケットプレース アプリケーションを表示および変更できるようになる役割に関連付けられます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>OrganizationClientAccess</code></p></td>
<td><p><a href="organization-client-access-role-exchange-2013-help.md">&quot;Organization Client Access/組織クライアント アクセス&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内のクライアント アクセス サーバーの設定を管理できるようになる役割に関連付けられます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>OrganizationConfiguration</code></p></td>
<td><p><a href="organization-configuration-role-exchange-2013-help.md">&quot;Organization Configuration/組織の構成&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内で組織全体の設定を管理できるようになる役割に関連付けられます。この役割の種類で制御可能な組織の構成には以下が含まれます。</p>
<ul>
<li><p>組織に対してメール ヒントを有効にするかそれとも無効にするか。</p></li>
<li><p>管理フォルダー ホーム ページの URL。</p></li>
<li><p>Microsoft Exchange 受信者の SMTP アドレスと代替電子メール アドレス。</p></li>
<li><p>リソース メールボックスのプロパティ スキーマの構成。</p></li>
<li><p>Exchange 管理センターと Outlook Web App のヘルプの URL。</p></li>
</ul>
<p>この役割の種類には、<code>OrganizationClientAccess</code> または <code>OrganizationTransportSettings</code> の役割の種類に含まれているアクセス許可は含まれていません。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>OrganizationTransportSettings</code></p></td>
<td><p><a href="organization-transport-settings-role-exchange-2013-help.md">&quot;Organization Transport Settings/組織トランスポート設定&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者がシステム メッセージ、Active Directory サイト構成、および組織内のその他の組織全体のトランスポート設定などの組織全体のトランスポート設定を管理できるようになる役割に関連付けられます。</p>
<p>この役割では、トランスポート受信と送信コネクタ、キュー、検疫、エージェント、リモート ドメインと承認済みドメイン、またはルールの作成や管理を行うことはできません。各トランスポート機能を作成または管理するには、次の役割の種類に関連付けられた役割を割り当てられる必要があります。</p>
<ul>
<li><p><strong>受信コネクタ</strong> <code>ReceiveConnectors</code></p></li>
<li><p><strong>送信コネクタ</strong> <code>SendConnectors</code></p></li>
<li><p><strong>トランスポート キュー</strong> <code>TransportQueues</code></p></li>
<li><p><strong>トランスポート検疫</strong> <code>TransportHygiene</code></p></li>
<li><p><strong>トランスポート エージェント</strong> <code>TransportAgents</code></p></li>
<li><p><strong>リモート ドメインおよび承認済みドメイン</strong> <code>RemoteAndAcceptedDomains</code></p></li>
<li><p><strong>トランスポート ルール</strong> <code>TransportRules</code></p></li>
</ul></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>POP3AndIMAP4Protocols</code></p></td>
<td><p><a href="pop3-and-imap4-protocols-role-exchange-2013-help.md">&quot;POP3 and IMAP4 Protocols/POP3 および IMAP4 プロトコル&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が個々のサーバーの認証と接続設定などの POP3 および IMAP4 構成を管理できるようになる役割に関連付けられます。</p></td>
<td><p>サーバー</p></td>
</tr>
<tr class="odd">
<td><p><code>PublicFolders</code></p></td>
<td><p><a href="public-folders-role-exchange-2013-help.md">&quot;Public Folders/パブリック フォルダー&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内のパブリック フォルダーを管理できるようになる役割に関連付けられます。</p>
<p>この役割の種類では、パブリック フォルダーのメールを有効にするかどうかを管理することはできません。パブリック フォルダーのメールを有効または無効にするには、<code>MailEnabledPublicFolders</code> の役割の種類に関連付けられている役割を割り当てられる必要があります。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>ReceiveConnectors</code></p></td>
<td><p><a href="receive-connectors-role-exchange-2013-help.md">&quot;Receive Connectors/受信コネクタ&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者に個々のサーバーのサイズ制限などのトランスポート受信コネクタ構成の管理を許可する役割に関連付けられています。</p></td>
<td><p>サーバー</p></td>
</tr>
<tr class="odd">
<td><p><code>RecipientPolicies</code></p></td>
<td><p><a href="recipient-policies-role-exchange-2013-help.md">&quot;Recipient Policies/受信者ポリシー&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内のプロビジョニング ポリシーやモバイル デバイス ポリシーなどの受信者ポリシーを管理できるようになる役割に関連付けられます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>RemoteAndAcceptedDomains</code></p></td>
<td><p><a href="remote-and-accepted-domains-role-exchange-2013-help.md">&quot;Remote and Accepted Domains/リモートおよび承認済みドメイン&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内のリモートおよび承認済みドメインを管理できるようになる役割に関連付けられます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>ResetPassword</code></p></td>
<td><p><a href="reset-password-role-exchange-2013-help.md">&quot;Reset Password/パスワードのリセット&quot; 役割</a></p></td>
<td><p>この役割の種類は、ユーザーが自分のパスワードをリセットできるようになり、管理者が組織内のユーザーのパスワードをリセットできるようになる役割に関連付けられます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>RetentionManagement</code></p></td>
<td><p><a href="retention-management-role-exchange-2013-help.md">&quot;Retention Management/保有管理&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内のアイテム保持ポリシーを管理できるようになる役割に関連付けられます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>RoleManagement</code></p></td>
<td><p><a href="role-management-role-exchange-2013-help.md">&quot;Role Management/役割管理&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内の管理役割グループ、役割割り当てポリシー、管理役割、役割エントリ、割り当て、およびスコープを管理できるようになる役割に関連付けられます。</p>
<p>この役割の種類に関連付けられている役割を割り当てられたユーザーは、プロパティ<strong>role group managed by</strong>の上書き、任意の役割グループの構成、任意の役割グループに対するメンバーの追加または削除を実行できます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>SecurityGroupCreationAndMembership</code></p></td>
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">&quot;Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内の USG とそのメンバーシップを作成および管理できるようになる役割に関連付けられます。</p>
<p>組織が分割アクセス許可モデルを維持していて、Exchange サーバーを管理するグループと USG の作成と管理を実行するグループが異なる場合は、この役割の種類に関連付けられている役割を対象のグループに割り当ててください。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>SendConnectors</code></p></td>
<td><p><a href="send-connectors-role-exchange-2013-help.md">&quot;Send Connectors/送信コネクタ&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内のトランスポート送信コネクタを管理できるようになる役割に関連付けられます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>SupportDiagnostics</code></p></td>
<td><p><a href="support-diagnostics-role-exchange-2013-help.md">&quot;Support Diagnostics/サポート診断&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内でプロダクト サポートの契約先の指示に従って高度な診断を実行できるようになる役割に関連付けられます。</p>

> [!NOTE]
> この役割の種類に関連付けられている役割は、マイクロソフト カスタマー サービスとサポートから指示があった場合のみ使用するコマンドレットとスクリプトへのアクセス許可を与えます。


</td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>TeamMailboxes</code></p></td>
<td><p><a href="team-mailboxes-role-exchange-2013-help.md">&quot;Team Mailboxes/チーム メールボックス&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内の 1 つ以上のサイト メールボックスのプロビジョニング ポリシーを定義し、サイト メールボックスを管理できるようになる役割に関連付けられます。この役割の種類に関連付けられた役割が割り当てられた管理者は、所有していないサイト メールボックスを管理できます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>TeamMailboxLifecycleApplication</code></p></td>
<td><p><a href="teammailboxlifecycleapplication-role-exchange-2013-help.md">TeamMailboxLifecycleApplication 役割</a></p></td>
<td><p>この役割の種類は、パートナー アプリケーションに組織内のサイト メールボックスのライフサイクル状態の更新を許可する役割に関連付けられています。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>TransportAgents</code></p></td>
<td><p><a href="transport-agents-role-exchange-2013-help.md">&quot;Transport Agents/トランスポート エージェント&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内のトランスポート エージェントを管理できるようになる役割に関連付けられます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>TransportHygiene</code></p></td>
<td><p><a href="transport-hygiene-role-exchange-2013-help.md">&quot;Transport Hygiene/トランスポート検疫&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内のスパム対策およびマルウェア対策の機能を管理できるようになる役割に関連付けられます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>TransportQueues</code></p></td>
<td><p><a href="transport-queues-role-exchange-2013-help.md">&quot;Transport Queues/トランスポート キュー&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が個々のサーバーのトランスポート キューを管理できるようになる役割に関連付けられます。</p></td>
<td><p>サーバー</p></td>
</tr>
<tr class="even">
<td><p><code>TransportRules</code></p></td>
<td><p><a href="transport-rules-role-exchange-2013-help.md">&quot;Transport Rules/トランスポート ルール&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内のトランスポート ルールを管理できるようになる役割に関連付けられます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>UMMailboxes</code></p></td>
<td><p><a href="um-mailboxes-role-exchange-2013-help.md">&quot;UM Mailboxes/UM メールボックス&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内のメールボックスおよびその他の受信者のユニファイド メッセージング (UM) 構成を管理できるようになる役割に関連付けられます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>UMPrompts</code></p></td>
<td><p><a href="um-prompts-role-exchange-2013-help.md">&quot;UM Prompts/UM プロンプト&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内のカスタムの UM 音声プロンプトを作成および管理できるようになる役割に関連付けられます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>UnifiedMessaging</code></p></td>
<td><p><a href="unified-messaging-role-exchange-2013-help.md">ユニファイド メッセージングの役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内のユニファイド メッセージング サービスを管理できるようになる役割に関連付けられます。</p>
<p>この役割では、UM 固有のメールボックスの構成や、UM プロンプトの管理を実行することはできません。UM 固有のメールボックスの構成を管理するには、<code>UMMailboxes</code> の役割の種類に関連付けられている役割を使用します。UM プロンプトを管理するには、<code>UMPrompts</code> 役割の種類に関連付けられている役割を使用します。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>UnScopedRoleManagement</code></p></td>
<td><p><a href="unscoped-role-management-role-exchange-2013-help.md">&quot;Unscoped Role Management/スコープ外役割管理&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者に組織内のスコープ外の最上位レベルの管理役割の作成および管理を許可する役割に関連付けられています。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>UserOptions</code></p></td>
<td><p><a href="user-options-role-exchange-2013-help.md">&quot;User Options/ユーザー オプション&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者に組織内のユーザーの Outlook Web App オプションの表示を許可する役割に関連付けられています。この役割の種類に関連付けられた役割を使用すると、ユーザー構成の問題を容易に診断できます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>UserApplication</code></p></td>
<td><p><a href="userapplication-role-exchange-2013-help.md">UserApplication 役割</a></p></td>
<td><p>この役割の種類は、パートナー アプリケーションに組織内のエンド ユーザーの代わりに作業の実行を許可する役割に関連付けられています。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>ViewOnlyAuditLogs</code></p></td>
<td><p><a href="view-only-audit-logs-role-exchange-2013-help.md">&quot;View-Only Audit Logs/表示専用監査ログ&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者に組織内の監査ログの検索を許可する役割に関連付けられています。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>ViewOnlyConfiguration</code></p></td>
<td><p><a href="view-only-configuration-role-exchange-2013-help.md">&quot;View-Only Configuration/表示専用構成&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内の受信者以外の Exchange 構成設定すべてを表示できるようになる役割に関連付けられます。表示可能な構成の例として、サーバー構成、トランスポート構成、データベース構成、および組織全体にわたる構成があります。</p>
<p>この役割の種類に関連付けられている役割は、<code>ViewOnlyRecipients</code> の役割の種類に関連付けられている役割と組み合わせて、組織内のすべてのオブジェクトを表示できる役割を作成できます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>ViewOnlyRecipients</code></p></td>
<td><p><a href="view-only-recipients-role-exchange-2013-help.md">&quot;View-Only Recipients/表示専用受信者&quot; 役割</a></p></td>
<td><p>この役割の種類は、管理者がメールボックス、メール ユーザー、メール連絡先、配布グループ、および動的配布グループなどの受信者の構成を表示できるようになる役割に関連付けられます。</p>
<p>この役割の種類に関連付けられている役割は、<code>ViewOnlyConfiguration</code> 役割の種類に関連付けられている役割と組み合わせて、組織内のすべてのオブジェクトを表示できる役割を作成できます。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>WorkloadManagement</code></p></td>
<td><p><a href="workloadmanagement-role-exchange-2013-help.md">WorkloadManagement 役割</a></p></td>
<td><p>この役割の種類は、管理者が組織内のワークロード管理ポリシーを管理できるようになる役割に関連付けられます。管理者は、リソース正常性の定義、ワークロードの分類、ワークロード管理の有効化や無効化を構成できます。</p></td>
<td><p>組織</p></td>
</tr>
</tbody>
</table>


次の表は、Exchange 2013 のすべてのユーザーフォーカス管理の役割の種類、およびそれに関連する組み込みの管理役割の一覧です。

**ユーザーフォーカスの役割の種類**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>管理の役割の種類</th>
<th>組み込みのユーザーフォーカスの役割</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>MyBaseOptions</code></p></td>
<td><p><a href="mybaseoptions-role-exchange-2013-help.md">MyBaseOptions 役割</a></p></td>
<td><p>この役割の種類は、個々のユーザーが自分のメールボックスおよび関連する設定の基本構成を表示および変更できるようになる役割に関連付けられます。</p></td>
</tr>
<tr class="even">
<td><p><code>MyContactInformation</code></p></td>
<td><p><a href="myaddressinformation-role-exchange-2013-help.md">MyAddressInformation 役割</a></p>
<p><a href="mycontactinformation-role-exchange-2013-help.md">MyContactInformation 役割</a></p>
<p><a href="mymobileinformation-role-exchange-2013-help.md">MyMobileInformation 役割</a></p>
<p><a href="mypersonalinformation-role-exchange-2013-help.md">MyPersonalInformation 役割</a></p></td>
<td><p>この役割の種類は、個々のユーザーが自分の連絡先情報を変更できるようになる役割に関連付けられます。この情報には、各自のアドレスと電話番号が含まれています。</p></td>
</tr>
<tr class="odd">
<td><p>MyCustomApps</p></td>
<td><p><a href="my-custom-apps-role-exchange-2013-help.md">&quot;My Custom Apps/自分のカスタム アプリ&quot; 役割</a></p></td>
<td><p>この役割の種類は、個々のユーザーが自分のカスタム アプリケーションを表示および変更できるようになる役割に関連付けられます。</p></td>
</tr>
<tr class="even">
<td><p>MyDiagnostics</p></td>
<td><p><a href="mydiagnostics-role-exchange-2013-help.md">MyDiagnostics 役割</a></p></td>
<td><p>この役割の種類は、個人ユーザーがメールボックスに対して、予定表の診断情報の取得など、基本的な診断を実行できるようにする役割と関連付けられています。</p></td>
</tr>
<tr class="odd">
<td><p><code>MyDistributionGroupMembership</code></p></td>
<td><p><a href="mydistributiongroupmembership-role-exchange-2013-help.md">MyDistributionGroupMembership 役割</a></p></td>
<td><p>この役割の種類は、組織内の配布グループがグループのメンバーシップの操作を許可されている場合、個々のユーザーが組織内の配布グループのユーザーのメンバーシップを表示および変更できるようになる役割に関連付けられます。</p></td>
</tr>
<tr class="even">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><a href="mydistributiongroups-role-exchange-2013-help.md">MyDistributionGroups 役割</a></p></td>
<td><p>この役割の種類は、個々のユーザーが配布グループの作成、変更、表示を実行すること、および個々のユーザーが所有する配布グループのメンバーの変更、表示、削除、追加を実行できるようになる役割に関連付けられます。</p></td>
</tr>
<tr class="odd">
<td><p><code>MyProfileInformation</code></p></td>
<td><p><a href="mydisplayname-role-exchange-2013-help.md">MyDisplayName 役割</a></p>
<p><a href="myname-role-exchange-2013-help.md">MyName 役割</a></p>
<p><a href="myprofileinformation-role-exchange-2013-help.md">MyProfileInformation 役割</a></p></td>
<td><p>この役割の種類は、個々のユーザーが自分の名前を変更できるようになる役割に関連付けられます。</p></td>
</tr>
<tr class="even">
<td><p>MyMarketplaceApps</p></td>
<td><p><a href="my-marketplace-apps-role-exchange-2013-help.md">&quot;My Marketplace Apps/マイ マーケットプレイス アプリ&quot; 役割</a></p></td>
<td><p>この役割の種類は、個々のユーザーが自分のマーケットプレース アプリケーションを表示および変更できるようになる役割に関連付けられます。</p></td>
</tr>
<tr class="odd">
<td><p><code>MyRetentionPolicies</code></p></td>
<td><p><a href="myretentionpolicies-role-exchange-2013-help.md">MyRetentionPolicies 役割</a></p></td>
<td><p>この役割の種類は、個々のユーザーが自分の保持タグの表示、および保持タグの設定と既定値の表示と変更を実行できるようになる役割に関連付けられます。</p></td>
</tr>
<tr class="even">
<td><p>MyTeamMailboxes</p></td>
<td><p><a href="myteammailboxes-role-exchange-2013-help.md">MyTeamMailboxes 役割</a></p></td>
<td><p>この役割の種類は、個々のユーザーがサイト メールボックスを作成し、Microsoft SharePoint サイトに接続できるようになる役割に関連付けられます。</p></td>
</tr>
<tr class="odd">
<td><p><code>MyTextMessaging</code></p></td>
<td><p><a href="mytextmessaging-role-exchange-2013-help.md">MyTextMessaging 役割</a></p></td>
<td><p>この役割の種類は、個々のユーザーが自分のテキスト メッセージング設定の作成、表示、変更を実行できるようになる役割に関連付けられます。</p></td>
</tr>
<tr class="even">
<td><p><code>MyVoiceMail</code></p></td>
<td><p><a href="myvoicemail-role-exchange-2013-help.md">MyVoiceMail 役割</a></p></td>
<td><p>この役割の種類は、個々のユーザーが自分のボイス メール設定を表示および変更できるようになる役割に関連付けられます。</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## 詳細情報

[New-ManagementRole](https://technet.microsoft.com/ja-jp/library/dd298073\(v=exchg.150\))

[New-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335193\(v=exchg.150\))

[Set-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335173\(v=exchg.150\))

[New-ManagementScope](https://technet.microsoft.com/ja-jp/library/dd335137\(v=exchg.150\))

[Set-ManagementScope](https://technet.microsoft.com/ja-jp/library/dd297996\(v=exchg.150\))

[New-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335193\(v=exchg.150\))

[Set-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335173\(v=exchg.150\))

