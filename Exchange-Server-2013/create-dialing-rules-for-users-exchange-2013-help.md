---
title: 'ユーザーのダイヤル ルールを作成する: Exchange Online Help'
TOCTitle: ユーザーのダイヤル ルールを作成する
ms:assetid: c11e3d62-3eb1-4d7e-8741-9bede593e2df
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ898502(v=EXCHG.150)
ms:contentKeyID: 51407576
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ユーザーのダイヤル ルールを作成する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ダイヤル ルール グループは、ダイヤル ルール エントリで構成されます。ダイヤル ルールは、発信された電話番号を、社内の電話システム (PBX) または IP PBX に送る前に変更するためのものです。ダイヤル ルールには次の 2 つの用途があります。

  - 発信呼び出しでダイヤルできる番号を指定する。ダイヤル ルールを作成するときには、ダイヤルできる番号の形式を指定します。指定した形式のいずれかに一致しない番号は拒否されます。ダイヤル ルールを設定しないと、呼び出しが組織内に制限され、発信呼び出しを行うことができなくなります。

  - ダイヤル ルールによって、発信された番号は社内の電話システムに送信する前に変換されます。ダイヤル ルールでは、ダイヤルされた番号から番号を取り去ることも、番号を追加することもできます。たとえば、電話システムの外線発信コードを追加したり、国/地域番号を追加または削除して、番号を市外通話の番号に変換したり市内通話の番号に変換したりすることができます。

UM ダイヤル プランで許可する発信の種類を指定するには、ダイヤル ルールを含むダイヤル ルール グループを作成します。それから、そのダイヤル ルール グループを使用して Outlook Voice Access ユーザーおよび UM 自動応答を呼び出した発信者による発信を認証します。ダイヤル ルール グループは国内/地域通話用と国際通話用に分けて作成します。


> [!NOTE]
> UM を Microsoft Lync Server と統合する場合は、少なくとも 1 つのダイヤル ルール グループを作成することをお勧めします。そして、そのダイヤル ルール グループを使用して SIP URI ダイヤル プラン、UM メールボックス ポリシー、および UM 自動応答を認証し、すべての発信を Lync Server に転送するようにします。



アウトダイヤルに関するその他の管理タスクについては、「[呼び出しプロシージャの作成をユーザーに許可する](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/allow-users-to-make-calls-procedures)」を参照してください。

## よく使用されるダイヤル ルールの例


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>番号パターン</strong></p></td>
<td><p><strong>ダイヤル番号</strong></p></td>
<td><p><strong>このダイヤル ルールを使用する場合</strong></p></td>
</tr>
<tr class="even">
<td><p>*</p></td>
<td><p>*</p></td>
<td><p>すべての発信呼び出しを許可する場合。</p></td>
</tr>
<tr class="odd">
<td><p>1425xxxxxxx</p></td>
<td><p>91425xxxxxxx</p></td>
<td><p>外線発信番号をダイヤルし忘れても内線番号が呼び出されたりエラーになったりしないようにする場合。</p></td>
</tr>
<tr class="even">
<td><p>1xxxxxxxxxx</p></td>
<td><p>1xxxxxxxxxx</p></td>
<td><p>1 で始まるすべての番号を許可する場合。</p></td>
</tr>
<tr class="odd">
<td><p>xxxxxxx</p></td>
<td><p>1425xxxxxxx</p></td>
<td><p>7 桁の番号に 1 と市外局番 425 を追加する場合。</p></td>
</tr>
</tbody>
</table>


## 始める前に把握しておくべき情報

  - 予想所要時間 : 3 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ダイヤル プラン」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)」を参照してください。

  - ダイヤル ルール グループを UM メールボックス ポリシーに適用する場合は、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/set-up-voice-mail/create-um-mailbox-policy)」を参照してください。

  - ダイヤル ルール グループを UM 自動応答に適用する場合は、UM 自動応答が作成されていることを確認してください。詳細な手順については、「[UM 自動応答を作成する](create-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## EAC を使用してダイヤル ルールを作成する

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  <strong>UM ダイヤル プラン</strong> ページで、<strong>構成</strong> をクリックします。

3.  <strong>UM ダイヤル プラン</strong> ページの <strong>ダイヤル ルール</strong> で、<strong>国/地域内ダイヤル ルール</strong> または <strong>国際ダイヤル ルール</strong> の <strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

4.  <strong>ダイヤル ルールの新規作成</strong> ページで、以下の情報を入力します。
    
      - <strong>ダイヤル ルール名</strong>   このダイヤル ルールを追加するダイヤル ルール グループの名前を入力します。このルールを他のルールと組み合わせて使用する場合は同じグループ名を使用します。新しいダイヤル ルール グループを作成する場合は新しい一意の名前を入力します。
    
      - <strong>変換する番号のパターン (番号マスク)</strong>   ダイヤル前に変換する番号パターンを入力します (例: 91425xxxxxxx)。パターンに一致する番号をダイヤルすると、電話をかける前にダイヤル番号に変換されます。数字とワイルドカード (x) 以外は入力しないでください。番号パターンは*番号マスク*とも呼ばれます。
    
      - <strong>ダイヤル番号</strong>   ダイヤルする番号を入力してください。番号パターン 9xxxxxxx のように、数値とワイルドカード (x) のみを使用してください。ワイルドカード (x) は、ユーザーがダイヤルした元の番号の数値に置き換えられます。ダイヤル番号のワイルドカードの数と番号パターンのワイルドカードの数が同じになるようにしてください。
    
      - <strong>コメント</strong>   このダイヤル ルールのコメントまたは説明を入力してください。ルールの処理内容を説明するために使用できます (例: 「発信呼び出しに 9 を追加します」)。

5.  <strong>OK</strong> をクリックしてダイヤル ルールを保存します。続けてルールを入力することもできます。このとき、一緒に認証するルールに同じダイヤル ルール グループ名を使用します。

