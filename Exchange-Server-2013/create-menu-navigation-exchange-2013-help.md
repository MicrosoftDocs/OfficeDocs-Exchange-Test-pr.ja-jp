---
title: 'メニューのナビゲーションの作成: Exchange Online Help'
TOCTitle: メニューのナビゲーションの作成
ms:assetid: 3cfc9a01-0a61-4d15-9561-621568dc30d9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997471(v=EXCHG.150)
ms:contentKeyID: 49896216
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.UnifiedMessaging.AutoAttendantKeyMappingControl
ms.translationtype: HT
---

# メニューのナビゲーションの作成

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

<strong>新しいメニュー ナビゲーション エントリ</strong> ページでは、勤務時間または勤務時間外の自動応答のメイン メニューの音声ガイダンスに 1 つまたは複数のキー マッピングを作成できます。 電話のキーパッドでキーを押したときに実行される操作 (たとえば、内線番号または別の自動応答への通話の転送) を定義できます。

UM 自動応答に関連する追加の管理タスクについては、「[UM 自動応答の管理](manage-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM 自動応答」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM 自動応答が作成されていることを確認してください。詳細な手順については、「[UM 自動応答を作成する](create-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して UM 自動応答ナビゲーション メニューを構成する

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  <strong>UM 自動応答</strong> の下の <strong>UM ダイヤル プラン</strong> ページで、メニュー ナビゲーションを作成する UM 自動応答を選択します。ツール バーの <strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>UM 自動応答</strong> ページで、<strong>メニュー ナビゲーション</strong> をクリックし、<strong>勤務時間のメニュー ナビゲーションを有効にする</strong> か <strong>勤務時間外のメニュー ナビゲーションを有効にする</strong> を選択し、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン")をクリックします。

4.  <strong>新しいメニュー ナビゲーション エントリ</strong> ページで、以下の内容を構成します。
    
      - <strong>音声ガイダンス</strong>   このボックスを使用して、新しいナビゲーション メニューの名前を入力します。ナビゲーション メニュー名は、表示のみを目的としています。これは必須フィールドです。
        
        新しいナビゲーション メニューを複数指定する必要がある場合もあるため、キー マッピングにはわかりやすい名前を付けることをお勧めします。 キー マッピング名の最大長は 64 文字です。スペースも使用できます。 ただし、次の文字を含めることはできません。" / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - <strong>このキーを押したとき</strong>   このリストを使用して、キー マッピングを有効にします。 キー マッピングとは、自動応答で特定の操作 (たとえば、別の自動応答またはオペレーターへの通話の転送) を実行するために発信者が押す数字キーのことです。 既定では、定義されているエントリはありません。
        
        このドロップダウン リストを使用して、発信者が押す数字キー (1 ～ 9) を選択します。 ゼロ (0) は、自動応答オペレーター用に予約されています。
        
        ドロップダウン リストから<strong>タイムアウト</strong> を選択すると、発信者が電話のキーパッドのキーを押さない場合に内線番号または別の自動応答に転送されるようにします。 たとえば、"担当者がお応えするまで、しばらくお待ちください" という音声を再生できます。 既定では 5 秒に設定されています。 このオプションを有効にすると、空のキー マッピングが作成されます。
    
      - <strong>次のオーディオ ファイルを再生する</strong>   このオプションを使用して、発信者に対して録音済みのオーディオ ファイルを選択します。<strong>変更</strong> をクリックし、<strong>参照</strong> をクリックしてオーディオ ファイルを指定します。
    
      - <strong>この追加アクションを実行する</strong>   次のいずれかのオプションを使用して、自動応答が発信者に対して実行する操作を定義します。
        
          - <strong>なし</strong>   自動応答で通話を内線番号や別の自動応答に転送しない場合や、ユーザーにメッセージを残させない場合は、このオプションを使用します。
        
          - <strong>内線番号への転送</strong>   このオプションを選択して、内線番号に通話が転送されるようにします。このオプションを有効にする場合は、このボックスを使用して、通話を転送する内線番号を入力します。 このフィールドには、数字のみを入力できます。 次の文字を含めることはできません。" / \\ \[ \] : ; | = , + \* ? \< \>.
        
          - <strong>この UM 自動応答に転送</strong>   このオプションを選択すると、通話が自動応答に転送されます。 <strong>参照</strong> をクリックして、使用する自動応答を見つけます。 このオプションを有効にする前に、自動応答を作成して構成する必要があります。 このオプションは、UM 自動応答の親/子構造を作成する場合に使用します。
        
          - <strong>このユーザーに音声メッセージを残す</strong>   このオプションを選択すると、構成中の UM 自動応答と同じダイヤル プランにあるユーザーに、発信者がボイス メール メッセージを残せるようになります。発信者が自動応答メニューからこのオプションを選択すると、選択されたユーザーにボイス メールを残すように求められます。<strong>参照</strong> をクリックして、UM が有効なユーザーを指定します。
        
          - <strong>勤務地のアナウンス</strong>   このオプションを選択すると、発信者は自動応答メニューのオプションを選択し、UM 自動応答で構成されている勤務地を聞けるようになります。この機能が正しく動作するようにするには、最初に UM 自動応答の <strong>全般</strong> ページの <strong>勤務地</strong> ボックスに勤務地を入力する必要があります。
        
          - <strong>勤務時間のアナウンス</strong>   このオプションを選択すると、発信者は自動応答メニューのオプションを選択し、UM 自動応答で構成されている勤務時間を聞けるようになります。この機能が正しく動作するようにするには、最初に UM 自動応答の <strong>勤務時間</strong> ページに勤務時間を入力する必要があります。

5.  <strong>OK</strong> をクリックして新しいメニュー ナビゲーションを作成します。

6.  <strong>UM 自動応答</strong> ページで、<strong>保存</strong> をクリックして変更を保存します。

## シェルを使用して UM 自動応答キー マッピングを構成する

この例では、業務時間のキー マッピングが以下のようになります。

  - 発信者が 1 を押すと、`SalesAutoAttendant` という名前の別の UM 自動応答に転送されます。

  - 2 を押すと、サポート用の内線番号 12345 に転送されます。

  - 3 を押すと、オーディオ ファイルを再生する別の自動応答に送信されます。

<!-- end list -->

    Set-UMAutoAttendant -id MyAutoAttendant -BusinessHoursKeyMappingEnabled $true -BusinessHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

この例では、コンマ区切り値 (.csv) ファイルで定義されたキー マッピングを設定します。 最初に、次の見出しと正しいエントリで .csv ファイルを作成する必要があります。 \<key\>,\<description\>,\[\<extension\>\],\[\<autoattendant name\>\],\[\<promptfilenamepath\>\],\[\<asrphrase1;asrphrase2\>\],\[\<leavevoicemailfor\>\],\[\<transfertomailbox\>\]. 角かっこ内の値は省略可能です。 .csv ファイルの作成後、**Import-csv** コマンドレットを使用して .csv ファイルをインポートします。

    $o = Import-csv -path "C:\UMFiles\AutoAttendants\keymappings.csv"
    Set-UMAutoAttendant MyAutoAttendant -BusinessHoursKeyMapping $o

この例では、既存の UM 自動応答から .csv ファイルにキー マッピングをエクスポートしてから、同じキー マッピングを別の UM 自動応答にインポートします。 キー マッピングを .csv ファイルにエクスポートし, .csv ファイル内のキー マッピングを編集または変更してから、それらのキー マッピングを別の UM 自動応答にインポートすることもできます。

    $aa = Get-UMAutoAttendant -id MyAutoAttendant
    $aa1 = Get-UMAutoAttendant -id MyAutoAttendant2
    $aa.BusinessHoursKeyMapping | Export-csv -path "C:\UMFiles\AutoAttendants\keymappings.csv"
    $aa1.BusinessHoursKeyMapping = (Import-csv -path "C:\UMFiles\AutoAttendants\keymappings.csv")

