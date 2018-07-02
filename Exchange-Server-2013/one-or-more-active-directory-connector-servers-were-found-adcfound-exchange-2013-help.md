---
title: '1 つ以上の Active Directory コネクタ サーバーが見つかった_ADCFound: Exchange 2013 Help'
TOCTitle: 1 つ以上の Active Directory コネクタ サーバーが見つかった_ADCFound
ms:assetid: a874f51f-09a2-4a76-9695-d61fb1ee6c1c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.adcfound(v=EXCHG.150)
ms:contentKeyID: 48269889
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 1 つ以上の Active Directory コネクタ サーバーが見つかった\_ADCFound

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2016-12-15_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

現在の Microsoft Exchange 環境で 1 つ以上の Active Directory コネクタ (ADC) が見つかったため、Microsoft Exchange Server 2007 および Exchange Server 2010 のセットアップ プログラムを続行できません。

ADC は混在モードの Microsoft Exchange 環境で Exchange Server Version 5.5 から Active Directory ディレクトリ サービスにオブジェクトをレプリケートします。これは Exchange 2007 または Exchange 2010 ではサポートされていません。

Exchange 2007 または Exchange 2010 のセットアップ プログラムを実行するには、すべての ADC コンポーネントを削除する必要があります。

この問題を解決するには、すべての ADC コンポーネントを削除してから、Exchange 2007 または Exchange 2010 のセットアップ プログラムを再実行します。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Active Directory コネクタ コンポーネントを削除するには、次の操作を行います。</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>ADC サービスを実行しているサーバーで ADC サービスを無効にするには、デスクトップの <strong>[マイ コンピューター]</strong> を右クリックし、<strong>[管理]</strong> をクリックします。</p></li>
<li><p><strong>[サービスとアプリケーション]</strong> ノードを展開し、<strong>[サービス]</strong> ノードをクリックします。</p></li>
<li><p>右側のペインで <strong>[Microsoft Active Directory Connector]</strong> を右クリックし、<strong>[プロパティ]</strong> をクリックします。</p></li>
<li><p><strong>[スタートアップの種類]</strong> を <strong>[無効]</strong> に変更します。これにより、次回コンピューターを起動する際に ADC サービスが開始されなくなります。</p></li>
<li><p><strong>[適用]</strong> をクリックし、<strong>[OK]</strong> をクリックします。</p></li>
<li><p>ADC サービスをアンインストールするには、Microsoft Exchange 2000 Server または Microsoft Exchange Server 2003 の CD に含まれている Active Directory インストール ウィザードを使用します。\ADC\I386 フォルダーを開き、Setup.exe プログラムをダブルクリックします。表示されるメッセージに従って、ADC サービス コンポーネントを<strong>すべて削除</strong>します。</p>

> [!IMPORTANT]
> この問題を解決するには、手順 6. を完了して ADC コンポーネントを<STRONG>すべて削除</STRONG>する必要があります。ADC サービスを無効にするだけでは不十分です。


</li>
</ol></td>
</tr>
</tbody>
</table>


ADC の詳細については、以下の Microsoft サポート技術情報の文書を参照してください。

  - 文書番号 325300、Active Directory コネクタの概要に関するサポート Web キャスト（[https://go.microsoft.com/fwlink/?linkid=3052\&kbid=325300](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=325300))

  - 文書番号 325221、Microsoft の詳細な Active Directory コネクタに関するサポート Web キャスト （[https://go.microsoft.com/fwlink/?linkid=3052\&kbid=325221](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=325221))

  - 文書番号 312632「\[HOW TO\] Exchange 2000 Server で Active Directory コネクタをインストールおよび構成する方法」([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=312632](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=312632))

