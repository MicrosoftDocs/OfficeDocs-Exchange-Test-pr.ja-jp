---
title: 'Exchange ActiveSync での Information Rights Management: Exchange 2013 Help'
TOCTitle: Exchange ActiveSync での Information Rights Management
ms:assetid: ebf04460-4d61-4b00-86b9-85ec1dbbd6a1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff657743(v=EXCHG.150)
ms:contentKeyID: 49896539
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange ActiveSync での Information Rights Management

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2016-12-09_

インフォメーション ワーカーは、電子メールを使用して機密情報を頻繁にやり取りします。この情報をセキュリティ保護するため、組織は Information Rights Management (IRM) を使用して、メッセージング コンテンツに強力な保護を適用できます。電子メールへのアクセスにモバイル デバイスが使用される機会が多くなっているため、モバイル デバイスのユーザーが IRM 保護コンテンツを作成して使用できることが重要です。

**目次**

Exchange 2013 におけるモバイル IRM 保護

要件

セキュリティ

Exchange ActiveSync で IRM を有効にする

IRM に関連する管理タスクについては、「[Information Rights Management の手順](information-rights-management-procedures-exchange-2013-help.md)」を参照してください。

## Exchange 2013 におけるモバイル IRM 保護

Exchange 2013 では、Microsoft Exchange ActiveSync の IRM により、AD RMS のアクセス許可を構成したり、コンピューターにデバイスを接続してデバイスの IRM を有効にする必要なしに、サポートされる Exchange ActiveSync デバイスで豊富な IRM 機能にアクセスできます。また、モバイル デバイスは Windows を実行している必要はありません。Exchange ActiveSync はマイクロソフトにより、モバイル デバイス製造業者、相手先ブランド供給 (OEM) などにライセンスされています。現在の Exchange ActiveSync ライセンシーの一覧については、「[Microsoft Technology Licensing](https://go.microsoft.com/fwlink/p/?linkid=198562)」ページの「Exchange ActiveSync プロトコル」セクションを展開して、ご参照ください。

Exchange ActiveSync で IRM を使用することにより、モバイル デバイスのユーザーは次の操作を実行できます。

  - IRM で保護されたメッセージの作成。

  - IRM で保護されたメッセージの読み取り。

  - IRM で保護されたメッセージの返信と転送。

Exchange 2013 におけるモバイル IRM 保護

## 要件

次の要件が適用されます。

  - 組織内のクライアント アクセス サーバーは Exchange 2010 SP1 以降を実行している必要があります。

  - 組織に AD RMS サーバーを展開する必要があります。

  - 内部メッセージ用に IRM を有効にする必要があります。これは、Exchange 2010 の IRM 機能すべての前提条件です。詳細については、「[内部メッセージの IRM を有効または無効にする](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md)」を参照してください。

  - Exchange ActiveSync メールボックス ポリシーで IRM を有効にする必要があります。異なる Exchange ActiveSync メールボックス ポリシーを使用することにより、異なるユーザーの集まりごとに IRM を有効または無効にできます。

  - Exchange ActiveSync プロトコル Version 14.1 をサポートするデバイス (Windows フォンを含む) は、Exchange ActiveSync で IRM をサポートできます。デバイスのモバイル電子メール アプリケーションでは、Exchange ActiveSync プロトコル Version 14.1 で定義される RightsManagementInformation タグがサポートされる必要があります。

Exchange 2013 におけるモバイル IRM 保護

## セキュリティ

Exchange ActiveSync で IRM を有効にすると、サポートされるモバイル デバイスのアクセスのためにメッセージを提供する前に、クライアント アクセス サーバーが IRM 保護メッセージを復号化します。同期すると、IRM 保護メッセージはモバイル デバイスに復号化された形式で記録されます。IRM 保護は、モバイル デバイスの IRM 対応電子メール クライアント アプリケーションにより実行されます。

Exchange ActiveSync の IRM は、クライアント アクセス サーバー上で IRM 保護された添付ファイルを復号化しません。IRM 保護ファイルへのアクセスは、ファイルの作成または表示に使用されるアプリケーションが実行します。たとえば、Windows Phone では、Microsoft Office ファイルの IRM 保護は [Microsoft Office Mobile](https://go.microsoft.com/fwlink/p/?linkid=205121) により実行されます。IRM 保護 Office ファイルにアクセスするには、ユーザーはコンピューターにデバイスを接続して、RMS サーバーで Office Mobile を有効にする必要があります。

Exchange ActiveSync で IRM を有効にするとき、次の表にある Exchange ActiveSync ポリシー設定を使用して、モバイル デバイスをセキュリティ保護することを推奨します。

### Exchange ActiveSync ポリシーの設定

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>設定</th>
<th>Exchange ActiveSync メールボックス ポリシーの新規作成ウィザードを使用して構成する</th>
<th>New-ActiveSyncMailboxPolicy コマンドレットを使用して構成する</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ユーザーはモバイル デバイスの情報にアクセスするのに、パスワードを入力する必要がある。</p></td>
<td><p><strong>[パスワードを要求する]</strong> チェック ボックスをオンにします。</p></td>
<td><p><em>DevicePasswordEnabled</em> パラメーターを <code>$true</code> に設定します。</p></td>
</tr>
<tr class="even">
<td><p>モバイル デバイスの暗号化を有効にする。</p></td>
<td><p><strong>[パスワードを要求する]</strong> チェック ボックスをオンにし、<strong>[デバイスでの暗号化を要求する]</strong> チェックボックスをオンにします。</p></td>
<td><p><em>RequireDeviceEncryption</em> パラメーターを <code>$true</code> に設定します。</p>

> [!IMPORTANT]
> <EM>RequireDeviceEncryption</EM> パラメーターを <CODE>$true</CODE> に設定すると、デバイスの暗号化をサポートしないモバイル デバイスは接続できなくなります。


</td>
</tr>
<tr class="odd">
<td><p>サポートしていないモバイル デバイスの Exchange サーバーとの同期を禁止する。</p></td>
<td><p><strong>[サポートしていないデバイスのアクセスを許可する]</strong> チェックボックスをオフにします。</p></td>
<td><p><em>AllowNonProvisionableDevices</em> パラメーターを <code>$false</code> に設定します。</p></td>
</tr>
</tbody>
</table>


詳細については、「[モバイル デバイス メールボックス ポリシー](mobile-device-mailbox-policies-exchange-2013-help.md)」を参照してください。

Exchange 2013 におけるモバイル IRM 保護

## Exchange ActiveSync で IRM を有効にする

Exchange ActiveSync で IRM を有効にするには、以下の操作を実行します。

1.  AD RMS 内のスーパー ユーザー グループにフェデレーション メールボックス (Exchange 2013 および Exchange 2010 セットアップによって作成されるシステム メールボックス) を追加します。これにより、Exchange 2013 および Exchange 2010 サーバーは IRM で保護されたメッセージにアクセスできるようになります。詳細については、「[フェデレーション メールボックスを AD RMS のスーパー ユーザー グループに追加する](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)」を参照してください。

2.  Exchange 管理シェルで [Set-IRMConfiguration](https://technet.microsoft.com/ja-jp/library/dd979792\(v=exchg.150\)) コマンドレットを使用して、クライアント アクセス サーバーの IRM を有効にします。これにより、組織の Exchange ActiveSync の IRM、および Microsoft OfficeOutlook Web App の IRM が有効になります。詳細については、「[クライアント アクセス サーバーで Information Rights Management を有効または無効にする](enable-or-disable-information-rights-management-on-client-access-servers-exchange-2013-help.md)」を参照してください。

Exchange 2013 におけるモバイル IRM 保護

