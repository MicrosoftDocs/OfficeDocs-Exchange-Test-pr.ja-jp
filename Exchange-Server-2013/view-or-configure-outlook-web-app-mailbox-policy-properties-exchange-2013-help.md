---
title: 'Outlook Web App メールボックス ポリシーのプロパティの表示または構成: Exchange Online Help'
TOCTitle: Outlook Web App メールボックス ポリシーのプロパティの表示または構成
ms:assetid: be012ffe-8fdb-4fb7-aebd-78b3a55593fa
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd351097(v=EXCHG.150)
ms:contentKeyID: 49896448
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Web App メールボックス ポリシーのプロパティの表示または構成

 

_**適用先:** Exchange Online, Exchange Server 2013_

Outlook Web App メールボックス ポリシーを作成後、Outlook Web App 内のユーザーに使用可能な、さまざまな機能制御用のオプションを構成できます。たとえば、受信トレイのルールの有効、無効を設定したり、添付ファイルで使用できるファイルの種類の一覧を作成できたりします。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:3 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「Outlook Web App メールボックス ポリシー」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して Outlook Web App メールボックス ポリシーを表示または構成する

1.  EAC で、<strong>アクセス許可</strong> \> <strong>Outlook Web App policies</strong> の順にクリックします。

2.  結果ウィンドウで、表示または構成するメールボックス ポリシーをクリックして選択します。

3.  <strong>編集</strong> をクリックします。

4.  
    
    <strong>全般</strong> タブで、ポリシー名を表示および編集できます。

5.  
    
    <strong>機能</strong> タブで、チェック ボックスを使用して機能を有効または無効にします。既定では、最も一般的な機能が表示されます。有効または無効にできるすべての機能を表示するには、<strong>その他のオプション</strong> をクリックします。
    

    > [!NOTE]
    > Outlook Web App メールボックス ポリシーの機能の設定は、Outlook Web App 仮想ディレクトリの設定より優先されます。シェルで <STRONG>Set-CASMailbox</STRONG> コマンドレットを使用して、個々のユーザーのセグメンテーションの設定を変更できます。



6.  
    
    <strong>ファイル アクセス</strong> タブで、<strong>ファイルへの直接アクセス</strong> チェック ボックスを使って、ユーザーのファイル アクセスと表示オプションを構成します。ファイル アクセスによって、ユーザーはメール メッセージに添付されているファイルの内容を開いたり、表示したりすることができます。
    
    ファイル アクセスは、ユーザーが公共または個人のコンピューターにサインインしているかどうかに基づいて制御できます。ユーザーがプライベート コンピューター アクセスを選択するか、パブリック コンピューター アクセスを選択するかのオプションは、フォーム ベース認証を使用している場合のみ使用できます。個人のコンピューターへのアクセスに対する他の形態の既定認証。

7.  <strong>オフライン アクセス</strong> タブで、オプション ボタンを使用してオフライン アクセスの可用性を構成します。

8.  <strong>保存</strong> をクリックしてポリシーの更新を完了します。

## シェルを使用して Outlook Web App メールボックス ポリシーを構成する

この例では、既定のメールボックス ポリシーで予定表へのアクセスを有効にしています。

    Set-OwaMailboxPolicy -Identity Default -CalendarEnabled $true

構文およびパラメーターの詳細については、「[Set-OwaMailboxPolicy](https://technet.microsoft.com/ja-jp/library/dd297989\(v=exchg.150\))」を参照してください。

## シェルを使用して Outlook Web App メールボックス ポリシーを表示する

この例では、組織 `Executives` の Outlook Web App メールボックス ポリシー `Fabrikam` のプロパティを取得します。

    Get-OwaMailboxPolicy -Identity Fabrikam\Executives

構文およびパラメーターの詳細については、「[Get-OwaMailboxPolicy](https://technet.microsoft.com/ja-jp/library/dd351095\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

Outlook Web App メールボックス ポリシーを正常に編集できたことを確認するには、次の手順を実行します。

1.  EAC で、<strong>アクセス許可</strong> \> <strong>Outlook Web App ポリシー</strong> をクリックしてから、特定の Outlook Web App メールボックス ポリシーを選択します。

2.  <strong>編集</strong> ボタンをクリックしてメールボックス ポリシーのプロパティを表示します。

3.  <strong>保存</strong> または <strong>キャンセル</strong> をクリックしてプロパティ ページを閉じます。

