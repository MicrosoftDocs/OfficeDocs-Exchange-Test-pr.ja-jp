---
title: '詳細テンプレートを既定の構成に復元する: Exchange 2013 Help'
TOCTitle: 詳細テンプレートを既定の構成に復元する
ms:assetid: 84c5f49b-614d-4f0e-8701-0979a2eb90bf
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb232102(v=EXCHG.150)
ms:contentKeyID: 49896342
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 詳細テンプレートを既定の構成に復元する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-12_

詳細テンプレート エディターには、<strong>元に戻す</strong> ボタンがなく、操作を元に戻すためのショートカット キーを使用することもできません。 テンプレートへの追加を元に戻すには、Delete キーを使用する必要があります。 削除を元に戻すには、設定を再度適用する必要があります。 また、変更を保存しないで詳細テンプレート エディターを終了することにより、元の設定に戻すことができます。 保存した後に変更を元に戻す場合は、テンプレートを復元することができます。 テンプレートを復元すると、すべてのカスタマイズ設定は失われ、テンプレートは元の構成に復元されます。

ここでは、Exchange 2013 ツールボックスまたは Exchange 管理シェルを使用して、詳細テンプレートを既定の構成に復元する方法について説明します。

詳細テンプレートの詳細については、「[詳細テンプレート](details-templates-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[電子メール アドレスおよびアドレス帳のアクセス許可](email-address-and-address-book-permissions-exchange-2013-help.md)」の「詳細テンプレート」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## Exchange ツールボックスを使用して詳細テンプレートを既定の構成に復元する

1.  <strong>スタート</strong> \> <strong>すべてのプログラム</strong> \> <strong>Microsoft Exchange Server 2013</strong> \> <strong>Exchange ツールボックス</strong> の順にクリックします。

2.  <strong>Exchange ツールボックス</strong> で、<strong>詳細テンプレート エディター</strong> をクリックしてから、操作ウィンドウで <strong>ツールを開く</strong> をクリックします。

3.  <strong>詳細テンプレート エディター</strong> の詳細ウィンドウで、復元するテンプレートを右クリックし、操作ウィンドウで <strong>復元</strong> をクリックします。

4.  <strong>はい</strong> をクリックして、このテンプレートを元の状態に復元することを確認します。 カスタマイズした内容はすべて失われます。

## シェルを使用して詳細テンプレートを既定の構成に復元する

この例では、英語 (米国) の連絡先の詳細テンプレートを復元します。

    Restore-DetailsTemplate -Identity "en-US\Contact"

構文およびパラメーターの詳細については、「[Restore-DetailsTemplate](https://technet.microsoft.com/ja-jp/library/bb125188\(v=exchg.150\))」を参照してください。

