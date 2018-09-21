---
title: '組織内のすべてのユーザーのユーザー調整設定を変更する: Exchange 2013 Help'
TOCTitle: 組織内のすべてのユーザーのユーザー調整設定を変更する
ms:assetid: c45cacfc-768d-4605-9bb0-53e30273fe4d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ863578(v=EXCHG.150)
ms:contentKeyID: 50555868
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 組織内のすべてのユーザーのユーザー調整設定を変更する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-08-05_

既定の調整設定を変更することにより、Exchange 組織の個々のユーザーによるリソースの消費状況を制御できます。

個々のユーザーによるリソースの消費状況を制御する方法は Exchange Server 2010 で可能であり、この機能は拡張して Exchange Server 2013 にも適用されています。調整ポリシーをカスタマイズしない限り、GlobalThrottlingPolicy という名前のポリシーにより、組織のすべての新しいユーザーまたは既存のユーザーに対する既定の調整設定が定義されます。多くの標準的な Exchange 展開シナリオでは、GlobalThrottlingPolicy という名前のポリシーでユーザー管理に十分対応できます。

組織内のすべてのユーザーに適用する調整設定をカスタマイズするには、スコープの割り当てを Organization にして新しい調整ポリシーを作成します。シェルを使用する場合は、既定のスロットル調整設定のみを変更できます。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 10 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[サーバーの状態とパフォーマンスのアクセス許可](server-health-and-performance-permissions-exchange-2013-help.md)」の「ユーザー調整」。

  - 新しい組織スコープ ポリシーでは、GlobalThrottlingPolicy という名前のポリシーと、その他すべての組織ポリシーの調整設定と異なる調整設定だけを設定してください。これにより、将来的な Exchange の更新において追加される調整ポリシーに対するすべての更新と同様に、GlobalThrottlingPolicy という名前のポリシーからの残りのポリシー設定が継承されます。次の手順に従う前に、「[Exchange ワークロード管理](exchange-workload-management-exchange-2013-help.md)」の「スコープを使用して調整ポリシーを管理する」を参照することをお勧めします。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## シェルを使用して、組織全体のすべてのユーザーによるリソースの使用方法を変更する

この例では、組織内のすべてのユーザーに適用される調整ポリシーを作成します。省略するパラメーターはすべて、既定の調整ポリシーの GlobalThrottlingPolicy から値を継承します。

```powershell
New-ThrottlingPolicy -Name AllUsersEWSPolicy EwsMaxConcurrency 4 -ThrottlingPolicyScope Organization
```

構文およびパラメーターの詳細については、「[New-ThrottlingPolicy](https://technet.microsoft.com/ja-jp/library/dd351045\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

組織調整ポリシーが正常に作成されたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
    ```powershell
Get-ThrottlingPolicy | Format-List
```

2.  作成したばかりの組織調整ポリシーが、GlobalThrottlingPolicy を示す列に表示されていることを確認します。

3.  次のコマンドを実行します。
    
    ```powershell
Get-ThrottlingPolicy | Format-List
```

4.  新しい組織ポリシーのプロパティが構成した値と一致していることを確認します。

