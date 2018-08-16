---
title: '管理ストアの制限: Exchange 2013 Help'
TOCTitle: 管理ストアの制限
ms:assetid: bea9ec15-bfb5-4716-b14e-010e389c9f9e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Mt741981(v=EXCHG.150)
ms:contentKeyID: 73226006
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理ストアの制限

 

_**トピックの最終更新日:** 2016-09-15_

**概要**:管理ストアの接続の制限と制限の設定方法を説明します。

MicrosoftExchange Server 2013 では、接続と使用量の制限が Exchange 管理ストアに設定され、単一のアプリケーションや 1 人のユーザーが管理ストアに対して利用可能な接続を使用してしまうのを防ぎます。1 人のユーザーや単一のアプリケーションがすべての接続を使用できると、他のユーザーやアプリケーションは管理ストアにアクセスできなくなり、その結果ダウンタイムが発生します。


> [!NOTE]
> 管理特権を持つアカウントによる接続については、セッションの上限がサーバーあたり 64,000 に増加しました。



## 用語集

以下の用語について知っておくと、このトピックで参照する接続の種類を理解しやすくなります。

  - セッション  
    セッションは、Microsoft Outlook のような、サービスおよびクライアント アプリケーションが管理ストアへの接続に使用する接続を表します。サービスとクライアントは、特定の時点で複数のセッションを持つことができます。*接続*と*セッション*という用語は同じ意味で使用されます。

<!-- end list -->

  - スレッド  
    スレッドは、同時に実行中の管理ストアへの要求を表します。例えば、ユーザーが Outlook のフォルダーを開くと、Outlook はユーザーの代理として管理ストアへの要求を実行します。その要求の実行は単一のスレッドです。
    
    Exchange Server 2013 では、クライアントの種類に基づくスレッドの制限はなくなりました。その代わり、すべてのクライアントについて、**メールボックス データベースあたり**のスレッド数は最大 50 です。空き時間情報サービスは例外で、ユーザーあたりの上限は 16 です。

ページのトップへ

## セッションの制限

以下の表では、管理ストアへのクライアントの接続の種類と、それらの接続に基づいた制限を一覧表示します。セッションの制限を変更する場合は、次の表のすぐ下の「セッションの制限を構成する」をご覧ください。

Exchange の以前のバージョンでは、サーバーあたりの接続数に基づいて、管理ストアへの接続数の制限を設定しました。Exchange 2013 では、セッションの制限はメールボックス データベースあたりの接続数に基づいています。

Exchange 2013 の接続制限の種類は、以下のとおりです。

  - **プロセスあたりの最大セッション数**   Exchange サービスがメールボックス データベース上で同時に開くことのできる、セッションの最大数を指定します。

  - **プロセスあたりの最大ユーザー セッション数**   1 人のユーザーの特定のプロトコルに対するセッションの最大数を指定します。

次のセクション「セッションの制限を構成する」では、これらの制限を変更する方法を説明します。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>クライアントの種類</th>
<th></th>
<th>メールボックス データベースあたりの最大セッション数</th>
<th>メールボックス データベースあたりの既定のユーザー セッション数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>管理者</p></td>
<td></td>
<td><p>10,000</p></td>
<td><p>該当しない</p></td>
</tr>
<tr class="even">
<td><p>空き時間情報サービス</p></td>
<td></td>
<td><p>10,000</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>コンテンツのインデックス作成</p></td>
<td></td>
<td><p>10,000</p></td>
<td><p>該当しない</p></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync</p></td>
<td></td>
<td><p>該当しない</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Web サービス</p></td>
<td></td>
<td><p>該当しない</p></td>
<td><p>16</p></td>
</tr>
<tr class="even">
<td><p>管理</p></td>
<td></td>
<td><p>該当しない</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>中間層の MAPI (MoMT)</p></td>
<td></td>
<td><p>該当しない</p></td>
<td><p>32</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMailboxAssistants:イベント</p></td>
<td></td>
<td><p>10,000</p></td>
<td><p>該当しない</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeMailboxAssistants:時間指定</p></td>
<td></td>
<td><p>10,000</p></td>
<td><p>該当しない</p></td>
</tr>
<tr class="even">
<td><p>MSExchange リモート プロシージャ コール</p></td>
<td></td>
<td><p>該当しない</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft OfficeOutlook Web App</p></td>
<td></td>
<td><p>該当しない</p></td>
<td><p>16</p></td>
</tr>
<tr class="even">
<td><p>POP3 と IMAP4</p></td>
<td></td>
<td><p>該当しない</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>転送</p></td>
<td></td>
<td><p>10,000</p></td>
<td><p>該当しない</p></td>
</tr>
<tr class="even">
<td><p>ユニファイド メッセージング</p></td>
<td></td>
<td><p>該当しない</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>その他</p></td>
<td></td>
<td><p>該当しない</p></td>
<td><p>16</p></td>
</tr>
</tbody>
</table>


## セッションの制限を構成する

既定のセッションの制限を変更できます。


> [!NOTE]
> セッションの制限を変更する場合、すべてのデータベース可用性グループ (DAG) 内のすべてのメールボックス サーバー上で変更する必要があります。すべてのサーバーで同じ変更を行わないと、不整合が発生します。クライアント アクセス サーバーのセッション制限を大きくするには、調整ポリシーの <CODE>RCAMaxConcurrency</CODE> 値を大きくする必要があります。詳しくは、「<A href="https://technet.microsoft.com/ja-jp/library/dd298094(v=exchg.150)">Set-ThrottlingPolicy</A>」をご覧ください。




> [!NOTE]
> レジストリを不適切に編集すると、重大な問題が発生し、オペレーティング システムを再インストールする必要が生じることがあります。レジストリを不適切に編集したことによって生じた問題は、解決できない可能性があります。レジストリを編集する前に、価値のあるあらゆるデータをバックアップしてください。



1.  レジストリ エディター (regedit) を起動します。

2.  以下のレジストリ サブキーに移動します。
    
    **\\\\HKEY\_LOCAL\_MACHINE \\SYSTEM\\CurrentControlSet\\Services\\MSExchangeIS\\ParametersSystem**。

3.  <strong>ParametersSystem</strong> を右クリックし、<strong>新規</strong> をポイントし、<strong>DWORD (32 ビット) 値</strong> をクリックします。
    
    新しい値が結果ウィンドウに作成されます。

4.  キーの名前を以下のいずれかの値に変更してから、Enter キーを押します。
    
      - **ユーザーあたりの最大許容セッション数**   この制限は、ユーザーごとに許容される最大セッション数を指定します。
    
      - **ユーザーあたりの最大許容サービス セッション数**   この制限は、ユーザーごとに許容される最大サービス セッション数を指定します。
    
      - **サービスあたりの最大許容 Exchange セッション数**   この制限は、サービスごとに許容される最大 Exchange セッション数を指定します。既定値は 10,000 です。

5.  新規作成したキーを右クリックし、<strong>変更</strong> をクリックします。

6.  <strong>値** **データ</strong> ボックスに、このエントリに設定するオブジェクト数の制限値を入力し、<strong>OK</strong> をクリックします。既定の設定を表示するには、上記の表を使用します。

ページのトップへ

## 開くアイテムの制限

開くアイテムの制限は、1 つのセッションの単一のメールボックスで開くことができるアイテムの数を設定する制限です。ただし、ユーザーは同時に複数のセッションを開くことができます。例えば、ユーザーが 2 つのセッションを開いている場合、ユーザーは 1,000 フォルダーを開くことができます。

これらの制限を変更する場合は、次の表のすぐ下の「開くアイテムの制限を構成する」をご覧ください。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>アイテムの種類</th>
<th>レジストリ オブジェクトの種類</th>
<th>セッションあたりに開くアイテムの最大数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ACL の表示</p></td>
<td><p>objtACLView</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>添付ファイル</p></td>
<td><p>objtAttachment</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>添付ファイルの表示</p></td>
<td><p>objtAttachmentView</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>CStream</p></td>
<td><p>objtCStream</p></td>
<td><p>該当しない</p></td>
</tr>
<tr class="odd">
<td><p>フォルダー</p></td>
<td><p>objtFolder</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>フォルダーの表示</p></td>
<td><p>objtFolderView</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>FX の送信先のストリーム</p></td>
<td><p>objtFXDstStrm</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>FX の送信元のストリーム</p></td>
<td><p>objtFXSrcStrm</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>メッセージ</p></td>
<td><p>objtMessage</p></td>
<td><p>250</p></td>
</tr>
<tr class="even">
<td><p>メッセージの表示</p></td>
<td><p>objtMessageView</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>通知</p></td>
<td><p>objtNotify</p></td>
<td><p>500,000</p></td>
</tr>
<tr class="even">
<td><p>ルールの表示</p></td>
<td><p>objtRulesView</p></td>
<td><p>該当しない</p></td>
</tr>
<tr class="odd">
<td><p>ストリーム</p></td>
<td><p>objtStream</p></td>
<td><p>250</p></td>
</tr>
</tbody>
</table>


## 開くアイテムの制限を構成する

MAPI クライアントが同時に使用できるリソースの最大数を制限できます。


> [!NOTE]
> 開くアイテムの制限を変更する場合、すべての DAG とクライアント アクセス アレイ内のすべてのメールボックス サーバー上で変更する必要があります。すべてのサーバーで同じ変更を行わないと、不整合が発生します。




> [!NOTE]
> レジストリを不適切に編集すると、重大な問題が発生し、オペレーティング システムを再インストールする必要が生じることがあります。レジストリを不適切に編集したことによって生じた問題は、解決できない可能性があります。レジストリを編集する前に、価値のあるあらゆるデータをバックアップしてください。



1.  レジストリ エディター (regedit) を起動します。

2.  以下のレジストリ サブキーに移動します。
    
    **\\\\HKEY\_LOCAL\_MACHINE \\SYSTEM\\CurrentControlSet\\Services\\MSExchangeIS\\ParametersSystem**

3.  <strong>ParametersSystem</strong> を右クリックし、<strong>新規</strong> をポイントして、<strong>キー</strong> をクリックします。
    
    新しいキーがコンソール ツリーに作成されます。

4.  **MaxObjsPerMapiSession** キーの名前を変更して Enter キーを押します。

5.  <strong>MaxObjsPerMapiSession</strong> を右クリックし、<strong>新規</strong> をポイントして、<strong>DWORD (32 ビット) 値</strong> をクリックします。
    
    新しい値が結果ウィンドウに作成されます。

6.  キーの名前を *\<Object\_type\>* に変更します。*\<Object\_type\>* は、変更するレジストリ オブジェクトの種類の名前です。例えば、開くことができるメッセージの数を変更するには *objtMessage* を使用します。Enter キーを押します。

7.  新規作成したキーを右クリックし、<strong>変更</strong> をクリックします。

8.  <strong>値データ</strong> ボックスで、このエントリに設定するオブジェクト数の制限値を入力し、<strong>OK</strong> をクリックします。例えば、オブジェクトの値を増やすために <strong>350</strong> と入力します。

9.  Microsoft Exchange Information Store サービスを再起動します。

ページのトップへ

## アイテムのサイズ制限

アイテムのサイズ制限は、ユーザーのメールボックス内のアイテムに設定される制限です。アイテムのサイズ制限は、[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\)) コマンドレットで *MaxSendSize* パラメーターと *MaxReceiveSize* パラメーターを使用して構成できます。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>アイテムの種類</th>
<th>制限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>メッセージ (保存済み)</p></td>
<td><p>SendLimit、ReceiveLimit の最大サイズ</p></td>
</tr>
<tr class="even">
<td><p>メッセージ (送信済み)</p></td>
<td><p>SendLimit の最大サイズ</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
</tr>
</tbody>
</table>


ページのトップへ

