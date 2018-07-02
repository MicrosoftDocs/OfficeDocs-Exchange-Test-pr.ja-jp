---
title: 'アクセス制御リスト (ACL) の継承がブロックされている_InhBlockPublicFolderTree: Exchange 2013 Help'
TOCTitle: アクセス制御リスト (ACL) の継承がブロックされている_InhBlockPublicFolderTree
ms:assetid: e3b89c8a-d6f8-4864-8bf0-35a78ce87cc4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.inhblockpublicfoldertree(v=EXCHG.150)
ms:contentKeyID: 48270160
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# アクセス制御リスト (ACL) の継承がブロックされている\_InhBlockPublicFolderTree

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2015-03-09_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

必要なアクセス許可が伝達できなかったため、Microsoft Exchange Server 2007 または Exchange Server 2010 のセットアップ プログラムを続行できません。

Exchange セットアップ プログラムでは、次の Exchange オブジェクトでアクセス許可の継承が有効になっている必要があります。

  - Exchange 組織オブジェクト

  - Exchange 管理グループ オブジェクト

  - Exchange サーバー コンテナー オブジェクト

  - Exchange アドレス一覧オブジェクト

  - Exchange パブリック フォルダー オブジェクト

  - Exchange パブリック フォルダー ツリー オブジェクト

これらのオブジェクトのアクセス許可の継承を有効にできないと、メール フローの問題、ストア マウントの問題、その他のサービスの停止が発生する場合があります。

この問題を解決するには、オブジェクトの "親からの継承可能なアクセス許可をこのオブジェクトとすべての子オブジェクトに伝達できるようにします" 設定が有効なことを確認してから、Exchange Server 2007 または Exchange 2010 のセットアップ プログラムを再実行してください。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2003 Exchange システム マネージャーを使用して Exchange 構成オブジェクトのアクセス許可の継承を再度有効にするには、次の操作を行います。</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>レジストリ パラメーターを設定することにより、Exchange システム マネージャーのオブジェクトのプロパティ ボックスにある <strong>[セキュリティ]</strong> タブを有効にします。</p>
<ol>
<li><p>レジストリ エディター (Regedt32.exe) を起動します。</p></li>
<li><p>レジストリ内で次のキーを見つけます。</p>
<p><strong>HKEY_CURRENT_USER\Software\Microsoft\Exchange\EXAdmin</strong></p></li>
<li><p><strong>[編集]</strong> メニューで、<strong>[新規]</strong> をクリックし、次のレジストリ値を追加します。</p>
<p><strong>[値の名前]</strong>: ShowSecurityPage</p>
<p><strong>[データの種類]</strong>: REG_DWORD</p>
<p><strong>[基数]</strong>: バイナリ</p>
<p><strong>Value</strong>:1</p></li>
<li><p>レジストリ エディターを終了します。</p></li>
</ol>

> [!NOTE]
> 既定では、構成オブジェクトのプロパティ ボックスの <STRONG>[セキュリティ]</STRONG> タブは無効になっています。


</li>
<li><p>Exchange システム マネージャーを開き、問題のオブジェクトを見つけ、そのオブジェクトを右クリックして <strong>[プロパティ]</strong> を選択します。</p></li>
<li><p><strong>[セキュリティ]</strong> タブをクリックし、<strong>[詳細設定]</strong> をクリックします。</p></li>
<li><p><strong>[親からの継承可能なアクセス許可をこのオブジェクトとすべての子オブジェクトに伝達できるようにします]</strong> を選択して、アクセス許可の継承を再度有効にします。</p></li>
<li><p>Exchange Server を再起動します。</p></li>
</ol></td>
</tr>
</tbody>
</table>



> [!NOTE]
> ADSI Edit、LDP ツール、またはその他の LDAP Version&nbsp;3 クライアントを使用する際に Active Directory オブジェクトの属性を誤って変更すると、重大な問題が発生する可能性があります。これらの問題によって、Microsoft Windows Server™ 2003 または Exchange Server、あるいはその両方の再インストールが必要になる場合があります。Active&nbsp;Directory オブジェクトの属性の変更は、ユーザー自身の責任において行ってください。




<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2007 または Exchange Server 2010 から ADSIEdit を使用して Exchange 構成オブジェクトのアクセス許可の継承を再度有効にするには、次の操作を行います。</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>ADSI Edit をインストールします。</p></li>
<li><p>ADSI Edit を起動します。<strong>[スタート]</strong> ボタンをクリックし、<strong>[ファイル名を指定して実行]</strong> をクリックします。次に、テキスト ボックスに「<strong>adsiedit.msc</strong>」と入力し、[OK] をクリックします。</p></li>
<li><p>問題のオブジェクトに移動し、そのオブジェクトを右クリックして <strong>[プロパティ]</strong> を選択します。</p></li>
<li><p><strong>[セキュリティ]</strong> タブをクリックし、<strong>[詳細設定]</strong> をクリックします。</p></li>
<li><p><strong>[親からの継承可能なアクセス許可をこのオブジェクトとすべての子オブジェクトに伝達できるようにします]</strong> を選択して、アクセス許可の継承を再度有効にします。</p></li>
<li><p><strong>[OK]</strong> を 2 回クリックして、変更を適用します。</p></li>
<li><p>Active Directory レプリケーションにより変更が伝達されるまで待つか、またはマイクロソフト サポート技術情報の記事 232072「Active Directory ダイレクト複製パートナー間での複製の開始」(<a href="http://go.microsoft.com/fwlink/?linkid=3052%26kbid=232072" class="uri">http://go.microsoft.com/fwlink/?linkid=3052&amp;kbid=232072</a>) の説明に従って強制的に Active Directory レプリケーションを行います。</p></li>
</ol></td>
</tr>
</tbody>
</table>

