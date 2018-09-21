---
title: 'UM 言語パックの削除: Exchange 2013 Help'
TOCTitle: UM 言語パックの削除
ms:assetid: a2bc2753-2c25-4ea0-a9d5-e3d42a699c6c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124004(v=EXCHG.150)
ms:contentKeyID: 49896392
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM 言語パックの削除

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2013-02-14_

EAC またはシェルを使用して、Microsoft Exchange ユニファイド メッセージング サービスを実行するメールボックス サーバー上のユニファイド メッセージング (UM) の言語を管理できます。ただし、UM ダイヤル プランの一覧から言語を削除するには、**Setup.exe /RemoveUmLanguagePack** コマンドを使用して、メールボックス サーバーから適切な UM 言語パックを削除する必要があります。メールボックス サーバーから UM 言語パックを削除すると、UM ダイヤル プランまたは UM 自動応答を構成するときにその言語は表示されなくなります。インストールされている UM 言語パックを確認するには、メールボックス サーバーのプロパティを表示するか、**Get-UMService** コマンドレットを使用します。

UM 言語に関連する追加のタスクについては、「[UM 言語、プロンプト、および案内応答の手順](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「メールボックス サーバー (UM サービス)」。

  - en-US 以外の UM 言語パックがインストールされていることを確認します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## Setup.exe を使用して UM 言語パックを削除する

コマンド プロンプトで、次のコマンドを実行します。

```powershell
Setup.exe /RemoveUmLanguagePack:<UmLanguagePackName>
```

このコマンドで、*\<UmLanguagePackName\>* は、たとえば fr-FR のように、UM 言語パックの名前です。


> [!NOTE]
> 更新プログラムをインストールした後は、UM 言語パックを削除する目的で \Bin フォルダーにある Setup.exe ファイルを使用することはできません。Exchange 2013 DVD またはダウンロードしたソース ファイルにある Setup.exe ファイルを使用する必要があります。それ以外の場合は、次のエラーが表示されます。"これは、実行中のアプリケーションとインストールされたアプリケーションのバージョンが異なることを示しています。"


