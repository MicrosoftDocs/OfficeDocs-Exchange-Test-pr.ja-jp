---
title: 'ファイルからカスタムの DLP ポリシー テンプレートをインポートする: Exchange Online Help'
TOCTitle: ファイルからカスタムの DLP ポリシー テンプレートをインポートする
ms:assetid: 83f49dbd-f9b1-498e-b548-1529c5e1ccdb
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ150531(v=EXCHG.150)
ms:contentKeyID: 48269054
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ファイルからカスタムの DLP ポリシー テンプレートをインポートする

 

_**適用先:** Exchange Online, Exchange Server 2013_

DLP ポリシーを通じて機密情報を管理するには、ポリシー情報設定を含むファイルをインポートします。DLP ポリシー テンプレートは、XML ファイルとして Exchange とは独立して開発できます。ただし、ポリシーが正しく動作するために特定の形式要件を満たす必要があります。または、前のバージョンの Exchange からエクスポートしたポリシーを Microsoft Exchange Server 2013 にインポートすることもできます。


> [!NOTE]
> 運用環境で DLP ポリシーを実行する前に、テスト モードでこれらのポリシーを有効にする必要があります。テスト中は、サンプルのユーザー メールボックスを構成し、テスト ポリシーを呼び出すテスト メッセージを送信することによって、結果を確認することをお勧めします。



## 始める前に把握しておくべき情報

  - 予想所要時間: 15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「データ損失防止 (DLP)」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EAC を使用してファイルからカスタムの DLP ポリシー テンプレートをインポートする

次の手順を使用してファイルからカスタムの DLP ポリシー テンプレートをインポートします。混乱を避けるため、独自の名前を入力できる場合、ポリシーまたはルールの各部分に一意の名前を指定してください。

1.  EAC 内で、**コンプライアンス管理** \> **データ損失防止** に移動します。

2.  <strong>追加</strong> ![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") アイコンの横にある矢印をクリックし、<strong>ポリシーのインポート</strong> をクリックします。

3.  <strong>ポリシーのインポート</strong> ページで、以下のフィールドに入力します。
    
    1.  <strong>インポートするファイルの選択</strong>   インストールするポリシー ファイルの名前を追加します。
    
    2.  <strong>名前</strong>   このポリシーを他と区別する名前を追加します。
    
    3.  <strong>説明</strong>   オプションで、このポリシーを要約した説明を追加します。
    
    4.  <strong>その他のオプション</strong>   このポリシーのモードまたは状態を選択します。新しいポリシーを完全に有効にするには、そのように指定する必要があります。ポリシーの既定のモードは、通知なしのテストです。
    
    5.  <strong>次へ</strong> をクリックして、ポリシーを検証およびインポートします。

## シェルを使用してファイルからカスタムの DLP ポリシー テンプレートをインポートする

この例では、ファイル C:\\My Documents\\DLP Backup.xml 内のカスタムの DLP ポリシー テンプレート ファイルをインポートします。XML ファイルから DLP ポリシー コレクションをインポートすると、組織内で定義された既存のすべての DLP ポリシーが削除または上書きされます。現在の DLP ポリシーをインポートして上書きする前に、現在の DLP ポリシー コレクションを必ずバックアップしてください。

```powershell
    Import-DlpPolicyCollection -FileData ([Byte[]]$(Get-Content -Path " C:\My Documents\DLP Backup.xml " -Encoding Byte -ReadCount 0))
```

## 詳細情報

[データ損失防止](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)

