---
title: 'Windows Server バックアップを使用した Exchange のバックアップ: Exchange 2013 Help'
TOCTitle: Windows Server バックアップを使用した Exchange のバックアップ
ms:assetid: 188a8291-0a41-4ca2-b6d2-94242e2b1ffc
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd876854(v=EXCHG.150)
ms:contentKeyID: 48269214
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Windows Server バックアップを使用した Exchange のバックアップ

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-06-18_

Windows Server Backup を使用して、Exchange データベースのバックアップと復元を行うことができます。Exchange には、ボリューム シャドウ コピー サービス (VSS) ベースで Exchange のデータのバックアップを作成できる Windows Server Backup のプラグインが組み込まれています。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分とデータのバックアップにかかる時間を合計した時間

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「メールボックス回復」。

  - Windows Server Backup 機能はローカル コンピューターにインストールする必要があります。

  - バックアップ操作中、ファイルが正常な状態で復元に使用できることを確認するために Exchange データ ファイルの整合性チェックが実行されます。整合性チェックが成功すると、Exchange データは当該バックアップからの復元に使用できます。整合性チェックが失敗した場合は、Exchange データは復元用に使用できません。Windows Server Backup は、バック用に作成したスナップショットの整合性チェックを実行します。これにより、スナップショットからバックアップ メディアにファイルをコピーする前に、バックアップの整合性が確認され、ユーザーに整合性チェックの結果が通知されます。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## Windows Server バックアップを使用した Exchange のバックアップ

1.  Windows Server Backup を起動します。

2.  <strong>ローカル バックアップ</strong> を選択します。

3.  操作ウィンドウで <strong>バックアップ 1 回限り...</strong> をクリックすると、バックアップ (1 回限り) ウィザードが開始します。

4.  <strong>バックアップ オプション</strong> ページで、<strong>別のオプション</strong> を選択し、<strong>次へ</strong> をクリックします。

5.  <strong>バックアップの構成の選択</strong> ページで <strong>ユーザー設定</strong> を選択し、<strong>次へ</strong> をクリックします。

6.  <strong>バックアップ項目の選択</strong> ページで、<strong>項目の追加</strong> をクリックしてバックアップするボリュームを選択し、<strong>OK</strong> をクリックします。
    

    > [!NOTE]
    > 個々のフォルダーではなく、ボリュームを選択します。アプリケーション レベルのバックアップまたは復元を実行する唯一の方法は、ボリューム全体を選択することです。



7.  <strong>詳細設定</strong> をクリックします。<strong>除外</strong> タブで、<strong>除外の追加</strong> をクリックして、バックアップから除外するファイルまたはファイルの種類を追加します。
    

    > [!NOTE]
    > 既定では、オペレーティング システム コンポーネントまたはアプリケーションを含むボリュームはバックアップに含まれ、除外することはできません。



8.  <strong>VSS 設定\] タブ**で、<strong>VSS 完全バックアップ</strong> を選択し、<strong>OK</strong>、<strong>次へ</strong> の順にクリックします。

9.  <strong>作成先の種類の指定</strong> ページで、バックアップを保存する場所を選択し、<strong>次へ</strong> をクリックします。
    
      - <strong>ローカル ドライブ</strong> を選択すると、<strong>バックアップ先の選択</strong> ページが表示されます。<strong>バックアップ先</strong> ドロップダウンからオプションを選択し、<strong>次へ</strong> をクリックします。
    
      - <strong>リモート共有フォルダー</strong> を選択した場合は、<strong>リモート フォルダーの指定</strong> ページが表示されます。バックアップ ファイル用の UNC パスを指定してから、アクセス制御設定を構成します。特定のアカウントを通してのみバックアップにアクセスできるようにする場合は、<strong>継承しない</strong> を選択します。リモート フォルダーをホストしているコンピューターへの書き込みアクセス許可を持っているアカウントのユーザー名とパスワードを入力し、<strong>OK</strong> をクリックします。代わりに、リモート フォルダーへのアクセス許可を持っているすべてのユーザーがバックアップにアクセスできるようにするには、<strong>継承</strong> を選択します。<strong>次へ</strong> をクリックします。

10. <strong>確認</strong> ページで、バックアップの設定を確認し、<strong>バックアップ</strong> をクリックします。

11. <strong>バックアップの進行状況</strong> ページで、バックアップ操作の状態と進行状況を確認できます。

12. <strong>閉じる</strong> をクリックすると、いつでも <strong>バックアップの進行状況</strong> ページを終了できます。進行中のバックアップはすべてバックグラウンドで続行されます。

## 正常な動作を確認する方法

データを正常にバックアップできたことを確認するには、次のいずれかを実行します。

  - Windows Server Backup が実行されていたサーバーで、前回のバックアップ状況が「成功」と表示されます。Windows Server Backup のログを表示することでも、バックアップが正常に完了したことを確認できます。

  - イベント ビューアーを開いて、バックアップ完了イベントがアプリケーション イベント ログに記録されたことを確認します。

  - Exchange 管理シェルで次のコマンドを実行して、選択したボリュームの各データベースが正常にバックアップされたことを確認します。
    
        Get-MailboxDatabase -Server <ServerName> -Status | fl Name,*FullBackup
    
    データベースの *SnapshotLastFullBackup* および *LastFullBackup* プロパティは、前回バックアップに成功した日時と、それが VSS の完全バックアップであったかどうかを示しています。

