---
title: '受信者向けのカスタム メール ヒントを構成する: Exchange Online Help'
TOCTitle: 受信者向けのカスタム メール ヒントを構成する
ms:assetid: df8ee7ae-2486-4890-b057-cda87b4cb1ec
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd638199(v=EXCHG.150)
ms:contentKeyID: 52057526
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 受信者向けのカスタム メール ヒントを構成する

 

_**適用先:**Exchange Online, Exchange Server 2013_

*メール ヒント*とは、Outlook Web App と Microsoft Outlook 2010 およびそれ以降のバージョンでユーザーが電子メール メッセージの作成中に次の操作を行ったときに情報バーに表示される情報メッセージです。

  - 受信者を追加する

  - 添付ファイルを追加する

  - \[返信\] または \[全員に返信\] を選択する

  - 既に受信者にアドレス指定されているメッセージを \[下書き\] フォルダーから開く

あらかじめ用意されたメール ヒントに加え、すべての種類の受信者に対してカスタム メール ヒントを作成することができます。あらかじめ用意されたメール ヒントの詳細については、「[MailTips](mailtips-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 10 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「メール ヒント」。

  - 基本のメール ヒントの構成は、Exchange 管理センター (EAC) またはシェルで行います。ただし、追加のメール ヒント翻訳はシェルでしか構成できません。

  - 受信者にメール ヒントを追加すると、次の 2 つのことが行われます。
    
      - テキストに HTML タグが自動的に追加されます。たとえば、「`This mailbox is not monitored`」 と入力すると、メール ヒントは自動的に次のようになります。`<html><body>This mailbox is not monitored</body></html>`。メール ヒントの追加の HTML タグはサポートされません。
    
      - テキストが自動的に受信者の *MailTipTranslations* プロパティに既定値として追加されます。メール ヒント テキストを変更すると、*MailTipTranslations* プロパティの既定値が自動的に更新されます。

  - メール ヒントの長さは 175 文字 を超えることはできません。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## 受信者のメール ヒントを構成する

## EAC を使用して受信者のメール ヒントを構成する

1.  EAC で、**\[受信者\]** に移動します。

2.  受信者の種類に基づいて、次のいずれかの受信者タブを選択します。
    
      - **メールボックス**
    
      - **グループ**
    
      - **リソース**
    
      - **連絡先**
    
      - **Shared**

3.  受信者タブで、変更する受信者を選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

4.  表示される受信者のプロパティ ページで、**\[メール ヒント\]** をクリックします。

5.  メール ヒントのテキストを入力します。完了したら、**\[Save\]** をクリックします。

## シェルを使用して受信者のメール ヒントを構成する

受信者のメール ヒントを構成するには、次の構文を使用します。

    Set-<RecipientType> <RecipientIdentity> -MailTip "<MailTip text>"

*\<RecipientType\>* には、受信者の種類を指定します。たとえば、`Mailbox`、`MailUser`、`MailContact`、`DistributionGroup`、`DynamicDistributionGroup` などです。

たとえば、"Help Desk" という名前のメールボックスに送信されたサポート要求に 2 時間以内に応答することになっているとします。このことを説明するカスタム メール ヒントを構成するには、次のコマンドを実行します。

    Set-Mailbox "Help Desk" -MailTip "A Help Desk representative will contact you within 2 hours."

## シェルを使用して異なる言語の追加のメール ヒントを構成する

既存のメール ヒント テキストやメール ヒント翻訳に影響を与えずに追加のメール ヒント翻訳を構成するには、次の構文を使用します。

    Set-<RecipientType> -MailTipTranslations @{Add="<culture1>:<localized text 1>","<culture2>:<localized text 2>"...; Remove="<culture1>:<localized text 1>","<culture2>:<localized text 2>"...}

*\<culture\>* には、言語に関連付けられている ISO 639 の 2 文字の有効なカルチャ コードを指定します。

たとえば、Notifications という名前のメールボックスに、"監視対象外のメールボックス" というメール ヒントがあるとします。このメール ヒントにスペイン語の翻訳を追加するには、次のコマンドを実行します。

    Set-Mailbox -MailTipTranslations @{Add="ES:Esta caja no se supervisa."}

## 正常な動作を確認する方法

受信者のメール ヒントが正常に構成されたことを確認するには、次の手順を実行します。

1.  Outlook Web App か Outlook 2010 またはそれ以降のバージョンで、該当する受信者宛ての電子メール メッセージを作成します (ただし、送信は行いません)。

2.  情報バーにメール ヒントが表示されることを確認します。

3.  追加のメール ヒント翻訳を構成した場合は、メール ヒント翻訳の言語と一致する言語設定の Outlook Web App でメッセージを作成し結果を確認します。

