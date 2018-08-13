---
title: '電子メール アドレス ポリシーの作成: Exchange 2013 Help'
TOCTitle: 電子メール アドレス ポリシーの作成
ms:assetid: eb2bf42e-2058-4e17-85d5-97546433b40a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb125137(v=EXCHG.150)
ms:contentKeyID: 49896536
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.NewEmailAddressPolicyWizardForm.EmailAddressPolicyIntroductionPage
ms.translationtype: MT
---

# 電子メール アドレス ポリシーの作成

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-12-10_

受信者が電子メール メッセージを送受信するには、電子メール アドレスが必要です。電子メール アドレス ポリシーは、受信者が電子メールの送受信を行えるように、受信者 (ユーザー、連絡先、およびグループを含む) のプライマリ電子メール アドレスおよびセカンダリ電子メール アドレスを生成します。

電子メール アドレス ポリシーの作成では、次の電子メール アドレスの種類を使用できます。

  - **既定の SMTP 電子メール アドレス**。*既定*の SMTP 電子メール アドレスは、既に用意されている一般的に使用される電子メール アドレスの種類です。

  - **カスタム SMTP 電子メール アドレス**。既定の SMTP 電子メール アドレスを使用しない場合、カスタム SMTP 電子メール アドレスを指定できます。
    
    カスタム SMTP 電子メール アドレスを作成する場合、次の表の変数を使用して電子メール アドレスのローカル部分に代替値を指定できます。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>変数</th>
    <th>値</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>%g</p></td>
    <td><p>名 (姓名の名)</p></td>
    </tr>
    <tr class="even">
    <td><p>%i</p></td>
    <td><p>ミドル ネームのイニシャル</p></td>
    </tr>
    <tr class="odd">
    <td><p>%s</p></td>
    <td><p>姓 (名字)</p></td>
    </tr>
    <tr class="even">
    <td><p>%d</p></td>
    <td><p>表示名</p></td>
    </tr>
    <tr class="odd">
    <td><p>%m</p></td>
    <td><p>Exchange エイリアス</p></td>
    </tr>
    <tr class="even">
    <td><p>%<em>x</em>s</p></td>
    <td><p>姓から最初の <em>x</em> 文字を使用します。たとえば、<em>x</em> が 2 の場合、姓の最初の 2 文字が使用されます。</p></td>
    </tr>
    <tr class="odd">
    <td><p>%<em>x</em>g</p></td>
    <td><p>名から最初の <em>x</em> 文字を使用します。たとえば、<em>x</em> が 2 の場合、名の最初の 2 文字が使用されます。</p></td>
    </tr>
    </tbody>
    </table>


  - **SMTP 以外の電子メール アドレス**。SMTP 以外の電子メール アドレスでは、次の種類がサポートされます。
    
      - EX (従来の DN プロキシ アドレス プレフィックス DisplayName)
    
      - X.500
    
      - X.400
    
      - MSMail
    
      - CcMail
    
      - ロータス ノーツ
    
      - Novell GroupWise
    
      - Exchange ユニファイド メッセージング プロキシ アドレス (EUM プロキシ アドレス)
    

    > [!IMPORTANT]
    > Exchange では、SMTP 以外の電子メール アドレスはすべてカスタム アドレスと見なされます。X.400、GroupWise、ロータス ノーツなどの電子メール アドレスの種類に固有のダイアログ ボックスやプロパティ ページは、Exchange には用意されていません。SMTP 以外のカスタム電子メール アドレスを追加する場合は、適切な DLL (ダイナミック リンク ライブラリ) ファイルが必要になります。適切な DLL ファイルがないと、カスタマイズされた電子メール アドレス ポリシーを作成することはできません。以下のエラーがイベント ビューアーのログに記録されます。"コンピューター 'i386' 上のアドレスの種類 'SADF' に対する、Microsoft Exchange ディレクトリ内の電子メール アドレス記述オブジェクトが見つかりません。"



電子メール アドレス ポリシーを作成する詳細な手順については、以下のトピックを参照してください。

[電子メール アドレス ポリシーの作成](create-an-email-address-policy-exchange-2013-help.md)

[受信者フィルターを使用した電子メール アドレス ポリシーの作成](create-an-email-address-policy-by-using-recipient-filters-exchange-2013-help.md)

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[電子メール アドレスとアドレス帳](email-addresses-and-address-books-exchange-2013-help.md)」の「電子メール アドレス ポリシー」。

  - 電子メール アドレス ポリシーで SMTP アドレス ドメインを使用する前に、承認済みドメインを構成する必要があります。詳細については、「[承認済みドメイン](accepted-domains-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!WARNING]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EAC を使用して電子メール アドレス ポリシーを作成する

1.  **\[メール フロー\]** \> **\[電子メール アドレス ポリシー\]** に移動して、**\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン")をクリックします。

2.  **\[電子メール アドレス ポリシー\]** で、次の各フィールドに値を入力します:
    
      - **\[ポリシー名\]**
    
      - **\[電子メール アドレスの形式\]**
    
      - **このメール アドレスが適用される受信者の種類を指定します**

3.  
    
    **\[ルールを追加する\]** をクリックして、ポリシーの適用対象にする受信者をさらに制限します。この操作には、ブール値の **And** をステートメント作成します。
    

    > [!NOTE]
    > 適用するルールが多すぎると、電子メール アドレス ポリシーの範囲が狭まりユーザーがまったく含まれなくなる可能性があります。



4.  **\[ポリシーを適用する受信者をプレビューします\]** をクリックして、ポリシーの適用対象になる受信者を表示します。

5.  
    
    **\[保存\]** をクリックし、この変更を保存してポリシーを作成します。

6.  更新が済むまでは電子メール アドレス ポリシーが適用されないことを説明する警告が表示されます。ポリシーの作成後、そのポリシーを選択して、\[詳細\] ウィンドウで **\[適用\]** をクリックします。

## シェルを使用して電子メール アドレス ポリシーを作成する

この例を実行すると、Southeast offices のメールボックス ユーザーが姓のすべての文字と名の最初の 2 文字を組み合わせた電子メール アドレスを持つような電子メール アドレス ポリシーが作成されます。

    New-EmailAddressPolicy -Name "southeast offices" -IncludedRecipients MailboxUsers -ConditionalStateorProvince "Georgia","Alabama","Louisiana" -EnabledEmailAddressTemplates "SMTP:%s%2g@southeast.contoso.com"

構文およびパラメーターの詳細については、「[New-EmailAddressPolicy](https://technet.microsoft.com/ja-jp/library/aa996800\(v=exchg.150\))」を参照してください。

