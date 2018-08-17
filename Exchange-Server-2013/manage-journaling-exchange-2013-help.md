﻿---
title: 'ジャーナリングの管理: Exchange Online Help'
TOCTitle: ジャーナリングの管理
ms:assetid: d517f27e-f80a-4a06-988c-cbbf981c701d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ651670(v=EXCHG.150)
ms:contentKeyID: 49896497
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ジャーナリングの管理

 

_**適用先:** Exchange Online, Exchange Server 2013_

ジャーナリングは、受信および送信電子メールを記録することで、組織が法的、規則、および組織のコンプライアンス要件に応答するのに役立ちます。このトピックでは、Exchange 2013 および Exchange Online におけるジャーナリングの管理に関連する基本的なタスクを実行する方法を示します。

標準ジャーナリングはメールボックス データベース上で構成します。このオプションでは、ジャーナリング エージェントを有効にして、特定のメールボックス データベースにあるメールボックスが送受信したすべてのメッセージをジャーナル処理することができます。また、プレミアム ジャーナリングを使用してジャーナリング エージェントを有効にし、ジャーナル ルールを使用して、より詳細にジャーナリングすることもできます。メールボックス データベースにあるすべてのメールボックスをジャーナリングする代わりに、個々の受信者または配布グループのメンバーをジャーナル処理することで、組織のニーズに合うようにジャーナル ルールを構成できます。プレミアム ジャーナリングを使用するには、Exchange Enterprise クライアント アクセス ライセンス (CAL) が必要です。

ジャーナルの詳細については、「[ジャーナル](journaling-exchange-2013-help.md)」を参照してください。

**内容**

ジャーナル ルールの作成

ジャーナル ルールを表示または変更する

ジャーナル ルールを有効または無効にする

ジャーナル ルールの削除

メールボックス データベースごとのジャーナリングを有効または無効にする

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」トピックの「Journaling (ジャーナル)」エントリ。

  - ジャーナリング メールボックスが作成済みか、既存のメールボックスがジャーナリング メールボックスとして利用できます。Exchange Online メールボックスをジャーナリング メールボックスに指定することはできません。ジャーナル レポートは、オンプレミスのアーカイブ システムまたはサード パーティのアーカイブ サービスに配信できます。メールボックスがオンプレミス サーバーと Exchange Online に分かれて格納されているハイブリッド展開を実行している場合には、オンプレミスのメールボックスを Exchange Online およびオンプレミスのメールボックスのジャーナリング メールボックスとして指定することができます。
    

    > [!IMPORTANT]
    > 存在しなかったりコピー先が無効であったりするジャーナル用メールボックスにジャーナル レポートを送信するよう Exchange Online にジャーナル ルールを構成してしまった場合、そのジャーナル レポートは Microsoft データセンターのサーバー上のトランスポート キューに残ります。このような場合は、Microsoft データセンターの担当者が組織に連絡をし、ジャーナル レポートがジャーナル メールボックスに正常に送信されるよう問題の解決を要請します。連絡後 2 日経っても問題が解決しない場合、Microsoft は問題のあるジャーナル ルールを無効化します。



  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。<STRONG>JournalingReportDNRTo</STRONG> メールボックスに問題が発生している場合は、「<A href="https://go.microsoft.com/fwlink/p/?linkid=331674">Exchange Online のトランスポート ルールおよびメールボックス ルールが正常に動作しない</A>」を参照してください。



## ジャーナル ルールの作成

## EAC を使用してジャーナル ルールを作成する

1.  EAC で、<strong>コンプライアンス管理</strong>、<strong>ジャーナル ルール</strong> の順に移動して、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  <strong>\[ジャーナル ルール\]</strong>でジャーナル ルールの名前を指定し、次のフィールドを入力します。
    
      - <strong>メッセージの送信先または受信元が次の場合</strong>   ルールの対象となる受信者を指定します。特定の受信者を指定するか、またはすべてのメッセージにルールを適用できます。
    
      - <strong>以下のメッセージをジャーナリングします</strong>   ジャーナル ルールの範囲を指定します。内部メッセージのみ、外部メッセージのみ、または発信元や宛先に関係なくすべてのメッセージをジャーナリングできます。
    
      - <strong>ジャーナル レポートの送信先</strong>   すべてのジャーナル レポートを受信するジャーナル メールボックスのアドレスを入力します。
        

        > [!NOTE]
        > 表示名またはメール ユーザーかメール連絡先の別名も、ジャーナル メールボックスとして入力できます。この場合、ジャーナル レポートは、、メール ユーザーまたはメール連絡先の外部の電子メール アドレスに送信されます。ただし、前述したように、メール ユーザーまたはメール連絡先の外部の電子メール アドレスは Exchange Online メールボックスのアドレスにはできません。



3.  <strong>保存</strong> をクリックして、ジャーナル ルールを作成します。

## シェルを使用してジャーナル ルールを作成する

この例では、受信者 user1@contoso.com によって送受信されるすべてのメッセージをジャーナリングするジャーナル ルール Discovery Journal Recipients を作成します。

    New-JournalRule -Name "Discovery Journal Recipients" -Recipient user1@contoso.com -JournalEmailAddress "Journal Mailbox" -Scope Global -Enabled $True

## 正常な動作を確認する方法

ジャーナル ルールが正常に作成されたことを確認するには、次のいずれかの手順を実行します。

  - EAC から、作成した新しいジャーナル ルールが <strong>ジャーナル ルール</strong> タブの一覧に表示されていることを確認します。

  - シェルから次のコマンドを実行して、新しいジャーナル ルールが存在することを確認します (下記の例では、上記のシェル例で作成したルールを確認します)。
    
        Get-JournalRule "Discovery Journal Recipients"

先頭へ戻る

## ジャーナル ルールを表示または変更する

## EAC を使用してジャーナル ルールを表示または変更する

1.  EAC で、<strong>コンプライアンス管理</strong>、<strong>ジャーナル ルール</strong> の順に移動します。

2.  リスト ビューに、組織のすべてのジャーナル ルールが表示されます。

3.  表示または変更するルールをダブルクリックします。

4.  <strong>ジャーナル ルール</strong> で、必要な設定を変更します。このダイアログ ボックスの設定の詳細については、このトピックで前述した「EAC を使用してジャーナル ルールを作成する」の手順を参照してください。

## シェルを使用してジャーナル ルールを表示または変更する

この例では、Exchange 組織のすべてのジャーナル ルールの要約リストを表示します。

    Get-JournalRule

この例では、「Brokerage Journal Rule」というジャーナル ルールを取得し、出力結果を **Format-List** コマンドにパイプして一覧形式でルールのプロパティを表示します。

    Get-JournalRule "Brokerage Journal Rule" | Format-List

特定のルールのプロパティを変更する場合は、[Set-JournalRule](https://technet.microsoft.com/ja-jp/library/bb125010\(v=exchg.150\)) コマンドレットを使用する必要があります。次の例では、ジャーナル ルールの名前を `JR-Sales` から `TraderVault` に変更しています。次のルール設定も変更されます。

  - 受信者

  - JournalEmailAddress

  - 範囲

<!-- end list -->

    Set-JournalRule JR-Sales -Name TraderVault -Recipient traders@woodgrovebank.com -JournalEmailAddress tradervault@woodgrovebank.com -Scope Internal

## 正常な動作を確認する方法

ジャーナル ルールが正常に変更されたことを確認するには、次のいずれかの手順を実行します。

  - EAC から、<strong>コンプライアンス管理</strong> \> <strong>ジャーナル ルール</strong> に移動します。変更したルールをダブルクリックし、変更が保存されたことを確認します。

  - シェルから次のコマンドを実行して、ジャーナル ルールが正常に変更されたことを確認します。このコマンドでは、変更したプロパティとルールの名前の一覧が表示されます (下記の例では、上記のシェル例で作成したルールを確認します)。
    
        Get-TransportRule "TraderVault" | Format-List Name,Recipient,JournalEmailAddress,Scope

先頭へ戻る

## ジャーナル ルールを有効または無効にする


> [!IMPORTANT]
> ジャーナル ルールを無効にすると、ジャーナリング エージェントは、そのルールの対象となるメッセージのジャーナリングを停止します。ジャーナル ルールが無効になっている間は、そのルールによって本来はジャーナリングされるすべてのメッセージはジャーナリングされません。ジャーナル ルールを無効にすることにより、組織の規制要件やコンプライアンス要件が損なわれないことを確認してください。



## EAC を使用してジャーナル ルールを有効または無効にする

1.  EAC で、<strong>コンプライアンス管理</strong>、<strong>ジャーナル ルール</strong> の順に移動します。

2.  リスト ビューのルールの名前の横にある <strong>オン</strong> 列で、チェック ボックスをオンにしてルールを有効にするか、またはチェック ボックスをオフにしてルールを無効にします。

## シェルを使用してジャーナル ルールを有効または無効にする

この例では、ルール Contoso を有効にします。

    Enable-JournalRule "Contoso Journal Rule"

この例では、ルール Contoso を無効にします。

    Disable-JournalRule "Contoso Journal Rule"

## 正常な動作を確認する方法

ジャーナル ルールが正常に有効化または無効化されたことを確認するには、次のいずれかの手順を実行します。

  - EAC からジャーナル ルールの一覧を表示し、<strong>オン</strong> 列のチェック ボックスの状態を確認します。

  - シェルから、組織内のすべてのジャーナル ルールの一覧を返す次のコマンドを実行します。これには、それぞれのジャーナル ルールの状態が含まれています。
    
        Get-JournalRule | Format-Table Name,Enabled

先頭へ戻る

## ジャーナル ルールの削除

## EAC を使用してジャーナル ルールを削除する

1.  EAC で、<strong>コンプライアンス管理</strong>、<strong>ジャーナル ルール</strong> の順に移動します。

2.  リスト ビューで、削除するルールを選択し、<strong>削除</strong>![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") をクリックします。

## シェルを使用してジャーナル ルールを削除する

この例では、Brokerage ジャーナル ルールを削除します。

    Remove-JournalRule "Brokerage Journal Rule"

## 正常な動作を確認する方法

ジャーナル ルールが正常に削除されたことを確認するには、次のいずれかの手順を実行します。

  - EAC から、削除したジャーナル ルールが <strong>ジャーナル ルール</strong> タブの一覧に表示されていないことを確認します。

  - シェルから次のコマンドを実行して、削除したルールが一覧に表示されていないことを確認します。
    
        Get-JournalRule

先頭へ戻る

## メールボックス データベースごとのジャーナリングを有効または無効にする


> [!NOTE]
> メールボックス データベース上でのメッセージのジャーナリングを無効にすると、適用されるメッセージングのアイテム保持ポリシーに組織が準拠できなくなる場合があります。メールボックス データベース上でのメッセージのジャーナリングを無効にすると、そのメールボックス データベース上のメールボックスによって送受信されたメッセージのジャーナル確認メッセージは送信されなくなります。



## EAC を使用してメールボックス データベースごとのジャーナリングを有効または無効にする

1.  EAC で、<strong>サーバー</strong> \> <strong>データベース</strong> に移動します。

2.  リスト ビューで、ジャーナリングを有効にするメールボックス データベースをダブルクリックします。

3.  <strong>メンテナンス</strong> をクリックし、<strong>ジャーナルの受信者</strong> ボックスの横にある <strong>参照</strong> をクリックして、ジャーナル メールボックスを選択します。ジャーナル受信者を指定すると、データベースのジャーナリングが有効になります。
    
    ジャーナリングを無効にするには、<strong>Remove X (X の削除)</strong> をクリックしてジャーナル受信者を削除します。

## シェルを使用してメールボックス データベースごとのジャーナリングを有効または無効にする

この例では、メールボックス データベース Sales Database のジャーナリングを有効にし、Sales Database ジャーナル メールボックスをジャーナル受信者として設定します。

    Set-MailboxDatabase "Sales Database" -JournalRecipient "Sales Database Journal Mailbox"

この例では、Sales Database メールボックス データベース上でのメールボックス データベースごとのジャーナリングを無効にします。

    Set-MailboxDatabase "Sales Database" -JournalRecipient $Null

この例では、Exchange 組織内のすべてのメールボックス データベース上でのメールボックス データベースごとのジャーナリングを無効にします。[Get-MailboxDatabase](https://technet.microsoft.com/ja-jp/library/bb124924\(v=exchg.150\)) コマンドレットを使用して、Exchange 組織内のすべてのメールボックス データベースを取得し、コマンドレットからの結果を [Set-MailboxDatabase](https://technet.microsoft.com/ja-jp/library/bb123971\(v=exchg.150\)) コマンドレットにパイプ処理します。

    Get-MailboxDatabase | Set-MailboxDatabase -JournalRecipient $Null

## 正常な動作を確認する方法

メールボックス データベースごとのジャーナリングが正常に有効化または無効化されたことを確認するには、次のいずれかの手順を実行します。

1.  EAC で、<strong>サーバー</strong> \> <strong>データベース</strong> に移動します。

2.  確認するデータベースをダブルクリックし、<strong>メンテナンス</strong> タブを選択します。

3.  <strong>ジャーナルの受信者</strong> ボックスに正しいジャーナル受信者が表示されている場合は、メールボックス データベースのジャーナリングが正常に有効になっています。ジャーナル受信者が表示されていない場合は、データベースのジャーナリングが無効になっています。

<!-- end list -->

  - シェルから、組織内のすべてのメールボックス データベースの一覧を返す次のコマンドを実行します。これには、それぞれのメールボックス データベースに関連付けられたジャーナル受信者が含まれています。ジャーナル受信者が一覧に表示されているデータベースでは、ジャーナリングが有効になっており、表示されていない場合は無効になっています。
    
        Get-MailboxDatabase | Format-Table Name,JournalRecipient

先頭へ戻る

## 詳細情報

[ジャーナル](journaling-exchange-2013-help.md)

[ボイス メールと不在着信通知のジャーナリングを有効または無効にする](disable-or-enable-journaling-of-voice-mail-and-missed-call-notifications-exchange-2013-help.md)

[New-JournalRule](https://technet.microsoft.com/ja-jp/library/bb125242\(v=exchg.150\))

[Get-JournalRule](https://technet.microsoft.com/ja-jp/library/aa998866\(v=exchg.150\))

[Set-JournalRule](https://technet.microsoft.com/ja-jp/library/bb125010\(v=exchg.150\))

[Enable-JournalRule](https://technet.microsoft.com/ja-jp/library/bb123902\(v=exchg.150\))

[Disable-JournalRule](https://technet.microsoft.com/ja-jp/library/aa995925\(v=exchg.150\))

[Remove-JournalRule](https://technet.microsoft.com/ja-jp/library/bb123489\(v=exchg.150\))

[Set-MailboxDatabase](https://technet.microsoft.com/ja-jp/library/bb123971\(v=exchg.150\))

