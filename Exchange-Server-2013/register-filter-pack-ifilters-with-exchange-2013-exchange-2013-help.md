---
title: 'Exchange 2013 でフィルター パック IFilter を登録する: Exchange 2013 Help'
TOCTitle: Exchange 2013 でフィルター パック IFilter を登録する
ms:assetid: 0338980f-3a64-49d3-bc3c-bf6f10f88cb4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ837174(v=EXCHG.150)
ms:contentKeyID: 50555721
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 でフィルター パック IFilter を登録する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

添付ファイルのスキャン条件が指定されているトランスポート ルールは、添付ファイルのコンテンツの分析時にテキスト展開を実行します。Exchange 2013 は、最もよく使用される添付ファイルの種類をネイティブでスキャンできます。その他の添付ファイルの種類をスキャンの対象にするには、Exchange 2013 で IFilter を登録します。このトピックでは、Microsoft およびサードパーティ プロバイダーによってリリースされた IFilter を登録する方法を示します。

特定のファイルの種類に対応した IFilter を登録したら、添付ファイルの処理条件が指定されているトランスポート ルールでこれらの添付ファイルをスキャンできます。結果として、これらのファイルの種類は *AttachmentIsUnsupported* 条件をトリガーしなくなります。


> [!NOTE]
> このトピックに記載されている手順には、Exchange サーバーのレジストリの変更が含まれています。レジストリを不適切に編集すると、重大な問題が発生し、オペレーティング システムを再インストールする必要が生じることがあります。レジストリを不適切に編集したことによって生じた問題は、解決できない可能性があります。レジストリを編集する前に、価値のあるあらゆるデータをバックアップしてください。<BR>これらの手順では、メールボックス サーバー上で Microsoft Exchange Transport サービスを停止および再開する必要もあります。



トランスポート ルールに関連する追加の管理タスクについては、「[メール フロー ルールを管理します](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:サーバーごとに 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[Exchange およびシェル インフラストラクチャのアクセス許可](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)」の「Exchange サーバー構成設定」。

  - 既に Exchange 2013 メールボックス サーバーの役割がインストールされているサーバー上で、以下の手順を実行する必要があります。これらの手順の実行後にさらにメールボックス サーバーを追加する場合、新たに準備されたサーバー上でこれらの手順を再度実行する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## Microsoft Office 2010 Filter Pack を登録する

既定では、次の Office のファイルの種類は、Exchange トランスポート ルールではサポートされません。

  - Office OneNote

  - Office Publisher

これらのファイルをサポートする場合、Microsoft Office 2010 Filter Pack を展開する必要があります。この Filter Pack は Exchange 2013 セットアップ中は展開されず、展開に必須ではありません。

## Microsoft Office 2010 Filter Pack を展開する

Office 2010 Filter Pack の展開は、次の 2 つの主要な手順で構成されます。

  - Filter Pack をダウンロードおよびインストールします。これで IFilter が Windows (Search) で登録されます。

  - IFilter が Exchange 2013 でも登録されるようにレジストリを変更します。これで、Exchange がファイル形式での添付ファイルのスキャンをサポートできるようになります。


> [!IMPORTANT]
> 組織内のすべてのメールボックス サーバーに対して実行する必要があります。



1.  [Microsoft Download Center](https://go.microsoft.com/fwlink/?linkid=191548) から、Microsoft Office 2010 Filter Pack (`FilterPack64bit.exe`) をダウンロードし、保存します。

2.  メールボックス サーバー上で `FilterPack64bit.exe` ファイルを実行し、指示に従ってインストールを完了します。

3.  レジストリ エディターを起動し、次のレジストリ サブキーを見つけます。
    
    ```powershell
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\CLSID
    ```

4.  <strong>CLSID</strong> で、次のように OneNote ファイルのサブキーを追加します。
    
    1.  <strong>CLSID</strong> を右クリックし、<strong>新規</strong> をポイントして、<strong>キー</strong> をクリックします。
    
    2.  新しいキーの名前を `{B8D12492-CE0F-40AD-83EA-099A03D493F1}` に変更します。
    
    3.  作成したキーをクリックし、<strong>(既定)</strong> の値を Office 2010 Filter Pack をインストールした場所に設定します。既定では、フィルター パックは `C:\Program Files\Common Files\Microsoft Shared\Filters\ONIFilter.dll` にインストールされます。
    
    4.  <strong>{B8D12492-CE0F-40AD-83EA-099A03D493F1}</strong> を右クリックし、<strong>新規</strong> をポイントします。次に、<strong>文字列値</strong> をクリックします。
    
    5.  新しい文字列値に `ThreadingModel` という名前を付け、`Both` に設定します。

5.  <strong>CLSID</strong> で、次のように Publisher ファイルのサブキーを追加します。
    
    1.  <strong>CLSID</strong> を右クリックし、<strong>新規</strong> をポイントして、<strong>キー</strong> をクリックします。
    
    2.  新しいキーの名前を `{A7FD8AC9-7ABF-46FC-B70B-6A5E5EC9859A}` に変更します。
    
    3.  作成したキーをクリックし、<strong>(既定)</strong> の値を Office 2010 Filter Pack をインストールした場所に設定します。既定では、フィルター パックは `C:\Program Files\Common Files\Microsoft Shared\Filters\PUBFILT.dll` にインストールされます。
    
    4.  <strong>{A7FD8AC9-7ABF-46FC-B70B-6A5E5EC9859A}</strong> を右クリックし、<strong>新規</strong> をポイントします。次に、<strong>文字列値</strong> をクリックします。
    
    5.  新しい文字列値に `ThreadingModel` という名前を付け、`Both` に設定します。

6.  次のレジストリ キーを見つけます。
    
    ```powershell
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\filters
    ```

7.  <strong>フィルター</strong> で、次のように .one 拡張子のサブキーを追加します。
    
    1.  <strong>フィルター</strong> を右クリックし、<strong>新規</strong> をポイントして、<strong>キー</strong> をクリックします。
    
    2.  新しいキーの名前を `.one` に変更します。
    
    3.  作成したキーをクリックし、<strong>(既定)</strong> の値を `{B8D12492-CE0F-40AD-83EA-099A03D493F1}` に設定します。

8.  <strong>フィルター</strong> で、次のように .pub 拡張子のサブキーを追加します。
    
    1.  <strong>フィルター</strong> を右クリックし、<strong>新規</strong> をポイントして、<strong>キー</strong> をクリックします。
    
    2.  新しいキーの名前を `.pub` に変更します。
    
    3.  作成したキーをクリックし、<strong>(既定)</strong> の値を `{A7FD8AC9-7ABF-46FC-B70B-6A5E5EC9859A}` に設定します。

9.  レジストリ エディターを終了します。

10. メールボックス サーバー上で、次のサービスを指定された順に停止してから再開します。
    
    1.  Microsoft Exchange Transport サービスを停止します。
    
    2.  Microsoft Filtering Management サービスを停止します。
    
    3.  Microsoft Filtering Management サービスを開始します。
    
    4.  Microsoft Exchange Transport サービスを開始します。

## 正常な動作を確認する方法

Microsoft Office 2010 Filter Pack の IFilter を正常に登録したことを確認するには、次の手順を実行します。

1.  次のプロパティを持つトランスポート ルールを作成します。トランスポート ルールを作成する方法の詳細については、「[メール フロー ルールを管理します](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules)」を参照してください。
    
      - 送信者は自分のメールボックスにします。
    
      - 添付ファイルのコンテンツには、「IFilter のテスト中」という語句を含めます。
    
      - インシデント レポートを生成して、自分のメールボックスに送信します。

2.  「IFilter のテスト中」という語句を含む OneNote ファイルを作成し、そのファイルを新しい電子メール メッセージに添付して、自分自身に送信します。

3.  作成したルールに関するトランスポート ルールのインシデント レポートを受信したことを確認します。これで、ルール エンジンが OneNote ファイルのコンテンツを分析できたことを確認できます。

4.  Publisher ファイルについて手順 2 と 3 を繰り返します。

## 追加のファイル形式をサポートするためにサードパーティ製 Ifilter を登録する

追加のサードパーティ製 Ifilter を登録することで、その他のファイルの種類に対応した添付ファイルのスキャン機能を拡張できます。その他のファイルのサポートを追加するには、各メールボックス サーバー上にそのファイルの種類の Ifilter をインストールおよび登録します。


> [!IMPORTANT]
> Microsoft ではトランスポート ルールを使用してサードパーティ製 IFilter をテストしていないため、運用環境に展開する前に、テスト環境でサードパーティ製 IFilter を展開してテストすることをお勧めします。



## Adobe PDF IFilter を展開する

この手順では、[Adobe PDF IFilter](https://www.adobe.com/support/downloads/detail.jsp?ftpid=4025) を展開してトランスポート ルールでの PDF 添付ファイルの処理をサポートする方法を示します。


> [!NOTE]
> Exchange 2013 では、既定でトランスポート ルールでの PDF ファイルのスキャンがサポートされます。ここに示す PDF の例は、サードパーティ製 IFilter を使用して追加のファイルの種類のサポートを拡張する方法を示すためだけのものです。



1.  [Adobe PDF IFilter](https://www.adobe.com/support/downloads/detail.jsp?ftpid=4025) をダウンロードし、インストールの指示に従います。

2.  レジストリ エディターを起動し、次のサブキーを見つけます。
    
    ```powershell
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\CLSID
    ```

3.  <strong>CLSID</strong> で、次のように PDF ファイルのサブキーを追加します。
    
    1.  <strong>CLSID</strong> を右クリックし、<strong>新規</strong> をポイントして、<strong>キー</strong> をクリックします。
    
    2.  新しいキーの名前を `{E8978DA6-047F-4E3D-9C78-CDBE46041603}` に変更します。
        

        > [!NOTE]
        > 各 IFilter には、一意なクラス ID (CLSID) があります。CLSID は、登録している IFilter のインストール マニュアル、またはレジストリの <CODE>HKEY_CLASSES_ROOT\CLSID</CODE> キーの下にあるファイル拡張子を検索すると見つけることができます。

    
    3.  作成したキーをクリックし、<strong>(既定)</strong> の値を PDF IFilter をインストールした場所に設定します。既定では、PDF IFilter は `C:\Program Files\Adobe\Adobe PDF IFilter 9 for 64-bit platforms\bin\PDFFilter.dll` にインストールされます。

4.  次のレジストリ キーを見つけます。
    
    ```powershell
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\filters
    ```

5.  <strong>フィルター</strong> で、次のように .pdf 拡張子のサブキーを追加します。
    
    1.  <strong>フィルター</strong> を右クリックし、<strong>新規</strong> をポイントして、<strong>キー</strong> をクリックします。
    
    2.  新しいキーの名前を `.pdf` に変更します。
    
    3.  作成したキーをクリックし、<strong>(既定)</strong> の値を `{E8978DA6-047F-4E3D-9C78-CDBE46041603}` に設定します。

6.  レジストリ エディターを終了します。

7.  メールボックス サーバー上で、次のサービスを指定された順に停止してから再開します。
    
    1.  Microsoft Exchange Transport サービスを停止します。
    
    2.  Microsoft Filtering Management サービスを停止します。
    
    3.  Microsoft Filtering Management サービスを開始します。
    
    4.  Microsoft Exchange Transport サービスを開始します。

## 正常な動作を確認する方法

このトピックの前の項「正常な動作を確認する方法」の手順で Publisher ファイルを Adobe PDF ファイルに置き換えて実行します。

## 詳細情報

[トランスポート ルールを使用してメッセージの添付を検査する](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)

[メール フローやトランスポート ルール](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[トランスポート ルールの条件 (述語)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[トランスポート ルールのアクション](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

