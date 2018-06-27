---
title: 'ジャーナル レポート復号化を有効または無効にする: Exchange 2013 Help'
TOCTitle: ジャーナル レポート復号化を有効または無効にする
ms:assetid: 1dedbe73-2c1a-4b14-8799-5091aaec7965
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd638092(v=EXCHG.150)
ms:contentKeyID: 49895282
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ジャーナル レポート復号化を有効または無効にする

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2016-12-09_

ジャーナル レポート復号を有効にすると、ジャーナリング エージェントが、権利が保護されたメッセージの解読コピーをジャーナル レポートに添付できます。ジャーナル レポートの復号を有効にする前に、[Active Directory Rights Management サービス (AD RMS)](https://technet.microsoft.com/ja-jp/library/hh831364.aspx) サーバーに構成されたスーパー ユーザー グループにフェデレーション配信用メールボックスを追加する必要があります。

Information Rights Management (IRM) に関連するその他の管理タスクについては、「[Information Rights Management の手順](information-rights-management-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「権限での保護」。

  - スーパー ユーザー グループのメンバーが AD RMS クラスターからライセンスを要求すると、そのメンバーには所有者使用ライセンスが付与されます。これにより、AD RMS クラスターによって作成された、RMS で保護されたすべてのコンテンツを解読できるようになります。

  - AD RMS クラスターが Active Directory フォレストにインストールされている必要があります。

  - フェデレーション配信メールボックスが AD RMS スーパー ユーザー グループに追加されている。詳細については、「[フェデレーション メールボックスを AD RMS のスーパー ユーザー グループに追加する](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)」を参照してください。

  - Exchange 管理センター (EAC) を使用して、ジャーナル レポート復号化を有効にすることはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用してジャーナル レポート復号を有効にする

この例では、Exchange 組織のジャーナル レポート復号を有効にします。

    Set-IRMConfiguration -JournalReportDecryptionEnabled $true

構文およびパラメーターの詳細については、「[Set-IRMConfiguration](https://technet.microsoft.com/ja-jp/library/dd979792\(v=exchg.150\))」を参照してください。

## シェルを使用してジャーナル レポート復号を無効にする

この例では、Exchange 組織のジャーナル レポート復号を無効にします。

    Set-IRMConfiguration -JournalReportDecryptionEnabled $false

構文およびパラメーターの詳細については、「[Set-IRMConfiguration](https://technet.microsoft.com/ja-jp/library/dd979792\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

ジャーナル レポート復号化が有効または無効になっていることを確認するには、**Get-IRMConfiguration** コマンドレットを実行して *JournalDecryptionEnabled* プロパティの値を確認します。

IRM 構成の確認方法の例については、「**Get-IRMConfiguration**」の「[Examples](https://technet.microsoft.com/ja-jp/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples)」を参照してください。

