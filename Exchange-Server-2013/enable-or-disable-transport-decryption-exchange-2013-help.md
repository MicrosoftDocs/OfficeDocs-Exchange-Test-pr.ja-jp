---
title: 'トランスポート解読を有効または無効にする: Exchange 2013 Help'
TOCTitle: トランスポート解読を有効または無効にする
ms:assetid: 4663f54e-dd0a-4a42-983e-8765e2adc412
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd638126(v=EXCHG.150)
ms:contentKeyID: 49896229
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# トランスポート解読を有効または無効にする

 

_**適用先:**Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:**2016-12-09_

トランスポート復号化を有効にすると、Microsoft Exchange Server 2013 メールボックス サーバー上のトランスポート ルール エージェントが、Information Rights Management (IRM) で保護されたメッセージ内のコンテンツにアクセスできるようになります。結果として、他のトランスポート エージェントがメッセージ コンテンツにアクセスして、変更を行う可能性があります。たとえば、トランスポート ルール エージェントは、メッセージ コンテンツを検査し、トランスポート ルール (免責条項をメッセージに適用するルールなど) を適用する必要がある場合があります。IRM で保護されたメッセージを正常に復号化するには、[Active Directory Rights Management サービス (AD RMS)](https://technet.microsoft.com/ja-jp/library/hh831364.aspx) サーバー上で構成されているスーパー ユーザー グループにフェデレーション配信メールボックスを追加する必要があります。


> [!IMPORTANT]
> スーパー ユーザー グループのメンバーが AD&nbsp;RMS クラスターからライセンスを要求すると、そのメンバーには所有者使用ライセンスが付与されます。これにより、AD&nbsp;RMS クラスターによって作成された、RMS で保護されたすべてのコンテンツを解読できるようになります。



トランスポート復号化を有効にする場合、次の設定を指定できます。

  - **必須**   復号化できないメッセージを拒否し、配信不能レポート (NDR) を送信者に返します。

  - **省略可能**   復号化にベストエフォート アプローチを使用します。メッセージは可能なら復号化し、復号化が失敗しても配信します。これは既定の設定です。

トランスポート復号化の詳細については、「[トランスポート復号化](transport-decryption-exchange-2013-help.md)」を参照してください。

IRM に関連する追加の管理タスクについては、「[Information Rights Management の手順](information-rights-management-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「権限での保護」。

  - AD RMS サーバーは、Active Directory フォレスト内に存在し、アクセス可能です。

  - フェデレーション配信メールボックスが AD RMS スーパー ユーザー グループに追加されている。詳細については、「[フェデレーション メールボックスを AD RMS のスーパー ユーザー グループに追加する](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)」を参照してください。

  - Exchange 管理センター (EAC) を使用してトランスポート復号化を有効にすることはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用してトランスポート復号化を有効にする

この例では、Exchange 2013 組織のトランスポート復号化を有効にします。復号化できないメッセージは拒否され、サーバーに NDR が返されます。

    Set-IRMConfiguration -TransportDecryptionSetting Mandatory

構文およびパラメーターの詳細については、「[Set-IRMConfiguration](https://technet.microsoft.com/ja-jp/library/dd979792\(v=exchg.150\))」を参照してください。

## シェルを使用してトランスポート復号化を無効にする

この例では、Exchange 2013 組織のトランスポート復号化を無効にします。

    Set-IRMConfiguration -TransportDecryptionSetting Disabled

構文およびパラメーターの詳細については、「[Set-IRMConfiguration](https://technet.microsoft.com/ja-jp/library/dd979792\(v=exchg.150\))」を参照してください。

## 設定が適用されたことを確認する方法

トランスポート復号化が有効または無効になっていることを確認するには、**Get-IRMConfiguration** コマンドレットを使用して、*JournalDecryptionEnabled* プロパティの値を確認します。

IRM 構成の確認方法の例については、「**Get-IRMConfiguration**」の「[Examples](https://technet.microsoft.com/ja-jp/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples)」を参照してください。

