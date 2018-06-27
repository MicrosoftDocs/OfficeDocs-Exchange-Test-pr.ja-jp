---
title: '電子メールにアクセスできるように携帯電話を構成する: Exchange Online Help'
TOCTitle: 電子メールにアクセスできるように携帯電話を構成する
ms:assetid: 8d6e2cea-265a-43d9-a074-076f35658436
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb123704(v=EXCHG.150)
ms:contentKeyID: 52057471
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 電子メールにアクセスできるように携帯電話を構成する

 

_**適用先:**Exchange Online, Exchange Server 2013_

Windows Phone などの携帯電話を構成して、MicrosoftExchange ActiveSync を使用することができます。組織内の各携帯電話についてこの手順を実行する必要があります。

## 前提条件

  - 構成する携帯電話の製造元のドキュメントを確認している。

  - 所属する組織で Exchange ActiveSync が有効である。


> [!NOTE]
> 電話またはタブレットで Microsoft Exchange ベースの電子メールを設定する方法に関するデバイス固有の情報については、「<A href="https://support.office.com/ja-jp/article/set-up-a-mobile-device-using-office-365-for-business-7dabb6cb-0046-40b6-81fe-767e0b1f014f">一般法人向け Office 365 を使ってモバイル デバイスをセットアップする</A>」を参照してください。



## 携帯電話を Exchange ActiveSync を使用するように構成する

ほとんどの携帯電話やモバイル デバイスは、自動検出を使用して、Exchange ActiveSync を使用するように携帯電子メール クライアントを構成することができます。ほとんどの携帯電話では、電子メール アカウントを構成する際は、次の 2 つの情報が必要になります。

  - ユーザーの電子メール アドレス

  - ユーザーのパスワード

自動検出で Exchange サーバーに自動的に接続できない携帯電話の場合は、手動で携帯電話をセットアップする必要があります。手動でのセットアップには、ユーザーの電子メール アドレスとパスワードに加えて、Exchange ActiveSync サーバー名も必要です。ほとんどの組織では、Exchange ActiveSync サーバー名は、Outlook Web App サーバー名から /owa を除いたものと同じです (たとえば mail.contoso.com など)。

## Windows Phone の同期

Exchange ActiveSync を使用して Exchange メールボックスと同期するように Windows Phone の携帯電話を構成する場合、モバイル デバイス メールボックス ポリシーの一部の設定のみがサポートされます。このようなポリシー設定の詳細は、「[Windows Phone とデバイスでサポートされているモバイル デバイス メールボックス ポリシー](supported-mobile-device-mailbox-policies-for-windows-phones-and-devices-exchange-2013-help.md)」に記載されています。

使用中の Windows Phone のバージョンでサポートされていないモバイル デバイス メールボックス ポリシー設定を構成する場合は、**AllowNonProvisionableDevices** ポリシー設定を True に設定するか、または Windows Phone の携帯電話のために個別にモバイル デバイス メールボックス ポリシーを作成する必要もあります。

