---
title: 'スキーマ マスター サイト/ドメインがない_NotInSchemaMasterDomain: Exchange 2013 Help'
TOCTitle: スキーマ マスター サイト/ドメインがない_NotInSchemaMasterDomain
ms:assetid: 5e44eb33-4c30-4c3d-ba68-5c30bef1731f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.notinschemamasterdomain(v=EXCHG.150)
ms:contentKeyID: 48269562
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# スキーマ マスター サイト/ドメインがない\_NotInSchemaMasterDomain

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2016-12-09_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

セットアップ プログラムを実行するコンピューター (FSMO (Flexible Single Master Operation) とも呼ばれる) が、ドメイン スキーマ マスターの役割を割り当てられたサーバーと同じ Active Directory® ディレクトリ サービス サイトまたはドメインにないため、Microsoft® Exchange Server 2007 セットアップ プログラムを続行できません。

Exchange 2007 セットアップ プログラムは、Exchange セットアップ プログラムを実行するローカル コンピューターと同じサイトおよびドメイン内にあるドメイン スキーマ マスターとして機能するドメイン コントローラーが必要です。

ドメイン スキーマ マスターは、Active Directory スキーマに対するすべての更新と変更を制御します。

この問題を解決するには、ドメイン スキーマ マスターと同じサイトおよびドメインから、**/prepareschema** スイッチと **/prepareAD** スイッチを使用して Exchange Server 2007 セットアップ プログラムを実行します。

**/prepareschema** および **/prepareAD** セットアップ スイッチの詳細については、Exchange 2007 の製品ドキュメントの「Active Directory とドメインを準備する方法」(<https://go.microsoft.com/fwlink/?linkid=78453>) を参照してください。

スキーマ マスター ツールを使用して役割を識別することができます。ただし、スキーマ ツールを MMC スナップインとして使用できるようにするには、Schmmgmt.dll DLL を登録する必要があります。

**現在のスキーマ マスターを表示するには**

1.  コマンド プロンプトで、<strong>「regsvr32 schmmgmt.dll」</strong>と入力します。
    

    > [!NOTE]
    > 次のダイアログ ボックスが表示される場合、<STRONG>RegSvr32</STRONG> は正常に登録されています。<BR>[DllRegisterServer in schmmgmt.dll succeeded.]



2.  新しい管理コンソールを開くには、<strong>スタート</strong> ボタンをクリックし、<strong>ファイル名を指定して実行</strong> をクリックして、「**mmc**」と入力します。

3.  コンソールのメニューで、<strong>スナップインの追加と削除</strong> をクリックします。

4.  <strong>追加</strong> をクリックし、<strong>スタンドアロン スナップインの追加</strong> ダイアログ ボックスを開きます。

5.  <strong>Active Directory スキーマ</strong> を選択し、<strong>追加</strong> をクリックします。

6.  \[スナップインの追加と削除\] に「Active Directory スキーマ」が表示されます。<strong>閉じる</strong> をクリックし、<strong>OK</strong> をクリックしてコンソールに戻ります。

7.  <strong>Active Directory スキーマ</strong> を選択すると、<strong>クラス</strong> と <strong>属性</strong> セクションが右側に表示されます。

8.  <strong>Active Directory スキーマ</strong> を右クリックし、<strong>操作マスター</strong> をクリックします。

9.  現在のスキーマ マスターが表示されます。

現在のスキーマ マスターを特定した後、スキーマ マスターがどのサブネットにあるかを判断します。その後、次のいずれかの方法で、Exchange をインストールします。

  - Exchange サーバー上のサブネットを変更し、それをスキーマ マスターがあるサイトへ移動します。その後、Exchange をインストールします。

  - 一時的に Exchange サーバー上のサイト メンバーシップを強制的に変更し、その後 Exchange をインストールします。Exchange をインストールした後は、Exchange サーバーを元のサイトに戻します。

**サイトのメンバーシップを強制的に変更する方法**

1.  Exchange をインストールするサーバー上で、レジストリ エディターを起動します。これを実行するには、<strong>スタート</strong> ボタンをクリックし、<strong>ファイル名を指定して実行</strong> をクリックします。次に、「**regedit**」と入力し、<strong>OK</strong> をクリックします。

2.  次のレジストリ サブキーを見つけます。
    
    **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\Netlogon\\Parameters**

3.  次の新しい <strong>文字列</strong> 値を作成します。
    
    値の名前: **SiteName**
    
    値の種類: **REG\_SZ**
    
    値のデータ: **\<site\_that\_contains\_the\_schema\_master\>**

4.  レジストリ エディターを終了し、Netlogon サービスを再起動します。この操作により、Exchange サーバーは指定したサイトに強制的に参加します。

5.  Exchange をインストールします。

6.  手順 3 で追加したレジストリ エントリを削除します。

7.  Netlogon サービスを再起動します。この操作で、Exchange は元のサイトに戻ります。

