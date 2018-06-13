---
title: 'Exchange ハイブリッド展開での Exchange ActiveSync デバイスの設定: Exchange 2013 Help'
TOCTitle: Exchange ハイブリッド展開での Exchange ActiveSync デバイスの設定
ms:assetid: 77f7cd72-2a8a-467e-9ffd-b93f5eeb2f69
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn931281(v=EXCHG.150)
ms:contentKeyID: 64965202
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange ハイブリッド展開での Exchange ActiveSync デバイスの設定

 

_**適用先:**Exchange Online, Exchange Server, Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:**2016-01-27_

Exchange のオンプレミスの組織から Office 365 にメールボックスを移動する際に Exchange ActiveSync デバイスが自動的に再構成されます。Exchange ActiveSync は Office 365 内の新しいメールボックスの場所を検索し、Office 365 と直接通信できるように構成を更新します。Exchange ActiveSync デバイスは、Office 365 に正常にリダイレクトされた後は、オンプレミスの Exchange サーバーとの通信を試行しなくなります。いくつかの例外 (詳細は後述) を除いて、メールが動作し続けるようにユーザーがこのデバイスを手動で設定する必要はなくなりました。

Office 365 にメールボックスを移動する場合は、「[ハイブリッド展開においてオンプレミスの組織と Exchange Online 組織間でメールボックスを移動する](move-mailboxes-between-on-premises-and-exchange-online-organizations-in-hybrid-deployments-exchange-2013-help.md)」を参照してください。

ハイブリッド展開の詳細については、「[Exchange Server のハイブリッド展開](exchange-server-hybrid-deployments-exchange-2013-help.md)」を参照してください。

自動リダイレクトを使用するには、オンプレミスのサーバーが Exchange 2010、Exchange 2013、Exchange 2016 以降の最新リリースを実行している必要があります。また、[ハイブリッド構成ウィザード](hybrid-configuration-wizard-exchange-2013-help.md) を使用してハイブリッド展開をセットアップしている必要もあります。Exchange ActiveSync のリダイレクト機能は、組織の関係オブジェクトで設定されている Web 上の Outlook のターゲット URL を使用します。このオブジェクトは、ハイブリッド構成ウィザードの実行時に構成されます。

組織が上記の要件を満たしている場合は、ユーザーのメールボックスを移動すると、追加の構成を行わなくてもモバイル デバイスが Office 365 に自動的にリダイレクトされるはずです。最善のエクスペリエンスを実現するため、ユーザーのモバイル デバイスで最新バージョンのオペレーティング システムと電子メール クライアントが実行されていることを確認してください。Android オペレーティング システムを実行しているデバイスなど、一部のモバイル デバイスではリダイレクトに予想よりも長い時間がかかる場合があります。また一部のデバイスでは、Exchange から送信された Exchange ActiveSync 451 のリダイレクトの指示が正しく解釈されない場合があります。これらのデバイスの場合、現在でもユーザーがデバイス上で電子メール アカウントを手動で再構成するか再作成する必要があります。デバイスが Exchange ActiveSync 451 リダイレクトをサポートしているかどうかについては、そのデバイスの製造元にお問い合わせください。

次のシナリオでは、Exchange ActiveSync の自動リダイレクトはサポートされていません。

  - Office 365 からオンプレミスの Exchange 組織へのメールボックスの移動。

  - オンプレミスの Exchange 組織間でのメールボックスの移動。

  - Exchange 2007 サーバーから Office 365 へのメールボックスの移動。

