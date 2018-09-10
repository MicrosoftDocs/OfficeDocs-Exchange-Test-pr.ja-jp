---
title: 'チェックリスト: Exchange 2013 UM と Lync Server の統合: Exchange 2013 Help'
TOCTitle: 'チェックリスト: Exchange 2013 UM と Lync Server の統合'
ms:assetid: 3b82e86f-9f30-4445-96ad-744082abeaeb
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd638120(v=EXCHG.150)
ms:contentKeyID: 52057812
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# チェックリスト: Exchange 2013 UM と Lync Server の統合

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2016-12-09_

このチェックリストを使用して、ユニファイド メッセージング (UM) および Microsoft Lync Server 2013 をインストールして展開します。このトピックでは、Lync Server 2010 も "Lync Server" と呼びます。ただし、Microsoft Office Communications Server 2007 R2 をユニファイド メッセージングと合わせて展開することもできます。

このチェックリストを使用して作業を開始する前に、次のトピックで説明されている概念を理解している必要があります。

  - [Exchange 2013 UM および Lync Server の展開の概要](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [Office Communications Server 2007 R2 および Lync Server との共存](coexistence-with-office-communications-server-2007-r2-and-lync-server-exchange-2013-help.md)

Lync Server 用に実行が必要なタスクの実行方法の詳細については、「[Microsoft Lync Server 2013](https://go.microsoft.com/fwlink/p/?linkid=265752)」を参照してください。

## Microsoft Lync Server とユニファイド メッセージングを展開するためのチェックリスト


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>完了?</th>
<th>タスク</th>
<th>トピック</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange Server 2013 をインストールする前に、システム要件を確認します。</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 のシステム要件</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>インストールの前提条件を満たしていることを確認します。</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 の前提条件</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Microsoft Lync Server 2013 および Microsoft Exchange Server 2013 を統合する前提条件を確認します。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282082">Skype for Business と Exchange の統合の計画</a></p>

> [!TIP]  
> Exchange 2013 と Lync Server 2010 および 2013 には、インストール時にインストールされる Unified Communications Managed API (UCMA) 4.0 Runtime が必要です。UCMA 4.0 に関する情報をダウンロードして確認するには、「<A href="https://go.microsoft.com/fwlink/p/?linkid=258269">Unified Communications Managed API 4.0 Runtime</A>」を参照してください。


</td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>必要なクライアント アクセス サーバーとメールボックス サーバーをインストールします。</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">セットアップ ウィザードを使用した Exchange 2013 のインストール</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>インストールを確認し、サーバーのセットアップ ログを確認します。</p></td>
<td><p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Exchange 2013 のインストールの確認</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>必要に応じて、UM 言語パックをインストールします。</p></td>
<td><p><a href="install-a-um-language-pack-exchange-2013-help.md">UM 言語パックをインストールする</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>組織で必要な数の SIP URI ダイヤル プランを作成します。</p></td>
<td><p><a href="https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan">UM ダイヤル プランを作成する</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>ダイヤル プランのセキュリティ設定を構成します。</p></td>
<td><p><a href="https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/connect-voice-mail-system/configure-voip-security-setting">VoIP セキュリティ設定の構成</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>メールボックス サーバーで同時呼び出し数を構成します。</p></td>
<td><p><a href="configure-the-number-of-incoming-calls-on-a-mailbox-server-exchange-2013-help.md">メールボックス サーバーで着信呼び出し数を構成する</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Outlook Voice Access の番号とその他の設定を構成します。</p></td>
<td><p><a href="https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/connect-voice-mail-system/manage-um-dial-plan">UM ダイヤル プランの管理</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>すべてのクライアント アクセス サーバーおよびメールボックス サーバーを各 SIP URI ダイヤル プランに追加します。</p></td>
<td><p><a href="add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md">メールボックス サーバーとクライアント アクセス サーバーを SIP URI ダイヤル プランに追加する</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>ユニファイド メッセージングの送信ダイヤルを構成します。SIP URI ダイヤル プランとそれらのダイヤル プランにリンクされた UM メールボックス ポリシーのすべての通話を許可します。</p></td>
<td><p><a href="https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/authorize-calls-for-users-in-a-dial-plan">ダイヤル プランでユーザーの呼び出しを承認する</a></p>
<p><a href="https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/authorize-calls-for-a-group-of-users">ユーザー グループの呼び出しを承認する</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>必要な数の自動応答を作成します。</p></td>
<td><p><a href="create-a-um-auto-attendant-exchange-2013-help.md">UM 自動応答を作成する</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>UM 自動応答をそれぞれに設定し、構成します。</p></td>
<td><p><a href="set-up-a-um-auto-attendant-exchange-2013-help.md">UM 自動応答の設定</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>UM 用の新しい Exchange 証明書を作成しインポートして有効にするか、相互に信頼されたサード パーティの証明書を有効にします。</p></td>
<td><p><a href="add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md">メールボックス サーバーとクライアント アクセス サーバーを SIP URI ダイヤル プランに追加する</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>クライアント アクセス サーバーおよびメールボックス サーバーそれぞれに対して、UM スタートアップ モードをデュアルまたは TLS に構成します。</p></td>
<td><p><a href="configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md">メールボックス サーバーのスタートアップ モードを構成する</a></p>
<p><a href="configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md">クライアント アクセス サーバーのスタートアップ モードを構成する</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>すべての Exchange サーバー上で Microsoft Exchange ユニファイド メッセージング サービスおよびユニファイド メッセージング呼び出しルーター サービスを再起動して、必要な証明書を読み込みます。</p></td>
<td><p><a href="stop-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Microsoft Exchange Unified Messaging Service を停止する</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Microsoft Exchange Unified Messaging Service を開始する</a></p>
<p><a href="stop-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスの停止</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスを開始する</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>UM メールボックス ポリシーを作成するか、既定の UM メールボックス ポリシーを構成します。</p></td>
<td><p><a href="https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/set-up-voice-mail/create-um-mailbox-policy">UM メールボックス ポリシーの作成</a></p>
<p><a href="https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/set-up-voice-mail/manage-um-mailbox-policy">UM メールボックス ポリシーの管理</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>ユーザーに対して SIP アドレスを使用したユニファイド メッセージングを有効にし、それらを SIP URI ダイヤル プランとリンクします。</p></td>
<td><p><a href="https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/set-up-voice-mail/enable-a-user-for-voice-mail">ボイス メール用にユーザーを有効にする</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Lync Server 2013 の計画ドキュメントを確認します。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282081">計画</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Lync Server 2013 をインストールして展開します。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282051">Lync Server 2013 の展開</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exchange UM サーバーにインポートされている、相互に信頼された内部 PKI またはサード パーティ証明書をインポートします。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281863">サーバーの証明書の構成</a></p>
<p><a href="http://go.microsoft.com/fwlink/p/?linkid=281865">Microsoft Exchange Server ユニファイド メッセージングを実行しているサーバーでの証明書の構成</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>必要に応じて、サーバーで Lync サービスを開始して証明書を読み込みます。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282084">サーバーでのサービスの開始</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exchange 管理シェルを開き、%Program Files%\Microsoft\Exchange Server\V15\Scripts フォルダーにある exchucutil.ps1 スクリプトを実行します。</p>
<p></p></td>
<td><p><a href="configure-um-to-work-with-lync-server-exchange-2013-help.md">Lync Server で動作するように UM を構成する</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>エンタープライズ VoIP の要件を確認します。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281876">エンタープライズ VoIP のソフトウェア前提条件</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=281875">エンタープライズ VoIP のセキュリティおよび構成の前提条件</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>メディア ゲートウェイまたは仲介サーバーを展開および構成し、ピアを定義します。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281872">仲介サーバーの展開とピアの定義</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>仲介サーバーと 1 つまたは複数のピア間のトランクを構成して、公衆交換電話網 (PSTN) に接続します。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281868">トランクの構成</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Lync ダイヤル プランを作成および構成して、正規化ルールを作成、定義し、関連付けます。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281867">ダイヤル プランの構成</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>音声ポリシーを構成して、電話の使用法と発信通話ルートを定義します。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281869">音声ポリシー、PSTN 使用法レコード、およびボイス ルートの構成</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exchange 統合ユーティリティ (ocsumutil.exe) を実行します。このコマンドは、Outlook Voice Access 用および自動応答用の連絡先オブジェクトを作成します。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281866">Microsoft Exchange Server のユニファイド メッセージングと連動させるための Lync Server 2013 の構成</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>必要なエンタープライズ VoIP の高度な機能のすべてを定義、展開、および構成します。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281871">高度なエンタープライズ VoIP 機能の展開</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>エンタープライズ VoIP に対してユーザーを有効にします。回線 URI を入力して、音声ポリシーと Lync ダイヤル プランを割り当てます。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281873">エンタープライズ VoIP に対するユーザーの有効化</a></p></td>
</tr>
</tbody>
</table>

