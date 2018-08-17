---
title: 'Exchange ActiveSync: Exchange 2013 Help'
TOCTitle: Exchange ActiveSync
ms:assetid: 5fafaff3-eb37-4fdb-95f0-e56c45ea5884
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998357(v=EXCHG.150)
ms:contentKeyID: 48269555
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange ActiveSync

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

Exchange Server 2013 の Exchange ActiveSync クライアント プロトコルについて説明します。Exchange ActiveSync の機能については、セキュリティ機能、管理できる事項、セキュリティで保護する方法、Windows Phone 7 と同期する際に問題を回避する方法を取り上げます。


> [!TIP]
> このトピックは、管理者を対象としています。Windows Phone、iOS、Android デバイスから Office 365 または Exchange Server のメールボックスにアクセスするように設定する方法については、次のトピックを参照してください。 
> <UL>
> <LI>
> <P><A href="https://go.microsoft.com/fwlink/p/?linkid=615415">Windows Phone で電子メールを設定する</A></P>
> <LI>
> <P><A href="https://go.microsoft.com/fwlink/p/?linkid=615414">Apple iPhone、iPad、または iPod Touch でメールを設定する</A></P>
> <LI>
> <P><A href="https://go.microsoft.com/fwlink/?linkid=615417">Android 携帯電話またはタブレットで電子メールを設定する</A></P></LI></UL>



Exchange ActiveSync は、モバイル デバイスを Exchange メールボックスと同期できるようにするクライアント プロトコルです。Microsoft Exchange 2013 をインストールすると Exchange ActiveSync は既定で有効になります。

**目次**

Exchange ActiveSync の概要

Exchange ActiveSync の機能

Exchange ActiveSync の管理

Windows Phone 7 の同期

## Exchange ActiveSync の概要

Exchange ActiveSync は、待機時間が長く帯域幅が狭いネットワークで機能するように最適化された Microsoft Exchange 同期プロトコルです。HTTP および XML に基づくこのプロトコルにより、携帯電話が Microsoft Exchange を実行しているサーバー上の組織の情報にアクセスできます。Exchange ActiveSync を使用すると、携帯電話ユーザーは、電子メール、予定表、連絡先、およびタスクにアクセスできるようになります。また、オフライン作業の間も継続してこの情報にアクセスできます。


> [!NOTE]
> Exchange ActiveSync は共有メールボックスまたは代理人アクセスをサポートしていません。




> [!IMPORTANT]
> Windows Phone 7 の携帯電話は、すべての Exchange ActiveSync メールボックス ポリシー設定のうちの一部だけをサポートしています。完全な一覧については、「Windows Phone 7 の同期」を参照してください。



## Exchange ActiveSync の機能

Exchange ActiveSync には次の機能があります。

  - HTML メッセージのサポート

  - フラグのサポート

  - 電子メール メッセージのスレッドのグループ化

  - 会話全体を同期するか、同期しないかの機能

  - ショート メッセージ サービス (SMS) のメッセージとユーザーの Exchange メールボックスの同期

  - メッセージ返信ステータスの表示のサポート

  - 高速メッセージ取得のサポート

  - 会議の出席者の情報

  - Exchange Search の拡張

  - PIN のリセット

  - パスワード ポリシーによるデバイス セキュリティの拡張

  - Over The Air プロビジョニングの自動検出

  - 退席時、休暇時、外出時の自動応答設定のサポート

  - タスクの同期のサポート

  - ダイレクト プッシュ

  - 連絡先の空き時間情報のサポート

## Exchange ActiveSync の管理

Exchange ActiveSync は既定で有効になっています。Exchange メールボックスを持つすべてのユーザーがモバイル デバイスと Microsoft Exchange サーバーを同期することができます。

次の Exchange ActiveSync タスクを行うことができます。

  - ユーザーの Exchange ActiveSync の有効化と無効化

  - パスワードの最小文字数、デバイスのロック、パスワードの入力ミスが許される回数などのポリシーの設定

  - 紛失したり盗難にあった携帯電話からすべてのデータを消去するリモート ワイプの開始

  - さまざまな形式で表示またはエクスポートするためのさまざまなレポートの実行

  - デバイス アクセス ルールにより、組織との同期を許可するモバイル デバイスの種類を制御します。

## Exchange ActiveSync のセキュリティ

Exchange サーバーとモバイル デバイス間の通信で SSL (Secure Sockets Layer) 暗号化を使用するように Exchange ActiveSync を構成できます。

## Exchange ActiveSync でモバイル デバイスのアクセスを管理する

どのモバイル デバイスと同期できるかを制御できます。この管理を行うには、組織に接続する新しいモバイル デバイスを監視するか、接続を許可するモバイル デバイスの種類を判断するルールを設定します。どのモバイル デバイスが同期できるかの指定方法の選択に関係なく、特定のユーザーの特定のモバイル デバイスに対するアクセスをいつでも承認または拒否できます。

## Exchange ActiveSync のデバイス セキュリティ機能

Exchange では、Exchange ActiveSync サーバーとモバイル デバイス間の通信のセキュリティ オプションを構成する機能に加えて、モバイル デバイスのセキュリティを強化する次の機能が提供されています。

  - <strong>リモート ワイプ</strong>   モバイル デバイスが紛失や盗難などで危険にさらされている場合、Outlook Web App を使用して、Exchange Server コンピューターまたは任意の Web ブラウザーからリモート ワイプ コマンドを発行できます。このコマンドは、モバイル デバイスからすべてのデータを消去します。

  - <strong>デバイス パスワード ポリシー</strong>   Exchange ActiveSync を使用すると、デバイス パスワードのいくつかのオプションを構成できます。
    

    > [!WARNING]
    > iOS7 の指紋リーダー技術はデバイスのパスワードには使えません。組織のモバイル デバイス メールボックス ポリシーでデバイスのパスワードが必要な場合は、iOS7 の指紋リーダーを使っていても、デバイスのパスワードを作成して入力する必要があります。

    
    デバイスのパスワードのオプションには、次のものがあります。
    
      - <strong>最低限必要なパスワードの長さ (文字数) を指定する</strong>   このオプションでは、モバイル デバイスのパスワードの長さを指定します。既定の長さは 4 文字ですが、最大で 18 文字まで使用できます。
    
      - <strong>文字セットの最小数</strong>   このテキスト ボックスを使用して英数字のパスワードの複雑さを指定し、ユーザーが以下の中からいくつかの文字セットを使用するよう強制します。小文字、大文字、記号、および数字。
    
      - <strong>英数字のパスワードが必要</strong>   このオプションを使用すると、パスワードの強さを決定できます。数字だけでなく、文字や記号をパスワードに含めるように強制することができます。
    
      - <strong>休止時間 (分) を指定する</strong>   モバイル デバイスの休止時間がこのオプションで指定した値に達すると、ユーザーにモバイル デバイスのロックを解除するためのパスワードの入力を要求します。
    
      - <strong>パスワード履歴を強制する</strong>   このチェック ボックスをオンにすると、ユーザーが以前のパスワードを再利用するのを防ぐよう携帯電話に強制します。設定する数字により、ユーザーによる再利用を許可しない過去のパスワードの数が決まります。
    
      - <strong>パスワードの回復を有効にする</strong>   モバイル デバイスに対してパスワードの回復を有効にするには、このチェック ボックスをオンにします。管理者は、**Get-ActiveSyncDeviceStatistics** コマンドレットを使用して、ユーザーの回復のパスワードを検索できます。
    
      - <strong>次の回数、試行に失敗したらデバイスを無効にする</strong>   このオプションを使用すると、パスワードの入力に何回失敗したら携帯電話のメモリを無効にするかを指定できます。

  - <strong>デバイスの暗号化ポリシー</strong>   ユーザーのグループに対して強制可能な、モバイル デバイスの暗号化ポリシーがいくつかあります。これらのポリシーには次のようなものがあります。
    
      - <strong>デバイスでの暗号化を要求する</strong>   モバイル デバイスでの暗号化を要求するには、このチェック ボックスをオンにします。このオプションを使用すると、モバイル デバイスでのすべての情報が暗号化されるため、セキュリティが向上します。
    
      - <strong>メモリカードでの暗号化を要求する</strong>   モバイル デバイスのメモリカードでの暗号化を要求するには、このチェック ボックスをオンにします。このオプションを使用すると、モバイル デバイスのストレージ カードのすべての情報が暗号化されるため、セキュリティが向上します。

## Windows Phone 7 の同期

組織において Windows Phone 7 のモバイル デバイスを導入している場合、モバイル デバイス メールボックス ポリシー プロパティの設定によっては、該当のデバイスに同期の問題が発生することがあります。Windows Phone 7 の携帯電話を Exchange メールボックスと同期させるには、**AllowNonProvisionableDevices** プロパティを true に設定するか、または次のモバイル デバイス メールボックス ポリシー プロパティのみを構成してください。

  - PasswordRequired

  - MinPasswordLength

  - IdleTimeoutFrequencyValue

  - DeviceWipeThreshold

  - AllowSimplePassword

  - PasswordExpiration

  - PasswordHistory

  - DisableRemovableStorage

  - DisableIrDA

  - DisableDesktopSync

  - BlockRemoteDesktop

  - BlockInternetSharing

