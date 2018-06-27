---
title: 'Exchange 2013 から Exchange Online へのパブリック フォルダーの移行をロールバックする: Exchange Online Help'
TOCTitle: Exchange 2013 から Exchange Online へのパブリック フォルダーの移行をロールバックする
ms:assetid: bcd54aa0-aa45-4c68-b504-1475842d4b96
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Mt798259(v=EXCHG.150)
ms:contentKeyID: 74432688
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 から Exchange Online へのパブリック フォルダーの移行をロールバックする

 

**概要**:次の手順に従って、Exchange 2013 のオンプレミスの組織で、パブリック フォルダーのインフラストラクチャを移行前の状態に戻します。

Exchange Online へのパブリック フォルダーの移行に関連して問題が発生しているなどの理由で、Exchange 2013 のパブリック フォルダーを再度有効にする必要がある場合は、次の手順を実行します。

## 移行のロールバック

移行をロールバックすると、Exchange Online への移行後にパブリック フォルダーに追加された内容がすべて失われることにご注意ください。この内容には、クライアントにより追加されたものも、メールが有効なパブリック フォルダーに対応した電子メールにより追加されたものも該当します。この内容を保存するには、移行後のパブリック フォルダーの内容を .pst ファイルにエクスポートして、ロールバックの完了時にオンプレミスのパブリック フォルダーにインポートできます。

1.  Exchange のオンプレミスの環境で、次のコマンドを実行し、Exchange 2013 のパブリック フォルダーのロックを解除します。ロックが解除されるまでに数時間かかる場合があるのでご注意ください。
    
        Set-OrganizationConfig -PublicFolderMailboxesLockedForNewConnections:$false -PublicFolderMailboxesMigrationComplete:$false -PublicFoldersEnabled Local 

2.  Exchange のオンプレミス環境で、SetMailPublicFolderExternalAddress.ps1 によって更新された、メールが有効なパブリック フォルダーの `ExternalEmailAddress` を元に戻します。このスクリプトは、*手順 8: Exchange Online のパブリック フォルダーをテストしてロックを解除する* (「[バッチ移行を使用して、Exchange 2013 のパブリック フォルダーを Exchange Online に移行する](use-batch-migration-to-migrate-exchange-2013-public-folders-to-exchange-online-exchange-online-help.md)」内) で使用したスクリプトです。このスクリプトによって作成された要約ファイルを参照して、変更内容を特定できます。また、同じバッチ移行プロセスの早い段階で生成された OnPrem\_MEPF.xml ファイルを使用して、すべてのメールが有効なパブリック フォルダーの元のプロパティを取得することもできます。

3.  Exchange Online PowerShell で次のコマンドを実行し、Exchange Online のパブリック フォルダーとメールボックスをすべて削除します。
    
        Get-MailPublicFolder -ResultSize Unlimited | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false 
        Get-PublicFolder -GetChildren \ -ResultSize Unlimited | Remove-PublicFolder -Recurse -Confirm:$false
        $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
        Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
        Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
        Get-Mailbox -PublicFolder -SoftDeletedMailbox | Remove-Mailbox -PublicFolder -PermanentlyDelete:$true

4.  Exchange Online 環境で次のコマンドを実行し、パブリック フォルダーのトラフィックをリダイレクトしてオンプレミス (Exchange 2013) に戻します。
    
        Set-OrganizationConfig -PublicFoldersEnabled Remote

5.  Exchange Online ユーザーがアクセスできるように、オンプレミスのパブリック フォルダーへのアクセスを再構成することに関する指示については、「[ハイブリッド展開用に Exchange 2013 パブリック フォルダーを構成する](configure-exchange-2013-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)」を参照してください。

