---
title: '携帯電話でリモート ワイプを実行する: Exchange Online Help'
TOCTitle: 携帯電話でリモート ワイプを実行する
ms:assetid: 67ba838e-031d-4a98-b277-170683b6f520
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998614(v=EXCHG.150)
ms:contentKeyID: 52057439
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 携帯電話でリモート ワイプを実行する

 

_**適用先:** Exchange Online, Exchange Server 2013_

ユーザーは、会社の機密情報をポケットに入れて毎日持ち歩いています。そのうちの 1 人が携帯電話を紛失すれば、データは他人の手に渡ってしまう可能性があります。ユーザーの 1 人が携帯電話を紛失した場合、Exchange 管理センター (EAC) または Exchange 管理シェルを使用して、その電話から会社とユーザーに関するすべての情報を完全に消去することができます。


> [!NOTE]
> ここでは、MicrosoftOutlook Web App を使用して電話に対してリモート ワイプを実行する手順についても説明します。リモート ワイプを実行するには、Outlook Web App にサインインする必要があります。



## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「モバイル デバイス」。

  - この手順では、インストールされているアプリケーション、写真、および個人情報を含む、携帯電話のすべてのデータが消去されます。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してユーザーの電話をワイプする

EAC を使用して、ユーザーの電話をワイプしたり、まだ完了していないリモート ワイプをキャンセルしたりできます。

1.  EAC で、<strong>受信者</strong> \> <strong>メールボックス</strong>に移動します。

2.  ユーザーを選択し、<strong>モバイル デバイス</strong> の <strong>詳細の表示</strong> を選択します。

3.  <strong>モバイル デバイスの詳細</strong> ページで、紛失したモバイル デバイスを選択して <strong>データのワイプ</strong> を選択します。

4.  <strong>保存</strong> を選択します。

## シェルを使用してユーザーの電話をワイプする

シェルで **Clear-MobileDevice** コマンドレットを使用して、ユーザーの電話をワイプできます。

次のコマンドは、WM\_TonySmith という名前のデバイスの内容を消去して、確認メッセージを admin@contoso.com に送信します。

    Clear-MobileDevice -Identity WM_TonySmith -NotificationEmailAddresses "admin@contoso.com"

## Outlook Web App を使用してユーザーの電話をワイプする

ユーザーは Outlook Web App を使用して自分の電話をワイプできます。

1.  Outlook Web App で、<strong>設定\] \> \[電話\] \> \[モバイル デバイス</strong> の順に選択します。

2.  携帯電話を選択します。

3.  <strong>デバイスのワイプ</strong> アイコンをクリックまたはタップします。

## 正常な動作を確認する方法

リモート ワイプが完了したことを確認する方法はいくつかあります。

  - *–NotificationEmailAddresses* パラメーターを構成して、**Clear-MobileDevice** コマンドレットを実行します。リモート ワイプが完了すると、指定された電子メール アドレスにメッセージが送信されます。

  - EAC でモバイル デバイスの状態を確認します。状態が <strong>ワイプ保留中</strong> から <strong>ワイプ成功</strong> に変わります。

  - Outlook Web App で、モバイル デバイスの状態を確認します。状態が <strong>ワイプ保留中</strong> から <strong>ワイプ成功</strong> に変わります。

