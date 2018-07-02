---
title: 'サポートされる VoIP ゲートウェイ、IP Pbx、および PBX の構成に関する注意事項: Exchange Online Help'
TOCTitle: サポートされる VoIP ゲートウェイ、IP Pbx、および PBX の構成に関する注意事項
ms:assetid: 1583674f-5a57-45fd-8125-087d1624e686
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee681657(v=EXCHG.150)
ms:contentKeyID: 50555736
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# サポートされる VoIP ゲートウェイ、IP Pbx、および PBX の構成に関する注意事項

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ここでは、Microsoft または VoIP ゲートウェイ パートナーによって作成およびテストされた構成に関する注意事項へのリンクを示します。Microsoft またはパートナーが新しい VoIP ゲートウェイおよび PBX または IP PBX 構成を使用してユニファイド メッセージングを展開する際、前提条件および構成設定がドキュメント化されます。この情報を使用して構成に関する注意事項が作成されます。

PBX の構成に関する注意事項にはそれぞれ、VoIP ゲートウェイ、IP PBX、または PBX の製造元、モデル、およびファームウェア バージョンを含め、特定のテレフォニー構成を使用してユニファイド メッセージングを展開する方法についての情報が含まれます。さらに、それぞれの PBX 構成に関する注意事項には、次のようなその他の情報も含まれます。

  - 構成に関する注意事項の作成者。

  - 詳細な前提条件 :
    
      - PBX 上で有効または無効にする必要がある機能。
    
      - インストールする必要がある特別なハードウェア。
    
      - VoIP ゲートウェイが必要かどうか。
    
      - VoIP ゲートウェイが必要な場合は、その VoIP ゲートウェイで必要な機能。
    
      - IP ゲートウェイと PBX との間の特定のケーブル接続要件。
    
      - 特定のテレフォニー構成では利用できない場合があるユニファイド メッセージング機能の一覧。

資格のある SIP PSTN ゲートウェイと IP PBX の検索、テレフォニー インフラストラクチャ ベンダーがプログラムに参加するプロセスなど、エンタープライズ テレフォニー インフラストラクチャの Microsoft Unified Communications Open Interoperability Program の詳細については、「[Microsoft Unified Communications Open Interoperability Program](https://go.microsoft.com/fwlink/p/?linkid=132071)」を参照してください。

## VoIP ゲートウェイ、IP PBX、および PBX の構成に関する注意事項

Microsoft は、VoIP ゲートウェイ パートナーである AudioCodes および Dialogic と共同で、テスト済みの PBX の一覧に項目を追加しています。テレフォニー コンポーネントのさまざまな組み合わせを現在テスト中であるため、このトピックは頻繁に更新されます。実際の展開に適した構成に関する注意事項が見つからない場合は、再度アクセスしてください。

以下の構成に関する注意事項があります。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Aastra</p></li>
<li><p>Alcatel</p></li>
<li><p>Avaya</p></li>
<li><p>Cisco</p></li>
<li><p>Inter-Tel</p></li>
<li><p>Intecom</p></li>
<li><p>Mitel</p></li>
<li><p>NEC</p></li>
</ul></td>
<td><ul>
<li><p>NeXspan</p></li>
<li><p>Nortel</p></li>
<li><p>Panasonic</p></li>
<li><p>Rolm</p></li>
<li><p>ShoreTel</p></li>
<li><p>Siemens</p></li>
<li><p>Sonus</p></li>
<li><p>Tadiran</p></li>
<li><p>Toshiba</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Aastra


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX モデル</th>
<th>PBX ソフトウェア リリース</th>
<th>プロトコル</th>
<th>ゲートウェイ ベンダー</th>
<th>ゲートウェイ モデル</th>
<th>構成の作成者</th>
<th>構成ファイルのダウンロード</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aastra MD110 (以前の Ericsson MD110)</p></td>
<td><p>MX1 TSW R2A (aka BC13)</p></td>
<td><p>アナログ - シリアル MD110</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>Aastra MD110 (以前の Ericsson MD110)</p></td>
<td><p>MX1 TSW R2A (aka BC13)</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">ダウンロード</a></p></td>
</tr>
<tr class="odd">
<td><p>Aastra MX-ONE</p></td>
<td><p>4.0</p></td>
<td><p>直接 SIP 接続</p></td>
<td><p>該当なし</p></td>
<td><p>該当なし</p></td>
<td><p>Aastra</p></td>
<td><p><a href="http://www.aastra.com/cps/rde/aareddownload?file_id=4384-14746-_p06_xml%26dsproject=aastra%26mtype=pdf">ダウンロード</a></p></td>
</tr>
</tbody>
</table>


## Alcatel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX モデル</th>
<th>PBX ソフトウェア リリース</th>
<th>プロトコル</th>
<th>ゲートウェイ ベンダー</th>
<th>ゲートウェイ モデル</th>
<th>構成の作成者</th>
<th>構成ファイルのダウンロード</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>OmniPCX 4400</p></td>
<td><p>R4.2-d2.304-4-h-il-c6s2</p></td>
<td><p>アナログ – インバンド DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
</tbody>
</table>


## Avaya


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX モデル</th>
<th>PBX ソフトウェア リリース</th>
<th>プロトコル</th>
<th>ゲートウェイ ベンダー</th>
<th>ゲートウェイ モデル</th>
<th>構成の作成者</th>
<th>構成ファイルのダウンロード</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aura</p></td>
<td><p>Communication Manager 5.2.1 SP 5</p>
<p>Session Manager 5.2.</p></td>
<td><p>直接 SIP 接続</p></td>
<td><p>該当なし</p></td>
<td><p>該当なし</p></td>
<td><p>Avaya</p></td>
<td><p><a href="https://support.avaya.com/downloads/">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>CS 2100</p></td>
<td><p>CS 2100 SE13</p></td>
<td><p>直接 SIP 接続</p></td>
<td><p>該当なし</p></td>
<td><p>該当なし</p></td>
<td><p>Avaya</p></td>
<td><p><a href="https://support.avaya.com/css/p8/documents/100149819">ダウンロード</a></p></td>
</tr>
<tr class="odd">
<td><p>Definity G3</p></td>
<td><p>R009i.05.122.4</p></td>
<td><p>Digital Set Emulation (DNI7434)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>Definity G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>アナログ – インバンド DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="odd">
<td><p>Definity G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>T1 CAS – インバンド DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>Definity G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="odd">
<td><p>Definity G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>Merlin Magix</p></td>
<td><p>Release 1.5 v.6.0</p></td>
<td><p>アナログ – インバンド DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="odd">
<td><p>S8300</p></td>
<td><p>G3xV11 Communication Manager 1.3</p></td>
<td><p>アナログ – インバンド DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>S8300</p></td>
<td><p>R013x.01.2.632.1</p></td>
<td><p>T1 CAS – インバンド DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="odd">
<td><p>S8300</p></td>
<td><p>R013x.01.2.632.1</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>S8500</p></td>
<td><p>Communication Manager 3.0 (R013x00.1.346.0)</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">ダウンロード</a></p></td>
</tr>
<tr class="odd">
<td><p>S8500</p></td>
<td><p>Communication Manager 3.0 (R013x00.1.346.0)</p></td>
<td><p>T1 CAS – インバンド DTMF</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>S8500</p></td>
<td><p>Communication Manager 3.0 (R013x00.1.346.0)</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">ダウンロード</a></p></td>
</tr>
<tr class="odd">
<td><p>S8700</p></td>
<td><p>R011x.02.0.110.4</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
</tbody>
</table>


## Cisco


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX モデル</th>
<th>PBX ソフトウェア リリース</th>
<th>プロトコル</th>
<th>ゲートウェイ ベンダー</th>
<th>ゲートウェイ モデル</th>
<th>構成の作成者</th>
<th>構成ファイルのダウンロード</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cisco Call Manager 4.x</p></td>
<td><p>4.x</p></td>
<td><p>IP-to-IP</p></td>
<td><p>AudioCodes</p></td>
<td><p>AudioCodes</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>Cisco Call Manager 5.1</p></td>
<td><p>5.1.0.9921-12</p></td>
<td><p>直接 SIP 接続</p></td>
<td><p>該当なし</p></td>
<td><p>該当なし</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=225083">ダウンロード</a></p></td>
</tr>
<tr class="odd">
<td><p>Cisco Unified Communications Manager 6.0 および 6.1</p></td>
<td><p>6.x</p></td>
<td><p>直接 SIP 接続</p></td>
<td><p>該当なし</p></td>
<td><p>該当なし</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=225083">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>Cisco Unified Communications Manager 7.0</p></td>
<td><p>7.0.2.20000-5</p></td>
<td><p>直接 SIP 接続</p></td>
<td><p>該当なし</p></td>
<td><p>該当なし</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=196361">ダウンロード</a></p></td>
</tr>
<tr class="odd">
<td><p>Cisco Unified Communications Manager 8.0</p></td>
<td><p>8.0.3.20000-5</p></td>
<td><p>直接 SIP 接続</p></td>
<td><p>該当なし</p></td>
<td><p>該当なし</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=213007">ダウンロード</a></p></td>
</tr>
</tbody>
</table>


## Inter-Tel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX モデル</th>
<th>PBX ソフトウェア リリース</th>
<th>プロトコル</th>
<th>ゲートウェイ ベンダー</th>
<th>ゲートウェイ モデル</th>
<th>構成の作成者</th>
<th>構成ファイルのダウンロード</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>5000</p></td>
<td><p>Inter-Tel 5000 v2.1</p></td>
<td><p>T1 CAS – インバンド DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>Axxess</p></td>
<td><p>Axxess V9.0</p></td>
<td><p>T1 CAS – インバンド DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
</tbody>
</table>


## Intecom


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX モデル</th>
<th>PBX ソフトウェア リリース</th>
<th>プロトコル</th>
<th>ゲートウェイ ベンダー</th>
<th>ゲートウェイ モデル</th>
<th>構成の作成者</th>
<th>構成ファイルのダウンロード</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PointSpan M6880</p></td>
<td><p>40PS3.5.K.2</p></td>
<td><p>T1 CAS - SMDI</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
</tbody>
</table>


## Mitel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX モデル</th>
<th>PBX ソフトウェア リリース</th>
<th>プロトコル</th>
<th>ゲートウェイ ベンダー</th>
<th>ゲートウェイ モデル</th>
<th>構成の作成者</th>
<th>構成ファイルのダウンロード</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>3300</p></td>
<td><p>5.1.4.8</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>3300</p></td>
<td><p>5.1.4.8</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">ダウンロード</a></p></td>
</tr>
<tr class="odd">
<td><p>SX2000</p></td>
<td><p>5.0.24</p></td>
<td><p>Digital Set Emulation (DNISS430)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008MTLDNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>3300</p></td>
<td><p>7</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
</tbody>
</table>


## NEC


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX モデル</th>
<th>PBX ソフトウェア リリース</th>
<th>プロトコル</th>
<th>ゲートウェイ ベンダー</th>
<th>ゲートウェイ モデル</th>
<th>構成の作成者</th>
<th>構成ファイルのダウンロード</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Electra Elite 192</p></td>
<td><p>SP034V4.5</p></td>
<td><p>アナログ – インバンド DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>NEAX2400IMX</p></td>
<td><p>Version 7400</p></td>
<td><p>T1 CAS - シリアル MCI</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">ダウンロード</a></p></td>
</tr>
<tr class="odd">
<td><p>NEAX2400IMX &amp; IPX</p></td>
<td><p>Version 7400</p></td>
<td><p>Digital Set Emulation (DNIDtermIII)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>NEAX2400IPX</p></td>
<td><p>バージョンR18.06.24.000</p></td>
<td><p>T1 CAS - シリアル MCI</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="odd">
<td><p>NEAX2400IPX</p></td>
<td><p>バージョンR18.06.24.000</p></td>
<td><p>アナログ - シリアル MCI</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>NEAX2400IPX</p></td>
<td><p>Ver.17 Rel.03.46.001</p></td>
<td><p>T1 Q.SIG – シリアル MCI</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">ダウンロード</a></p></td>
</tr>
</tbody>
</table>


## NeXspan


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX モデル</th>
<th>PBX ソフトウェア リリース</th>
<th>プロトコル</th>
<th>ゲートウェイ ベンダー</th>
<th>ゲートウェイ モデル</th>
<th>構成の作成者</th>
<th>構成ファイルのダウンロード</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>S</p></td>
<td><p>RMS1 Version R1.3 E1TA</p></td>
<td><p>アナログ – インバンド DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
</tbody>
</table>


## Nortel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX モデル</th>
<th>PBX ソフトウェア リリース</th>
<th>プロトコル</th>
<th>ゲートウェイ ベンダー</th>
<th>ゲートウェイ モデル</th>
<th>構成の作成者</th>
<th>構成ファイルのダウンロード</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CS1000</p></td>
<td><p>3.0 &amp; 4.5</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>Meridian 81C</p></td>
<td><p>4.5</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="odd">
<td><p>Meridian 81C</p></td>
<td><p>4.5</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>Option11c</p></td>
<td><p>Release 25</p></td>
<td><p>Digital Set Emulation (DNI2616)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">ダウンロード</a></p></td>
</tr>
<tr class="odd">
<td><p>Option11c</p></td>
<td><p>Release 25</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>Option11c</p></td>
<td><p>Release 25</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">ダウンロード</a></p></td>
</tr>
<tr class="odd">
<td><p>CS-1000M (連続)</p></td>
<td><p>Release 25.40</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">ダウンロード</a></p></td>
</tr>
</tbody>
</table>


## Panasonic


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX モデル</th>
<th>PBX ソフトウェア リリース</th>
<th>プロトコル</th>
<th>ゲートウェイ ベンダー</th>
<th>ゲートウェイ モデル</th>
<th>構成の作成者</th>
<th>構成ファイルのダウンロード</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KX-TDA200</p></td>
<td><p>001-001</p></td>
<td><p>アナログ - インバンド DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>KX-TDA200</p></td>
<td><p>3</p></td>
<td><p>アナログ - インバンド DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="odd">
<td><p>KX-TES824</p></td>
<td><p>2.0.2</p></td>
<td><p>アナログ - インバンド DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
</tbody>
</table>


## Rolm


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX モデル</th>
<th>PBX ソフトウェア リリース</th>
<th>プロトコル</th>
<th>ゲートウェイ ベンダー</th>
<th>ゲートウェイ モデル</th>
<th>構成の作成者</th>
<th>構成ファイルのダウンロード</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>9751</p></td>
<td><p>9005</p></td>
<td><p>Digital Set Emulation (DNIRP400)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008RLMDNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">ダウンロード</a></p></td>
</tr>
</tbody>
</table>


## ShoreTel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX モデル</th>
<th>PBX ソフトウェア リリース</th>
<th>プロトコル</th>
<th>ゲートウェイ ベンダー</th>
<th>ゲートウェイ モデル</th>
<th>構成の作成者</th>
<th>構成ファイルのダウンロード</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IP テレフォニー システム</p></td>
<td><p>6.1</p></td>
<td><p>アナログ – SMDI</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>IP テレフォニー システム</p></td>
<td><p>7.5</p></td>
<td><p>アナログ – SMDI</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
</tbody>
</table>


## Siemens


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX モデル</th>
<th>PBX ソフトウェア リリース</th>
<th>プロトコル</th>
<th>ゲートウェイ ベンダー</th>
<th>ゲートウェイ モデル</th>
<th>構成の作成者</th>
<th>構成ファイルのダウンロード</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>HiCom 150E</p></td>
<td><p>Rel.2.2</p></td>
<td><p>アナログ – インバンド DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>HiCom 300</p></td>
<td><p>SA300-V3.05</p></td>
<td><p>BRI QSIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG3000</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">ダウンロード</a></p></td>
</tr>
<tr class="odd">
<td><p>HiCom 300</p></td>
<td><p>9006.4SMR3</p></td>
<td><p>Digital Set Emulation (DNIOptiset)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>HiCom 300</p></td>
<td><p>9006.4SMR3</p></td>
<td><p>T1 CAS – インバンド DTMF</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">ダウンロード</a></p></td>
</tr>
<tr class="odd">
<td><p>HiPath 3550</p></td>
<td><p>Rel.3</p></td>
<td><p>アナログ – インバンド DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>HiPath 4000</p></td>
<td><p>Version 3.0 SMR5 SMP4</p></td>
<td><p>アナログ – インバンド DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="odd">
<td><p>HiPath 4000</p></td>
<td><p>SA300-V3.05</p></td>
<td><p>BRI QSIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG3000</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>HiPath 4000</p></td>
<td><p>Version 3.0 SMR5 SMP4</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="odd">
<td><p>HiPath 4000</p></td>
<td><p>Version 2.0 SMR9 SMP0</p></td>
<td><p>アナログ - インバンド DTMF</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>HiPath 4000</p></td>
<td><p>Version 2.0 SMR9 SMP0</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">ダウンロード</a></p></td>
</tr>
</tbody>
</table>


## Sonus


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>VoIP ゲートウェイ モデル</th>
<th>VoIP ゲートウェイ ソフトウェア リリース</th>
<th>サポートされるプロトコル</th>
<th>構成の作成者</th>
<th>構成ファイルのダウンロード</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SBC 1000/2000</p></td>
<td><p>2.2.1 以降</p></td>
<td><ul>
<li><p>TDM シグナリング (ISDN): AT&amp;T 4ESS/5ESS、Nortel DMS- 100、Euro ISDN (ETSI 300-102)、QSIG、NTT InsNet (日本)、ANSI National ISDN-2 (NI-2)</p></li>
<li><p>TDM Signaling (CAS): T1 CAS (E&amp;M、ループ スタート)、E1 CAS (R2)</p></li>
</ul></td>
<td><p>Sonus</p></td>
<td><p><a href="http://www.sonus.net/sites/default/files/sonussbc1k2kconfigo365.pdf">ダウンロード</a></p></td>
</tr>
</tbody>
</table>


## Tadiran


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX モデル</th>
<th>PBX ソフトウェア リリース</th>
<th>プロトコル</th>
<th>ゲートウェイ ベンダー</th>
<th>ゲートウェイ モデル</th>
<th>構成の作成者</th>
<th>構成ファイルのダウンロード</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Coral Flexicom</p></td>
<td><p>14.67.49</p></td>
<td><p>アナログ – インバンド DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>Coral Flexicom</p></td>
<td><p>14.67.49</p></td>
<td><p>BRI QSIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant</p>
<p>1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="odd">
<td><p>Coral Flexicom</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 CAS – インバンド DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>Coral Flexicom</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="odd">
<td><p>Coral IPX</p></td>
<td><p>14.67.49</p></td>
<td><p>アナログ – インバンド DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>Coral IPX</p></td>
<td><p>14.67.49</p></td>
<td><p>BRI QSIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="odd">
<td><p>Coral IPX</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 CAS – インバンド DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>Coral IPX</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 QSIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant</p>
<p>1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">ダウンロード</a></p></td>
</tr>
</tbody>
</table>


## Toshiba


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX モデル</th>
<th>PBX ソフトウェア リリース</th>
<th>プロトコル</th>
<th>ゲートウェイ ベンダー</th>
<th>ゲートウェイ モデル</th>
<th>構成の作成者</th>
<th>構成ファイルのダウンロード</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CTX</p></td>
<td><p>AR1ME021.00</p></td>
<td><p>アナログ – SMDI</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">ダウンロード</a></p></td>
</tr>
<tr class="even">
<td><p>CTX</p></td>
<td><p>AR1ME021.00</p></td>
<td><p>アナログ – インバンド DTMF</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">ダウンロード</a></p></td>
</tr>
</tbody>
</table>

