---
title: 'モバイル デバイス メールボックス ポリシーの作成または変更: Exchange 2013 Help'
TOCTitle: モバイル デバイス メールボックス ポリシーの作成または変更
ms:assetid: b4a37a81-25e3-40ff-a18a-a62ae4493635
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124315(v=EXCHG.150)
ms:contentKeyID: 49896425
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# モバイル デバイス メールボックス ポリシーの作成または変更

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-16_

モバイル デバイス メールボックス ポリシーを使用すると、共通する一連のセキュリティとモバイル デバイスの設定をユーザー グループに適用できます。複数のモバイル デバイス メールボックス ポリシーを作成できます。 組織の各受信者には、モバイル デバイス メールボックス ポリシーが割り当てられている必要があります。 Microsoft Exchange Server 2013 をインストールすると、既定のモバイル デバイス メールボックス ポリシーが作成され、新しいユーザーは自動的にこのポリシーに割り当てられます。 モバイル デバイス メールボックス ポリシーに特定のユーザーを割り当てるには、[モバイル メールボックス ポリシーでのユーザーの追加または削除](add-or-remove-users-from-a-mobile-mailbox-policy-exchange-2013-help.md) を参照してください。

モバイル デバイス メールボックス ポリシーに関連した追加情報については、[モバイル デバイス メールボックス ポリシー](mobile-device-mailbox-policies-exchange-2013-help.md) を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:10 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「モバイル デバイス メールボックス ポリシー」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## 新しい モバイル デバイス メールボックス ポリシーを作成します。

EAC またはシェルを使用して新しいモバイル デバイス メールボックス ポリシーを作成できます。

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「モバイル デバイス メールボックス ポリシー」。

## EAC を使用して、新しいモバイル デバイス メールボックス ポリシーを作成するには

EAC を使用して、新しいモバイル デバイス メールボックス ポリシーを作成できます。


> [!NOTE]
> EAC でモバイル デバイス メールボックス ポリシー設定のサブセットを設定するだけです。 すべてのモバイル デバイス メールボックス ポリシー設定を設定するには、シェルを使用する必要があります。



1.  EAC で、**\[モバイル\]** \> **\[モバイル デバイス メールボックス ポリシー\]** をクリックしてから、**\[新規作成\]** をクリックします。

2.  さまざまなチェック ボックスおよびドロップ ダウン リストを使用して、モバイル デバイス メールボックス ポリシーの設定を構成します。
    

    > [!WARNING]
    > <STRONG>[これを既定のポリシーにする]</STRONG> を選択すると、新しいモバイル メールボックス ポリシーが既定のモバイル メールボックス ポリシーになります。 モバイル メールボックス ポリシーを既定のポリシーにすると、その後作成されるすべての新しいユーザーに自動的にこのポリシーが割り当てられます。



3.  **\[保存\]** をクリックします。

## シェルを使用して、新しいモバイル デバイス メールボックス ポリシーの作成

New-MobileDeviceMailboxPolicy コマンドレットを使用して、新しいモバイル デバイス メールボックス ポリシーを作成できます。


> [!WARNING]
> 新しいモバイル デバイス メールボックス ポリシーの作成には、2 つのコマンドレットが使用できます。<STRONG>New-ActiveSyncMailboxPolicy</STRONG> コマンドレットと、 <STRONG>New-MobileDeviceMailboxPolicy</STRONG> コマンドレットは、同一のタスクを実行します。 Microsoft Exchange サーバーの今後のバージョンでは、<STRONG>New-ActiveSyncMailboxPolicy</STRONG> コマンドレットは削除される予定です。 <STRONG>New-MobileDeviceMailboxPolicy</STRONG> コマンドレットを使用するようスクリプトおよび手順を更新しておくことをお勧めします。



1.  シェルで、次のコマンドを実行します。
    
        New-MobileDeviceMailboxPolicy -Name:"Management" -AllowBluetooth:$true -AllowBrowser:$true -AllowCamera:$true -AllowPOPIMAPEmail:$false -PasswordEnabled:$true -AlphanumericPasswordRequired:$true -PasswordRecoveryEnabled:$true -MaxEmailAgeFilter:10 -AllowWiFi:$true -AllowStorageCard:$true -AllowPOPIMAPEmail:$false

## 正常な動作を確認する方法

モバイル デバイス メールボックス ポリシーが正常に作成されたことを確認するには、次の手順のいずれかを使用します。

1.  EAC で、**\[モバイル\]** \> **\[モバイル デバイス メールボックス ポリシー\]** をクリックし、新しいポリシーがリスト ビューに表示されていることを確認します。

2.  シェルで、次のコマンドを実行します。
    
        Get-MobileDeviceMailboxPolicy -Identity <PolicyName> 

## 既存のモバイル メールボックス ポリシーを編集する

EAC またはシェルを使用してモバイル デバイス メールボックス ポリシーを編集できます。

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「モバイル デバイス メールボックス ポリシー」。

## EAC を使用してモバイル デバイス メールボックス ポリシーを編集するには

EAC を使用してモバイル デバイス メールボックス ポリシーを編集できます。


> [!NOTE]
> EAC でモバイル デバイス メールボックス ポリシー設定のサブセットを編集するだけです。 すべてのモバイル デバイス メールボックス ポリシー設定を編集するには、シェルを使用する必要があります。



1.  EAC で、**\[モバイル\]** \> **\[モバイル デバイス メールボックス ポリシー\]** をクリックします。

2.  リスト ビューからポリシーを選択し、**\[編集\]** ボタンをクリックします。

3.  **\[全般\]** および**\[セキュリティ\]** タブを使用してモバイル デバイス メールボックス ポリシー設定を編集します。

4.  **\[保存\]** をクリックしてポリシーの更新を完了します。

## シェルを使用してモバイル デバイス メールボックス ポリシーの設定を編集する

シェルを使用して、モバイル デバイス メールボックス ポリシーを編集することができます。


> [!WARNING]
> 新しいモバイル デバイス メールボックス ポリシーの編集には、2 つのコマンドレットが使用できます。 Set-ActiveSyncMailboxPolicyコマンドレットと、 Set-MobileDeviceMailboxPolicyコマンドレットは、同一のタスクを実行します。 Microsoft Exchange サーバーの今後のバージョンでは、 <STRONG>Set-ActiveSyncMailboxPolicy</STRONG>コマンドレットは削除される予定です。 <STRONG>Set-MobileDeviceMailboxPolicy</STRONG> コマンドレットを使用するようスクリプトおよび手順を更新しておくことをお勧めします。



1.  シェルで、次のコマンドを実行します。
    
        Set-MobileDeviceMailboxPolicy -Identity:Default -DevicePasswordEnabled:$true -AlphanumericDevicePasswordRequired:$true -PasswordRecoveryEnabled:$true -MaxEmailAgeFilter:ThreeDays -AllowWiFi:$false -AllowStorageCard:$true -AllowPOPIMAPEmail:$false -IsDefault:$true -AllowTextMessaging:$true -Confirm:$true

## 正常な動作を確認する方法

モバイル デバイス メールボックス ポリシーが正常に編集されたことを確認するには、次の手順のいずれかを実行します。

1.  EAC で、**\[モバイル\]** \> **\[モバイル デバイス メールボックス ポリシー\]** をクリックしてから、特定のポリシーを選択します。 詳細ウィンドウに多くのポリシー設定が一覧表示されます。

2.  シェルで、次のコマンドを実行します。
    
        Get-MobileDeviceMailboxPolicy -Identity <PolicyName>

