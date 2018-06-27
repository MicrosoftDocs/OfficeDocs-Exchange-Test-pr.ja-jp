---
title: '携帯電話とタブレットの機能: Exchange 2013 Help'
TOCTitle: 携帯電話とタブレットの機能
ms:assetid: ad54d9e6-7a1c-4fb0-b5a9-0b042b98ada3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb232162(v=EXCHG.150)
ms:contentKeyID: 50555852
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 携帯電話とタブレットの機能

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-03-09_

ユーザーは Microsoft Exchange ActiveSync を使用して、携帯電話、タブレット、および他のポータブル デバイス上の電子メール、予定表、連絡先、およびタスクの情報にアクセスできます。Microsoft Exchange ActiveSync を使用して、署名や自動返信を設定することもできます。さまざまな携帯電話やモバイル デバイスが Exchange ActiveSync で動作します。


> [!NOTE]
> Exchange Server 2013 にアクセスするデバイスを常に携帯電話と呼んでいますが、Exchange 2013 にアクセスでき、携帯電話機能を持たないデバイスは多数あります。このドキュメントでは、そうしたデバイスも "携帯電話" と呼んでいます。



## Exchange ActiveSync 互換デバイス

ユーザーは、Exchange ActiveSync と互換性のある携帯電話を選択することによって、Exchange ActiveSync の豊富な機能を活用できます。これらの携帯電話は多くの製造元から、多くのキャリアで入手できます。詳細については、各携帯電話のドキュメントを参照してください。

Microsoft Exchange と互換性のある携帯電話には、次のようなものがあります。

  - **Apple**   Apple 社製の iPhone、iPod Touch および iPad Exchange ActiveSync はいずれもサポート対象です。

  - **Windows Phone**   Windows Phone 8、Windows Phone 7、およびすべての旧バージョンは、Exchange ActiveSync をサポートしています。

  - **Android**   Android オペレーティング システムを搭載した多くの携帯電話およびタブレットが Exchange ActiveSync をサポートしています。ただし、これらのモバイル デバイスでは、使用可能なモバイル デバイス メールボックス ポリシーの一部がサポートされない場合があります。詳細については、「[モバイル デバイス メールボックス ポリシー](mobile-device-mailbox-policies-exchange-2013-help.md)」を参照してください。

## Windows Phone ソフトウェアの機能

何らかのバージョンの Windows Phone ソフトウェアをオペレーティング システムとして搭載した携帯電話は、Exchange 2013 と同期する場合に優れた機能を提供します。次の表に、Windows Phone 8 および Windows Phone 7 で使用可能なモバイル デバイス メールボックス ポリシーを示します。

### Windows Phone 7 および Windows Phone 8 の機能

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>オペレーティング システム</th>
<th>機能</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Phone 8</p></td>
<td><p>Windows Phone 8 では、次のモバイル デバイス メールボックス ポリシーがサポートされます。</p>
<ul>
<li><p>簡易デバイス パスワードを許可する</p></li>
<li><p>英数字のパスワードが必要</p></li>
<li><p>デバイス パスワードが有効</p></li>
<li><p>デバイス パスワードの有効期限</p></li>
<li><p>IRM が有効</p></li>
<li><p>デバイス パスワードの入力ミスが許される最大回数</p></li>
<li><p>デバイスのロックをかけるまでの最大休止時間</p></li>
<li><p>デバイスのパスワードの複雑な文字の最少数</p></li>
<li><p>デバイス パスワードの最小文字数</p></li>
<li><p>デバイスでの暗号化が必要</p></li>
<li><p>リモート ワイプ</p></li>
</ul>

> [!WARNING]
> 組織が他のモバイル デバイス メールボックス ポリシー設定を使用する場合は、<STRONG>[サポートしていないデバイスのアクセスを許可する]</STRONG> ポリシーを true に設定する必要があります。モバイル デバイスのポリシー設定の一部の要件を満たしていない他の携帯電話およびモバイル デバイスでは同期が許可されないため、これには、組織のセキュリティとの密接な関係があります。詳細については、「<A href="mobile-device-mailbox-policies-exchange-2013-help.md">モバイル デバイス メールボックス ポリシー</A>」を参照してください。


</td>
</tr>
<tr class="even">
<td><p>Windows Phone 7</p></td>
<td><p>Windows Phone 7 の携帯電話は、すべての Exchange ActiveSync メールボックス ポリシー設定のうちの一部だけをサポートしています。</p>
<ul>
<li><p>パスワードが必要</p></li>
<li><p>パスワードの最小文字数</p></li>
<li><p>ロックをかけるまでの休止時間</p></li>
<li><p>デバイス パスワードの入力ミスが許される最大回数</p></li>
<li><p>簡易パスワードを許可する</p></li>
<li><p>パスワードの期限切れ</p></li>
<li><p>パスワードの履歴</p></li>
<li><p>リムーバブル記憶域の無効化</p></li>
<li><p>IrDA の無効化</p></li>
<li><p>デスクトップ同期の無効化</p></li>
<li><p>リモート デスクトップのブロック</p></li>
<li><p>インターネット共有のブロック</p></li>
</ul></td>
</tr>
</tbody>
</table>

