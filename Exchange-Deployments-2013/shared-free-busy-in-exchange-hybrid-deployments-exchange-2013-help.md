﻿---
title: 'Exchange ハイブリッド展開における空き時間情報の共有: Exchange 2013 Help'
TOCTitle: Exchange ハイブリッド展開における空き時間情報の共有
ms:assetid: bd3884de-80ee-4ff2-a8a3-eacd5aa3e51b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ650274(v=EXCHG.150)
ms:contentKeyID: 49894954
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange ハイブリッド展開における空き時間情報の共有

 

_<strong>適用先:</strong>Exchange Server 2013, Exchange Server 2016_

_<strong>トピックの最終更新日:</strong>2016-04-29_

ハイブリッド展開の大きなメリットの 1 つとして、社内組織ユーザーと Exchange Online 組織ユーザーの間で空き時間 (予定表の空き時間) 情報を共有できることが挙げられます。両方の組織のユーザーは、あたかも物理的に同じ組織内にいるかのように、互いの予定表を閲覧することができます。これにより、会議やリソースを簡単にしかも効率的にスケジューリングできます。

オンプレミス Exchange 組織と Exchange Online 間の空き時間情報の共有機能を有効にするには、ハイブリッド展開において次のようないくつかのコンポーネントが必要になります。

  - **フェデレーションの信頼**   オンプレミスの組織と Office 365 サービス組織の両方で、Azure AD 認証システムとのフェデレーションの信頼を確立しておく必要があります。フェデレーション信頼は、Exchange 組織のパラメーターを定義する Azure AD 認証システムとの 1 対 1 の関係です。システムはこれらのパラメーターを使用することにより、社内組織と Office 365 サービス組織の間の信頼を仲介し、社内組織ユーザーと Exchange Online 組織ユーザーとの間で空き時間情報を交換します。
    
    システムによるフェデレーション信頼は、Office 365 サービス組織でアカウントが作成された時点で自動的に設定されます。ハイブリッド構成ウィザードは、オンプレミスの組織の Azure AD 認証システムとの既存のフェデレーション信頼が存在するかどうかを自動的に確認します。存在する場合は、既存のフェデレーション信頼がハイブリッド展開のサポートに使用されます。存在しない場合、ウィザードはオンプレミスの組織の Azure AD 認証システムとのフェデレーションの信頼を作成します。また、ウィザードは、ハイブリッド構成ウィザード内で選択されたすべてのドメインを社内組織のフェデレーションの信頼に追加します。
    
    詳細については、「[共有](https://technet.microsoft.com/ja-jp/library/dd638083\(v=exchg.150\))」を参照してください。

  - **組織上の関係**   組織上の関係は、社内組織と Exchange Online 組織の両方に必要で、ハイブリッド構成ウィザードによって自動的に構成されます。組織で共有される空き時間情報のレベルは、組織上の関係によって定義されます。
    
    規定では、空き時間データの共有アクセス レベルは、社内組織と Exchange Online 組織の両方で **\[時刻、件名、場所を指定して空き時間情報にアクセス\]** に設定されています。社内組織ユーザーと Exchange Online 組織ユーザー間の空き時間データの共有アクセスを変更する場合は、ハイブリッド構成ウィザードの終了後に組織上の関係を手動で設定できます。
    
    詳細については、「[共有](https://technet.microsoft.com/ja-jp/library/dd638083\(v=exchg.150\))」を参照してください。

ハイブリッド展開するように組織を構成する場合、空き時間予定表の共有アクセス権限は、どのシナリオでも、ハイブリッド構成ウィザードによって自動的に構成されます。Azure AD 認証システムを使用してフェデレーションの信頼を作成することと、オンプレミスの組織と Exchange Online 組織の組織上の関係を構成することは、ハイブリッド展開の要件です。ハイブリッド展開においてオンプレミスの組織ユーザーと Exchange Online 組織ユーザー間で空き時間情報の共有を有効にしない場合は、ハイブリッド構成ウィザードの終了後に、Exchange 管理シェル と [Set-HybridConfiguration](https://technet.microsoft.com/ja-jp/library/hh529932\(v=exchg.150\)) コマンドレットを使用して空き時間情報の共有を手動で無効にすることができます。

次の表に示すハイブリッド展開での機能は、フェデレーションの信頼と組織上の関係に応じて異なります。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>メッセージの範囲</th>
<th>機能</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>電子メール クライアント</p></td>
<td><ul>
<li><p>メッセージ追跡</p></li>
<li><p>メール ヒント</p></li>
<li><p>複数のメールボックスの検索</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>準拠</p></td>
<td><ul>
<li><p>Exchange Online Archiving</p></li>
<li><p>Exchange インプレース電子情報開示</p></li>
</ul></td>
</tr>
</tbody>
</table>

