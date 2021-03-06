﻿---
title: 'デジタル証明書の要求を作成する: Exchange 2013 Help'
TOCTitle: デジタル証明書の要求を作成する
ms:assetid: efb00de7-070b-46bf-a2fc-00d07ae085c1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb125165(v=EXCHG.150)
ms:contentKeyID: 52057872
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# デジタル証明書の要求を作成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2013-02-21_

Exchange Server 2013 では、EAC またはシェルを使用して証明書を管理できます。EAC には新しい証明書管理ユーザー インターフェイスが含まれています。この新しい UI を通じて、新しい証明書の作成、既存の証明書の編集、または証明書の削除を実行できます。

## 始める前に把握しておくべき情報

  - 予想所要時間: 10 分に、証明機関からの応答時間を合わせた時間。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「クライアント アクセス サーバーのセキュリティ」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して新しい証明書要求を作成する

1.  EAC で、<strong>サーバー</strong> \> <strong>証明書</strong> の順に移動します。

2.  <strong>サーバーの選択</strong> リストで、証明書を作成するサーバーを選択し、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

3.  <strong>Exchange 証明書の新規作成</strong> ウィザードで、<strong>証明機関からの証明書の要求を作成する</strong> または <strong>自己署名証明書を作成する</strong> のいずれかを選択し、<strong>次へ</strong> をクリックします。

4.  証明書のフレンドリ名を入力し、<strong>次へ</strong> を選択します。

5.  自己署名証明書を選択せず、ワイルドカード証明書を希望する場合は、<strong>ワイルドカード証明書を要求する</strong> チェックボックスをオンにし、ルート ドメイン (\*.contoso.com など) を入力して、<strong>次へ</strong> を選択します。自己署名証明書を選択した場合は、この手順をスキップします。

6.  この証明書を適用するサーバーを選択し、<strong>次へ</strong> を選択します。

7.  証明書に含めるドメインを指定し、<strong>次へ</strong> を選択します。

8.  含まれたドメインが正しいことを確認します。自己署名証明書を選択した場合は、<strong>完了</strong> を選択します。それ以外の場合は、<strong>次へ</strong> を選択します。

9.  組織名、部門名、市区町村、都道府県、および国または地域を入力し、<strong>次へ</strong> を選択します。

10. 証明書の要求を保存する場所を入力し、<strong>完了</strong> を選択します。

自己署名証明書を選択しなかった場合は、証明書要求ファイルを証明機関に送信して処理してもらう必要があります。

## シェルを使用して新しい証明書要求を作成する

次のコマンドを実行します。
  
  ```powershell
  $reqfile = New-ExchangeCertificate -GenerateRequest -SubjectName "C=US,o=Contoso,cn=contosotocert" -DomainName "contoso.com" -PrivateKeyExportable $true
  ```
  ```powershell
  $reqfile | out-file c:\certreq.txt
  ```

## 正常な動作を確認する方法

自己署名証明書を作成した場合は、新たに作成した証明書が証明書管理 UI に表示されます。証明機関からの証明書要求を作成した場合は、指定した場所に証明書要求ファイルが格納されます。このファイルを証明機関に送信します。

