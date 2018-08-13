---
title: 'トランスポート保護ルールを作成する: Exchange 2013 Help'
TOCTitle: トランスポート保護ルールを作成する
ms:assetid: 3a857185-ee16-4ee7-9e57-8be95f7e753a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd302432(v=EXCHG.150)
ms:contentKeyID: 49896207
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# トランスポート保護ルールを作成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

トランスポート保護ルールを使用すると、送信者、受信者、メッセージの件名、内容などのプロパティに基づいてメッセージの権利を永続的に保護できます。


> [!NOTE]
> 運用環境でトランスポート ルールを作成する前に、テスト環境で作成して入念にテストすることをお勧めします。このトピックで作成したトランスポート ルールは例です。要件に基づき適切なトランスポート ルールの述語と値を使用して、トランスポート ルールを作成できます。



Information Rights Management (IRM) に関連するその他の管理タスクについては、「[Information Rights Management の手順](information-rights-management-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 推定完了時間: 2 ～ 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「トランスポート ルール」。

  - [Active Directory Rights Management サービス (AD RMS)](https://technet.microsoft.com/ja-jp/library/hh831364.aspx) を実行しているサーバーが組織で使用でき、そのサーバーに既存の RMS テンプレートが格納されている必要があります。

  - IRM でメッセージを保護するためにトランスポート保護ルールを構成して、ジャーナリングも使用する場合、ジャーナル レポート復号化を有効にして、ジャーナリング エージェントがジャーナル レポート内のメッセージの非暗号化コピーを保存できるようにすることを検討してください。詳細については、「[ジャーナル レポート復号化](journal-report-decryption-exchange-2013-help.md)」を参照してください。

  - トランスポート保護ルールを作成しても、AD RMS サーバーを使用できないために、そのルールをメッセージに適用できない場合、メールボックス サーバーのトランスポート サービスによってメッセージがキューに格納されます。このようなメッセージの量によっては、メールボックス サーバーで余分なディスク領域が消費される場合があります。Exchange は、3 回、メッセージの IRM 保護を試みます。3 回試行した後、AD RMS サーバーに到達できないか、メッセージを IRM で保護できない場合、配信不能レポート (NDR) が送信者に送信されます。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EAC を使用してトランスポート保護ルールを作成する

1.  **\[メール フロー\]** \> **\[ルール\]** に移動します。

2.  リスト ビューで **\[新規\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン")をクリックします。

3.  **\[新しいルール\]** で、まず **\[その他のオプション\]** をクリックし、以下のフィールドに必要な情報を入力します。
    
      - **\[名前\]**   トランスポート ルールの名前を入力します。
    
      - **\[次の場合、このルールを適用します\]**   条件を選択し、条件に必要な値を入力します。条件をさらに追加するには、**\[条件の追加\]** をクリックします。
        

        > [!IMPORTANT]
        > トランスポート保護ルールの作成時に条件を選択しなければ、組織内で Exchange 2013 サーバーがトランスポート サービスで処理するすべてのメッセージが IRM で保護されます。すべてのメッセージを IRM で保護するには、より多くのリソースが必要になります。メールボックス サーバーと AD&nbsp;RMS の展開は、このことを踏まえて計画してください。

    
      - **\[実行する処理\]**   **\[メッセージに権利保護を適用する\]** を選択し、次に **\[RMS テンプレートの選択\]** ダイアログ ボックスでテンプレートを選択します。
    
      - **\[ただし次の場合を除く\]**   (オプション) **\[例外の追加\]** をクリックしてルールの例外を指定します。

4.  **\[保存\]** をクリックしてトランスポート ルールを作成します。

## シェルを使用してトランスポート保護ルールを作成する

  - トランスポート保護ルールは、AD RMS 展開に既存の RMS テンプレートがないと作成できません。この例では、AD RMS クラスターから使用できるテンプレートを取得します。
    
        Get-RMSTemplate | format-list
    
    構文およびパラメーターの詳細については、「[Get-RMSTemplate](https://technet.microsoft.com/ja-jp/library/dd297960\(v=exchg.150\))」を参照してください。

  - この例では、Protect-BusinessCriticalProject というトランスポート保護ルールを作成します。このルールでは、**\[転送不可\]** テンプレートを使用して、"件名" フィールドに "Business Critical" という語句を含むメッセージを IRM で保護します。
    

    > [!NOTE]
    > この例では、<CODE>SubjectContainsWords</CODE> 述語を使用します。ルールの条件や例外は、トランスポート ルール述語を任意に組み合わせて定義できます。使用できる述語については、<A href="mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md">トランスポート ルールの条件 (述語)</A> を参照してください。

    
        New-TransportRule -Name "Protect-BusinessCriticalProject" -SubjectContainsWords "Business Critical" -ApplyRightsProtectionTemplate "Do Not Forward"
    
    構文およびパラメーターの詳細については、「[New-TransportRule](https://technet.microsoft.com/ja-jp/library/bb125138\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

トランスポート保護ルールが正しく作成できたことを確認するには、以下の手順の 1 つを実行します。

  - EAC を使用してルールが作成されたことを確認し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックして、ルールのプロパティを表示します。

  - ルールを取得するには、[Get-TransportRule](https://technet.microsoft.com/ja-jp/library/aa998585\(v=exchg.150\)) コマンドレットを使用します。ルールの取得方法の例については、「**Get-TransportRule**」の「[Examples](https://technet.microsoft.com/ja-jp/aa998585\(exchg.150\)#examples)」を参照してください。

  - Outlook、Outlook Web App、またはモバイル デバイスを使用して、ルール条件を満たすテスト メッセージを送信して、受信者が受信するメッセージが IRM で保護されているか確認します。

