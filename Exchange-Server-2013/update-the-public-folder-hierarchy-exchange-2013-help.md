---
title: 'パブリック フォルダーの階層の更新: Exchange Online Help'
TOCTitle: パブリック フォルダーの階層の更新
ms:assetid: a7b2fb51-0207-4d7d-938d-466ae110bb90
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ945055(v=EXCHG.150)
ms:contentKeyID: 52057485
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# パブリック フォルダーの階層の更新

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

階層シンクロナイザーおよびメールボックス アシスタントを手動で実行する場合にのみ、パブリック フォルダーの階層を更新する必要があります。これらは両方とも、組織のパブリック フォルダー メールボックスのそれぞれにおいて少なくとも 24 時間に 1 回実行されます。階層シンクロナイザーは、Microsoft Outlook または Microsoft Exchange Web Services クライアントを通してユーザーがセカンダリ メールボックスにログオンしている場合に、15 分おきに実行されます。

Exchange Online のパブリック フォルダーに関するその他の管理タスクについては、「[Office 365 と Exchange Online のパブリック フォルダーの手順](https://technet.microsoft.com/ja-jp/library/jj966272\(v=exchg.150\))」を参照してください。

Exchange Server 2013 のパブリック フォルダーに関するその他の管理タスクについては、「[パブリック フォルダーの手順](public-folder-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[共有とコラボレーションのアクセス許可](sharing-and-collaboration-permissions-exchange-2013-help.md)」の「パブリック フォルダー」。

  - EAC でこのプロシージャは実行できません。シェルを使用する必要があります。

  - *InvokeSynchronizer* パラメーターでこのコマンドを実行する場合は、*SuppressStatus* パラメーターを使用することをお勧めします。このコマンドでこのパラメーターを使用しない場合、最大 1 分間にわたり 3 秒ごとに状態メッセージが出力されます。1 分が経過するまで、そのシェルのインスタンスは使用できません。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## パブリック フォルダーの階層の更新

この例ではパブリック フォルダー メールボックス PF\_marketing でパブリック フォルダー階層を更新し、コマンドの出力を抑制します。

    Update-PublicFolderMailbox -Identity PF_marketing -InvokeSynchronizer -SuppressStatus

この例では、すべてのパブリック フォルダー メールボックスを更新し、コマンドの出力を非表示にしています。

    Get-Mailbox -PublicFolder | Update-PublicFolderMailbox InvokeSynchronizer -SuppressStatus

