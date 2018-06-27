---
title: 'パブリック フォルダー メールボックスを作成する: Exchange Online Help'
TOCTitle: パブリック フォルダー メールボックスを作成する
ms:assetid: 64437ffd-231b-4c10-84df-232ccbe9538f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ552410(v=EXCHG.150)
ms:contentKeyID: 49129490
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# パブリック フォルダー メールボックスを作成する

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

パブリック フォルダーを作成する前に、まず、パブリック フォルダーのメールボックスを作成する必要があります。パブリック フォルダー メールボックスには、階層情報とパブリック フォルダーの内容が含まれています。最初に作成したパブリック フォルダー メールボックスは、階層の書き込み可能なコピーのみを含むプライマリ階層メールボックスになります。それより後に追加で作成したパブリック フォルダー メールボックスは、階層の読み取り専用コピーを含むセカンダリ メールボックスになります。


> [!NOTE]
> ストレージ クォータおよびパブリック フォルダーの制限に関する詳細については、次のトピックを参照してください。 
> <UL>
> <LI>
> <P>Office 365 のパブリック フォルダーについて詳しくは、「<A href="https://go.microsoft.com/fwlink/?linkid=391188">Exchange Online の制限</A>」を参照してください。</P>
> <LI>
> <P>オンプレミス Exchange Server 2013 のパブリック フォルダーについて詳しくは、「<A href="limits-for-public-folders-exchange-2013-help.md">パブリック フォルダーの制限</A>」を参照してください。</P></LI></UL>



Exchange 2013 のパブリック フォルダーに関するその他の管理タスクについては、「[パブリック フォルダーの手順](public-folder-procedures-exchange-2013-help.md)」を参照してください。

Exchange Online のパブリック フォルダーに関するその他の管理タスクについては、「[Office 365 と Exchange Online のパブリック フォルダーの手順](https://technet.microsoft.com/ja-jp/library/jj966272\(v=exchg.150\))」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間: 5 分未満。

  - Exchange 2013 パブリック フォルダーと従来の Exchange サーバーのパブリック フォルダーは、同じ組織内には共存できません。従来のパブリック フォルダーがまだ存在する場合に、パブリック フォルダー メールボックスを作成しようとすると、エラー **\[既存のパブリック フォルダーの展開が検出されました。既存のパブリック フォルダー データを移行するには、-HoldForMigration スイッチを使用して新しいパブリック フォルダー メールボックスを作成してください。\]** を受け取ります。
    
    Exchange 2013 でパブリック フォルダーを作成する前に、従来のパブリック フォルダーを Exchange 2013 に移行する必要があります。これを実行するには、「[シリアル移行を使用して以前のバージョンから Exchange 2013 にパブリック フォルダーを移行する](https://technet.microsoft.com/ja-jp/library/jj150486\(v=exchg.150\))」の手順に従います。それらの手順では、移行したパブリック フォルダーの格納に使用できるパブリック フォルダー メールボックスを作成する方法が示されています。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[共有とコラボレーションのアクセス許可](sharing-and-collaboration-permissions-exchange-2013-help.md)」の「パブリック フォルダー」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

## 必要な作業

## EAC を使用してパブリック フォルダー メールボックスを作成する

1.  **\[パブリック フォルダー\]** \> **\[パブリック フォルダー メールボックス\]** に移動して、**\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  **\[パブリック フォルダー メールボックス\]** ページで、パブリック フォルダー メールボックスの名前を入力します。

3.  **\[保存\]** をクリックします。

## シェルを使用して、パブリック フォルダー メールボックスを作成する

この例では、プライマリのパブリック フォルダー メールボックスを作成します。

    New-Mailbox -PublicFolder -Name MasterHierarchy

この例では、セカンダリのパブリック フォルダー メールボックスを作成します。プライマリ階層メールボックスとセカンダリ階層メールボックスの作成の相違点は、プライマリ メールボックスが組織で最初に作成されたメールボックスという点のみです。負荷分散を目的として、パブリック フォルダー メールボックスを追加で作成できます。

    New-Mailbox -PublicFolder -Name Istanbul 

構文およびパラメーターの詳細については、「[New-Mailbox](https://technet.microsoft.com/ja-jp/library/aa997663\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

プライマリのパブリック フォルダー メールボックスが正常に作成されたことを確認するには、次のシェル コマンドを実行します。

    Get-OrganizationConfig | Format-List RootPublicFolderMailbox

構文およびパラメーターの詳細については、「[Get-OrganizationConfig](https://technet.microsoft.com/ja-jp/library/aa997571\(v=exchg.150\))」を参照してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

