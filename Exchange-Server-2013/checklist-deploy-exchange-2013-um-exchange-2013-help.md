---
title: 'チェックリスト: Exchange 2013 UM の展開: Exchange 2013 Help'
TOCTitle: 'チェックリスト: Exchange 2013 UM の展開'
ms:assetid: 41b666a2-0d0d-471f-90a3-07c3c562af85
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ673520(v=EXCHG.150)
ms:contentKeyID: 52057813
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# チェックリスト: Exchange 2013 UM の展開

 

_**適用先:**Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:**2015-03-09_

このチェックリストは、組織へのユニファイド メッセージング (UM) のインストールおよび展開に役立ちます。

このチェックリストを使用して作業を開始する前に、次のトピックで説明されている概念を理解している必要があります。

  - [ユニファイド メッセージング](unified-messaging-exchange-2013-help.md)

  - [新しいボイス メール機能](new-voice-mail-features-exchange-2013-help.md)

  - [ユニファイド メッセージングの計画](planning-for-unified-messaging-exchange-2013-help.md)

UM および Microsoft Lync Server の展開方法に関する詳細なガイダンスは、「[チェックリスト: Exchange 2013 UM と Lync Server の統合](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md)」を参照してください。

## ユニファイド メッセージングを展開するためのチェックリスト


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
<td><p>テレフォニー コンポーネントを展開して構成します。</p></td>
<td><p><a href="connect-um-to-your-telephone-system-exchange-2013-help.md">UM を電話システムに接続する</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exchange 2013 をインストールする前に、システム要件を確認します。</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 のシステム要件</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>インストールの前提条件を満たしていることを確認します。</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 の前提条件</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>必要なクライアント アクセス サーバーとメールボックス サーバーをインストールします。</p>

> [!WARNING]
> VoIP ゲートウェイまたは IP PBX を構成して UM SIP および RTP トラフィックを Exchange 2013 クライアント アクセス サーバーへ送信する前に、少なくとも 1 つ以上の Exchange 2013 メールボックス サーバーを組織に展開する必要があります。


</td>
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
<td><p>組織で必要な数のダイヤル プランを作成します。</p></td>
<td><p><a href="create-a-um-dial-plan-exchange-2013-help.md">UM ダイヤル プランを作成する</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>ダイヤル プランのセキュリティ設定を構成します。</p></td>
<td><p><a href="configure-the-voip-security-setting-exchange-2013-help.md">VoIP セキュリティ設定の構成</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>各クライアント アクセス サーバーおよびメールボックス サーバーの UM 起動モードを構成します。</p></td>
<td><p><a href="configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md">メールボックス サーバーのスタートアップ モードを構成する</a></p>
<p><a href="configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md">クライアント アクセス サーバーのスタートアップ モードを構成する</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>メールボックス サーバーで同時呼び出し数を構成します。</p></td>
<td><p><a href="configure-the-number-of-incoming-calls-on-a-mailbox-server-exchange-2013-help.md">メールボックス サーバーで着信呼び出し数を構成する</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Outlook Voice Access の番号とその他の設定を構成します。</p></td>
<td><p><a href="manage-a-um-dial-plan-exchange-2013-help.md">UM ダイヤル プランの管理</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>ユニファイド メッセージングの送信ダイヤルを構成します。</p></td>
<td><p><a href="authorize-calls-using-dialing-rules-exchange-2013-help.md">ダイヤル ルールを使用して呼び出しを承認する</a></p>
<p><a href="authorize-calls-for-users-in-a-dial-plan-exchange-2013-help.md">ダイヤル プランでユーザーの呼び出しを承認する</a></p>
<p><a href="authorize-calls-for-a-group-of-users-exchange-2013-help.md">ユーザー グループの呼び出しを承認する</a></p></td>
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
<td><p><strong> </strong></p></td>
<td><p>UM 用の新しい Exchange 証明書を作成しインポートして有効にするか、相互に信頼されたサード パーティの証明書を有効にします。また、すべての VoIP ゲートウェイ、IP PBX、および SBC の証明書をインポートします。</p></td>
<td><p><a href="add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md">メールボックス サーバーとクライアント アクセス サーバーを SIP URI ダイヤル プランに追加する</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>すべての Exchange サーバー上で Microsoft Exchange ユニファイド メッセージング サービスおよびユニファイド メッセージング呼び出しルーター サービスを再起動して、必要な証明書を読み込みます。</p></td>
<td><p><a href="stop-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Microsoft Exchange Unified Messaging Service を停止する</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Microsoft Exchange Unified Messaging Service を開始する</a></p>
<p><a href="stop-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスの停止</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスを開始する</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>UM メールボックス ポリシーを作成するか、既定の UM メールボックス ポリシーを構成します。</p></td>
<td><p><a href="create-a-um-mailbox-policy-exchange-2013-help.md">UM メールボックス ポリシーの作成</a></p>
<p><a href="manage-a-um-mailbox-policy-exchange-2013-help.md">UM メールボックス ポリシーの管理</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>必要に応じて、ユーザーが内線番号および E.164 番号でユニファイド メッセージングを使用できるようにします。</p></td>
<td><p><a href="enable-a-user-for-voice-mail-exchange-2013-help.md">ボイス メール用にユーザーを有効にする</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>着信 FAX を有効にします (省略可能)。</p></td>
<td><p><a href="enable-voice-mail-users-to-receive-faxes-exchange-2013-help.md">ボイス メール ユーザーが FAX を受信できるようにする</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>保護されたボイス メールを設定します (省略可能)。</p></td>
<td><p><a href="protect-voice-mail-exchange-2013-help.md">ボイス メールを保護する</a></p></td>
</tr>
</tbody>
</table>


ユニファイド メッセージングを展開するためのチェックリスト

