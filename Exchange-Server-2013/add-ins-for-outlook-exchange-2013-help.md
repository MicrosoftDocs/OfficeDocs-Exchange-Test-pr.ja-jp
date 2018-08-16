---
title: 'Outlook 用アプリ: Exchange Online Help'
TOCTitle: Outlook 用アプリ
ms:assetid: 28b6f2a1-a235-4023-b561-6fd304962775
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ943753(v=EXCHG.150)
ms:contentKeyID: 52057804
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook 用アプリ

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

**概要**:Windows コンピューターや Macintosh コンピューター用、またはモバイル デバイス用の Outlook、Outlook Web App、Outlook on the web で機能する、Outlook 用アドインの概要です。

Outlook 用のアドインは、ユーザーが Outlook を終了せずに使用できる情報やツールを追加して、Outlook クライアントを便利にするアプリケーションです。アドインはサード パーティの開発者によって作成されたもので、ファイルや URL から、または Office ストアからインストールすることができます。既定では、すべてのユーザーがアドインをインストールできます。Exchange 管理者は、\[役割\] を使ってアドインをインストールできるユーザーを制御することができます。


> [!TIP]
> エンドユーザー向けの Outlook 用アドインの詳細については、Office.com のヘルプ トピック「<A href="https://go.microsoft.com/fwlink/p/?linkid=2823">インストールされているアドイン</A>」を参照してください。このトピックではアドインの概要について説明し、既定でインストールされている可能性がある Outlook 用アドインについて紹介します。



## Office ストア アドインとカスタム アドイン

Outlook クライアントでは、Office ストアで入手可能なさまざまなアドインがサポートされます。また Outlook では、自分で作成して組織のユーザーに配布できるカスタム アドインもサポートされます。


> [!NOTE]
> 特定の地域では、メールボックス、または組織での Office ストアへのアクセスはサポートされていません。<STRONG>Exchange 管理センター</STRONG>の <STRONG>[組織]</STRONG> &gt; <STRONG>[アドイン]</STRONG> &gt; <IMG title="[追加] アイコン" alt="[追加] アイコン" src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif"> の下のオプションに <STRONG>[Office ストアから追加]</STRONG> が表示されない場合は、URL またはファイルの場所から Outlook 用アドインをインストールできる場合があります。詳細については、サービス プロバイダーにお問い合わせください。




> [!NOTE]
> 一部の Outlook 用アドインは既定でインストールされています。Outlook の既定のアドインは英語のコンテンツのみで有効です。たとえば、メッセージ本文にドイツの住所があっても、Bing Maps アドインはアクティブになりません。



## アドインへのアクセスとインストール

既定では、すべてのユーザーがアドインをインストールしたり削除したりできます。Exchange 管理者は、アドインを管理したり、ユーザーによるアドインへのアクセスを管理したりするためのさまざまな制御を行うことができます。管理者は、Office ストアからダウンロードされたものではないアドインをユーザーがインストールできないようにすることができます (代わりに、これらのアドインをファイルや URL から "サイドロード" できます)。また管理者は、Office ストア アドインをユーザーがインストールできないようにしたり、他のユーザーの代理によるアドインのインストールを無効にしたりできます。組織のため、または組織内の一部のユーザーのためにアドインをインストールできる役割にユーザーを割り当てることもできます。

Office ストアからダウンロードしたものではないアドインをユーザーがインストールできないようにするには、そのユーザーの <strong>マイ カスタム アプリ</strong> 役割を削除します。Office ストアからダウンロードしたアドインをユーザーがインストールできないようにするには、そのユーザーの <strong>マイ マーケットプレース アプリ</strong> 役割を削除します。詳細については、「[Outlook 用のアドインをインストールおよび管理できる管理者とユーザーを指定する](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md)」をご覧ください。

組織内の一部またはすべてのユーザー用のアドインをインストールするには、「[組織の Outlook 用アプリをインストールまたは削除する](install-or-remove-add-ins-for-outlook-for-your-organization-exchange-2013-help.md)」をご覧ください。

必要に応じて、組織内でアドインの使用を特定のユーザーに制限することができます。詳細については、「[Outlook 用アプリへのユーザー アクセスを管理する](manage-user-access-to-add-ins-for-outlook-exchange-online-help.md)」をご覧ください。

## Outlook 用アドインでの一般的な管理タスク

Exchange 管理者が組織で管理する一般的なシナリオは複数あります。

**エンド ユーザーがすべての Outlook クライアント上で Outlook 用アドインをインストールできないようにする場合は、Exchange 管理センターで役割を次のように変更します。**

  - Office ストアのアドインをユーザーがインストールできないようにするには、そのユーザーの <strong>マイ マーケットプレース</strong> 役割を削除します。

  - ユーザーが Office ストア以外のソースからアドインを読み込めないようにするには、そのユーザーの <strong>マイ カスタム アプリ</strong> 役割を削除します。

  - ユーザーがすべてのアドインをインストールできないようにするには、そのユーザーの上記の役割の両方を削除します。

詳細については、「[Outlook 用のアドインをインストールおよび管理できる管理者とユーザーを指定する](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md)」を参照してください。

**エンド ユーザーが現在アドインにアクセスでき、そのアクセスを削除する場合は、`Get-App` コマンドレットを使用して各ユーザーがインストールしたアドインを確認します。**

次に、`Remove-App` コマンドレットを使用して、1 つまたは複数のユーザーからすべてのアドインを削除します。 

詳細については、Exchange 2013 の「[Get-App](https://technet.microsoft.com/ja-jp/library/jj218673\(v=exchg.150\))」および「[Remove-App](https://technet.microsoft.com/ja-jp/library/jj218709\(v=exchg.150\))」を参照してください。Exchange Online または Exchange 2016 の場合は、[ここ](https://go.microsoft.com/fwlink/p/?linkid=8447)にアクセスしてください。

## 管理者とユーザーにアドインのインストールを許可する

組織のどの管理者に Outlook 用のアドインをインストールして管理するアクセス許可を持たせるかを指定できます。また、組織のどのユーザーに、自分で使用するアドインをインストールして管理するアクセス許可を持たせるかを指定することもできます。詳細については、「[Outlook 用のアドインをインストールおよび管理できる管理者とユーザーを指定する](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md)」をご覧ください。

