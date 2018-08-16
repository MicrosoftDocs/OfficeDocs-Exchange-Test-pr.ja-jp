---
title: 'パブリック フォルダーの作成: Exchange 2013 Help'
TOCTitle: パブリック フォルダーの作成
ms:assetid: 6d252e60-c8d0-4efd-b9d7-ba5284a6f8ab
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb691104(v=EXCHG.150)
ms:contentKeyID: 49129515
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.PublicFolders.NewPublicFolderWizardForm.NewPublicFolderWizardPage
ms.translationtype: MT
---

# パブリック フォルダーの作成

 

_**適用先:** Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:** 2014-02-24_

パブリック フォルダーは、共有アクセスのために設計された、情報を収集、整理してワークグループや組織内の他のユーザーと共有するための容易かつ効果的な方法です。

既定では、パブリック フォルダーの設定 (アクセス許可の設定など) は、親フォルダーの設定を継承します。


> [!NOTE]
> ストレージ クォータおよびパブリック フォルダーの制限に関する詳細については、次のトピックを参照してください。 
> <UL>
> <LI>
> <P>Office 365 のパブリック フォルダーについて詳しくは、「<A href="https://go.microsoft.com/fwlink/?linkid=391188">Exchange Online の制限</A>」を参照してください。</P>
> <LI>
> <P>オンプレミス Exchange Server 2013 のパブリック フォルダーについて詳しくは、「<A href="limits-for-public-folders-exchange-2013-help.md">パブリック フォルダーの制限</A>」を参照してください。</P></LI></UL>



パブリック フォルダーの管理に関するその他の管理タスクについては、「[パブリック フォルダーの手順](public-folder-procedures-exchange-2013-help.md)」を参照してください。

パブリック フォルダーに関するその他の管理タスクについては、「[Office 365 と Exchange Online のパブリック フォルダーの手順](https://technet.microsoft.com/ja-jp/library/jj966272\(v=exchg.150\))」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間: 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[共有とコラボレーションのアクセス許可](sharing-and-collaboration-permissions-exchange-2013-help.md)」の「パブリック フォルダー」。

  - パブリック フォルダーは、先にパブリック フォルダー メールボックスを作成しておかないと、作成できません。パブリック フォルダー メールボックスを作成する方法の詳細については、「[パブリック フォルダー メールボックスを作成する](create-a-public-folder-mailbox-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

## 必要な作業

## EAC を使用してパブリック フォルダーを作成する

EAC を使用してパブリック フォルダーを作成する場合、パブリック フォルダーの名前とパスのみ設定できます。追加設定を構成するには、パブリック フォルダーを作成後に編集する必要があります。

1.  <strong>パブリック フォルダー</strong> \> <strong>パブリック フォルダー</strong> に移動します。

2.  このパブリック フォルダーを既存のパブリック フォルダーの子として作成する場合は、リスト ビューで既存のパブリック フォルダーをクリックします。最上位のパブリック フォルダーを作成する場合は、この手順を飛ばします。

3.  <strong>追加</strong> ![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

4.  <strong>パブリック フォルダー</strong> に、パブリック フォルダーの名前を入力します。
    

    > [!IMPORTANT]
    > パブリック フォルダーを作成するときは、名前にバック スラッシュ (\) を使用しないでください。



5.  <strong>パス</strong> ボックスで、パブリック フォルダーへのパスを確認します。このパスが適切でない場合は、<strong>キャンセル</strong> をクリックしてこの手順のステップ 2 に従います。

6.  <strong>保存</strong> をクリックします。

## シェルを使用したパブリック フォルダーの作成

この例では、パス Marketing\\2013 に Reports という名のパブリック フォルダーを作成します。

    New-PublicFolder -Name Reports -Path \Marketing\2013


> [!IMPORTANT]
> パブリック フォルダーを作成するときは、名前にバック スラッシュ (\) を使用しないでください。



構文およびパラメーターの詳細については、「[New-PublicFolder](https://technet.microsoft.com/ja-jp/library/aa996405\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

パブリック フォルダーが正常に作成されたことを確認するには、次の手順を実行します。

  - EAC で、<strong>最新の情報に更新</strong> をクリックし、パブリック フォルダーの一覧を更新します。一覧に新しいパブリック フォルダーが表示されます。

  - シェルで、次のいずれかのコマンドを実行します。
    ```
    Get-PublicFolder -Identity \Marketing\2013\Reports | Format-List
    ```
    ```
    Get-PublicFolder -Identity \Marketing\2013 -GetChildren
    ```
    ```
    Get-PublicFolder -Recurse
    ```

> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。


