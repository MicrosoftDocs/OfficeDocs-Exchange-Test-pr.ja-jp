---
title: 'エンジンおよび定義の更新プログラムのダウンロード: Exchange 2013 Help'
TOCTitle: エンジンおよび定義の更新プログラムのダウンロード
ms:assetid: 8f2ca383-e463-4df0-aa5d-29afe2f81aaf
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657471(v=EXCHG.150)
ms:contentKeyID: 49896363
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# エンジンおよび定義の更新プログラムのダウンロード

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-08_

Microsoft Exchange Server 2013 の管理者は、マルウェア対策エンジンと定義 (署名) の更新を手動でダウンロードできます。Exchange サーバーでは、運用前にエンジンと定義の更新をダウンロードすることを強くお勧めします。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分

  - 更新をダウンロードするには、コンピューターでインターネットに接続し、TCP ポート 80 (HTTP) で接続を確立できるようにする必要があります。

  - UNRESOLVED\_TOKEN\_VAL(PD\_Shell\_Only\_Procedure)

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[スパム対策とマルウェア対策のアクセス許可](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)」の「マルウェア対策」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用して手動でエンジンと定義の更新をダウンロードする

エンジンと定義の更新をダウンロードするには、次のコマンドを実行します。

    & $env:ExchangeInstallPath\Scripts\Update-MalwareFilteringServer.ps1 -Identity <FQDN of server>

この例では、mailbox01.contoso.com という名前のサーバーにエンジンと定義の更新を手動でダウンロードします。

    & $env:ExchangeInstallPath\Scripts\Update-MalwareFilteringServer.ps1 -Identity mailbox01.contoso.com

必要に応じて、既定値の「http://forefrontdl.microsoft.com/server/scanengineupdate」以外から更新をダウンロードするための「–EngineUpdatePath」パラメーターを指定できます。HTTP アドレスまたは UNC パスを使用できます。後者の場合は、パスにアクセスできるネットワーク サービスが必要です。次の使用例は、mailbox01.contoso.com という名前のサーバー上にローカル ディレクトリからエンジンおよび定義の更新プログラムを手動でダウンロードします。

    & $env:ExchangeInstallPath\Scripts\Update-MalwareFilteringServer.ps1 -Identity mailbox01.contoso.com -EngineUpdatePath \\Server\sharename

## 正常な動作を確認する方法

更新が正常にダウンロードされたことを確認するには、イベント ビューアーにアクセスしてイベント ログを表示する必要があります。次の手順で説明されているように、FIPFS イベントのみをフィルター処理することをお勧めします。

1.  **\[スタート\]** メニューから、**\[すべてのプログラム\]** \> **\[管理ツール\]** \> **\[イベント ビューアー\]** をクリックします。

2.  イベント ビューアーで、**Windows ログ** フォルダーを展開し、**\[アプリケーション\]** をクリックします。

3.  **\[操作\]** メニューの **\[現在のログをフィルター\]** をクリックします。

4.  **\[現在のログをフィルター\]** ダイアログ ボックスの **\[イベント ソース\]** ドロップダウン リストから **\[FIPFS\]** チェック ボックスをオンにし、**\[OK\]** をクリックします。

エンジンの更新が正常にダウンロードされると、次のメッセージと同様の内容を示すイベント ID 6033 が表示されます。

`MS Filtering Engine Update process performed a successful scan engine update.`

`Scan Engine: Microsoft`

`Update Path: http://forefrontdl.microsoft.com/server/scanengineupdate`

`Last Update time: ‎2012‎-‎08‎-‎16T13:22:17.000Z`

`Engine Version: 1.1.8601.0`

`Signature Version: 1.131.2169.0`

## 詳細情報

[マルウェア対策ポリシーを構成する](configure-anti-malware-policies-exchange-2013-help.md)

