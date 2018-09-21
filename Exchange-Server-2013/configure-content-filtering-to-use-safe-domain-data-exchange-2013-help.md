---
title: '安全なドメイン データを使用するようにコンテンツ フィルタリングを構成する: Exchange 2013 Help'
TOCTitle: 安全なドメイン データを使用するようにコンテンツ フィルタリングを構成する
ms:assetid: 1ee2b663-b4f3-4fef-8954-986f2d820924
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn467930(v=EXCHG.150)
ms:contentKeyID: 59634976
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 安全なドメイン データを使用するようにコンテンツ フィルタリングを構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-12-16_

安全なドメイン データは、ユーザーの差出人セーフ リストに保存されているドメイン全体 (たとえば、@contoso.com) です。既定では、コンテンツ フィルター エージェントが安全なドメイン データを使用して、コンテンツ フィルタリングを回避することが許可されている差出人を識別することはありません。

この既定の設定は、組織に送信されるスパムの量を減らすために役立ちます。たとえば、ユーザーが差出人セーフ リストに、ある大規模メール プロバイダーのドメインを追加したとします。このドメインがスパム送信者によって頻繁に使用またはスプーフィングされており、かつコンテンツ フィルタリングが安全なドメイン データを使用してメッセージは安全であるとのマーク付けを行うように構成されている場合は、そのドメイン内のすべての差出人からのメッセージが組織内の受信者に送信されます。

ほとんどの場合、既定の設定を変更しないことをお勧めします。ただし、ユーザーの安全なドメイン データを Active Directory に保管し、安全であるとのマークをメッセージに付けるためにコンテンツ フィルタリングがこれを使用するように構成できます。これを行うには、このトピックで後に詳しく説明されているように、Microsoft Exchange Mailbox Assistants サービスに関連付けられた MSExchangeMailboxAssistants.exe.config XML アプリケーション構成ファイルを変更する必要があります。この構成を変更すると、安全なドメイン データはハッシュされて、Active Directory 内の各ユーザーの **msExchSafeSenderHash** ユーザー オブジェクト属性に、セーフ リスト集約の一部として保管されます。その後、コンテンツ フィルター エージェントは安全なドメイン データを使用して、それらのドメイン内の差出人によるメッセージを安全であるとマーク付けすることができます。セーフ リスト集約について詳しくは、「[セーフリスト集約機能](safelist-aggregation-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 10 分

  - Exchange のアクセス許可は、このトピックの手順には適用されません。これらの手順は、Exchange Server のオペレーティング システムで実行されます。

  - MSExchangeMailboxAssistants.exe.config ファイルに保存した変更は、Microsoft Exchange メールボックス アシスタント サービスを再起動した後に適用されます。

  - Exchange XML アプリケーション構成ファイルで行うカスタマイズ済みのサーバーごとの設定 (クライアント アクセス サーバーの web.config ファイルまたはメールボックス サーバーの EdgeTransport.exe.config ファイルなど) は、Exchange 累積更新プログラム (CU) のインストール時に上書きされます。インストール後にサーバーを簡単に再構成できるよう、必ずこの情報を保存しておいてください。これらの設定は、Exchange 累積更新プログラムのインストール後に構成し直す必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## コマンド プロンプトを使用して、コンテンツ フィルタリングで安全なドメイン データが使用されるように構成する

1.  コマンド プロンプト ウィンドウで、次のコマンドを実行して、MSExchangeMailboxAssistants.exe.config ファイルをメモ帳で開きます。
    
    ```powershell
Notepad %ExchangeInstallPath%Bin\MSExchangeMailboxAssistants.exe.config
```

2.  ファイルの終わりにある *\</appsettings\>* キーを探して、次のキーを *\</appsettings\>* キーの前に貼り付けます。
    
    ```command line
<add key="IncludeSafeDomains" value="true" />
```

3.  完了したら、MSExchangeMailboxAssistants.exe.config ファイルを保存して閉じます。

4.  次のコマンドを実行して、Microsoft Exchange Mailbox Assistants サービスを再起動します。
    
        net stop MSExchangeMailboxAssistants && net start MSExchangeMailboxAssistants

## 正常な動作を確認する方法

コンテンツ フィルタリングの構成が成功し、安全なドメイン データが使用されるようになったことを確認するには、以下を行います。

1.  Outlook の差出人セーフ リストにドメインを追加すると、Active Directory 内のユーザーの **msExchSafeSenderHash** 属性が更新されることを確認します。これを行うには、ADSIEdit.exe または LDP.exe で属性を表示して、Outlook 内のユーザーのメールボックスを開き、差出人セーフ リストにドメインを追加して、コマンド `Update-Safelist <username>` を実行してから、**msExchSafeSenderHash** の元の値と現在の値とが異なっていることを確認します。

2.  安全なドメイン データが Active Directory に保管されたことを確認した後で、そのドメイン内の外部差出人から組織内のユーザーにテスト メッセージを送信します。メッセージ ヘッダーのスパム対策のヘッダ ・ フィールドを調べて、メッセージが安全であるとマーク付けされていることを確認します。

