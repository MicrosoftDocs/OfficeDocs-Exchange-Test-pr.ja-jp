---
title: 'DNS データベースにローカル コンピューターのホスト レコードが見つからない: Exchange 2013 Help'
TOCTitle: DNS データベースにローカル コンピューターのホスト レコードが見つからない
ms:assetid: 2f18cb65-29fe-4b72-8d68-52fd503d5673
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.hostrecordmissing(v=EXCHG.150)
ms:contentKeyID: 48269324
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# DNS データベースにローカル コンピューターのホスト レコードが見つからない

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2016-12-09_

ドメイン ネーム システム (DNS) データベースにこのコンピューターのホスト (A) レコードが見つからないため、Microsoft Exchange Server 2013 セットアップ プログラムを続行できません。

Exchange 2013 セットアップ プログラムを実行するには、ローカル コンピューターの有効なホスト (A) レコードが、ドメインに対して権限のある DNS データベースに登録されている必要があります。

Exchange は、内部または外部にある次の送信先サーバーの IP アドレスを解決するために DNS ホスト (A) レコードを使用します。

この問題を解決するには

  - ローカルの TCP/IP 構成が正しい DNS サーバーを示していることを確認します。詳細については、「[TCP/IP 設定を構成する](https://go.microsoft.com/fwlink/p/?linkid=108281)」を参照してください。

  - Nslookup.exe を使用して、DNS サーバーにホスト (A) レコードが存在することを確認します。詳細については、「[A リソース レコードが DNS 内に存在することを確認するには](https://go.microsoft.com/fwlink/?linkid=63001)」を参照してください。

DNS の名前解決、トラブルシューティング、およびホスト (A) レコードの詳細については、以下の文書を参照してください。

  - [DNS のトラブルシューティング](https://go.microsoft.com/fwlink/p/?linkid=294828)

  - [リソース レコードを管理する](https://go.microsoft.com/fwlink/p/?linkid=294829)

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

探しているものは見つかりましたか？検索したい情報に関する[フィードバックを送信](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback)してください。

