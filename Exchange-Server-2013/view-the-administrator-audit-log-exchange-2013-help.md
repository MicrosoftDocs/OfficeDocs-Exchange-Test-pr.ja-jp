---
title: '管理者監査ログを表示する: Exchange 2013 Help'
TOCTitle: 管理者監査ログを表示する
ms:assetid: 5c62072a-556d-4fea-9973-d668c6b9fd57
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn342832(v=EXCHG.150)
ms:contentKeyID: 56270005
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理者監査ログを表示する

 

_**適用先:**Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**トピックの最終更新日:**2016-05-03_

Microsoft Exchange Online Protection (EOP)、Microsoft Exchange Online、および Microsoft Exchange 2013 では、Exchange 管理センター (EAC) を使用して*管理者監査ログ*のエントリを検索および表示できます。管理者監査ログには、管理者や管理者特権を割り当てられたユーザーが実行する、Exchange 管理シェル コマンドレットに基づく特定の操作が記録されます。管理者監査ログのエントリは、実行されたコマンドレット、使われたパラメーター、コマンドレットを実行したユーザー、および影響を受けたオブジェクトに関する情報を提供します。


> [!NOTE]
> <UL>
> <LI>
> <P>既定では、管理者監査ログ出力は有効になっています。</P>
> <LI>
> <P>管理者監査ログには、Exchange 管理シェル コマンドレットに基づく <STRONG>Get</STRONG>、<STRONG>Search</STRONG>、または <STRONG>Test</STRONG> という動詞で始まる操作は記録されません。</P>
> <LI>
> <P>監査ログのエントリは 90 日間維持されます。90 日間の保存期間を過ぎたエントリは削除されます。</P></LI></UL>



## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[Feature permissions in EOP](https://technet.microsoft.com/ja-jp/library/jj723125\(v=exchg.150\))」トピックの「レポートの表示」。

  - 前述のとおり、管理者監査ログ出力は既定では有効になっています。管理者監査ログ出力が有効になっていることを確認するために、次のコマンドを実行できます。
    
        Get-AdminAuditLogConfig | FL AdminAuditLogEnabled
    
    Exchange 2013 で、管理者監査ログ出力が無効になっている場合、次のコマンドを実行してそれを有効にすることができます。
    
        Set-AdminAuditLogConfig -AdminAuditLogEnabled $True
    
    Exchange Online Protection と Exchange Online では、管理者監査ログ出力が常に有効です。それを無効にすることはできません。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## EAC を使用して管理者監査ログを表示する

1.  EAC で、**\[コンプライアンス管理\]** \> **\[監査\]** に移動し、**\[管理者監査ログ レポートを実行する\]** を選択します。

2.  **\[開始日\]** と **\[終了日\]** を選択して、**\[検索\]** を選択します。指定された期間中に行われたすべての構成の変更が表示されます。この一覧は次の情報を使用して並べ替えることができます。
    
      - **日付**   構成の変更が行われた日時。日時は、世界協定時刻 (UTC) 形式で格納されます。
    
      - **コマンドレット**   構成の変更に使用されたコマンドレットの名前。
    
      - **ユーザー**   構成の変更を行ったユーザーのユーザー アカウント名。
    
    最大 5,000 エントリが複数のページに表示されます。結果を絞り込む必要がある場合は、指定する日付範囲を短くします。個々の検索結果を選択すると、詳細ウィンドウに次の追加情報が表示されます。
    
      - **変更されたオブジェクト**   コマンドレットによって変更されたオブジェクト。
    
      - **パラメーター (パラメーター:値)**   使用されたコマンドレット パラメーターと、そのパラメーターで指定された値。

3.  特定の監査ログ エントリを印刷するには、詳細ウィンドウの **\[印刷\]** ボタンを選択します。

## 正常な動作を確認する方法

管理者監査ログ レポートを正常に実行できた場合は、指定した日付範囲内に行われた構成の変更が検索結果ウィンドウに表示されます。結果が表示されない場合は、日付の範囲を変更してレポートを再度実行します。


> [!NOTE]
> 組織内で行った変更が監査ログの検索結果に表示されるようになるまで最大 15 分かかります。管理者監査ログに変更が表示されない場合は、数分待機してから検索を再実行してください。


