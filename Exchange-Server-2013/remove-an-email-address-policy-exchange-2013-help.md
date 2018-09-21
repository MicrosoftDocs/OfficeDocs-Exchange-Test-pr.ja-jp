---
title: '電子メール アドレス ポリシーの削除: Exchange 2013 Help'
TOCTitle: 電子メール アドレス ポリシーの削除
ms:assetid: f1d05223-7d41-406d-8fae-f4227be1c1c2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb125181(v=EXCHG.150)
ms:contentKeyID: 49896549
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 電子メール アドレス ポリシーの削除

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-13_

既定で、Exchange には、電子メール アドレスのローカル部分として受信者のエイリアスを指定し、既定の承認済みドメインを使用する電子メール アドレス ポリシーがあります。 電子メール アドレスのローカル部分は、アットマーク (@) より前の名前です。この電子メール アドレス ポリシーは、組織内のすべてのユーザーに適用されます。 この電子メール アドレス ポリシーは削除できません。

電子メール アドレス ポリシーに関連する追加の管理タスクについては、「[電子メール アドレス ポリシーの手順](email-address-policy-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - 受信者がプライマリ ポリシーとして使用している電子メール アドレス ポリシーを削除すると、受信者に対して他のポリシーが構成されていない場合、既定のポリシーが使用されます。

  - 既定のポリシーは削除できません。 既定のポリシーを削除する場合は、まず別のポリシーを既定のポリシーとして割り当てる必要があります。

  - 削除する電子メール アドレス ポリシーに 3,000 を超える受信者が含まれている場合、この手順はシェルを使用して行う必要があります。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[電子メール アドレスとアドレス帳](email-addresses-and-address-books-exchange-2013-help.md)」の「電子メール アドレス ポリシー」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!WARNING]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EAC を使用して、電子メール アドレス ポリシーを削除する

1.  <strong>メール フロー</strong> \> <strong>Email address policies (電子メール アドレス ポリシー)</strong> に移動します。

2.  リスト ビューで、削除する電子メール アドレス ポリシーを選択し、<strong>削除</strong>![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") をクリックします。

3.  警告が表示されたら、<strong>はい</strong> をクリックしてポリシーを削除します。

## シェルを使用して、電子メール アドレス ポリシーを削除する

この例では、電子メール アドレス ポリシー South East Offices を削除します。

```powershell
Remove-EmailAddressPolicy -Identity "South East Offices"
```

「**Y**」と入力してポリシーの削除を確認し、Enter キーを押します。

構文およびパラメーターの詳細については、「[Remove-EmailAddressPolicy](https://technet.microsoft.com/ja-jp/library/bb124504\(v=exchg.150\))」を参照してください。

