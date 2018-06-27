---
title: 'Exchange リモート接続アナライザー: Exchange 2013 Help'
TOCTitle: Exchange リモート接続アナライザー
ms:assetid: dd26698e-d00c-47f5-a7aa-c3894fe86c75
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff701693(v=EXCHG.150)
ms:contentKeyID: 49896513
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange リモート接続アナライザー

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2014-09-22_

MicrosoftExchange リモート接続アナライザー (ExRCA) は、Exchange サーバーの接続が正しくセットアップされていることを確認するのに役立ちます。 問題がある場合は、それらの問題の発見と解決も支援します。 ExRCA ウェブサイトでは、MicrosoftExchange ActiveSync、Exchange Web サービス、MicrosoftOutlook、およびインターネット メール接続を確認するテストを実行することができます。

## リモート接続アナライザーによるテスト

ExRCA を使用して、いくつかのテストを実行できます。 次のテストは Exchange 2007 以降のバージョンで動作します。

  - Exchange ActiveSync

  - Exchange Web サービス

  - Outlook

  - インターネット電子メール

## Exchange ActiveSync のテスト

次のテストは Exchange ActiveSync で実行することができます。

  - **\[Exchange ActiveSync\]:** このテストでは、接続するモバイル デバイスで Exchange ActiveSync を使用して Exchange サーバーに手順をシミュレーションします。

  - \[**Exchange ActiveSync の自動検出**\]: Exchange ActiveSync デバイスで、自動検出サービスから設定を取得する手順をシミュレーションします。

## Exchange Web サービス接続テスト

Exchange Web サービスは、さまざまな Exchange Web サービスの設定をテストします。 次のテストを Exchange Web サービスに実行することができます。

  - \[**同期、通知、空き時間情報、自動返信**\]: これらのテストでは、多数の基本的な Exchange Web サービス タスクをシミュレーションして動作を確認します。 これは、Entourage EWS またはその他の Web サービス クライアントを使用する外部アクセスをトラブルシューティングする IT 管理者に役立ちます。

  - **\[サービス アカウント アクセス (開発者)\]:** このテストはサービス アカウントから、指定したメールボックスへのアクセス、その中でのアイテムの作成/削除、さらに Exchange 偽装を経由したアクセスを実行できることを確認します。 このテストは、まずアプリケーション開発者が代替資格情報を使用してメールボックスにアクセスする機能をテストするために使用されます。

## Microsoft Office Outlook 接続テスト

次のテストは Outlook 接続で実行することができます。

  - \[**Outlook Anywhere (RPC over HTTP)**\]: このテストは、Outlook が Outlook Anywhere (RPC over HTTP) 経由の接続で使用する手順をシミュレーションします。

  - \[**Outlook 自動検出**\]: このテストでは Outlook が、自動検出サービスから設定を取得するために使用する手順をシミュレーションします。 このテストでは、実際にはメールボックスに接続しません。

## インターネット電子メールのテスト

インターネット メールには、次のテストを実行することができます。

  - \[**受信 SMTPメール**\]: このテストは、インターネット メール サーバーが受信 SMTP メールをドメインへ送信する際に使用する手順をシミュレーションします。

  - \[**送信 SMTP メール**\]: このテストは、送信 IP アドレスを特定の要件でチェックします。 これには、逆引き DNS、送信者 ID、および RBL 確認が含まれます。

  - **\[POP メール\]:** このテストでは、メール クライアントが POP3 を使用してメールボックスへ接続する際に使用する手順をシミュレーションします。

  - **\[IMAP メール\]:** このテストでは、メール クライアントが IMAP を使用してメールボックスへ接続する際に使用する手順をシミュレーションします。

