---
title: 'インターネット予定表の公開を無効にする: Exchange 2013 Help'
TOCTitle: インターネット予定表の公開を無効にする
ms:assetid: f26dbf04-9dae-460f-a987-2ad3dfbc7b7e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ853047(v=EXCHG.150)
ms:contentKeyID: 50555898
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# インターネット予定表の公開を無効にする

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-02-15_

インターネット予定表の公開を無効にする方法は、この公開を有効にした方法に左右されます。インターネット予定表公開に特化した共有ポリシーを作成した場合は、ポリシーを無効にするかまたは完全に削除できます。インターネット予定表公開を既定の共有ポリシー内部の共有ルールとして構成した場合は、<strong>\[匿名\]</strong>ドメインの共有ルールを削除するだけで公開を無効にすることができます。

インターネット予定表の公開を無効にすると、共有ポリシーを使用するよう設定されたユーザーは、ポリシーで指定された<strong>\[匿名\]</strong>インターネット ドメインと予定表の情報を共有できなくなります。ただし、そのポリシーを使用するように設定されているすべてのユーザーがそのユーザーのメールボックスからポリシー設定を削除するまでは、インターネット予定表公開専用の共有ポリシーの削除や無効化は行えません。ユーザーの共有ポリシー設定の変更方法の詳細ついては、「[ユーザー メールボックスの管理](manage-user-mailboxes-exchange-2013-help.md)」を参照してください。


> [!NOTE]
> 共有ポリシーを無効にするか削除しても、そのポリシーを使用するように設定されたユーザーは、共有ポリシー アシスタントが実行されるまでは引き続き情報を共有できます。共有ポリシー アシスタントの実行頻度を指定するには、<A href="https://technet.microsoft.com/ja-jp/library/aa998651(v=exchg.150)">Set-MailboxServer</A> コマンドレットを <EM>SharingPolicySchedule</EM> パラメーターと共に使用します。



インターネット予定表の共有を完全に無効にするには、予定表の公開に使用される Outlook Web App 仮想ディレクトリも無効にする必要があります。これを行うには、過去に Exchange 組織のユーザーによって外部のインターネット ユーザーと共有されていた、公開された予定表のリンクへのアクセスを禁止します。この手順については、後で説明します。

インターネット予定表の公開と共有ポリシーの詳細については、「[共有](sharing-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - このタスクの予想所要時間:15 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md) トピックにおける「予定表と共有のアクセス許可」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 実行方法

## 手順 1:EAC またはシェルを使用して、インターネットの予定表公開のための共有ポリシーを無効にするかまたは削除する

## EAC を使用する

1.  <strong>組織</strong> \> <strong>共有</strong> に移動します。

2.  リストビューの <strong>個別共有</strong> で、次のいずれかの手順を実行します。
    
      - インターネット予定表公開に特化した共有ポリシーを作成した場合は、そのポリシーを選択して、<strong>オン</strong> 列のチェックボックスをオフにして共有ポリシーを無効にするかまたは<strong>\[削除\]</strong>![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") クリックして削除します。
    
      - インターネット予定表公開を既定の共有ポリシー内部の共有ルールとして構成した場合は、次の手順を実行します。
        
        1.  既定の共有ポリシーを選択して、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。
        
        2.  <strong>共有ポリシー</strong> で、<strong>匿名</strong> 共有ルールを選択して、<strong>削除</strong>![\[削除\] アイコン](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[削除] アイコン") をクリックし共有ルールを削除します。
        
        3.  <strong>保存</strong> をクリックします。

## シェルを使用する

この例では、インターネットの予定表公開に特化した共有ポリシー **インターネット**を無効にします。

    Set-SharingPolicy -Identity "Internet" -Enabled $false

この例では、インターネットの予定表公開に特化した共有ポリシー **インターネット**を削除します。

    Remove-SharingPolicy -Identity "Internet"

構文およびパラメーターの詳細については、「[Set-SharingPolicy](https://technet.microsoft.com/ja-jp/library/dd297931\(v=exchg.150\))」を参照してください。

## このステップの検証方法

共有ポリシーが正常に削除または更新されたことを確認するには、次のシェル コマンドを実行して共有ポリシーの情報を確認します。

    Get-SharingPolicy <policy name> | format-list

インターネット予定表公開に特化した共有ポリシーを削除した場合は、コマンドレットの結果にポリシーは表示されません。

既定の共有ポリシーを更新した場合は、*Domains* パラメーターから `Anonymous` ドメインが削除されていることを確認します。

構文およびパラメーターの詳細については、「[Get-SharingPolicy](https://technet.microsoft.com/ja-jp/library/dd335081\(v=exchg.150\))」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 手順 2:シェルを使用して Outlook Web App 仮想ディレクトリの匿名機能を無効にする


> [!NOTE]
> EAC を使用して、Outlook Web App 仮想ディレクトリの匿名機能を無効にすることはできません。



この例では、クライアント アクセス サーバー CAS01 上の Outlook Web App 仮想ディレクトリに対する匿名機能を無効にします。

    Set-OwaVirtualDirectory -Identity "CAS01" - AnonymousFeaturesEnabled -$false

構文およびパラメーターの詳細については、「[Set-OwaVirtualDirectory](https://technet.microsoft.com/ja-jp/library/bb123515\(v=exchg.150\))」を参照してください。

## このステップの検証方法

クライアント アクセス サーバー上で Outlook Web App 仮想ディレクトリの匿名機能を正常に無効にしたことを検証するには、次のシェルコマンドを実行して、*AnonymousFeaturesEnabled* パラメーターが `$false` になっていることを確認します。

    Get-OwaVirtualDirectory | format-list

構文およびパラメーターの詳細については、「[Get-OwaVirtualDirectory](https://technet.microsoft.com/ja-jp/library/aa998588\(v=exchg.150\))」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。


