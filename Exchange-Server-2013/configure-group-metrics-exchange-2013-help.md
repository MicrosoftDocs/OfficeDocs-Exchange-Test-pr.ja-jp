---
title: 'グループ測定値を構成する: Exchange 2013 Help'
TOCTitle: グループ測定値を構成する
ms:assetid: 76ccd6a7-e2ec-42f4-9ab3-e8cc257ac896
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ649327(v=EXCHG.150)
ms:contentKeyID: 49896323
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# グループ測定値を構成する

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-04-08_

配布グループおよび動的配布グループのサイズに関する情報を示すメール ヒントは、グループ測定値データを使用します。グループ メトリックス データは、指定されたメールボックス サーバーで生成されます。グループ測定値の詳細については、「[グループ メトリックとメール ヒント](group-metrics-and-mailtips-exchange-2013-help.md)」を参照してください。

メールボックス サーバー上でグループ メトリックス生成を有効または無効にできます。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:10 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「グループ測定値」。

  - グループ測定値データは、メール ヒントに対してのみ使用されます。グループ測定メール ヒントが組織内で有効になっていることを確認します。詳細な手順については、「[組織上の関係のメール ヒントの管理](manage-mailtips-for-organization-relationships-exchange-2013-help.md)」を参照してください。

  - この手順を実行するには、シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用してグループ測定値の生成を有効または無効にする


> [!NOTE]
> 既定では、グループ測定値はオフライン アドレス帳 (OAB) を生成する役割を果たすすべてのサーバー上で生成されます。これらの例は、OAB を使用していない組織でのみ必要になります。



メールボックス サーバー上でグループ メトリックス生成を有効または無効にするには、次のコマンドを実行します。

    Set-MailboxServer <ServerIdentity> -ForceGroupMetricsGeneration <$true | $false>

この例では、MBX1 という名前のメールボックス サーバー上でグループ メトリックス生成を有効にします。

    Set-MailboxServer MBX1 -ForceGroupMetricsGeneration $true

## 正常な動作を確認する方法

OAB を使用していない組織でグループ メトリックス生成が正常に有効または無効になったことを確認するには、次の操作を実行します。

1.  次のコマンドを実行します。
    
        Get-MailboxServer <ServerIdentity> | Format-List ForceGroupMetricsGeneration

2.  表示される設定が構成した設定であることを確認します。

