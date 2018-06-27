---
title: 'サポートされているセッション ボーダー コントローラーの構成に関する注意事項: Exchange 2013 Help'
TOCTitle: サポートされているセッション ボーダー コントローラーの構成に関する注意事項
ms:assetid: d161f94a-a243-4294-93b3-2bf1dc17b59f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ673565(v=EXCHG.150)
ms:contentKeyID: 50555876
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# サポートされているセッション ボーダー コントローラーの構成に関する注意事項

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:**2017-07-25_

セッション ボーダー コントローラー (SBC) により、社内テレフォニー ネットワークを専用の公衆 WAN 接続経由で Microsoft データセンターに接続できます。SBC は社内 IP ネットワークのエッジに配置され、Microsoft データセンターの第 2 の SBCに接続されます。

SBC では、デジタル証明書を使用して、社内組織とマイクロソフトのデータセンター間のすべてのトラフィックを暗号化する必要があります。Exchange ハイブリッド展開および Exchange オンライン展開との通信に使用するネットワーク境界要素 (セッション ボーダー コントローラーなど) のデジタル証明書を取得する必要があります。デジタル証明書によって、社内組織とマイクロソフトのデータセンターの間に信頼が確立され、相互トランスポート層セキュリティ (相互 TLS) が有効になります。この信頼の確立後に、社内組織とマイクロソフトのデータセンターのネットワーク境界要素でセッション キーが交換され、これらのキーを使用して以降のデータ トラフィックが暗号化されます。

ハイブリッド展開またはオンライン展開では、UM IP ゲートウェイは SBC を表します。証明書のサブジェクトの共通名は、作成した UM IP ゲートウェイの "アドレス" ボックスにある完全修飾ドメイン名 (FQDN) の値と一致する必要があります。たとえば、UM IP ゲートウェイの FQDN アドレス sbcexternal.contoso.com を指定した場合は、証明書のサブジェクト名とサブジェクトの別名に同じ値 (sbcexternal.contoso.com) が含まれていることを確認します。使用する名前では大文字と小文字が区別されるため、証明書と UM IP ゲートウェイの両方において大文字と小文字が同じであることを確認してください。Acme Packet SBC を使用していて、共通名が UM IP ゲートウェイの FQDN と一致しない場合、403 エラーが発生して呼び出しは拒否されます。


> [!NOTE]
> SBC は、ネットワーク エッジに配置するように設計されているため、ファイアウォールとしても機能します。組織のファイアウォールの背後に SBC を設定すると、構成上の問題が発生する可能性があり、Office 365 への接続でサポートされていません。



## サポートされるセッション ボーダー コント ローラー

以下の SBC は、Exchange ハイブリッド展開および Exchange オンライン展開との相互運用性のテストに合格しています。SBC の機能と互換性は変化する可能性があり、SBC を設定する方法は、ネットワーク上のその他の機器に応じて異なる可能性があります。SBC の製造元に連絡して、ハイブリッド展開またはオンライン展開のユニファイド メッセージングについて、特定の構成に関する注意事項があるかどうかを確認してください。


> [!NOTE]
> SBCs の運営、顧客からの直接接続を使用してサード パーティの PBX システムのサポート オンライン UM は、2018年 7 月で終了します。 詳細については Exchange チームのブログ<A href="https://blogs.technet.microsoft.com/exchange/2017/07/18/discontinuation-of-support-for-session-border-controllers-in-exchange-online-unified-messaging/">で Exchange のオンライン セッションの枠線のコント ローラーのサポートの提供中止はユニファイド メッセージング</A>を参照してください。




<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>ベンダー</strong></p></td>
<td><p><strong>モデル</strong></p></td>
<td><p><strong>構成に関する注意事項</strong></p></td>
<td><p><strong>コメント</strong></p></td>
</tr>
<tr class="even">
<td><p><a href="http://www.acmepacket.com">Acme パケット</a></p></td>
<td><p>Net-Net 3820 または 4500</p></td>
<td><p><strong>それらのデバイスを設定する方法の最新の手順については、ハードウェア ベンダーにお問い合わせください。</strong></p></td>
<td><p>専用の SBC</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://www.audiocodes.com">AudioCodes</a></p></td>
<td><p>Mediant 1000B MSBG</p></td>
<td><p><strong>それらのデバイスを設定する方法の最新の手順については、ハードウェア ベンダーにお問い合わせください。</strong></p></td>
<td><p>専用の SBC</p></td>
</tr>
<tr class="even">
<td><p><a href="https://www.audiocodes.com">AudioCodes</a></p></td>
<td><p>Mediant 1000B MSBG</p></td>
<td><p><strong>それらのデバイスを設定する方法の最新の手順については、ハードウェア ベンダーにお問い合わせください。</strong></p></td>
<td><p>SBC と IP ゲートウェイ</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://www.cisco.com/c/dam/en/us/solutions/collateral/enterprise-networks/unified-access/cube-asr-release-10-0.pdf">Cisco</a></p></td>
<td><p>ASR 1000</p>

> [!NOTE]
> IOS 15.4(3)S3 以降がインストールされている必要があります。


</td>
<td><p><strong>それらのデバイスを設定する方法の最新の手順については、ハードウェア ベンダーにお問い合わせください。</strong></p></td>
<td><p>専用の SBC</p></td>
</tr>
<tr class="even">
<td><p><a href="https://www.ingate.com/">Ingate</a></p></td>
<td><p>SIParator</p></td>
<td><p><strong>それらのデバイスを設定する方法の最新の手順については、ハードウェア ベンダーにお問い合わせください。</strong></p></td>
<td><p>専用の SBC</p></td>
</tr>
<tr class="odd">
<td><p><a href="http://www.net.com">NET</a></p></td>
<td><p>VX1200 &amp; VX1800</p></td>
<td><p><strong>それらのデバイスを設定する方法の最新の手順については、ハードウェア ベンダーにお問い合わせください。</strong></p></td>
<td><p>VoIP ゲートウェイ製品用の SBC オプション</p></td>
</tr>
<tr class="even">
<td><p><a href="http://www.sonus.net/">Sonus</a></p></td>
<td><p>SBC 1000/2000 2.2.1 以上</p></td>
<td><p><strong>それらのデバイスを設定する方法の最新の手順については、ハードウェア ベンダーにお問い合わせください。</strong></p></td>
<td><p>専用の SBC</p></td>
</tr>
</tbody>
</table>

