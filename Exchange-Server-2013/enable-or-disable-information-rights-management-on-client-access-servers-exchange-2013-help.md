---
title: 'クライアント アクセス サーバーで Information Rights Management を有効または無効にする'
TOCTitle: クライアント アクセス サーバーで Information Rights Management を有効または無効にする
ms:assetid: c7ce069b-a572-4755-90a3-7105472e4c83
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd876938(v=EXCHG.150)
ms:contentKeyID: 49896467
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# クライアント アクセス サーバーで Information Rights Management を有効または無効にする

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

クライアント アクセス サーバーで Information Rights Management (IRM) を有効にすると、次の機能が有効になります。

  - Microsoft Office Outlook Web App

  - Microsoft Exchange ActiveSync の IRM

クライアント アクセス サーバーで IRM を有効にすると、Outlook Web App ユーザーは、AD RMS クラスターに作成された[Active Directory Rights Management サービス (AD RMS)](https://technet.microsoft.com/ja-jp/library/hh831364.aspx) テンプレートを適用してメッセージを IRM で保護できます。Outlook Web App ユーザーも、IRM で保護されたメッセージやサポートされた添付ファイルを表示できます。クライアント アクセス サーバーの IRM を有効にする前に、AD RMS クラスターのスーパー ユーザー グループにフェデレーション メールボックスを追加する必要があります。


> [!IMPORTANT]
> スーパー ユーザー グループのメンバーが AD&nbsp;RMS クラスターからライセンスを要求すると、そのメンバーには所有者使用ライセンスが付与されます。これにより、そのクラスターによって RMS で保護されたすべてのコンテンツの暗号化を解除できます。



IRM に関連する追加の管理タスクについては、「[Information Rights Management の手順](information-rights-management-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 推定完了時間: 1 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「Information Rights Management (IRM) の構成」。

  - AD RMS クラスターが Active Directory フォレストにインストールされている必要があります。

  - フェデレーション メールボックスが AD RMS スーパー ユーザー グループに追加されている。詳細な手順については、「[フェデレーション メールボックスを AD RMS のスーパー ユーザー グループに追加する](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)」を参照してください。

  - 組織で IRM 機能が有効になっている必要があります。詳細な手順については、「[内部メッセージの IRM を有効または無効にする](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md)」を参照してください。

  - **Set-IRMConfiguration** コマンドレットを使用して、Exchange 組織全体または個別レベルで、Outlook Web App および Exchange ActiveSync の IRM を有効または無効にできます。
    
    Outlook Web App の IRM は、次のレベルで制御することができます。
    
      - **Per-Outlook Web App 仮想ディレクトリ**   Outlook Web App 仮想ディレクトリの Outlook Web App 内の IRM を有効または無効にするには、**Set-OWAVirtualDirectory** コマンドレットを使用して、*IRMEnabled* パラメーターを `$false` または `$true` (既定) に設定します。これで、Exchange 2013 クライアント アクセス サーバー上のある仮想ディレクトリを有効にしたまま、別のクライアント アクセス サーバー上の別の仮想ディレクトリの Outlook Web App 内の IRM を無効にできます。
    
      - **Per-Outlook Web App メールボックス ポリシー**   Outlook Web App メールボックス ポリシーの Outlook Web App 内の IRM を有効または無効にするには、**Set-OWAMailboxPolicy** コマンドレットを使用して、*IRMEnabled* パラメーターを `$false` または `$true` (既定) に設定します。これで、Outlook Web App 内の IRM を、ある 1 組のユーザーに対して有効し、別の 1 組のユーザーに対して無効にできます。これを行うには、それぞれの組に対して別の Outlook Web App メールボックス ポリシーを割り当てます。
    
    Exchange ActiveSync メールボックス ポリシーに従って、Exchange ActiveSync の IRM を制御できます。Exchange ActiveSync メールボックス　ポリシーで Exchange ActiveSync の IRM を無効または有効にするには、**Set-ActiveSyncMailboxPolicy** コマンドレットを使用して *IRMEnabled* パラメーターを `$false` または `$true` (既定) に設定します。これにより、ユーザーのセットごとに異なる Exchange ActiveSync メールボックス ポリシーを割り当てて、Exchange ActiveSync の IRM を、あるユーザーのセットでは有効に、別のユーザーのセットでは無効にできます。

  - Exchange 管理センター (EAC) を使用してクライアント アクセス サーバーの IRM を有効または無効にすることはできません。シェルを使用する必要があります。

## 必要な作業

## シェルを使用して、クライアント アクセス サーバーで IRM を有効にする

この例では、Exchange 組織のクライアント アクセス サーバーで IRM を有効にします。

```powershell
Set-IRMConfiguration -ClientAccessServerEnabled $true
```

構文およびパラメーターの詳細については、「[Set-IRMConfiguration](https://technet.microsoft.com/ja-jp/library/dd979792\(v=exchg.150\))」を参照してください。

## シェルを使用して、クライアント アクセス サーバーで IRM を無効にする

この例では、Exchange 組織のクライアント アクセス サーバーで IRM を無効にします。

```powershell
Set-IRMConfiguration -ClientAccessServerEnabled $false
```

構文およびパラメーターの詳細については、「[Set-IRMConfiguration](https://technet.microsoft.com/ja-jp/library/dd979792\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

クライアント アクセス サーバーの IRM の有効化または無効化が正常に実行されたことを確認するには、次の操作を行います。

  - **Get-IRMConfiguration** コマンドレットを実行して *ClientAccessServerEnabled* プロパティの値を確認します。
    
    IRM 構成を取得する方法の例については、**Get-IRMConfiguration** の「[Examples](https://technet.microsoft.com/ja-jp/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples)」を参照してください。

  - IRM で保護されたメッセージを作成または開封するには、Outlook Web App を使用します。

