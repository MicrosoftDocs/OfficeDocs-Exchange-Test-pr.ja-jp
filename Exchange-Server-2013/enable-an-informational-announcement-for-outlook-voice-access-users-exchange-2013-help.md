---
title: 'Outlook Voice Access ユーザーの情報アナウンスを有効にする: Exchange Online Help'
TOCTitle: Outlook Voice Access ユーザーの情報アナウンスを有効にする
ms:assetid: b69ed0e1-f978-498a-963e-42a047678db4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124344(v=EXCHG.150)
ms:contentKeyID: 50555860
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Voice Access ユーザーの情報アナウンスを有効にする

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) ダイヤル プランで情報アナウンスを有効にすることができます。情報アナウンスは、案内応答より頻繁に変化する一般的なお知らせまたは企業の準拠ポリシーで必要なお知らせに使用します。

既定では、発信者 (構成済みの Outlook Voice Access 番号にダイヤルする Outlook Voice Access ユーザーを含む) に情報アナウンスは再生されません。情報アナウンスを再生するには、ダイヤル プランの作成後、情報アナウンスに使用する .wav ファイルまたは .wma ファイルを作成し、ダイヤル プランの情報アナウンスを有効にする必要があります。

発信者に情報アナウンス全体を聞かせることが重要である場合、アナウンスを中断できないように構成できます。このように構成すると、発信者はキーを押したりコマンドを言ってアナウンスを中断したり停止したりすることはできません。

Outlook Voice Access ユーザーが使用できるメニュー オプションの詳細については、Outlook Voice Access のクイック リファレンス ガイドを参照してください。このガイドは、[Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/p/?linkid=272767)から入手できます (このサイトは英語の場合があります)。

UM ダイヤル プランに関連するその他の管理タスクについては、「[UM ダイヤル プラン手順](um-dial-plan-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ダイヤル プラン」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して情報アナウンスを有効にする

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。

2.  リスト ビューで、変更する UM ダイヤル プランを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>UM ダイヤル プラン</strong> ページで、<strong>構成</strong> をクリックします。

4.  <strong>Outlook Voice Access</strong> の <strong>情報アナウンス</strong> で <strong>変更</strong> をクリックし、<strong>参照</strong> をクリックして情報アナウンス ファイルを特定します。
    

    > [!IMPORTANT]
    > 情報アナウンスとして使用するファイルは, .wav ファイルまたは .wma ファイルである必要があります。



5.  ファイルを特定した後に <strong>開く</strong> をクリックし、<strong>保存</strong> をクリックします。

## シェルを使用して情報アナウンスを有効にする

この例では、`MyUMDialPlan` という UM ダイヤル プランで、informational.wav という情報アナウンス ファイルを使用する情報アナウンスを有効にします。

    Set-UMDialPlan -Identity MyUMDialPlan -InfoAnnouncementEnabled $true-InfoAnnouncementFilename c:\UMGreetings\informational.wav

