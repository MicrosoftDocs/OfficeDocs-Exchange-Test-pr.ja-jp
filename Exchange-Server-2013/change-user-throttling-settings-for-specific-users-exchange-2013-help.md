---
title: '特定のユーザーのユーザー調整設定を変更する: Exchange 2013 Help'
TOCTitle: 特定のユーザーのユーザー調整設定を変更する
ms:assetid: c5f834d6-189d-485e-9800-5e0066815ecf
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ863577(v=EXCHG.150)
ms:contentKeyID: 50555871
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 特定のユーザーのユーザー調整設定を変更する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-08-05_

既定の調整設定を変更することにより、Exchange 組織の個々のユーザーによるリソースの消費状況を制御できます。

個々のユーザーによるリソースの消費状況を制御する方法は Exchange Server 2010 で可能であり、この機能は拡張して Exchange Server 2013 にも適用されています。調整ポリシーをカスタマイズしない限り、GlobalThrottlingPolicy という名前のポリシーにより、組織のすべての新しいユーザーまたは既存のユーザーに対する既定の調整設定が定義されます。多くの標準的な Exchange 展開シナリオでは、GlobalThrottlingPolicy という名前のポリシーでユーザー管理に十分対応できます。

組織内の特定のユーザーだけに適用する調整設定をカスタマイズするには、スコープの割り当てを Regular にして新しい調整ポリシーを作成します。シェルを使用する場合は、既定のスロットル調整設定のみを変更できます。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 10 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[サーバーの状態とパフォーマンスのアクセス許可](server-health-and-performance-permissions-exchange-2013-help.md)」の「ユーザー調整」。

  - 新しい正規スコープ ポリシーでは、GlobalThrottlingPolicy という名前のポリシーと、その他すべての組織ポリシーの調整設定と異なる調整設定だけを設定してください。これにより、将来的な Exchange の更新において追加される調整ポリシーに対するすべての更新と同様に、GlobalThrottlingPolicy という名前のポリシーからの残りのポリシー設定が継承されます。次の手順に従う前に、「[Exchange ワークロード管理](exchange-workload-management-exchange-2013-help.md)」の「スコープを使用して調整ポリシーを管理する」を参照することをお勧めします。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## シェルを使用して、組織全体の特定のユーザーによるリソースの使用方法を変更する

この例では、特定のユーザーに関連付けることができる ITStaffPolicy という名前の既定以外のユーザー調整ポリシーを作成します。省略するパラメーターはすべて、既定の調整ポリシーの GlobalThrottlingPolicy から値を継承します。このポリシーは、作成後に特定のユーザーに関連付ける必要があります。

    New-ThrottlingPolicy -Name ITStaffPolicy -EwsMaxConcurrency 4 -ThrottlingPolicyScope Regular

この例では、ユーザー名が tonysmith のユーザーを (より上限の高い) 調整ポリシー ITStaffPolicy に関連付けます。

    Set-ThrottlingPolicyAssociation -Identity tonysmith -ThrottlingPolicy ITStaffPolicy

ユーザーとポリシーの関連付けに **Set-ThrottlingPolicyAssociation** コマンドレットを使用する必要はありません。次のコマンドは、tonysmith を調整ポリシー ITStaffPolicy に関連付ける別の方法を表します。
```
$b = Get-ThrottlingPolicy ITStaffPolicy
```
```
Set-Mailbox -Identity tonysmith -ThrottlingPolicy $b
```

構文およびパラメーターの詳細については、「[New-ThrottlingPolicy](https://technet.microsoft.com/ja-jp/library/dd351045\(v=exchg.150\))」と「[Set-ThrottlingPolicyAssociation](https://technet.microsoft.com/ja-jp/library/ff459231\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

正規調整ポリシーが正常に作成されたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
        Get-ThrottlingPolicy | Format-List

2.  作成したばかりの正規調整ポリシーが、GlobalThrottlingPolicy を示す列に表示されていることを確認します。

3.  次のコマンドを実行します。
    
        Get-ThrottlingPolicy | Format-List

4.  新しい正規ポリシーのプロパティが構成した値と一致していることを確認します。

5.  次のコマンドを実行します。
    
        Get-ThrottlingPolicyAssociation

6.  新しい正規ポリシーが、関連付けを行った目的のユーザーに関連付けられていることを確認します。

