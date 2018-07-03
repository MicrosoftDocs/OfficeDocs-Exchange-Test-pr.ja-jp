---
title: 'S/MIME によるメッセージの署名と暗号化: Exchange Online Help'
TOCTitle: S/MIME によるメッセージの署名と暗号化
ms:assetid: 887c710b-0ec6-4ff0-8065-5f05f74afef3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn626158(v=EXCHG.150)
ms:contentKeyID: 61212680
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# S/MIME によるメッセージの署名と暗号化

 

_**適用先:** Exchange Online, Exchange Server 2013_

S/MIME (Secure/Multipurpose Internet Mail Extensions) は、デジタル署名され、暗号化されたメッセージを送信するための広く受け入れられた方式、より正確に言えばプロトコルです。S/MIME では電子メールを暗号化し、デジタル署名を行うことができます。電子メールで S/MIME を使用すると、そのメッセージを受信する人は、受信箱にあるものが確かに送信者により開始された正しいメッセージであることがわかります。また、メッセージを受信する人は、そのメッセージが確かに特定の送信者から送信されたものであり、その送信者になりすました別の誰かからのものでないことも分かります。このために、S/MIME には認証、メッセージの整合性、発信元の否認防止 (デジタル署名の使用) などの暗号化セキュリティ サービスが用意されています。また、これは電子メッセージングのプライバシーとデータ セキュリティ (暗号化を使用) の強化にも役立ちます。電子メール関連での S/MIME の歴史とアーキテクチャーに関する完全な背景については、「[S/MIME について](https://go.microsoft.com/fwlink/?linkid=393948)」を参照してください。

Exchange 2013 SP1 または Exchange Online (Office 365 の一部) にメールボックスがある場合、管理者として、組織の S/MIME ベースのセキュリティを有効にできます。S/MIME をセットアップするには、Exchange 管理シェルおよびここにリンクされているトピックのガイダンスを使用します。Exchange 2013 SP1 または Exchange Online の環境で、Outlook や ActiveSync のサポートされているバージョンで S/MIME を使用するには、組織内のユーザーが署名と暗号化を目的として証明書が発行され、データが社内 Active Directory ドメイン サービス (AD DS) に公開されている必要があります。ユーザーの AD DS は、離れた施設やインターネットのどこかのクラウドベースのサービスではなく、ユーザーが管理している物理的な場所にあるコンピューターになければなりません。AD DS の詳細については、「[Active Directory ドメイン サービス](https://go.microsoft.com/fwlink/?linkid=394064)」を参照してください。

## サポートされるシナリオと技術的な考慮事項

組織で Exchange 2013 SP1 か Exchange Online が使用されている場合、次の任意のエンドポイントで機能するように S/MIME をセットアップできます。

  - Outlook 2010

  - Outlook 2013

  - Outlook Web App

  - Exchange ActiveSync (EAS)

これらの各エンドポイントに S/MIME をセットアップする手順は、どのエンドポイントを選択するかにより、若干異なってきます。一般的には、次の作業をする必要があります。

  - Windows ベースの証明機関をインストールし、S/MIME 証明書を発行するように公開キー基盤を設定します。サードパーティの証明書プロバイダーによって発行された証明書もサポートされています。詳細については、「[Active Directory 証明書サービスの概要](https://technet.microsoft.com/library/hh831740.aspx)」をご覧ください。

  - UserSMIMECertificate および/または UserCertificate 属性の社内 AD DS アカウントでユーザー証明書を発行します。

  - Exchange Online 組織の場合は、DirSync の該当するバージョンを使用して、AD DS のユーザー証明書を Azure Active Directory に同期します。次に、これらの証明書は Azure Active Directory から Exchange Online のディレクトリーに同期され、受信者へのメッセージの暗号化に使用されます。

  - S/MIME を検証するためには、仮想の証明書のコレクションを設定します。この情報は、電子メールの署名を検証する際に OWA により使用され、そのメールが信頼される証明書により署名されたことが確認されます。

  - S/MIME を使用する Outlook エンド ポイントまたは EA エンド ポイントを設定します。

## Outlook Web App で S/MIME を設定する

Outlook Web App がある Exchange 2013 SP1 または Exchange Online の S/MIME 設定には、次の重要な手順が含まれます。

1.  [Outlook Web App 用 S/MIME 設定値の構成](configure-s-mime-settings-for-outlook-web-app-exchange-2013-help.md)

2.  [S/MIME を検証するための仮想証明書コレクションをセットアップする](set-up-virtual-certificate-collection-to-validate-s-mime-exchange-2013-help.md)

3.  [S/MIME 用にユーザー証明書を Office 365 に同期させる](https://technet.microsoft.com/ja-jp/library/dn626159\(v=exchg.150\)) この手順は Exchange Online にのみ適用されます。

## 関連するメッセージ暗号化テクノロジ

メッセージのセキュリティがますます重要になっているため、管理者はセキュリティで保護されたメッセージングの原則と概念を理解しておく必要があります。S/MIME をはじめ、保護に関連したさまざまなテクノロジが発達して利用可能になってきたため、そのような理解は特に重要です。S/MIME と、電子メールでのその動作の詳細は、「[S/MIME について](https://go.microsoft.com/fwlink/?linkid=393948)」を参照してください。さまざまな暗号化テクノロジが連携して、保管されているメッセージと転送中のメッセージの保護を提供します。S/MIME は次のようなテクノロジと同時に機能しますが、それらに依存してはいません。

  -  **トランスポート層セキュリティ (TLS)** は、盗聴防止に役立てるために電子メール サーバー間のトンネルまたはルートを暗号化します。

  -  **Secure Sockets Layer (SSL)** は、電子メール クライアントと Office 365 サーバーとの間の接続を暗号化します。

  -  **BitLocker** は、データセンターのハード ディスク上のデータを暗号化することにより、何者かが無許可でアクセスしても内容を読み取れないようにします。

## S/MIME と Office 365 のメッセージ暗号化との比較

S/MIME には B2B (企業間取引) および B2C (企業と一般消費者間取引) 状況で頻繁に使用される証明書および公開のインフラストラクチャが必要です。ユーザーは、S/MIME で暗号化キーを制御し、送信する各メッセージにキーを使用するかどうかを選択できます。Outlook などの電子メール プログラムはデジタル署名と署名の検証を実行するために、信頼できるルート機関の場所を検索します。Office 365 のメッセージの暗号化は、組織内外の任意の受信者に送信されるメールを暗号化するための、管理者が構成できるポリシー ベースの暗号化サービスです (個々のユーザーは構成できません)。Azure Rights Management (RMS) 上に構築されたオンライン サービスであり、公開キー基盤に依存しません。Office 365 のメッセージの暗号化では、組織のブランドでメールをカスタマイズする機能などの追加機能も提供されます。Office 365 のメッセージの暗号化の詳細については、「[Office 365 のメッセージの暗号化](https://go.microsoft.com/fwlink/?linkid=392525)」を参照してください。

## 詳細情報

[Outlook Web App](outlook-web-app-exchange-2013-help.md)

[セキュリティで保護されたメール (2000)](https://technet.microsoft.com/ja-jp/library/cc962043.aspx)

