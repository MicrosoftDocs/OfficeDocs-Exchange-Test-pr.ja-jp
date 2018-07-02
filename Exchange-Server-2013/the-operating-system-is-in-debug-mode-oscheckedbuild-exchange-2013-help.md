---
title: 'オペレーティング システムがデバッグ モードになっている_OSCheckedBuild: Exchange 2013 Help'
TOCTitle: オペレーティング システムがデバッグ モードになっている_OSCheckedBuild
ms:assetid: 93a1380f-1388-494d-8f78-92dfefd069bd
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.oscheckedbuild(v=EXCHG.150)
ms:contentKeyID: 48269801
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# オペレーティング システムがデバッグ モードになっている\_OSCheckedBuild

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2016-12-15_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft® Exchange Server アナライザー ツールは **Win32\_OperatingSystem** Microsoft WMI (Windows® Management Instrument) クラスに対してクエリを実行し、**Debug** プロパティに値が設定されているかどうかを判断します。Exchange Server コンピューターで、このキーの値が **True** に設定されている場合は、エラーが表示されます。

Windows デバッグ モードには、Boot.ini ファイルに **/debug** パラメーターを追加して切り替えます。Windows Server コンピューターの Boot.ini ファイルに **/debug** が指定されていると、起動時にカーネル デバッガーが読み込まれ、メモリ内に常に保持されます。これにより、システムがカーネルの停止画面で中断された場合でなくても、サポートの専門家がデバッグ中のシステムにダイヤルインし、デバッガーに入ることができます。**/crashdebug** スイッチとは異なり、**/debug** スイッチの使用時には、デバッグ中かどうかにかかわらず COM ポートが使用されます。このスイッチは、何度でも再現できる問題のデバッグを行う場合に使用されます。この **/debug** パラメーターは、問題のトラブルシューティングを行うための手段として設定され、誤って設定されたままになった可能性があります。

追加のプロセスが実行されるため、パフォーマンスが大幅に低下します。このため、Windows がデバッグ モードで実行されているコンピューターで Exchange Server を実行することはお勧めできません。

このエラーをなくすには、Boot.ini ファイルを編集し、**/debug** パラメーターを削除します。

## このエラーを修正するには、次の操作を行います。

1.  Windows エクスプローラーで、システム パーティションに移動します。このパーティションには、Boot.ini や NTLDR などのハードウェア固有のファイルが保持されています。

2.  Boot.ini ファイルが表示されない場合は、**\[フォルダー オプション\]** が **\[保護されたオペレーティング システム ファイルを表示しない\]** に設定されていることが考えられます。この場合は、Windows エクスプローラー ウィンドウで、**\[ツール\]** メニューの **\[フォルダー オプション\]** をクリックし、**\[表示\]** タブをクリックします。–**\[保護されたオペレーティング システム ファイルを表示しない (推奨)\]** チェック ボックスをオフにします。確認を求められたら、**\[はい\]** をクリックします。

3.  Boot.ini ファイルが Windows エクスプローラーに表示されたら、このファイルを右クリックし、**\[プログラムから開く\]** をクリックします。次に、**\[メモ帳\]** をクリックしてファイルを開きます。

4.  **\[Operating Systems\]** セクションで、**/debug** パラメーターを削除します。

5.  ファイルを保存して閉じてから、Exchange Server コンピューターを再起動して変更を有効にします。

Boot.ini ファイルで使用できるパラメーターの詳細については、Microsoft サポート技術情報の文書番号 833721「Windows XP および Windows Server 2003 の Boot.ini ファイルで使用可能なスイッチ オプション」([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=833721](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=833721)) を参照してください。

