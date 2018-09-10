---
title: 'Outlook Voice Access ユーザー用にカスタマイズした案内応答を有効にする: Exchange Online Help'
TOCTitle: Outlook Voice Access ユーザー用にカスタマイズした案内応答を有効にする
ms:assetid: abd418ec-2c65-4720-859d-c11a2698dc06
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124125(v=EXCHG.150)
ms:contentKeyID: 50555849
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Voice Access ユーザー用にカスタマイズした案内応答を有効にする

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

既定では、各ユニファイド メッセージング (UM) ダイヤル プランでは、発信者に再生される案内応答として標準の .wav ファイルが使用されます。これらの発信者には、構成されている Outlook Voice Acces 番号にダイヤルインする Outlook Voice Access ユーザーも含まれます。ただし、案内応答の .wav ファイルまたは .wma ファイルを作成し、そのファイルを UM ダイヤル プランで有効にできます。

たとえば、既定の案内応答を変更して、代わりに "こちらは Woodgrove 銀行の Outlook Voice Access です" などの、自社固有の案内応答を設定することもできます。それには、カスタマイズした案内応答を録音し、それを .wav ファイルまたは .wma ファイルとして保存します。次に、カスタマイズした案内応答を使用するようにダイヤル プランを構成します。

Outlook Voice Access ユーザーが使用できるメニュー オプションの詳細については、Outlook Voice Access のクイック リファレンス ガイドを参照してください。このガイドは、[Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/p/?linkid=272767)から入手できます。

UM ダイヤル プランに関連するその他の管理タスクについては、「[UM ダイヤル プラン手順](um-dial-plan-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ダイヤル プラン」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してカスタマイズした案内応答を有効にする

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。

2.  リスト ビューで、変更する UM ダイヤル プランを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>UM ダイヤル プラン</strong> ページで、<strong>構成</strong> をクリックします。

4.  <strong>Outlook Voice Access</strong> の <strong>案内応答</strong> で <strong>変更</strong> をクリックし、<strong>参照</strong> をクリックして案内応答ファイルを特定します。
    

    > [!IMPORTANT]
    > 案内応答として使用するファイルは, .wav ファイルまたは .wma ファイルである必要があります。



5.  ファイルを特定した後に <strong>開く</strong> をクリックし、<strong>保存</strong> をクリックします。

## シェルを使用してカスタマイズした案内応答を有効にする

この例では、`MyUMDialPlan` という UM ダイヤル プランで、C:\\UMPrompts\\welcome.wav ファイルを使用する応答案内を有効にします。

    Set-UMDialPlan -Identity MyUMDialPlan -WelcomeGreetingEnabled $true -WelcomeGreetingFilename c:\UMPrompts\welcome.wav

