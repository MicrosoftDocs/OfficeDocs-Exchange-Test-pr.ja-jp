---
title: 'POP3 および IMAP4 のメッセージ取得形式オプションを構成する: Exchange 2013 Help'
TOCTitle: POP3 および IMAP4 のメッセージ取得形式オプションを構成する
ms:assetid: 481096e0-4492-46c2-8ca8-bdf84a84531e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997869(v=EXCHG.150)
ms:contentKeyID: 50555772
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# POP3 および IMAP4 のメッセージ取得形式オプションを構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

POP3 と IMAP4 を使用して自分の電子メールに接続するユーザーのために、メッセージ取得形式を構成できます。メッセージ取得オプションは、EAC またはシェルを使用してサーバー レベルで構成でき、シェルを使用してユーザー レベルで構成できます。

POP3 および IMAP4 に関連する詳細情報については、「[Exchange Server 2013 での POP3 と IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「POP3 の設定」および「IMAP4 の設定」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## サーバー レベルで POP3 メッセージ取得形式を設定する

## EAC を使用してサーバー レベルで POP3 メッセージ取得形式を設定する

1.  EAC で <strong>サーバー</strong> \> <strong>サーバー</strong> に移動します。

2.  サーバーの一覧でクライアント アクセス サーバーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  サーバーのプロパティ ページで、<strong>POP3</strong> をクリックします。

4.  <strong>メッセージの MIME 形式</strong> の下で、次の設定から選択します。
    
      - テキスト
    
      - HTML
    
      - HTML と代替テキスト
    
      - リッチ テキスト
    
      - リッチ テキストと代替テキスト
    
      - 最適な本文形式
    
      - TNEF

5.  <strong>保存</strong> をクリックします。

POP3 のメッセージ取得形式を設定した後、POP3 サービスを再起動して設定を有効にする必要があります。POP3 サービスを再起動する方法の詳細については、「[POP3 サービスの開始および停止](start-and-stop-the-pop3-services-exchange-2013-help.md)」を参照してください。

## シェルを使用してサーバー レベルで POP3 メッセージ取得形式を設定する

この例では、サーバー CAS01 上のすべての POP3 ユーザーに対してメッセージ取得形式オプションをテキスト専用に設定します。

```powershell
Set-PopSettings -Identity CAS01 -MessageRetrievalMimeFormat TextOnly
```

次の設定から選択できます。数値またはテキスト文字列を使用して、*MessageRetrievalMimeFormat* パラメーターの値を指定できます。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>メッセージ形式</strong></p></td>
<td><p><strong>値</strong></p></td>
</tr>
<tr class="even">
<td><p>テキスト</p></td>
<td><p><code>0</code> または<code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> または<code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML と代替テキスト</p></td>
<td><p><code>2</code> または<code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>リッチ テキスト</p></td>
<td><p><code>3</code> または<code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>リッチ テキストと代替テキスト</p></td>
<td><p><code>4</code> または<code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>最適な本文形式</p></td>
<td><p><code>5</code> または<code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> または<code>Tnef</code></p></td>
</tr>
</tbody>
</table>


POP3 のメッセージ取得形式を設定した後、POP3 サービスを再起動して設定を有効にする必要があります。POP3 サービスを再起動する方法の詳細については、「[POP3 サービスの開始および停止](start-and-stop-the-pop3-services-exchange-2013-help.md)」を参照してください。

構文およびパラメーターの詳細については、「[Set-PopSettings](https://technet.microsoft.com/ja-jp/library/aa997154\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

以下を実行して、サーバー上で POP3 メッセージの取得形式を正常に設定したことを確認します。

1.  シェルで、次のコマンドを実行します。
    
    ```powershell
Get-PopSettings | format-list
```

2.  *MessageRetrievalMimeFormat* 設定が正しいことを確認します。

## サーバー レベルで IMAP4 メッセージ取得形式を設定する

## EAC を使用してサーバー レベルで IMAP4 メッセージ取得形式を設定する

1.  EAC で <strong>サーバー</strong> \> <strong>サーバー</strong> に移動します。

2.  サーバーの一覧でクライアント アクセス サーバーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  サーバーのプロパティ ページで、<strong>IMAP4</strong> をクリックします。

4.  <strong>メッセージの MIME 形式</strong> の下で、次の設定から選択します。
    
      - テキスト
    
      - HTML
    
      - HTML と代替テキスト
    
      - リッチ テキスト
    
      - リッチ テキストと代替テキスト
    
      - 最適な本文形式
    
      - TNEF

5.  <strong>保存</strong> をクリックします。

IMAP4 のメッセージ取得形式を設定した後、IMAP4 サービスを再起動して設定を有効にする必要があります。IMAP4 サービスを再起動する方法の詳細については、「[IMAP4 サービスの開始および停止](start-and-stop-the-imap4-services-exchange-2013-help.md)」を参照してください。

## シェルを使用してサーバー レベルで IMAP4 メッセージ取得形式を設定する

この例では、サーバー CAS01 上のすべての IMAP4 ユーザーに対してメッセージ取得形式オプションをテキスト専用に設定します。

```powershell
Set-ImapSettings -Identity CAS01 -MessageRetrievalMimeFormat TextOnly
```

次の設定から選択できます。数値またはテキスト文字列を使用して、*MessageRetrievalMimeFormat* パラメーターの値を指定できます。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>メッセージ形式</strong></p></td>
<td><p><strong>値</strong></p></td>
</tr>
<tr class="even">
<td><p>テキスト</p></td>
<td><p><code>0</code> または<code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> または<code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML と代替テキスト</p></td>
<td><p><code>2</code> または<code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>リッチ テキスト</p></td>
<td><p><code>3</code> または<code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>リッチ テキストと代替テキスト</p></td>
<td><p><code>4</code> または<code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>最適な本文形式</p></td>
<td><p><code>5</code> または<code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> または<code>Tnef</code></p></td>
</tr>
</tbody>
</table>


IMAP4 のメッセージ取得形式を設定した後、IMAP4 サービスを再起動して設定を有効にする必要があります。IMAP4 サービスを再起動する方法の詳細については、「[IMAP4 サービスの開始および停止](start-and-stop-the-imap4-services-exchange-2013-help.md)」を参照してください。

構文およびパラメーターの詳細については、「[Set-ImapSettings](https://technet.microsoft.com/ja-jp/library/aa998252\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

以下を実行して、サーバー上で IMAP4 メッセージの取得形式を正常に設定したことを確認します。

1.  シェルで、次のコマンドを実行します。
    
    ```powershell
Get-ImapSettings | format-list
```

2.  *MessageRetrievalMimeFormat* 設定が正しいことを確認します。

## ユーザーの POP3 メッセージ取得形式を設定する

## シェルを使用してユーザーの POP3 メッセージ取得形式を設定する

この例では、`USER01` の POP3 アクセスについてメッセージ取得形式をテキスト専用に設定します。

```powershell
Set-CASMailbox -Identity USER01 -PopMessagesRetrievalMimeFormat TextOnly
```

次の設定から選択できます。数値またはテキスト文字列を使用して、*PopMessagesRetrievalMimeFormat* パラメーターの値を指定できます。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>メッセージ形式</strong></p></td>
<td><p><strong>値</strong></p></td>
</tr>
<tr class="even">
<td><p>テキスト</p></td>
<td><p><code>0</code> または<code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> または<code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML と代替テキスト</p></td>
<td><p><code>2</code> または<code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>リッチ テキスト</p></td>
<td><p><code>3</code> または<code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>リッチ テキストと代替テキスト</p></td>
<td><p><code>4</code> または<code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>最適な本文形式</p></td>
<td><p><code>5</code> または<code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> または<code>Tnef</code></p></td>
</tr>
</tbody>
</table>


POP3 のメッセージ取得形式を設定した後、POP3 サービスを再起動して設定を有効にする必要があります。POP3 サービスを再起動する方法の詳細については、「[POP3 サービスの開始および停止](start-and-stop-the-pop3-services-exchange-2013-help.md)」を参照してください。

構文およびパラメーターの詳細については、「[Set-CASMailbox](https://technet.microsoft.com/ja-jp/library/bb125264\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

以下を実行して、ユーザーの POP3 メッセージ取得形式オプションを正常に設定したことを確認します。

1.  シェルで、次のコマンドを実行します。
    
    ```powershell
Get-CAS Mailbox <identity> | format-list
```

2.  *PopMessagesRetrievalMimeFormat* の値が正しいことを確認します。

## ユーザーの IMAP4 メッセージ取得形式を設定する

## シェルを使用してユーザーの IMAP4 メッセージ取得形式を設定する

この例では、`USER01` の IMAP4 アクセスについてメッセージ取得形式をテキスト専用に設定します。

```powershell
Set-CASMailbox -Identity USER01 -ImapMessagesRetrievalMimeFormat TextOnly
```

数値またはテキスト文字列を使用して、*ImapMessagesRetrievalMimeFormat* パラメーターの値を指定できます。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>メッセージ形式</strong></p></td>
<td><p><strong>値</strong></p></td>
</tr>
<tr class="even">
<td><p>テキスト</p></td>
<td><p><code>0</code> または<code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> または<code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML と代替テキスト</p></td>
<td><p><code>2</code> または<code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>リッチ テキスト</p></td>
<td><p><code>3</code> または<code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>リッチ テキストと代替テキスト</p></td>
<td><p><code>4</code> または<code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>最適な本文形式</p></td>
<td><p><code>5</code> または<code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> または<code>Tnef</code></p></td>
</tr>
</tbody>
</table>


IMAP4 のメッセージ取得形式を設定した後、IMAP4 サービスを再起動して設定を有効にする必要があります。IMAP4 サービスを再起動する方法の詳細については、「[IMAP4 サービスの開始および停止](start-and-stop-the-imap4-services-exchange-2013-help.md)」を参照してください。

構文およびパラメーターの詳細については、「[Set-CASMailbox](https://technet.microsoft.com/ja-jp/library/bb125264\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

以下を実行して、ユーザーの IMAP4 メッセージ取得形式オプションを正常に設定したことを確認します。

1.  シェルで、次のコマンドを実行します。
    
    ```powershell
Get-CAS Mailbox <identity> | format-list
```

2.  *ImapMessagesRetrievalMimeFormat* の値が正しいことを確認します。

## 詳細情報

IMAP4 および POP3 ユーザーのメッセージ取得形式を設定した後、次の操作も実行できます。

[ユーザーの POP3 アクセスを有効または無効にする](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

[ユーザーの IMAP4 アクセスを有効または無効にする](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

[IMAP4 の予定表オプションを構成する](configure-calendar-options-for-imap4-exchange-2013-help.md)

[POP3 の予定表オプションを構成する](configure-calendar-options-for-pop3-exchange-2013-help.md)

