﻿---
title: 'インプレース アーカイブ (社内) のアーカイブ クォータの構成: Exchange 2013 Help'
TOCTitle: インプレース アーカイブ (社内) のアーカイブ クォータの構成
ms:assetid: f10e77c7-e1d4-415a-bef9-cb3f00e74c34
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee633489(v=EXCHG.150)
ms:contentKeyID: 50555893
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# インプレース アーカイブ (社内) のアーカイブ クォータの構成

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-12-04_

社内展開では、既定で、インプレース アーカイブが格納域クォータの制限なしで作成されます。このため、メールボックスのプロパティを編集して、アーカイブの格納域クォータを設定する必要があります。アーカイブについて、次のクォータを設定できます。

  - **アーカイブ警告クォータ**   インプレース アーカイブが指定のアーカイブ警告クォータを超過すると、Exchange 管理者用にイベントがログに記録され、警告メッセージがメールボックス ユーザーに送信されます。

  - **アーカイブ クォータ**   インプレース アーカイブが指定のアーカイブ クォータを超過すると、メッセージがアーカイブに移動されなくなり、警告メッセージがメールボックス ユーザーに送信されます。

インプレース アーカイブの詳細については、「[Exchange 2013 のインプレース アーカイブ](in-place-archiving-in-exchange-2013-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - Exchange 管理センター (EAC) で、固定値を含むドロップダウン リストを使用して、アーカイブ クォータとアーカイブ警告クォータを構成できます。いずれかのクォータを EAC の一覧に表示されていない値に設定する場合は、シェルを使用します。

  - アーカイブ警告クォータの値は、アーカイブ クォータよりも低い値に構成します。ユーザーのアーカイブ増加のスピードによる違いはありますが、アーカイブ警告クォータとアーカイブ クォータの値に十分な差を設け、アーカイブからのアイテムの削除、管理者や IT ヘルプデスクへのアーカイブ クォータの追加要求など、ユーザーが適切な処置を取るための時間を確保できるように設定する必要があります。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「受信者プロビジョニングのアクセス許可」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EAC を使用して、メールボックスのアーカイブ クォータとアーカイブ警告クォータを構成する

1.  <strong>受信者</strong> \> <strong>メールボックス</strong> に移動します

2.  リスト ビューで、メールボックスを選択します。

3.  詳細ウィンドウの <strong>インプレース アーカイブ</strong> で、<strong>詳細を表示</strong> をクリックします。

4.  <strong>アーカイブ メールボックス</strong> で、<strong>クォータ値 (GB)</strong> および <strong>警告を表示するサイズ (GB)</strong> リストを使用して設定したい値を選択します。

5.  <strong>OK</strong> をクリックします。

## シェルを使用して、メールボックスのアーカイブ クォータとアーカイブ警告クォータを構成する

この例では、Chris Ashton のメールボックスのアーカイブ クォータを 10 ギガバイト (GB) に設定します。この値に達すると、インプレース アーカイブがいっぱいで、項目をアーカイブに移動できなくなることを伝える警告メッセージがユーザーに送信されます。また、この例では、アーカイブ警告クォータを 9.5 GB に設定します。この値に達すると、インプレース アーカイブがほぼいっぱいになったことを伝える警告メッセージがユーザーに送信されます。

```powershell
Set-Mailbox -Identity "Chris Ashton" -ArchiveQuota 10GB -ArchiveWarningQuota 9.5GB
```

構文およびパラメーターの詳細については、「[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

既存のメールボックスに対して社内アーカイブが正常に有効になったことを確認するには、次の手順のいずれかを実行します。

  - EAC で、<strong>受信者</strong> \> <strong>メールボックス</strong> の順に移動し、確認が必要なメールボックスを選択します。詳細ウィンドウの <strong>インプレース アーカイブ</strong> で、<strong>詳細を表示</strong> をクリックして、アーカイブのクォータ設定を確認します。

  - シェルで、次のコマンドを実行して、アーカイブに関するクォータ情報を表示します。
    
      ```powershell
      Get-Mailbox <Name> | FL Name,Archive*Quota
      ```

