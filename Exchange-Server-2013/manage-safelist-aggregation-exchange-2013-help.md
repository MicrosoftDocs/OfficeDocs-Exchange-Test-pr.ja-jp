---
title: 'セーフリスト集約を管理する: Exchange 2013 Help'
TOCTitle: セーフリスト集約を管理する
ms:assetid: 5ac17168-f411-4cb7-ae98-ebefb865b210
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998280(v=EXCHG.150)
ms:contentKeyID: 49896266
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# セーフリスト集約を管理する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-08_

*セーフリスト集約*とは、Microsoft Outlook から Microsoft Exchange Server 2013 に共有されるスパム対策機能を指します。この機能は、Outlook ユーザーが構成した信頼できる宛先のリスト、信頼できる差出人のリスト、受信拒否リスト、および連絡先のデータを収集して、このデータを Exchange スパム対策エージェントが使用できるようにします。セーフリスト集約は、スパム対策エージェントを実行している Exchange サーバーによって実行されるスパム対策フィルター処理における誤検知の発生を減らすのに役立ちます。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:10 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「受信者プロビジョニングのアクセス許可」および「[スパム対策とマルウェア対策のアクセス許可](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)」の「スパム対策機能」。

  - この手順を実行するには、シェルを使用する必要があります。

  - 既定では、メールボックス サーバーのトランスポート サービスでスパム対策機能が有効になっていません。一般的には、Exchange 組織が受信メッセージの受信前にスパム対策フィルターを事前に設定しない場合に限り、スパム対策機能を有効にします。詳細については、「[メールボックス サーバーのスパム対策機能を有効にする](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)」を参照してください。

  - **Update-SafeList** コマンドレットを実行するときに生成されるネットワークおよびレプリケーション トラフィックに注意してください。セーフ リストの使用頻度が高い複数のメールボックスに対してコマンドを実行すると、大量のトラフィックが生成される場合があります。複数のメールボックスに対してこのコマンドを実行する場合は、ピーク時間外や勤務時間外に実行することをお勧めします。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用してメールボックスのセーフリスト コレクションの制限を構成する

ユーザーが構成できる信頼できる差出人のリストおよび受信拒否リストの最大数を構成できます。ユーザーは既定で最大 5,000 の信頼できる差出人のリストと 500 の受信拒否リストを構成できます。

信頼できる差出人のリストおよび受信拒否リストの最大数を構成するには、次のコマンドを実行します。

    Set-Mailbox <MailboxIdentity> -MaxSafeSenders <Integer> -MaxBlockedSenders <Integer>

この例では、メールボックス john@contoso.com に対し、最大 2,000 の信頼できる差出人のリストと 200 の受信拒否リストを構成します。

```powershell
Set-Mailbox john@contoso.com -MaxSafeSenders 2000 -MaxBlockedSenders 200
```

## 正常な動作を確認する方法

メールボックス セーフリスト収集の制限を正常に構成したことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
        Get-Mailbox <Identity> | Format-List Name,Max*Senders

2.  表示される値が設定値と一致することを確認します。

## シェルを使用して Update-Safelist コマンドを実行する

Exchange 2013 ではセーフリスト集約が自動的に行われるため、**Update-Safelist** コマンドレットをスケジュールしたり手動で実行したりする必要はありません。ただし、このコマンドレットをときどき実行してセーフリスト集約をテストすることができます。

この例では、メールボックス john@contoso.com の信頼できる差出人のリストを Active Directory に書き込みます。

```powershell
Update-Safelist john@contoso.com -Type SafeSenders
```

構文およびパラメーターの詳細については、「[Update-SafeList](https://technet.microsoft.com/ja-jp/library/bb125034\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

セーフリスト集約が正常に構成されたことを確認するには、次の手順を実行します。

## ステップ 1:シェルを使用して Exchange サーバー上でコンテンツ フィルター エージェントが有効になっていることを確認する

1.  次のコマンドを実行します。
    
    ```powershell
Get-ContentFilterConfig | Format-List Enabled
```

2.  出力で *Enabled* パラメーターが `True` と表示されている場合は、コンテンツ フィルターが有効になっています。有効になっていない場合は、次のコマンドを実行して Exchange サーバー上でコンテンツ フィルターとコンテンツ フィルター エージェントを有効にします。
    
    ```powershell
Set-ContentFilterConfig -Enabled $true
```

## ステップ 2:(オプション) ADSI エディターを使用して、セーフリスト集約データのエッジ トランスポート サーバーへのレプリケーションを確認します

この手順は、境界ネットワークのエッジ トランスポート サーバー上でコンテンツ フィルター エージェントを実行している場合にのみ必要です。

エッジ トランスポート サーバー上の Active Directory ライトウェイト ディレクトリ サービス (AD LDS) インスタンスでユーザー オブジェクトを表示して、ユーザー オブジェクトに対してセーフリストのコレクション データが更新されていることと、Microsoft Exchange EdgeSync サービスがデータを AD LDS インスタンスにレプリケートしたことを確認できます。

ユーザー オブジェクトそれぞれについて、3 つのセーフリスト コレクション属性があります。

  - **msExchSafeRecipientsHash**   この属性は、ユーザーの信頼できる宛先のリスト コレクションのハッシュを格納します。

  - **msExchSafeSendersHash**   この属性は、ユーザーの信頼できる差出人のリスト コレクションのハッシュを格納します。

  - **msExchBlockedSendersHash**   この属性は、ユーザーの受信拒否リスト コレクションのハッシュを格納します。

`0xac 0xbd 0x03 0xca` などの 16 進数の文字列が属性に存在する場合、ユーザー オブジェクトは更新されています。属性に `<Not Set>` 値がある場合、属性は更新されていません。

AD LDS Active Directory サービス インターフェイス (ADSI) Edit スナップインを使用すると、属性を検索および表示できます。

## ステップ 3:セーフ リスト集約が動作していることを確認するテスト メッセージを送信する

セーフリスト集約が機能していることをテストするには、コンテンツ フィルターでブロックされる差出人以外の信頼できる差出人から自分自身にメッセージを送信する必要があります。セーフリスト集約が機能している場合、メッセージは受信トレイに届きます。

1.  使用する既存の外部メール アカウントを探すか、または Microsoft Hotmail のようなフリーの Web ベースのメール プロバイダーでメール アカウントを作成します。

2.  そのアカウントを Microsoft Outlook の信頼できる差出人のリストに追加します。

3.  **Update-SafeList** コマンドレットを使用して、そのメールボックスからのセーフリスト コレクションを Active Directory にコピーします。

4.  オプション: 境界ネットワークのエッジ トランスポート サーバー上でコンテンツ フィルター エージェントを実行している場合は、**Start-EdgeSynchronization** コマンドレットを実行して EdgeSync レプリケーションを強制的に実行します。

5.  特定の単語を、禁止する語句としてコンテンツ フィルター構成に追加します。詳細な手順については、「[コンテンツ フィルターの管理](manage-content-filtering-exchange-2013-help.md)」を参照してください。

6.  手順 1 の外部メール アカウントから、手順 5 で構成した禁止する語句を含むメッセージを Exchange メールボックスに送信します。
    
    メッセージが正常に受信トレイに配信されれば、セーフリスト集約は正常に動作しています。

