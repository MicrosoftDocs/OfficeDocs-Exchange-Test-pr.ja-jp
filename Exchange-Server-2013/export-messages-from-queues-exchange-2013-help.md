---
title: 'キューからメッセージをエクスポートする: Exchange 2013 Help'
TOCTitle: キューからメッセージをエクスポートする
ms:assetid: 688b342c-f380-4fe0-afce-7e38cf490627
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998625(v=EXCHG.150)
ms:contentKeyID: 51407540
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# キューからメッセージをエクスポートする

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-05-05_

キューからファイルにメッセージをエクスポートしても、このメッセージはキューから削除されません。メッセージのコピーは、指定した場所にテキスト ファイルとして作成されます。作成されたファイルは、テキスト エディターや電子メール クライアント アプリケーションなどのアプリケーションで表示できます。また、Exchange 組織内外にあるその他の任意のメールボックス サーバーまたはエッジ トランスポート サーバー上で、再生ディレクトリを使用することにより、メッセージ ファイルを再送信できます。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「キュー」。

  - エクスポート処理を正しく行うためには、メッセージが中断の状態になっている必要があります。配信キュー、到達不能キュー、または有害メッセージ キューからメッセージをエクスポートできます。有害メッセージ キューに置かれたメッセージは、既に中断状態になっています。発信キュー内のメッセージを中断またはエクスポートすることはできません。

  - Exchange ツールボックスのキュー ビューアーを使用して、メッセージをエクスポートすることはできません。ただし、シェルを使用してそれらをエクスポートする前にメッセージを検索、識別、および中断する場合は、キュー ビューアーを使うと便利です。

  - メッセージ ファイルの送信先ディレクトリの場所に関する以下の情報を確認します。
    
      - メッセージをエクスポートする前に、エクスポート先のディレクトリが存在している必要があります。ディレクトリは自動的には作成されません。絶対パスが指定されていない場合は、現在の Exchange 管理シェルの作業ディレクトリが使用されます。
    
      - 指定するパスは、Exchange サーバー上のローカル パスでも、リモート サーバー上で共有する汎用名前付け規則 (UNC) パスでもかまいません。
    
      - アカウントに対象のディレクトリへの**Write**アクセス許可が与えられている必要があります。
    
      - エクスポートされたメッセージのファイル名を指定する場合は、ファイルを電子メール アプリケーションで簡単に開くことができるか、または再生ディレクトリで正しく処理できるよう、ファイル名拡張子の .eml が含まれていることを確認してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用して、特定のキューから特定のメッセージをエクスポートする

特定のキューから特定のメッセージをエクスポートするには、次のコマンドを実行します。

    Export-Message -Identity <MessageIdentity> | AssembleMessage -Path <FilePath>\<FileName>.eml

この例では、Mailbox01 というサーバー上の contoso.com 配信キューにある **InternalMessageID** 値が 1234 のメッセージのコピーを、D:\\Contoso Export パスにある export.eml というファイルにエクスポートします。

    Export-Message -Identity Exchange01\Contoso.com\1234 | AssembleMessage -Path "D:\Contoso Export\export.eml"

## シェルを使用して、特定のキューからすべてのメッセージをエクスポートする

特定のキューからすべてのメッセージをエクスポートして、各メッセージの **InternetMessageID** 値をファイル名として使用するには、次の構文を使用します。

    Get-Message -Queue <QueueIdentity> | ForEach-Object {$Temp=<Path>+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

**InternetMessageID** 値には角括弧 (\> および \<) が含まれることに注意してください。この記号はファイル名に使用できないため、削除する必要があります。

この例では、Mailbox01 というサーバー上の contoso.com 配信キューからすべてのメッセージのコピーを、D:\\Contoso Export というローカル ディレクトリにエクスポートします。

    Get-Message -Queue Mailbox01\Contoso.com | ForEach-Object {$Temp="D:\Contoso Export\"+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

## シェルを使用して、サーバー上にあるすべてのキューから特定のメッセージをエクスポートする

サーバー上のすべてのキューから特定のメッセージをエクスポートして、各メッセージの **InternetMessageID** 値をファイル名として使用するには、次の構文を使用します。

    Get-Message -Filter {<MessageFilter>} [-Server <ServerIdentity>] | ForEach-Object {$Temp=<Path>+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

**InternetMessageID** 値には角括弧 (\> および \<) が含まれることに注意してください。この記号はファイル名に使用できないため、削除する必要があります。

この例では、Mailbox01 というサーバー上のすべてのキューから contoso.com ドメイン内の送信者が送信したすべてのメッセージのコピーを、D:\\Contoso Export というローカル ディレクトリにエクスポートします。

    Get-Message -Filter {FromAddress -like "*@contoso.com"} -Server Mailbox01 | ForEach-Object {$Temp="D:\Contoso Export\"+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}


> [!NOTE]
> <EM>Server</EM> パラメーターを省略すると、コマンドはローカル サーバー上で動作します。


