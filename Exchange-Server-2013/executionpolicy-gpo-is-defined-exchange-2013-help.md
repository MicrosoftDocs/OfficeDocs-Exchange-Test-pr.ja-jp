---
title: 'ExecutionPolicy GPO が定義されている: Exchange 2013 Help'
TOCTitle: ExecutionPolicy GPO が定義されている
ms:assetid: 63de83e2-9a6b-4f57-85b9-df445bea18dd
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.powershellexecutionpolicycheckset(v=EXCHG.150)
ms:contentKeyID: 61204839
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ExecutionPolicy GPO が定義されている

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2016-12-15_

**ExecutionPolicy** グループ ポリシー オブジェクト (GPO) で以下のポリシーのいずれか、または両方が定義されていることが検出されたため、Microsoft Exchange Server 2013 のセットアップを続行できません。

  - **MachinePolicy**

  - **UserPolicy**

ポリシーがどのように定義されているかは関係ありません。定義されていることだけが問題です。

Exchange 2013 のセットアップを実行すると、Exchange が停止し、Windows 管理インストルメンテーション (WMI) サービスが無効になります。これらのポリシーのいずれかが定義されている場合、Windows PowerShell スクリプトを実行するには、WMI サービスが有効になっている必要があります。ポリシーが定義されていて、WMI サービスが停止されると、セットアップが失敗し、サーバーは不整合状態のままになります。

セットアップを続行できるようにするには、**ExecutionPolicy** GPO の**MachinePolicy** または **UserPolicy** の定義を一時的に除去する必要があります。

**ExecutionPolicy** GPO の**MachinePolicy** または **UserPolicy** の定義を除去する方法については、「[Microsoft サポート技術情報の文書番号 KB981474](https://go.microsoft.com/fwlink/?linkid=3052&kbid=981474)」を参照してください。


> [!NOTE]
> このサポート技術情報の文書は Exchange 2010 を対象に作成されていますが、Exchange 2013 の累積更新および Service Pack にも適用されます。



問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

探しているものは見つかりましたか？検索したい情報に関する[フィードバックを送信](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback)してください。

