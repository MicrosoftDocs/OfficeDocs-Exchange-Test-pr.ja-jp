---
title: 'Re-create the Discovery system mailbox: Exchange 2013 Help'
TOCTitle: Re-create the Discovery system mailbox
ms:assetid: 5ae8426b-5661-4ecb-99c4-cdd342107fb1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg588318(v=EXCHG.150)
ms:contentKeyID: 49896267
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Re-create the Discovery system mailbox

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2018-01-17_

インプレース電子情報開示は、システム メールボックスを使用して、インプレース電子情報開示の検索メタデータを格納します。この探索システム メールボックスには、表示名 **SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}** があります。システム メールボックスは、Exchange 管理センター (EAC) または Exchange アドレス一覧には表示されないので、誤って削除してしまうことはほとんどありません。

ただし、探索システム メールボックスが誤って削除されると、探索マネージャーはインプレース電子情報開示検索の実行または既存の検索の管理を実行できなくなります。この場合、電子情報開示機能を有効にするには、探索システム メールボックスを再作成する必要があります。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 10 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「受信者プロビジョニングのアクセス許可」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

## シェルを使用して探索システム メールボックスを再作成する

1.  SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9} ユーザー アカウントが存在する場合は、Active Directory から削除します。既定では、Exchange Server 2013 セットアップによって Active Directory の \[Users\] コンテナーにメールボックスが作成されます。Active Directory からユーザー アカウントを削除する方法の詳細については、「[ユーザー アカウントを削除する](https://go.microsoft.com/fwlink/p/?linkid=215850)」を参照してください。

2.  シェルを使用して探索システム メールボックスを有効にする。
    

    > [!NOTE]
    > EAC を使用して、探索システム メールボックスを有効にすることはできません。<BR>次のコマンドは、Exchange のインストール メディアを展開した同じディレクトリから実行する必要があります。

    
    検出システム メールボックスを再作成するには、次のコマンドを実行します。
    
    ```powershell
.\Setup /preparead /IAcceptExchangeServerLicenseTerms
```

## 設定が適用されたことを確認する方法

探索システム メールボックスが正常に再作成されたことを確認するには、**Get-Mailbox** コマンドレットを *Arbitration* スイッチで使用してシステム メールボックスを取得します。コマンドの結果を表示して、システム メールボックス `SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}` が再作成されたことを確認します。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。


