---
title: 'サイト メールボックスのプロビジョニング ポリシーの管理: Exchange 2013 Help'
TOCTitle: サイト メールボックスのプロビジョニング ポリシーの管理
ms:assetid: 2f160d1a-a031-461f-8d29-c9cd49ca1645
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ710340(v=EXCHG.150)
ms:contentKeyID: 49896196
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# サイト メールボックスのプロビジョニング ポリシーの管理

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2013-02-21_

サイト メールボックス プロビジョニング ポリシーが適用されるのは、サイト メールボックスに対して送受信されるメールと Exchange サーバー上のサイト メールボックスのサイズだけです。

サイト メールボックスの詳細については、「[サイト メールボックス](site-mailboxes-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[共有とコラボレーションのアクセス許可](sharing-and-collaboration-permissions-exchange-2013-help.md)」の「サイト メールボックス」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

  - サイト メールボックス プロビジョニング ポリシーは複数作成できますが、すべてのサイト メールボックスに適用されるのは既定のプロビジョニング ポリシーだけです。組織内で複数のポリシーを適用することはできません。

  - Exchange 管理センター (EAC) を使用してこの手順を実行することはできません。シェルを使用する必要があります。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## サイト メールボックス プロビジョニング ポリシーを作成する

この例では、既定のプロビジョニング ポリシー SM\_ProvisioningPolicy を以下の設定で作成します。

  - このサイト メールボックスの警告クォータは 9 GB です。

  - サイト メールボックスは、メールボックス サイズが 10 GB に到達した時点で、メッセージを受信できなくなります。

  - サイト メールボックスに送信できる電子メール メッセージの最大サイズは 50 MB です。

<!-- end list -->

```powershell
New-SiteMailboxProvisioningPolicy -Name SM_ProvisioningPolicy -IsDefault -IssueWarningQuota 9GB -ProhibitSendReceiveQuota 10GB -MaxReceiveSize 50MB
```

## サイト メールボックス プロビジョニング ポリシーの設定を表示する

この例では、組織内のすべてのサイト メールボックスのプロビジョニング ポリシーに関する詳細情報が返されます。

```powershell
Get-SiteMailboxProvisioningPolicy | Format-List
```

この例では組織のすべてのポリシーが返されますが、どのポリシーが既定のポリシーであるかを特定する `IsDefault` 情報のみが表示されます。

```powershell
Get-SiteMailboxProvisioningPolicy | Format-List IsDefault
```

## 既存のサイト メールボックス プロビジョニング ポリシーを変更する

この例では、Default という名前のサイト メールボックス プロビジョニング ポリシーを変更して、サイト メールボックスが受信できる電子メール メッセージの最大サイズを 25 MB にします。(Exchange のインストール時に、**Default** という名前のプロビジョニング ポリシーが生成されます。)

```powershell
Set-SiteMailboxProvisioningPolicy -Identity Default -MaxReceiveSize 25MB
```

この例では、警告表示クォータを 9.5 GB、送受信禁止クォータを 10 GB に変更します。

```powershell
Set-SiteMailboxProvisioningPolicy -Identity Default -IssueWarningQuota 9GB -ProhibitSendReceiveQuota 10GB
```

## サイト メールボックス名のプレフィックスを構成する

新しいサイト メールボックスを作成すると、既定ではその電子メール アドレスにプレフィックスが付きます。電子メール アドレスのプレフィックスにより、サイト メールボックスの検索と照会が容易になり、サイト メールボックスを認識できるようになります。必要に応じてプレフィックスを無効にしたり、Office 365 のテナントまたは社内展開の特定フォレスト用にプレフィックスを変更したりできます。既定のプレフィックスの動作では、サイト メールボックスを Office 365 で作成した場合、既定のプレフィックスは **SMO-** になります。一方、サイト メールボックスを社内展開で作成した場合、プレフィックスは **SM-** になります。既定の動作はこの前提により異なるため、サイト メールボックスを両方の場所で作成してから社内全体で同期しても、ハイブリッド環境で矛盾が発生することはありません。

この例では *DefaultAliasPrefixEnabled* パラメーターを $false に設定し、プレフィックスが付けられないようにします。

```powershell
Set-SiteMailboxProvisioningPolicy -Identity Default -DefaultAliasPrefixEnabled $false -AliasPrefix $null
```

この例では既定のプロビジョニング ポリシーを変更し、*AliasPrefix* を FOREST01 に設定します。


> [!NOTE]
> フォレストが複数ある展開では、複数のフォレストで同じ名前を使用してサイト メールボックスを作成しても、フォレスト間でオブジェクトを同期したときの矛盾を回避できるよう、各フォレストに別のプレフィックスを使用することをお勧めします。



```powershell
Set-SiteMailboxProvisioningPolicy -Identity Default -AliasPrefix FOREST01 -DefaultAliasPrefixEnabled $false
```


> [!NOTE]
> 社内と Office 365 に Exchange があるハイブリッド展開の場合、すべてのクラウドベースのサイト メールボックスはプレフィックス <STRONG>SMO-</STRONG> を付けて作成されます。Office 365 と社内 Exchange ではプレフィックスが異なるため、サイト メールボックスを両方の場所で作成してから社内全体で同期しても、ハイブリッド環境で矛盾が発生することはありません。また、AliasPrefix パラメーターは DefaultAliasPrefixEnabled パラメーターより優先されるため、<EM>AliasPrefix</EM> パラメーターを NULL 以外の有効な文字列に設定した場合、新しい各サイト メールボックスのエイリアスの先頭にはその文字列が付きます。



## サイト メールボックス プロビジョニング ポリシーを削除する

この例では、Exchange のセットアップ時に生成された既定のサイト メールボックス ポリシーを削除します。

```powershell
Remove-SiteMailboxProvisioningPolicy -Identity Default
```


> [!IMPORTANT]
> <STRONG>Default</STRONG> という名前のポリシーを削除する前に、別の既定のポリシーを作成して指定する必要があります。



## 詳細情報

構文およびパラメーターの詳細については、以下のトピックを参照してください。

[New-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/ja-jp/library/jj218647\(v=exchg.150\))

[Get-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/ja-jp/library/jj218617\(v=exchg.150\))

[Set-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/ja-jp/library/jj218624\(v=exchg.150\))

[Remove-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/ja-jp/library/jj218672\(v=exchg.150\))

