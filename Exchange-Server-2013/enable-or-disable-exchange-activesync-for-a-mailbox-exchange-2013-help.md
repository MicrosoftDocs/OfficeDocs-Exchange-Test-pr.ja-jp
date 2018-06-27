---
title: 'メールボックスの Exchange ActiveSync を有効または無効にする: Exchange Online Help'
TOCTitle: メールボックスの Exchange ActiveSync を有効または無効にする
ms:assetid: dcf7c05b-b1b9-4b0f-800d-fec9f2ddc9e4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124809(v=EXCHG.150)
ms:contentKeyID: 50555884
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックスの Exchange ActiveSync を有効または無効にする

 

_**適用先:**Exchange Online, Exchange Server 2013_

EAC またはシェルを使用して、ユーザー メールボックスの Microsoft Exchange ActiveSync を有効または無効にすることができます。Exchange ActiveSync は、モバイル デバイスと Exchange メールボックスを同期できるようにするクライアント プロトコルです。既定では、Exchange ActiveSync は、ユーザー メールボックスの作成時に有効になります。詳細については、「[Exchange ActiveSync](exchange-activesync-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「Exchange ActiveSync 設定」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して Exchange ActiveSync を有効または無効にする

1.  EAC で、**\[受信者\]** \> **\[メールボックス\]**に移動します。

2.  ユーザー メールボックス リストで、Exchange ActiveSync を有効または無効にするメールボックスをクリックし、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン")をクリックします。

3.  メールボックスのプロパティ ページで、**\[メールボックスの機能\]** をクリックします。

4.  **\[モバイル デバイス\]** で、以下のいずれか 1 つの操作を行います。
    
      - Exchange ActiveSync を無効にするには、**\[Exchange ActiveSync を無効にする\]** をクリックします。
        
        Exchange ActiveSync を無効にするかどうかを確認する警告が表示されます。**\[はい\]** をクリックします。
    
      - Exchange ActiveSync を有効にするには、**\[Exchange ActiveSync を有効にする\]** をクリックします。

5.  **\[保存\]** をクリックして変更を保存します。


> [!NOTE]
> EAC の一括編集機能を使えば、複数のユーザー メールボックスの Exchange ActiveSync をまとめて有効および無効にすることができます。この操作の詳細については、<A href="manage-user-mailboxes-exchange-2013-help.md">ユーザー メールボックスの管理</A>の「ユーザー メールボックスの一括編集」を参照してください。



## シェルを使用して Exchange ActiveSync を有効または無効にする

この例では、Yan Li のメールボックスの Exchange ActiveSync を無効にします。

    Set-CASMailbox -Identity "Yan Li" -ActiveSyncEnabled $false

この例では、Elly Nkya のメールボックスの Exchange ActiveSync を有効にします。

    Set-CASMailbox -Identity Ellyn@contoso.com -ActiveSyncEnabled $true

構文およびパラメーターの詳細については、「[Set-CASMailbox](https://technet.microsoft.com/ja-jp/library/bb125264\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

ユーザーのメールボックスの Exchange ActiveSync が正常に有効または無効にされたことを確認するには、次のいずれかを実行します。

  - EAC で、**\[受信者\]** \> **\[メールボックス\]** の順に移動し、メールボックスをクリックし、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

  - メールボックスのプロパティ ページで、**\[メールボックスの機能\]** をクリックします。

  - **\[モバイル デバイス\]** で、Exchange ActiveSync が有効か無効かを確認します。

または

  - シェルで、次のコマンドを実行します。
    
        Get-CASMailbox <identity>
    
    Exchange ActiveSync が有効になっている場合、*ActiveSyncEnabled* プロパティの値は `True` です。Exchange ActiveSync が無効になっている場合、値は `False` です。

