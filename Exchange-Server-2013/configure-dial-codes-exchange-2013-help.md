---
title: 'ダイヤル コードを構成する: Exchange Online Help'
TOCTitle: ダイヤル コードを構成する
ms:assetid: e5b5efee-b734-4f70-8357-11be07b23bd0
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124992(v=EXCHG.150)
ms:contentKeyID: 51407590
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ダイヤル コードを構成する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) が有効なユーザーに対して着信呼び出しおよび発信呼び出しをダイヤルするために、UM で使用するダイヤル コード、番号プレフィックス、および番号形式を構成できます。ほとんどの場合、現在テレフォニー ネットワークで構成されているダイヤル コード、プレフィックス、および番号形式でダイヤル プランを構成します。

ダイヤル コードと番号プレフィクスは、UM が有効なユーザーによる発信呼び出しでダイヤルする正しい番号を決定するために使用されます。*アウトダイヤル*とは、UM ダイヤル プラン内のユーザーが発信呼び出しを開始するプロセスを説明するために使用される用語です。番号形式は、国または地域内の着信呼び出し、国際呼び出し、またはダイヤル プラン内で発信された呼び出しで使用されます。国/地域内の番号と国際番号の両方で着信呼び出し番号形式が一致するようにダイヤル プランを構成できます。国/地域内の番号と国際番号の形式を構成すると、ダイヤル プランにリンクされたユーザーの着信呼び出しを制限できます。

アウトダイヤルに関するその他の管理タスクについては、「[呼び出しプロシージャの作成をユーザーに許可する](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/allow-users-to-make-calls-procedures)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ダイヤル プラン」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してダイヤル コード、プレフィックス、および番号形式を構成する

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。

2.  管理する UM ダイヤル プランを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>UM ダイヤル プラン</strong> ページで、<strong>構成</strong> をクリックします。

4.  <strong>UM ダイヤル プラン</strong> ページの <strong>ダイヤル コード</strong> で、次のオプションを構成します。
    
      - **外線発信コード**
    
      - **国際アクセス コード**
    
      - **国番号のプレフィックス**
    
      - **国/地域番号**

5.  <strong>ダイヤル プラン間でダイヤルするための番号形式</strong> で、次の形式を構成します。
    
      - **国/地域番号の形式**
    
      - **国際番号の形式**
    
      - <strong>同じダイヤル プラン内での着信呼び出しの番号形式</strong>   番号形式を追加するには、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

6.  <strong>保存</strong> をクリックして変更を保存します。

## シェルを使用してダイヤル コード、プレフィックス、および番号形式を構成する

この例では、国内または地域内の番号の形式、国際番号の形式、および次のダイヤル コードで、`MyUMDialPlan` という名前の UM ダイヤル プランを構成します。

  - 外線発信コードは 9

  - 国際アクセス コードは 011

  - 国番号のプレフィックスは 1

  - 国/地域コードは 1

<!-- end list -->

    Set-UMDialPlan -Identity MyUMDialPlan -OutsideLineAccessCode 9 -InternationalAccessCode 011 -NationalNumberPrefix 1 CountryorRegionCode 1 -InCountryOrRegionNumberFormat 1425xxxxxxx -InternationalNumberFormat 441425xxxxxxx

