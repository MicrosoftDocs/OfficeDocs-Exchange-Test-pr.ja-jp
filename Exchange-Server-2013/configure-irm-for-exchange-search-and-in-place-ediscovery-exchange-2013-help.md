---
title: 'Exchange 検索およびインプレース電子情報開示のための IRM の構成: Exchange 2013 Help'
TOCTitle: Exchange 検索およびインプレース電子情報開示のための IRM の構成
ms:assetid: d96790e9-93ad-4a56-b90f-2dbfa2f2073c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg588319(v=EXCHG.150)
ms:contentKeyID: 49896505
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 検索およびインプレース電子情報開示のための IRM の構成

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-11-16_

Microsoft Exchange Server 2013 では、Exchange Search が IRM 保護メッセージをインデックス処理できるように Information Rights Management (IRM) を構成できます。

"Discovery Management/検出の管理" 役割グループのメンバーが [インプレース電子情報開示 (eDiscovery)](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery) 検索を実行すると、IRM 保護メッセージが検索結果に返され、検索で指定された探索メールボックスにコピーされます。さらに、"Discovery Management/検出の管理" 役割グループのメンバーは Outlook Web App を使用して、探索検索の結果として探索メールボックスにコピーされた IRM 保護メッセージにアクセスできます。


> [!NOTE]
> "Discovery Management/検出の管理" 役割グループのメンバーは、探索メールボックスから別のメールボックスまたは .pst ファイルにエクスポートされた IRM 保護メッセージにはアクセスできません。探索メールボックス内の IRM 保護メッセージは、Outlook Web App を使用してのみアクセスできます。



IRM に関連する追加の管理タスクについては、「[Information Rights Management の手順](information-rights-management-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 推定完了時間: 1 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「権限での保護」。

  - IRM が Exchange 2013 組織で構成されている必要があります。詳細については、「[内部メッセージの IRM を有効または無効にする](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md)」を参照してください。

  - フェデレーション メールボックスが Active Directory Rights Management Services (AD RMS) スーパー ユーザー グループに追加されている必要があります。詳細については、「[フェデレーション メールボックスを AD RMS のスーパー ユーザー グループに追加する](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)」を参照してください。

  - Exchange 管理センター (EAC) を使用して、Exchange 検索およびインプレース電子証拠開示の IRM を構成することはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用して Exchange Search の IRM を構成する

この例では、Exchange Search が IRM 保護メッセージをインデックス処理できるように IRM を構成します。


> [!NOTE]
> 既定では、<EM>SearchEnabled</EM> パラメーターは <CODE>$true</CODE> に設定されます。IRM 保護メッセージのインデックス処理を無効にするには、<CODE>$false</CODE> に設定します。IRM 保護メッセージのインデックス処理を無効にすることにより、ユーザーが自分のメールボックスを検索する場合、または検出マネージャーがインプレース電子証拠開示を使用する場合に、IRM 保護メッセージが検索結果に返されることを防ぎます。



```powershell
Set-IRMConfiguration -SearchEnabled $true
```

構文およびパラメーターの詳細については、「[Set-IRMConfiguration](https://technet.microsoft.com/ja-jp/library/dd979792\(v=exchg.150\))」を参照してください。

## シェルを使用してインプレース電子証拠開示の IRM を構成する

この例では、"Discovery Management/検出の管理" 役割グループのメンバーが、検出メールボックス内の IRM 保護メッセージにアクセスできるようにします。


> [!NOTE]
> 既定では、<EM>EDiscoverySuperUserEnabled</EM> パラメーターは <CODE>$true</CODE> に設定されます。"Discovery Management/検出の管理" 役割グループのメンバーによる IRM 保護メッセージへのアクセスを無効にするには、<CODE>$false</CODE> に設定します。



```powershell
Set-IRMConfiguration -EDiscoverySuperUserEnabled $true
```

構文およびパラメーターの詳細については、「[Set-IRMConfiguration](https://technet.microsoft.com/ja-jp/library/dd979792\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

Exchange 検索およびインプレース電子証拠開示の IRM が正常に構成されたことを確認するには、**Get-IRMConfigurtaion** コマンドレットを使用して IRM 構成情報を取得します。IRM 構成を取得する方法の例については、**Get-IRMConfiguration** の「[Examples](https://technet.microsoft.com/ja-jp/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples)」を参照してください。

