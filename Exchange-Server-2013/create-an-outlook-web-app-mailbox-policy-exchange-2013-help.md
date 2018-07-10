---
title: 'Outlook Web App のメールボックス ポリシーの作成: Exchange Online Help'
TOCTitle: Outlook Web App のメールボックス ポリシーの作成
ms:assetid: 347207fa-cfb7-40a6-b19a-831dcdb54ad5
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd335191(v=EXCHG.150)
ms:contentKeyID: 49896189
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Web App のメールボックス ポリシーの作成

 

_**適用先:** Exchange Online, Exchange Server 2013_

Outlook Web App メールボックス ポリシーを作成して、ポリシー設定の共通セットを適用することができます。Outlook Web App メールボックス ポリシーは、添付ファイルの設定など、特定のユーザー グループに対して設定を適用するときや、設定を標準化するときに便利です。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - このコマンドレットを実行する際には、あらかじめアクセス許可を割り当てる必要があります。このトピックにはこのコマンドレットのすべてのパラメーターが示されていますが、割り当てられているアクセス許可に含まれていない一部のパラメーターにはアクセスできません。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「Outlook Web App メールボックス ポリシー」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して、Outlook Web App メールボックス ポリシーを作成する

1.  EAC で、**\[アクセス許可\]** \> **\[Outlook Web App ポリシー\]** の順にクリックします。

2.  **\[新規作成\]** をクリックします。

3.  
    
    ポリシーの名前を入力します。

4.  
    
    このチェック ボックスを使用して、機能を有効または無効にします。既定では、最も一般的な機能が表示されます。有効または無効にできるすべての機能を表示するには、**\[その他のオプション\]** をクリックします。
    

    > [!NOTE]
    > Outlook Web App メールボックス ポリシーの機能の設定は、Outlook Web App 仮想ディレクトリの設定より優先されます。シェルで <STRONG>Set-CASMailbox</STRONG> コマンドレットを使用して、個々のユーザーのセグメンテーションの設定を変更できます。



5.  **\[保存\]** をクリックしてポリシーを保存します。

## シェルを使用して、Outlook Web App メールボックス ポリシーを作成する

この例では、`Policy1` という名前で Outlook Web App メールボックス ポリシーを作成します。

  - シェルで、次のコマンドを実行します。
    
        New-OwaMailboxPolicy -Name Policy1

構文およびパラメーターの詳細については、「[New-OwaMailboxPolicy](https://technet.microsoft.com/ja-jp/library/dd351067\(v=exchg.150\))」を参照してください。シェルを使って Outlook Web App メールボックス ポリシーを構成する方法については、「[Set-OwaMailboxPolicy](https://technet.microsoft.com/ja-jp/library/dd297989\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

Outlook Web App メールボックス ポリシーが正常に作成されたことを確認するには、次の手順を実行します。

  - EAC で、**\[アクセス許可\]** \> **\[Outlook Web App ポリシー\]** をクリックし、新しいメールボックス ポリシーを探します。

