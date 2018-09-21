---
title: '内部メッセージの IRM を有効または無効にする: Exchange 2013 Help'
TOCTitle: 内部メッセージの IRM を有効または無効にする
ms:assetid: a6a17f57-5304-41f1-954d-7301857d54a1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124077(v=EXCHG.150)
ms:contentKeyID: 49896398
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 内部メッセージの IRM を有効または無効にする

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-12_

Microsoft Exchange Server 2013 では、内部メッセージの Information Rights Management (IRM) は既定で有効になっています。 これによって、トランスポート保護ルールと Microsoft Outlook 保護ルールを作成し、送信中のメッセージと Microsoft Outlook 2010 以降のクライアント上のメッセージを IRM で保護することができます。内部メッセージの IRM を有効にすることは、トランスポート解読、ジャーナル ルール解読、Microsoft Exchange Server 2013 Office の IRM、Microsoft Outlook Web App の IRM など、Exchange ActiveSync の他のすべての IRM 機能に対する前提条件です。


> [!NOTE]
> 内部メッセージの IRM を無効にすると、Exchange 組織内の IRM 機能がすべて無効になります。 Outlook のクライアントサイドの IRM 機能 (例えば、Active Directory Rights Management サービス (AD RMS) サーバーを使用して IRM で保護されたメッセージの読み込み、返信、転送、作成を行う機能) は影響を受けません。



IRM に関連する追加の管理タスクについては、「[Information Rights Management の手順](information-rights-management-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「権限での保護」。

  - Exchange 管理センター (EAC) を使用して、内部メッセージの IRM を有効または無効にすることはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用して内部メッセージの IRM を有効にする

この例では、Exchange 組織の内部メッセージの IRM を有効にします。

```powershell
Set-IRMConfiguration -InternalLicensingEnabled $true
```

構文およびパラメーターの詳細については、「[Set-IRMConfiguration](https://technet.microsoft.com/ja-jp/library/dd979792\(v=exchg.150\))」を参照してください。

## シェルを使用して内部メッセージの IRM を無効にする

この例では、Exchange 組織の内部メッセージの IRM を無効にします。

```powershell
Set-IRMConfiguration -InternalLicensingEnabled $false
```

構文およびパラメーターの詳細については、「[Set-IRMConfiguration](https://technet.microsoft.com/ja-jp/library/dd979792\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

内部メッセージの IRM を有効または無効にしたことを確認するには、[Get-IRMConfiguration](https://technet.microsoft.com/ja-jp/library/dd776120\(v=exchg.150\)) コマンドレットを使用して構成を確認します。

