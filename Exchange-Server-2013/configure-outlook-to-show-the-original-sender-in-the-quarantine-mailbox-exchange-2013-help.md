---
title: '検疫メールボックス内で元の送信者を表示するように Outlook を構成する: Exchange 2013 Help'
TOCTitle: 検疫メールボックス内で元の送信者を表示するように Outlook を構成する
ms:assetid: 9249425d-1b06-48a0-ad95-c4eefb641ff4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee861109(v=EXCHG.150)
ms:contentKeyID: 49896370
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 検疫メールボックス内で元の送信者を表示するように Outlook を構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

スパム検疫は、正当なメッセージの消失の危険を減らすためのコンテンツ フィルター エージェントの機能です。スパム検疫は、スパムと識別され、組織内のユーザーのメールボックスに配信されないようにする必要があるメッセージの一時的な格納場所を提供します。

メッセージがスパム検疫のしきい値に一致する場合、そのメッセージは配信不能レポート (NDR) にラップされ、スパム検疫メールボックスに配信されます。検疫されたメッセージは検疫メールボックスに NDR として格納されるため、組織のポストマスターのアドレスがすべてのメッセージの送信元アドレスとして一覧表示されます。ただし、フィールドの一覧に元の送信者アドレス、元の受信者アドレス、および元の Spam Cnfidence Level (SCL) があると、復元するメッセージの検索がさらに容易になります。

既定では、Microsoft Outlook でこれらのフィールドを選択できません。メッセージ ビューでこれらのフィールドを追加する前に、選択可能なオプション フィールドとして元の送信者、元の受信者、および元の SCL を追加する Outlook フォームを最初に作成する必要があります。このカスタム フォームを作成すると、メッセージ ビューにこれらのフィールドを表示するように Outlook を構成できます。

## 始める前に把握しておくべき情報

  - この手順の予想所要時間:15 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「Mailbox access (メールボックス アクセス)」。

  - この手順では、スパム検疫メールボックスの構成が完了している必要があります。詳細については、「[スパム検疫メールボックスの構成](configure-a-spam-quarantine-mailbox-exchange-2013-help.md)」を参照してください。

  - 検疫メールボックスにアクセスするには、そのメールボックスの Outlook プロファイルを構成し、Outlook を使用してメールボックスを開く必要があります。構成と複数の Outlook プロファイルを使用する方法の詳細については、[概要の Outlook 電子メール プロファイル](https://go.microsoft.com/fwlink/p/?linkid=178975)を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## 手順 1:メモ帳を使用してカスタム Outlook フォームを作成する

1.  メモ帳を開き、ドキュメントに次のコードをコピーします。
    
        [Description]
        MessageClass=IPM.Note
        CLSID={00020D31-0000-0000-C000-000000000046}
        DisplayName=Quarantine Extension Form
        Category=Standard
        Subcategory=Form
        Comment=This form allows the Original Sender (ReceivedRepresentingEmailAddress), Original Recipient (To), and Original SCL (OriginalScl) values to be viewed as columns.
        LargeIcon=IPML.ico
        SmallIcon=IPMS.ico
        Version=3.0
        Locale=enu
        Hidden=1
        Owner=Microsoft Corporation
        Contact=Your Name
        
        [Platforms]
        Platform1=Win16
        Platform2=NTx86
        Platform9=Win95
        
        [Platform.Win16]
        CPU=ix86
        OSVersion=Win3.1
        
        [Platform.NTx86]
        CPU=ix86
        OSVersion=WinNT3.5
        
        [Platform.Win95]
        CPU=ix86
        OSVersion=Win95
        
        [Properties]
        Property01=ReceivedRepresentingEmailAddress
        Property02=DisplayTo
        Property03=OriginalScl
        
        [Property.ReceivedRepresentingEmailAddress]
        Type=31
        NmidInteger=0x0078
        DisplayName=ReceivedRepresentingEmailAddress
        
        [Property.DisplayTo]
        Type=31
        NmidInteger=0x0E04
        DisplayName=DisplayTo
        
        [Property.OriginalScl]
        Type=3
        NmidPropset={41F28F13-83F4-4114-A584-EEDB5A6B0BFF}
        NmidString=OriginalScl
        DisplayName=OriginalScl
        
        [Verbs]
        Verb1=1
        
        [Verb.1]
        DisplayName=&Open
        Code=0
        Flags=0
        Attribs=2
        
        [Extensions]
        Extensions1=1
        
        [Extension.1]
        Type=31
        NmidPropset={00020D0C-0000-0000-C000-000000000046}
        NmidInteger=1
        Value=1000000000000000

2.  ファイルは、次の値を使用して、Office Forms フォルダーに保存します。
    
      - **パス** *\<Office インストール パス\>*\\\<*OfficeVersion\>*\\Forms\\*\<LCID\>*
        
          - *\<Office インストール パス\>*   32 ビット バージョンの Microsoft Windows にインストールされた 32 ビット バージョンの Office、または 64 ビット バージョンの Windows にインストールされた 64 ビット バージョンの Office の場合、既定のパスは `C:\Program Files\Microsoft Office` です。64 ビット バージョンの Windows にインストールされた 32 ビット バージョンの Office の場合、既定のパスは `C:\Program Files (x86)\Microsoft Office` です。
        
          - *\<OfficeVersion\>* Outlook 2007 の場合、この値は `Office12` です。Outlook 2010 の場合、この値は `Office14` です。Outlook 2013 の場合、この値は `Office15` です。
        
          - *\<LCID\>*   これはロケール ID (LCID) の値です。たとえば、アメリカ英語の LCID は 1033 です。詳細については、「[KB221435:Word でサポートされているロケール識別子のリスト](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=221435)」を参照してください。
    
      - **名前**   この残りの手順では、ファイルの名前を `QTNE.cfg` とします。ファイルの名前は重要ではありませんが、ファイルが QTNE.cfg.txt ではなく QTNE.cfg として保存されるように値を二重引用符で囲んでください。
    
    64 ビット バージョンの Windows に 32 ビットのアメリカ英語バージョンの Outlook 2013 をインストールした場合、次のようにファイルを保存します。
    
        "C:\Program Files (x86)\Microsoft Office\Office15\Forms\1033\QTNE.cfg"
    

    > [!NOTE]
    > Windows ユーザー アカウント制御 (UAC) が原因で正しい場所にファイルを保存できない場合、最初に一時的な場所に保存してからコピーしてください。



## 手順 2:カスタム Outlook フォームを使用するように Outlook を構成する

コンピューターにインストールされている Outlook のバージョンに基づいて、次のいずれかの手順を実行します。

## Outlook 2010 または Outlook 2013 を構成する

1.  Outlook 2010 または Outlook 2013 で、<strong>ファイル</strong> \> <strong>オプション</strong> \> <strong>詳細設定</strong> をクリックします。

2.  <strong>開発者</strong> セクションで、<strong>カスタム フォーム</strong> をクリックします。

3.  <strong>オプション</strong> ダイアログ ボックスの <strong>フォームの管理</strong> をクリックします。

4.  <strong>フォーム マネージャー</strong> ダイアログ ボックスの <strong>インストール</strong> をクリックします。`QTNE.cfg` ファイルの場所を参照して選択し、<strong>開く</strong> をクリックします。<strong>フォームのプロパティ</strong> ダイアログ ボックスの情報を確認し、<strong>OK</strong> をクリックして検疫拡張フォームを個人用フォーム ライブラリにインストールします。

5.  <strong>フォーム マネージャー</strong> ダイアログ ボックスの <strong>閉じる</strong> をクリックします。<strong>OK</strong> を 2 回クリックして、残りのダイアログ ボックスを閉じて Outlook のメイン インターフェイスに戻ります。

6.  受信トレイの <strong>メール</strong> ビューの <strong>ホーム</strong> タブで、列見出しの行を右クリックし (列を表示するためにメッセージ リストの幅の拡張が必要になる場合がある)、<strong>ビューの設定</strong> を選択します。

7.  <strong>ビューの詳細設定</strong> ダイアログ ボックスで、<strong>列</strong> をクリックします。

8.  <strong>列の表示</strong> ダイアログ ボックスの <strong>対象となる列グループ</strong> ドロップダウン リストで、リストの終わりまでスクロールして <strong>フォーム</strong> を選択します。

9.  <strong>このフォルダー用にエンタープライズ フォームを選択</strong> ダイアログ ボックスの <strong>選択フォーム</strong> フィールドで、<strong>メッセージ</strong> を選択して <strong>削除</strong> をクリックします。<strong>個人用フォーム</strong> フィールドで、<strong>検疫拡張フォーム</strong> を選択して <strong>追加</strong> をクリックします。完了したら、<strong>閉じる</strong> をクリックします。

10. <strong>列の表示</strong> ダイアログ ボックスの <strong>利用可能な列</strong> セクションで、次のフィールドのうち 1 つ以上を選択し、各フィールドを選択した後に <strong>追加</strong> をクリックします。
    
      - **ReceivedRepresentingEmailAddress** 元の送信者
    
      - **DisplayTo** 元の受信者 (追加後には <strong>宛先</strong> として表示されます)
    
      - **OriginalScl** 元の SCL
    
    <strong>上へ移動</strong> または <strong>下へ移動</strong> ボタンを使用して、列をビューに配置します。最良の結果を得るには、この 3 つのフィールドを <strong>添付ファイル</strong> フィールドの後、なおかつ<strong>送信元</strong> フィールドの前に配置してください。完了したら、<strong>OK</strong> を 2 回クリックして Outlook のメイン インターフェイスに戻ります。

## Outlook 2007 を構成する

1.  Outlook 2007 で、<strong>ツール</strong> \> <strong>オプション</strong> をクリックします。

2.  <strong>オプション</strong> ダイアログ ボックスで <strong>その他</strong> タブをクリックし、<strong>全般</strong> の <strong>詳細オプション</strong> をクリックします。

3.  <strong>詳細オプション</strong> ダイアログ ボックスの <strong>カスタム フォーム</strong> をクリックし、<strong>カスタム フォーム</strong> ダイアログ ボックスの <strong>フォームの管理</strong> をクリックします。

4.  <strong>フォーム マネージャー</strong> ダイアログ ボックスの <strong>インストール</strong> をクリックします。`QTNE.cfg` ファイルの場所を参照して選択し、<strong>開く</strong> をクリックします。<strong>フォームのプロパティ</strong> ダイアログ ボックスの情報を確認し、<strong>OK</strong> をクリックして検疫拡張フォームを個人用フォーム ライブラリにインストールします。

5.  <strong>フォーム マネージャー</strong> ダイアログ ボックスを閉じてから 3 回 <strong>OK</strong> をクリックして残りのダイアログ ボックスを閉じ、Outlook 2007 のメイン インターフェイスに戻ります。

6.  受信トレイの <strong>メール</strong> ビューの列見出し行を右クリックし (列を表示するにはメッセージ リストの幅を広げなければならない場合があります)、<strong>現在のビューの編集</strong> を選択します。

7.  <strong>表示のカスタマイズ: メッセージ</strong> ダイアログ ボックスで、<strong>フィールドの表示</strong> をクリックします。

8.  <strong>フィールドの表示</strong> ダイアログ ボックスの <strong>対象となるフィールド グループ</strong> ドロップダウン リストで、リストの最後までスクロールして <strong>フォーム</strong> を選択します。

9.  <strong>このフォルダー用にエンタープライズ フォームを選択</strong> ダイアログ ボックスの <strong>選択フォーム</strong> フィールドで、<strong>メッセージ</strong> を選択して <strong>削除</strong> をクリックします。<strong>個人用フォーム</strong> フィールドで、<strong>検疫拡張フォーム</strong> を選択して <strong>追加</strong> をクリックします。完了したら、<strong>閉じる</strong> をクリックします。

10. <strong>フィールドの表示</strong> ダイアログ ボックスの <strong>選択可能なフィールド</strong> セクションで、次の 1 つ以上のフィールドを選択し、選択したフィールドごとに <strong>追加</strong> をクリックします。
    
      - **ReceivedRepresentingEmailAddress** 元の送信者
    
      - **DisplayTo** 元の受信者 (追加後には <strong>宛先</strong> として表示されます)
    
      - **OriginalScl** 元の SCL
    
    <strong>上へ移動</strong> または <strong>下へ移動</strong> ボタンを使用して、列をビューに配置します。最良の結果を得るには、この 3 つのフィールドを <strong>添付ファイル</strong> フィールドの後、なおかつ<strong>送信元</strong> フィールドの前に配置してください。完了したら、<strong>OK</strong> を 2 回クリックして Outlook 2007 のメイン インターフェイスに戻ります。

## 正常な動作を確認する方法

Outlook を使用してスパム検疫メールボックスで隔離されたメッセージの元の送信者、元の受信者、または元の SCL の値を確認できれば、この手順が正常に動作していることがわかります。

