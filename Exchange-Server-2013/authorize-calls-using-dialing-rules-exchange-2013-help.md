---
title: 'ダイヤル ルールを使用して呼び出しを承認する: Exchange Online Help'
TOCTitle: ダイヤル ルールを使用して呼び出しを承認する
ms:assetid: 4c18bc07-f55c-42b7-81c1-729878aa93aa
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ898499(v=EXCHG.150)
ms:contentKeyID: 51407525
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ダイヤル ルールを使用して呼び出しを承認する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

既定では、ユーザーは送信呼び出しを配置することはできません。ユーザーが実行できる呼び出しの種類を指定するには、まず、ダイヤル ルールを作成してから、それらのダイヤル ルールのグループを UM ダイヤル プラン、UM メールボックス ポリシー、または UM 自動応答で承認します。ダイヤル ルール グループを承認するには、UM ダイヤル プランでダイヤル ルールを定義する必要があります。詳細については、「[ユーザーのダイヤル ルールを作成する](create-dialing-rules-for-users-exchange-2013-help.md)」を参照してください。

作成するダイヤル ルールには、ユーザーがアクセスできるようにする呼び出しの種類または番号パターンを含めます。種類が異なるユーザーに、種類が異なる呼び出しを許可することができます。許可する呼び出しは、国内または地域内、あるいは国際を指定できます。

ダイヤルを承認または制限するには、次の設定を正しく構成する必要があります。

  - **ダイヤル ルール**   ダイヤル ルールは、UMが有効になっているユーザーがダイアルする番号と、ユニファイド メッセージングから送信され、構内交換機 (PBX) または IP PBX によってダイヤルされる番号を定義します。ダイヤル ルール グループは、ダイヤル ルールを追加して作成します。ダイヤル ルール グループを作成したら、国内/地域内または国際ダイヤル ルール グループの承認された呼び出しの一覧に追加します。

  - **ダイヤル ルール グループ**   ダイヤル ルール グループは、ダイヤル グループ内のユーザーが発信可能な通話の種類を定義します。

  - **ダイヤルの承認**   ダイヤルの承認を使用して、ユーザーが不要な電話料金を課せられたり、長距離電話を掛けたりすることを防ぐために適用される制限を決定します。

## ダイヤル ルール グループを承認する方法

ダイヤル ルール グループの承認先は、送信呼び出しの実行を許可する発信者の種類によって異なります。たとえば、Outlook Voice Access ユーザーのみが送信呼び出しを行えるようにするには、ダイヤル ルールを作成してそのダイヤル ルール グループを Outlook Voice Access ユーザーがリンクされた UM メールボックス ポリシーで承認します。次の表に、呼び出しの承認方法を発信者の種類別に示します。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>発信者の種類</th>
<th>ダイヤル ルール グループを承認する対象</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>認証されていない発信者が Outlook Voice Access 番号を呼び出し、PIN を入力しない場合</p></td>
<td><p>UM ダイヤル プラン。詳細については、「<a href="authorize-calls-for-users-in-a-dial-plan-exchange-2013-help.md">ダイヤル プランでユーザーの呼び出しを承認する</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>認証されている発信者が Outlook Voice Access 番号を呼び出し、PIN を入力する場合</p></td>
<td><p>その発信者の UM メールボックス ポリシー。詳細については、「<a href="authorize-calls-for-a-group-of-users-exchange-2013-help.md">ユーザー グループの呼び出しを承認する</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>認証されていない発信者が、UM 自動応答で構成された電話番号を呼び出す場合</p></td>
<td><p>UM 自動応答。詳細については、「<a href="authorize-calls-for-auto-attendant-callers-exchange-2013-help.md">自動応答の呼び出し元の呼び出しを承認する</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>


送信呼び出しの実行を承認するユーザーに応じて、ダイヤル プラン、自動応答、または UM メールボックス ポリシーに対する Exchange 管理センター (EAC) の <strong>ダイヤルの承認</strong> ページを使用します。

