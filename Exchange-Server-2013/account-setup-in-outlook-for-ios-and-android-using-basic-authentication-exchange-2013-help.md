---
title: 'Account setup in Outlook for iOS and Android using basic authentication: Exchange 2013 Help'
TOCTitle: Account setup in Outlook for iOS and Android using basic authentication
ms:assetid: 013dbe8c-30de-4c9c-baa9-75081b9229e8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Mt829322(v=EXCHG.150)
ms:contentKeyID: 74518365
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Account setup in Outlook for iOS and Android using basic authentication

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2018-04-30_

**概要**:Exchange 2013 組織のユーザーが基本認証を使用して iOS および Android 向けの Outlook アカウントをすばやくセットアップする方法。

iOS および Android 向けの Outlook には、Exchange 管理者が ActiveSync プロトコル経由で基本認証を使用するオンプレミス ユーザーにアカウント構成を「プッシュ」する機能が備えられています。この機能は、[Managed App Configuration](https://developer.apple.com/library/content/samplecode/sc2279/introduction/intro.html) チャネル (iOS の場合)、または [Android in the Enterprise](https://developer.android.com/samples/apprestrictions/index.html) チャネル (Android の場合) を使用するモバイル デバイス管理 (MDM) プロバイダーで機能します。

Microsoft Intune に登録されているオンプレミス ユーザーには、Azure Portal の Intune を使用してアカウント構成設定を展開できます。

アカウント構成が作成され、ユーザーがデバイスを登録すると、iOS および Android 向けの Outlook はアカウントが「見つかった」ことを検出し、ユーザーにアカウントの追加を促します。セットアップ プロセスを完了するためにユーザーが入力する必要がある唯一の情報はパスワードです。その後、ユーザーのメールボックスの内容が読み込まれ、ユーザーはアプリの使用を開始できます。

次の画像は、iOS および Android 向けの Outlook が Azure Portal の Intune で設定された後のエンドユーザーのセットアップ プロセスの例を示しています。

![オンプレミスでの iOS および Android 用の Outlook のアカウント セットアップ](images/Mt829322.04bd56f2-5c45-4268-8762-436994acd656(EXCHG.150).png "オンプレミスでの iOS および Android 用の Outlook のアカウント セットアップ")

## Microsoft Intune を使用して iOS および Android 向けの Outlook のアプリ構成ポリシーを作成する

モバイル デバイス管理プロバイダーとして Microsoft Intune を使用している場合、次の手順を使用して、ActiveSync プロトコルで基本認証を利用するオンプレミス メールボックスのアカウント構成設定を展開できます。構成が作成されたら、次のセクション「構成設定を割り当てる」で説明するように、ユーザーのグループに設定を割り当てることができます。


> [!NOTE]
> 組織内のユーザーが iOS デバイスと Android for Work デバイスの両方を使用する場合は、プラットフォームごとに個別のアプリ設定ポリシーを作成する必要があります。



1.  Azure Portal にサインインします。

2.  **\[その他のサービス\] \> \[監視 + 管理\] \> \[Intune\]** の順に選択します。

3.  管理リストの **\[Mobile Apps\]** ブレードで、**\[アプリ構成ポリシー\]** を選択します。

4.  **\[アプリ構成ポリシー\]** ブレードで、**\[追加\]** を選択します。

5.  **\[アプリの構成を追加する\]** ブレードで、アプリ構成設定の**名前**と**説明** (省略可能) を入力します。

6.  **\[デバイスの登録の種類\]** で、**\[管理対象デバイス\]** を選択します。

7.  **\[プラットフォーム\]** で、**\[iOS\]** または **\[Android for Work\]** を選択します。

8.  **\[関連付けられているアプリ\]** を選択し、**\[対象アプリ\]** ブレードで、**\[Microsoft Outlook for iOS\]** または **\[Microsoft Outlook for Android\]** を選択します。

9.  **\[OK\]** をクリックして、**\[アプリの構成を追加する\]** ブレードに戻ります。

10. **\[構成設定\]** を選択します。**\[構成設定\]** ブレードで、iOS および Android 向けの Outlook の構成を提供するキーと値のペアを定義します。入力するキーと値の組み合わせについては、この記事の後半のセクション「キーと値のペア」で定義されています。
    

    > [!NOTE]
    > キー値のペアの入力には、構成デザイナーを使用する方法と、XML プロパティ リストを入力する方法があります。



11. 完了したら、**\[OK\]** をクリックします。

12. **\[アプリの構成を追加する\]** ブレードで、**\[作成\]** を選択します。

新しく作成した構成ポリシーが **\[アプリ構成ポリシー\]** ブレードに表示されます。

## 構成設定を割り当てる

Azure Active Directory のユーザー グループに、前のセクションで作成した設定を割り当てます。ユーザーが Microsoft Outlook アプリをインストールしてある場合、アプリは指定された設定により管理されます。これを実行するには、次の操作を実行します。

1.  Intune モバイル アプリケーション管理ダッシュボードの**\[モバイル アプリ\]** ブレードで、**\[アプリ構成ポリシー\]** を選択します。

2.  アプリ構成ポリシーのリストから、割り当てるポリシーを選択し、**\[割り当て\]** を選択します。

3.  **\[割り当て\]** ブレードで、**\[グループの選択\]** を選択します。

4.  **\[グループの選択\]** ブレードで、アプリ構成ポリシーを割り当てる対象の Azure AD グループを選択してから、**\[選択\]**、**\[保存\]** の順に選択します。

## キーと値のペア

Azure Portal または MDM プロバイダーでアプリ構成ポリシーを作成する場合は、次のキーと値のペアが必要です。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>キー</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.EmailAccountName</p></td>
<td><p>この値は、ユーザーのデバイス上に表示される表示名の電子メール アカウントを指定します。</p>
<p><strong>指定できる値</strong>:String</p>
<p><strong>指定されていない場合の既定値</strong>: &lt;blank&gt;</p>
<p><strong>例</strong>: user@companyname.com</p>
<p><strong>Intune トークン*</strong>: {{username}}</p></td>
</tr>
<tr class="even">
<td><p>com.microsoft.outlook.EmailProfile.EmailAddress</p></td>
<td><p>この値は、メールを送受信するために使用する電子メール アドレスを指定します。</p>
<p><strong>指定できる値</strong>:String</p>
<p><strong>指定されていない場合の既定値</strong>: &lt;blank&gt;</p>
<p><strong>例</strong>: user@companyname.com</p>
<p><strong>Intune トークン*</strong>: {{mail}}</p></td>
</tr>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.EmailUPN</p></td>
<td><p>この値は、アカウントを認証するために使用する電子メール プロファイルのユーザー プリンシパル名を指定します。</p>
<p><strong>指定できる値</strong>:String</p>
<p><strong>指定されていない場合の既定値</strong>: &lt;blank&gt;</p>
<p><strong>例</strong>: userupn@companyname.com</p>
<p><strong>Intune トークン*</strong>: {{userprincipalname}}</p></td>
</tr>
<tr class="even">
<td><p>com.microsoft.outlook.EmailProfile.ServerAuthentication</p></td>
<td><p>この値は、ユーザーの認証方法を指定します。</p>
<p><strong>指定できる値</strong>:'Username and Password'、'Certificates'</p>
<p><strong>指定されていない場合の既定値</strong>:'Username and Password'</p>
<p><strong>例</strong>:'Username and Password'</p></td>
</tr>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.ServerHostName</p></td>
<td><p>この値は、Exchange サーバーのホスト名を指定します。</p>
<p><strong>指定できる値</strong>:String</p>
<p><strong>指定されていない場合の既定値</strong>: &lt;blank&gt;</p></td>
</tr>
</tbody>
</table>


**\*** Microsoft Intune ユーザーは、MDM 登録ユーザーに応じて正しい値に展開されるトークンを使用できます。詳細については、「[管理対象の iOS デバイス用アプリ構成ポリシーを追加する](https://docs.microsoft.com/ja-jp/intune/app-configuration-policies-use-ios)」を参照してください。

