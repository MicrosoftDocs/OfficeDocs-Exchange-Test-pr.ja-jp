﻿---
title: 'Outlook for iOS and Android: Exchange 2013 Help'
TOCTitle: Outlook for iOS and Android
ms:assetid: 3a66817c-30da-4965-a6db-2955b5365b0f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Mt465744(v=EXCHG.150)
ms:contentKeyID: 70061284
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook for iOS and Android

 

_**適用先:** Exchange Server 2010, Exchange Server 2013_

_**トピックの最終更新日:** 2018-04-02_

**概要**:この記事には、アプリで基本認証が使用される場合の Exchange 2013 オンプレミス環境における iOS および Android 用の Outlook に関する管理者向けのアーキテクチャ情報とセキュリティ情報が記載されています。

iOS および Android 用の Outlook アプリは、電子メール、予定表、連絡先、その他のファイルを集約し、組織内のユーザーがモバイル デバイスを使って、より多くのことを行えるように設計されています。この記事では、アプリのアーキテクチャと記憶域設計の概要を示します。それによって Exchange 管理者は、Exchange 組織内で iOS および Android 用の Outlook の展開と維持を行うことができます。

この記事では、Exchange 2013 環境におけるアプリの使用法について取り上げています。オンプレミスのメールボックスでのアプリによるハイブリッド先進認証の使用法については、「[Using hybrid Modern Authentication with Outlook for iOS and Android](using-hybrid-modern-authentication-with-outlook-for-ios-and-android-exchange-2013-help.md)」を参照してください。Exchange Online でのアプリの使用法については、「[Exchange Online での iOS および Android 用の Outlook](https://go.microsoft.com/fwlink/p/?linkid=845477)」を参照してください。

## iOS および Android 用の Outlook のアーキテクチャ

iOS および Android 用の Outlook は、モバイル デバイスにインストールされるフロントエンドのアプリと、*Outlook サービス*と呼ばれる、セキュリティで保護され、スケーラブルなバックエンドのクラウド サービスで構成されています。Outlook サービスでの情報処理により、Outlook の操作性を拡張する高度な機能が使用可能になり、パフォーマンスと安定性も向上します。このアーキテクチャは、集中的な処理のために Outlook サービスに依存しており、ユーザーのデバイスから必要とされるリソースを最小限に抑えます。

![iOS および Android 用の Outlook での基本認証のアーキテクチャ](images/Mt465744.f42e5af5-92fa-4d12-bf8c-994925c6084a(EXCHG.150).png "iOS および Android 用の Outlook での基本認証のアーキテクチャ")

ユーザーに提供される Outlook サービスには、次のようなものが含まれます。

  - 優先受信トレイに対するカテゴリ分類。

  - メーリング リストから 1 回のクリックで登録を解除する機能。

  - 検索の速度と効率性の向上。

  - 大きなファイルを、最初にモバイル デバイスにダウンロードせずに転送し、送信する機能。

このアーキテクチャでは、Azure Active Directory の条件付きアクセスや Intune アプリ保護ポリシーなどの Enterprise Mobility + Security 機能をサポートしていません。

## データ キャッシュ

パフォーマンスを向上させるため、各ユーザーのメールボックスから、電子メール、予定表、およびファイル データのサブセットが Outlook サービスに同期されます。基本認証によって認証するオンプレミスのメールボックスの場合、現在このサービスは Microsoft Azure 上で実行されています。

Outlook サービス内の情報は、接続クライアントの IP アドレスに応じて米国またはヨーロッパで現在キャッシュされています。Outlook サービスを Office 365 に移行するにつれて、Office 365 セキュリティ センターの原則と、地域ごとのデータ センター戦略とを連携させていきます。Office 365 では、お客様の国または地域で、お客様の管理者がサービスの初期セットアップ中に入力を行い、そのお客様のデータのプライマリ ストレージの場所を決定します。詳細については、「[Office 365 セキュリティ センター](https://go.microsoft.com/fwlink/p/?linkid=525776)」を参照してください。

## データ キャッシュのよく寄せられる質問

基本認証で使用する場合の iOS および Android 用の Outlook でのデータ保存に関するよく寄せられる質問を以下に示します。

## ユーザーのメールボックスのどれほどのデータが Outlook サービスと同期されますか。

約 1 か月分のメール、予定表、および連絡先のデータです。キャッシュ処理は、とりわけ次のような要素を考慮したアルゴリズムによって決定されます。メールボックスのサイズ、メールボックス内での特定のフォルダーの相対的な重要性 (たとえば、ユーザーによって作成されたフォルダーと比較した既定の受信トレイ フォルダー)、およびユーザーが特定のフォルダーにアクセスする頻度。

Outlook サービスでは、次のように添付ファイルのデータを格納します。ユーザーが Outlook でメールの添付ファイルを開くことを要求すると、サービスは添付ファイルを Exchange サーバーから取得し、一時的に格納します。その時点で、添付ファイルは、ユーザーのモバイル デバイス上のアプリに配信されます。1 か月以上古いデータは定期的にサービスから除外され、その時点で添付ファイルは Exchange サーバー上でのみ使用可能とされます。

## Outlook サービスからどのように自分の情報を削除すればいいですか。

Outlook サービスから自分の情報を削除するための 3 つのオプションがあります。

  - オプション 1:iOS および Android 用の Outlook アプリを使用した各ユーザーに対してリモート ワイプを開始して、Office 365 または Exchange に接続します。

  - オプション 2:すべてのユーザーに Outlook アプリを削除してもらいます。約 3 から 7 日間ですべてのデータが削除されます。

  - オプション 3:各ユーザーに、Outlook アプリから各自のアカウントを削除し、さらに各自のモバイル デバイスからアプリを削除してもらいます。アカウントを削除するには、各ユーザーに次の手順に従ってもらいます。
    
    1.  Outlook アプリの <strong>設定</strong> で、<strong>アカウント設定</strong> をタップします。
    
    2.  <strong>アカウントの選択</strong> をタップしてから、選択したアカウントで <strong>アカウントの削除</strong> をタップします。
    
    3.  <strong>デバイス & リモート データ</strong> をタップします。

## 一時的にキャッシュされたメールボックス データは、Outlook サービスに格納されている間、どのようにセキュリティで保護されるのでしょうか。

[Azure セキュリティ センター](https://azure.microsoft.com/support/trust-center/)で、データが現在、どのように保護されているかを参照できます。前述したように、Azure から Office 365 への移行を進めています。これらのサービスのセキュリティについては、[Office 365 セキュリティ センター](https://go.microsoft.com/fwlink/p/?linkid=525776)で網羅されています。

