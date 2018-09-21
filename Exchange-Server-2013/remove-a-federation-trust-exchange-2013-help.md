---
title: 'フェデレーション信頼の削除: Exchange 2013 Help'
TOCTitle: フェデレーション信頼の削除
ms:assetid: dc4d126d-b567-470d-a5d0-e1402bf8f369
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657500(v=EXCHG.150)
ms:contentKeyID: 49896510
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# フェデレーション信頼の削除

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-01-04_

フェデレーション信頼は Microsoft Exchange 2013 組織と Azure Active Directory 認証システムの間に信頼関係を確立し、他のフェデレーションされた Exchange 組織との共有をサポートしています。社内の Exchange 組織からフェデレーション信頼を削除すると、他の Exchange フェデレーション組織およびハイブリッド展開の一部として組織と接続される Office 365 組織とのフェデレーション共有が無効になります。フェデレーション信頼を削除する前に、組織に対する全体的な影響について考慮することをお勧めします。

フェデレーション信頼に関連する追加の管理タスクについては、「[フェデレーションの手順](federation-procedures-exchange-2013-help.md)」を参照してください。


> [!IMPORTANT]
> Exchange Server 2013 のこの機能は、中国で 21Vianet によって運用される Office 365 との完全な互換性を備えておらず、いくつかの機能制限が適用される場合があります。詳細については、「<A href="https://go.microsoft.com/fwlink/?linkid=313640">21Vianet が運用している Office 365 について</A>」を参照してください。



## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[Exchange およびシェル インフラストラクチャのアクセス許可](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)」の「フェデレーションと証明書のアクセス許可」。

  - フェデレーション信頼を削除した後には、各フェデレーション ドメインのパブリック DNS サーバーから TXT レコードを削除できます。パブリック DNS レコードをホストする組織による TXT レコードを削除するための要件を確認してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

## 必要な作業

## EAC を使用してフェデレーション信頼を削除する

1.  社内組織の Exchange 2013 サーバーで、<strong>組織</strong> \> <strong>共有</strong> に移動します。

2.  <strong>フェデレーション信頼</strong> セクションで、<strong>削除</strong> をクリックします。

3.  警告で <strong>はい</strong> をクリックして、フェデレーション信頼の削除を確認します。

4.  フェデレーション信頼が削除されたら、<strong>閉じる</strong> をクリックします。

## シェルを使用してフェデレーション信頼を削除する

この例では、フェデレーション信頼を削除します。

```powershell
Remove-FederationTrust
```

構文およびパラメーターの詳細については、「[Remove-FederationTrust](https://technet.microsoft.com/ja-jp/library/dd351153\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

フェデレーション信頼が正常に削除されたことを確認するには、次のいずれかの手順を実行します。

  - EAC で、<strong>組織</strong> \> <strong>共有</strong>に移動します。フェデレーション信頼が正常に削除された場合は、<strong>フェデレーション信頼</strong> の <strong>有効にする</strong> ボタンのみが使用可能になります。

  - シェルで次のコマンドを実行して、フェデレーション信頼の情報が Exchange 組織に返されないことを確認します。
    
    ```powershell
Get-FederationTrust
```
    
    構文およびパラメーターの詳細については、「[Get-FederationTrust](https://technet.microsoft.com/ja-jp/library/dd351262\(v=exchg.150\))」を参照してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

