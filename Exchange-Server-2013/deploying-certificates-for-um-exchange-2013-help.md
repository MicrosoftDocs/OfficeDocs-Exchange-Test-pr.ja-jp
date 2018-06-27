---
title: 'UM の証明書の展開: Exchange 2013 Help'
TOCTitle: UM の証明書の展開
ms:assetid: 95658f6f-eac2-4674-90e7-f2d3f25c5242
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee681661(v=EXCHG.150)
ms:contentKeyID: 52057848
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM の証明書の展開

 

_**適用先:**Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:**2013-04-29_

相互トランスポート層セキュリティ (相互 TLS) を使用して、ユニファイド メッセージング (UM) で、Microsoft Exchange 2013 サーバー間、VoIP ゲートウェイ、IP PBX、セッション ボーダー コントローラー (SBC) および Microsoft Lync Server で送信されるデータを暗号化することができます。証明書は、証明書の所有者の ID を、情報を電子的に暗号化し署名するために使用される一対の電子鍵 (パブリックとプライベート) にバインドします。

Exchange 2010 組織で、セキュリティ保護された SIP ダイヤル プラン、またはセキュリティで保護されたダイヤル プランを使用する場合、Microsoft Exchange UM Call Router サービスを実行している Exchange 2013 Client Access サーバーと、Microsoft Exchange UM サービスを実行しているメールボックス サーバーに対して使われた証明書をインポートする必要があります。UM サービスと UM Call Router サービスに対して、次のいずれかの証明書を使用できます:

  - 自己署名入り (Exchange) の証明書

  - 内部公開キー基盤 (PKI) の証明書

  - サード パーティの商用証明書

既定では、ユニファイド メッセージングをインストールすると、自己署名入りの証明書が作成され、使用されます。この自己署名入りの証明書は、VoIP ゲートウェイ、IP PBX、および SBC で使用できますが、UM を Lync Server と統合する際には使用できません。Lync Server で使用するために証明書を展開する場合は、Exchange 証明書ウィザードまたは **New-ExchangeCertificate** コマンドレットを使って、内部または PKI 証明機関 (CA) によって発行された証明書を取得するか、またはユニファイド メッセージングおよび Lync Server によって相互に信頼された商用証明書またはサード パーティ証明書を購入する必要があります。

## VoIP ゲートウェイ、IP PBX、および SBC の証明書の展開

UM において VoIP ゲートウェイ、IP PBX、SBC 間で送信されるデータを暗号化できるようにするには、以下の手順を実行する必要があります。

  - 自己署名入りの UM 証明書を使用するか、新しい Exchange 証明書の要求を作成して内部 PKI 証明書を取得するか、UM と VoIP ゲートウェイ、IP PBX、SBC 間の相互 TLS のために使用できるサード パーティの商用証明書を作成します。

  - 組織内のすべてのクライアント アクセス サーバーとメールボックス サーバー上で使用される証明書をインポートします。

  - UM サービスで証明書が使用できるようにします。

  - VoIP ゲートウェイ、IP PBX、および SBC に証明書をインポートします。

  - UM ダイヤル プランを、\[セキュリティで保護された SIP\] または \[セキュリティで保護\] として構成します。

  - 組織内のクライアント アクセス サーバーとメールボックス サーバー上で UM スタートアップ モードを構成します。

  - 完全修飾ドメイン名 (FQDN) を持つ、必要な UM IP ゲートウェイを作成します。

  - UM IP ゲートウェイのリスニング ポートが TLS ポート 5061 を使用するように構成します。

  - すべてのクライアント アクセス サーバー上でユニファイド メッセージング呼び出しルーター サービスを再起動し、すべてのメールボックス サーバー上で Microsoft Exchange ユニファイド メッセージング サービスを再起動します。

## Lync Server の証明書の展開

UM と Lync Server 間で送信されるデータを暗号化するには、以下の手順を実行する必要があります。

  - 新しい Exchange 証明書要求を作成し、内部 PKI 証明書を取得するか、サード パーティ商用証明書を購入します。証明書は、UM と Lync Server によって相互に信頼される必要があります。

  - 組織内のすべてのクライアント アクセス サーバーとメールボックス サーバー上で使用される証明書をインポートします。

  - UM サービスで証明書が使用できるようにします。

  - Lync Server を実行しているコンピューターに証明書をインポートします。

  - SIP URI UM ダイヤル プランを、\[セキュリティで保護された SIP\] または \[セキュリティで保護\] として構成します。

  - 組織内のクライアント アクセス サーバーとメールボックス サーバー上で UM スタートアップ モードを構成します。

  - Lync Server コンピューターから OcsUmUtil.exe を実行します。

  - 組織内のすべてのクライアント アクセス サーバー上でユニファイド メッセージング呼び出しルーター サービスを再起動し、すべてのメールボックス サーバー上で Microsoft Exchange ユニファイド メッセージング サービスを再起動します。詳細については、「[UM サービス手順](um-services-procedures-exchange-2013-help.md)」を参照してください。

  - Enterprise Edition フロントエンド プールの一部となっているすべての Lync Server で Lync Server フロントエンド サービスを再起動するか、Standard Edition フロントエンド サーバーを再起動します。**Stop-CsWindowsService** コマンドレットを使用して Lync Server サービスを停止し、**Start-CsWindowsService** コマンドレットで Lync Server サービスを開始できます。
    
    **Start-CsWindowsService** および **Stop-CsWindowsService** コマンドレットは、汎用的な Windows PowerShell コマンドレットである **Start-Service** および **Stop-Service** と類似しています。必要に応じて、**Start-Service** または **Stop-Service** コマンドレットを使用して Lync Server サービスを開始および停止できます。ただし、**Start-CsWindowsService** および **Stop-CsWindowsService** コマンドレットには、リモート コンピューター上での Lync Server サービスの停止と開始を容易にする *ComputerName* パラメーターが含まれています。リモート コンピューター上で Lync Server サービスを停止および開始する場合は、*ComputerName* パラメーターを含め、続けてリモート コンピューターの完全修飾ドメイン名 (FQDN) を入力します。**Start-Service** および **Stop-Service** コマンドレットには、このようなパラメーターがありません。
    

    > [!NOTE]
    > UM と Lync Server を完全に統合するには、組織内のいずれかのクライアント アクセス サーバーまたはメールボックス サーバー上で ExchUcUtil.ps1 スクリプトも実行する必要があります。


