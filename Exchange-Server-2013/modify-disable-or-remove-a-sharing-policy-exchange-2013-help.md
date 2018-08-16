---
title: '共有ポリシーの変更、無効化、削除: Exchange 2013 Help'
TOCTitle: 共有ポリシーの変更、無効化、削除
ms:assetid: 714af42d-ca29-4bb4-ac48-f0b3d4fd1c15
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657460(v=EXCHG.150)
ms:contentKeyID: 49896307
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 共有ポリシーの変更、無効化、削除

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-02-15_

ポリシーの共有によって、Exchange 組織の個人ユーザーは予定表の空き時間情報を他のフェデレーション Exchange 組織、非フェデレーション Exchange 組織、および個々のインターネット ユーザーと共有できます。通常の運用過程で、共有ルールの変更、空き時間アクセス レベルの変更、共有ポリシーの一時的無効化、共有ポリシーの完全削除など、いくつかの共有ポリシー プロパティを変更する必要がある場合があります。

フェデレーション共有の詳細については、「[共有](sharing-exchange-2013-help.md)」を参照してください。

共有ポリシーの作成方法については、「[共有ポリシーの作成](create-a-sharing-policy-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「予定表と共有のアクセス許可」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EAC を使用して共有ポリシーを変更する

1.  <strong>組織</strong> \> <strong>共有</strong> に移動します。

2.  <strong>個別共有</strong> 下でポリシーの共有を選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>共有ポリシー</strong> で、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

4.  <strong>共有ルール</strong> で、必要に応じて共有ルールを変更します。情報を共有する対象のドメインや、予定表の予定の共有レベルなどの設定を変更できます。完了したら、<strong>保存</strong> をクリックし、<strong>共有ルール</strong> ダイアログ ボックスを閉じます。

5.  <strong>共有ポリシー</strong> で <strong>保存</strong> をクリックし、共有ポリシーを更新します。

## EAC を使用して共有ポリシーを既定の共有ポリシーとして設定する

1.  <strong>組織</strong> \> <strong>共有</strong> に移動します。

2.  <strong>個別共有</strong> 下でポリシーの共有を選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>共有ポリシー</strong> で、<strong>このポリシーを既定の共有ポリシーにする</strong> チェック ボックスをオンにします。

4.  <strong>保存</strong> をクリックし、共有ポリシーを更新します。

## EAC を使用して共有ポリシーを無効にする

1.  <strong>組織</strong> \> <strong>共有</strong> に移動します。

2.  <strong>個別共有</strong> で、共有ポリシーを選択します。

3.  <strong>オン</strong> 列で、無効にする共有ポリシーのチェック ボックスをオフにします。

## EAC を使用して共有ポリシーを削除する


> [!IMPORTANT]
> 共有ポリシーを削除する前に、削除する共有ポリシーをすべてのユーザー メールボックスから削除する必要があります。



1.  <strong>組織</strong> \> <strong>共有</strong> に移動します。

2.  <strong>個別共有</strong> で、共有ポリシーを選択し、<strong>削除</strong>![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") をクリックします。

3.  警告が表示されたら、<strong>はい</strong> をクリックして、共有ポリシーを削除します。

## シェルを使用して共有ポリシーを変更、無効化、または削除する

  - この例は、組織外のドメインである contoso.com に対する共有ポリシー Contoso を変更します。このポリシーを使用すると、Contoso ドメイン内のユーザーが簡易版の空き時間情報を表示できます。
    
        Set-SharingPolicy -Identity Contoso -Domains 'sales.contoso.com: CalendarSharingFreeBusySimple'

  - この例は、Contoso という共有ポリシーにドメインをもう 1 つ追加します。既存のポリシーにドメインを追加する場合は、それまでの対象ドメインも指定する必要があります。
    
        Set-SharingPolicy -Identity Contoso -Domains 'contoso.com: CalendarSharingFreeBusySimple', 'atlanta.contoso.com: CalendarSharingFreeBusyReviewer', 'beijing.contoso.com: CalendarSharingFreeBusyReviewer'

  - この例では、共有ポリシー Contoso を既定の共有ポリシーとして設定します。
    
        Set-SharingPolicy -Identity Contoso -Default $True

  - この例では、Contoso という共有ポリシーを無効にします。
    
        Set-SharingPolicy -Identity "Contoso" -Enabled $False

  - 最初の例では、Contoso という共有ポリシーを削除しています。2 つ目の例では、Contoso という共有ポリシーを削除し、ポリシーを削除する際の確認メッセージが表示されないようにしています。
      ```
      Remove-SharingPolicy -Identity Contoso
      ```
      ```
      Remove-SharingPolicy -Identity Contoso -Confirm
      ```

構文およびパラメーターの詳細については、「[Set-SharingPolicy](https://technet.microsoft.com/ja-jp/library/dd297931\(v=exchg.150\))」と「[Remove-SharingPolicy](https://technet.microsoft.com/ja-jp/library/dd351071\(v=exchg.150\))」を参照してください。

