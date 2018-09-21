---
title: '複製構成を使用してエッジ トランスポート サーバーを構成する: Exchange 2013 Help'
TOCTitle: 複製構成を使用してエッジ トランスポート サーバーを構成する
ms:assetid: 0bbc83e3-e5e8-4480-a8a6-15f035360856
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa996008(v=EXCHG.150)
ms:contentKeyID: 61180550
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 複製構成を使用してエッジ トランスポート サーバーを構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-13_

付属の Exchange 管理シェル スクリプト (%ExchangeInstallPath%Scripts に配置) を使用すれば、エッジ トランスポート サーバーの構成を複製することができます。この手順は、*複製構成*と呼ばれます。*複製構成*とは、以前に構成された移動元のサーバーの構成情報に基づいて新しいエッジ トランスポート サーバーを展開する方法です。以前に構成された移動元のサーバーの構成情報がコピーされ、XML ファイルにエクスポートされた後で、移動先のサーバーにインポートされます。このプロセスの概要については、「[エッジ トランスポート サーバーの複製構成](edge-transport-server-cloned-configuration-exchange-2013-help.md)」を参照してください。

エッジ トランスポート サーバーの構成情報は、Active Directory ライトウェイト ディレクトリ サービス (AD LDS) に保存され、複数のエッジ トランスポート サーバー間でレプリケートされません。複製構成を使用すれば、境界ネットワーク内に展開されたすべてのエッジ トランスポート サーバーが確実に同じ構成を使用するようにできます。

複製構成タスクを実行するために 2 つのシェル スクリプトが使用されます。

  - **ExportEdgeConfig.ps1**   ユーザーが構成したすべての設定とデータをエッジ トランスポート サーバーからエクスポートして、XML ファイルに保存します。

  - **ImportEdgeConfig.ps1**   構成の検証の段階で、ImportEdgeConfig.ps1 スクリプトがエクスポートした XML ファイルをチェックして、サーバー固有のエクスポート設定が移動先のサーバーに対して有効かどうかを確認します。設定を変更する必要がある場合は、このスクリプトによって、無効な設定が応答ファイルに書き込まれます。このファイルを変更して、構成のインポートの段階で使用される移動先のサーバー情報を指定します。構成のインポートの段階で、このスクリプトは、ExportEdgeConfig.ps1 スクリプトによって作成された中間の XML ファイルに保存されているユーザーが構成したすべての設定とデータをインポートします。

これらのスクリプトはどちらも、%ExchangeInstallPath%Script フォルダーに配置されています。

## 開始する前に

  - このタスクの予想所要時間:30 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「エッジ トランスポート サーバー」。

  - 複製構成は、サーバーのエッジ サブスクリプション設定を複製しません。EdgeSync 証明書は複製されません。エッジ トランスポート サーバーごとに、EdgeSync プロセスを別々に実行する必要があります。EdgeSync は、複製構成情報と EdgeSync レプリケーション情報の両方に含まれている設定をすべて上書きします。

  - いずれかの送信コネクタが資格情報を使用するように構成されている場合、パスワードは、暗号化された文字列として中間 XML ファイルに書き込まれます。ImportEdgeConfig.ps1 および ExportEdgeConfig.ps1 スクリプトで *-key* パラメーターを使用して、パスワードの暗号化と解読に使用する 32 バイト文字列を指定することができます。*-key* パラメーターを使用しない場合は、既定の暗号化キーが使用されます。

  - この手順を実行するには、シェルを使用する必要があります。オンプレミスの Exchange 組織で Exchange 管理シェル を開く方法については、「[シェルを開く](https://technet.microsoft.com/ja-jp/library/dd638134\(v=exchg.150\))」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 実行方法

## 手順 1:移動元のサーバーの構成データを移動元のサーバー上のファイルにエクスポートする

1.  ExportEdgeConfig.ps1 スクリプトを、移動元のサーバー上のユーザー プロファイルのルート フォルダーにコピーします。

2.  移動元のサーバーの構成データを移動元のサーバー上のファイルにエクスポートするには、次の構文を使用します。
    
    ```powershell
./ExportEdgeConfig.ps1 -CloneConfigData:"<configuration file>"
```
    
    たとえば、移動元のサーバーの構成データを C:\\CloneConfigData.xml ファイルにエクスポートするには、次のコマンドを実行します。
    
    ```powershell
./ExportEdgeConfig.ps1 -CloneConfigData:"C:\CloneConfigData.xml"
```

## このステップの検証方法

「エッジ構成データが \<出力ファイル パス\> に正常にエクスポートされました」という確認メッセージが表示されたら、移動元の構成データが正常にファイルにエクスポートされています。

## 手順 2:移動先のサーバー上で構成ファイルを検証して応答ファイルを作成する

1.  前の手順でエクスポートした移動元のサーバーの構成ファイルを移動先のエッジ トランスポート サーバーにコピーします。

2.  ImportEdgeConfig.ps1 スクリプトを、移動先のサーバーのユーザー プロファイルのルート フォルダーにコピーします。

3.  移動先のサーバー上で構成ファイルを検証してその結果を使用して応答ファイルを作成するには、次の構文を使用します。
    
        ./ImportEdgeConfig.ps1 -CloneConfigData:"<configuration file>" -IsImport $false -CloneConfigAnswer:"<answer file>"
    
    たとえば、C:\\CloneConfigData.xml という構成ファイルを検証して、C:\\CloneConfigAnswer.xml という応答ファイルを作成するには、次のコマンドを実行します。
    
        ./ImportEdgeConfig.ps1 -CloneConfigData:"C:\CloneConfigData.xml" -IsImport $false -CloneConfigAnswer:"C:\CloneConfigAnswer.xml"

4.  応答ファイルを開き、移動先のサーバーで無効な設定をすべて変更します。変更が必要ない場合は、応答ファイルにエントリは存在しません。変更を保存します。

## このステップの検証方法

「応答ファイルが正常に作成されました」という確認メッセージが表示されたら、構成ファイルの検証と応答ファイルの作成が正常に終了しています。

## 手順 3: 移動先のサーバー上で構成ファイルをインポートする

移動先のサーバー上で構成ファイルをインポートするには、次の構文を使用します。

    ./ImportEdgeConfig.ps1 -CloneConfigData:"<Configuration file>" -IsImport $true -CloneConfigAnswer:"<answer file>"

たとえば、C:\\CloneConfigAnswer.xml という応答ファイルを使用して C:\\CloneConfigData.xml という構成ファイルをインポートするには、次のコマンドを実行します。

    ./ImportEdgeConfig.ps1 -CloneConfigData:"C:\CloneConfigData.xml" -IsImport $true -CloneConfigAnswer:"C:\CloneConfigAnswer.xml"

## このステップの検証方法

「エッジ構成情報のインポートが成功しました」という確認メッセージが表示されたら、移動先のサーバー上で構成ファイルが正常にインポートされています。

