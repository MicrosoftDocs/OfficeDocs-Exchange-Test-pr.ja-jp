---
title: 'Outlook Voice Access 番号の構成: Exchange Online Help'
TOCTitle: Outlook Voice Access 番号の構成
ms:assetid: 443c838e-f266-4893-b6b2-e5fc96579b55
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997680(v=EXCHG.150)
ms:contentKeyID: 50555769
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Voice Access 番号の構成

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

Outlook Voice Access 番号を使用すると、ユニファイド メッセージング (UM) とボイス メールが有効なユーザーが Outlook Voice Access を使用して自分のメールボックスにアクセスできます。ダイヤル プランに Outlook Voice Access またはサブスクライバー アクセス番号を構成すると、UM が有効なユーザーはその番号にアクセスして、メールボックスにサインインして、自分の電子メール、ボイス メール、予定表、および個人用連絡先情報にアクセスすることができます。

既定では、UM ダイヤル プランの作成時に、Outlook Voice Access 番号は構成されません。Outlook Voice Access 番号を構成するには、最初にダイヤル プランを作成する必要があり、続いてダイヤル プランの <strong>Outlook Voice Access</strong> オプションの下で Outlook Voice Access 番号を構成します。Outlook Voice Access 番号は必須ではありませんが、UM が有効なユーザーが Outlook Voice Access を使用して自分のメールボックスにアクセスできるようにするには、少なくとも 1 つの Outlook Voice Access 番号を構成する必要があります。1 つのダイヤル プランに複数の Outlook Voice Access 番号を構成することができます。

Outlook Voice Access 番号には、アルファベット、数字、特殊文字、区切り文字、空白を含めることができます。次に例を示します。

  - \+14255551010

  - \+1-425-555-1010

  - 4255551010

  - \+1 425 555 1010

  - 1-800-555-CALL

Outlook Voice Access ユーザーが使用できるメニュー オプションの詳細については、Outlook Voice Access のクイック リファレンス ガイドを参照してください。このガイドは、[Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/p/?linkid=64645)から入手できます。

UM ダイヤル プランに関連するその他の管理タスクについては、「[UM ダイヤル プラン手順](um-dial-plan-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ダイヤル プラン」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して Outlook Voice Access 番号を構成する

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。

2.  リスト ビューで、修正する UM ダイヤル プランを選択し、ツール バーで、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン")をクリックします。

3.  <strong>UM ダイヤル プラン</strong> ページで、<strong>構成</strong> をクリックします。

4.  <strong>Outlook Voice Access</strong> の <strong>Outlook Voice Access 番号</strong> の下で、使用する番号をボックスに入力してから <strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン")をクリックします。

5.  <strong>保存</strong> をクリックします。

## シェルを使用して Outlook Voice Access 番号を構成する

この例では、Outlook Voice Access 番号を `MyUMDialPlan` という名前の UM ダイヤル プランの 4255550100 と設定します。

    Set-UMDialPlan -identity MyUMDialPlan -AccessTelephoneNumbers 4255550100

