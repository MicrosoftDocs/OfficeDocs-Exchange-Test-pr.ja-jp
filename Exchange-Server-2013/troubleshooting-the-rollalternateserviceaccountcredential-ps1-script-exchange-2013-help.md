---
title: 'RollAlternateServiceAccountCredential.ps1 スクリプトのトラブルシューティング: Exchange 2013 Help'
TOCTitle: RollAlternateServiceAccountCredential.ps1 スクリプトのトラブルシューティング
ms:assetid: 2bbf36d3-eb89-4f92-a8de-259a7cb64d62
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff808310(v=EXCHG.150)
ms:contentKeyID: 63918669
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# RollAlternateServiceAccountCredential.ps1 スクリプトのトラブルシューティング

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-01-14_

ここでは、RollAlternateServiceAccountPassword.ps1 スクリプトを使用した場合に発生しうるエラーについて、ソリューションと情報を提供します。

## 1 台または複数のクライアント アクセス サーバーがパスワードで更新できない

## 問題

スクリプトでパラメーター *ToEntireForest* または *ToArrayMembers* を使用する場合、インスタンスによっては 1 台または複数のクライアント アクセス サーバーが更新されない可能性があります。

## 解決方法

以下の例で示すように、スクリプトが **Get-ClientAccessArray** コマンドレットを使用して必要なすべてのサーバーをターゲットとしていることを、サーバーで確認します。

    Get-ClientAccessArray | fl members

更新に失敗しているサーバーが、クライアント アクセス アレイのメンバーであり、依然として正しく更新されない場合は、Exchange セットアップ プログラムを再実行して、クライアント アクセス サーバーの役割をサーバーに再度追加します。パラメーター *ToSpecificServers* を使用して個別にサーバーを指定することもできます。

## 一部のサーバーがスクリプトに応答しません

## 問題

状況によっては、不安定なネットワーク接続などの一時的なエラーにより、サーバーの更新が失敗する場合があります。

## 解決方法

問題のサーバーがネットワークに接続されていて、Active Directory と接続できていることを確認してから、再度スクリプトを実行します。

## アレイ メンバーの一部が長期間にわたってサービスが停止している

## 問題

**Get-ClientAccessArray cmdlet**によって、サーバーが長期間にわたってローテーションの対象外にもかかわらず依然としてアレイのメンバーであると判断された場合に、パラメーター *ToArrayMembers* および *ToEntireForest* を使用すると、スクリプトの機能が損なわれる可能性があります。サーバーで永続的なエラーが発生しているもかかわらず、展開から正常に削除されていない場合にも同じ問題が発生します。

## 解決方法

この問題を解決するには、Exchange セットアップを使用してサーバーを展開から削除するか、サーバーが削除されるまでスクリプトを手動モードで実行します。

サーバーを短時間停止するだけで、Exchange を完全に削除しない場合は、パラメーター *ToSpecificServers* を使用して特定のサーバーに対してスクリプトを実行するよう調整し、アクティブなサーバーのみを対象とするようにできます。または次の例で示すように、**Remove-ClientAccessArray** コマンドレットを使用して、応答しないサーバーの Active Directory オブジェクトから、RPC クライアント アクセス サービスを削除することができます。

    Remove-RPCClientAccess -Server Server.Contoso.com

RPC クライアント アクセス サービスを削除した後は、サーバーは [Get-ClientAccessArray](https://technet.microsoft.com/ja-jp/library/dd297976\(v=exchg.150\)) によるアレイのメンバーとしては返されず、スクリプトも対象としません。サーバーが再び機能するとすぐに、**New-RpcClientAccess** コマンドレットを使用して RPC クライアント アクセス サービスを再び追加できます。RPC クライアント アクセス サービスを再び追加したら、影響するサーバー上の Microsoft Exchange アドレス帳サービスを忘れずに再起動してください。


> [!NOTE]
> サーバーから RPC クライアント アクセス サービスを削除する前に、「<A href="https://technet.microsoft.com/ja-jp/library/dd298151(v=exchg.150)">Remove-RPCClientAccess</A>」を参照してください。



## 詳細情報

Kerberos 認証をクライアント アクセス サーバー アレイまたは負荷分散ソリューションと共に使用する方法の詳細については、次のトピックを参照してください。

  - [負荷分散されたクライアント アクセス サーバーの Kerberos 認証の構成](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md)

  - [シェルでの RollAlternateserviceAccountCredential.ps1 スクリプトの使用](using-the-rollalternateserviceaccountcredential-ps1-script-in-the-shell-exchange-2013-help.md)

