---
title: '送信コネクタ: Exchange 2013 Help'
TOCTitle: 送信コネクタ
ms:assetid: 6aa19a12-c7b2-4eac-a8dc-9a4d26919ac5
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998662(v=EXCHG.150)
ms:contentKeyID: 49896296
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 送信コネクタ

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2012-10-15_

Microsoft Exchange Server 2013 では、送信コネクタが受信側サーバーへの送信メッセージのフローを制御します。送信コネクタは、トランスポート サービスを実行するメールボックス サーバー上に構成されます。 多くの場合、送信コネクタは、DNS を使用して送信電子メール メッセージをスマート ホストまたは受信者に直接送信するように構成します。

トランスポート サービスを実行する Exchange 2013 メールボックス サーバーがメッセージを送信ルート上の次のホップに配信するには、送信コネクタが必要です。 メールボックス サーバー上に作成した送信コネクタは Active Directory 内に保存され、組織内のすべての、トランスポート サービスを実行するメールボックス サーバーから利用できます。


> [!IMPORTANT]
> Exchange 2013 を展開する際、送信メールをインターネットにルーティングするように送信コネクタを構成するまで、送信メール フローは発生しません。詳細については、「<A href="create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md">インターネットへの電子メール送信に対応した送信コネクタの作成</A>」を参照してください。



## 送信コネクタの種類の選択

通常、送信コネクタは Exchange 管理センター (EAC) の **\[メール フロー\]** セクションで作成します。 新規の送信コネクタを作成する場合、接続シナリオに適した、使用可能な **\[種類\]** を選択します。 種類によって、コネクタに割り当てる既定のアクセス許可セットが決定され、決定されたアクセス許可が、信頼されるセキュリティ プリンシパルに与えられます。 セキュリティ プリンシパルには、ユーザー、コンピューター、およびセキュリティ グループが含まれます。

特定の **\[種類\]** の選択を説明する手順には、[送信コネクタを作成し送信電子メールをスマート ホスト経由でルーティングする](create-a-send-connector-to-route-outbound-email-through-a-smart-host-exchange-2013-help.md) および [送信コネクタを作成し、TLS (トランスポート層セキュリティ) を適用した状態でパートナーに電子メールを送信する](create-a-send-connector-to-send-email-to-a-partner-with-transport-layer-security-tls-applied-exchange-2013-help.md) が含まれます。

EAC に Exchange 管理シェルを使用したい場合には、[New-SendConnector](https://technet.microsoft.com/ja-jp/library/aa998936\(v=exchg.150\)) コマンドレットを使用して送信コネクタを作成し、種類を指定することができます。

## Exchange 2013 の送信コネクタの新機能

Exchange 2013 では、クライアント アクセス サーバー上のフロント エンド トランスポート サービスとメールボックス サーバー上のトランスポート サービス間の関係で、送信コネクタの動作が新しくなりました。 まず、[Set-SendConnector](https://technet.microsoft.com/ja-jp/library/aa998294\(v=exchg.150\)) コマンドレットの *FrontEndProxyEnabled* パラメーターを使用してメールボックス サーバーのトランスポート サービスに送信コネクタを設定し、ローカル Active Directory サイトのフロント エンド トランスポート サーバーを介して送信メールをルーティングすることができます。これにより、電子メールがトランスポート サービスからルーティングされる方法が統合されます。Exchange 2013 のトランスポート サービス、ルーティング動作、および送信先の詳細については、「[メール ルーティング](mail-routing-exchange-2013-help.md)」を参照してください。トランスポート パイプラインの概要および各トランスポート サービスの説明については「[メール フロー](mail-flow-exchange-2013-help.md)」を参照してください。

*IsCoexistenceConnector* パラメーターは廃止されました。 メールボックスの一部が社内で、一部がクラウドでホストされるようなハイブリッド環境を構成するときには、通常、ハイブリッド構成ウィザードの使用をお勧めします。

*LinkedReceiveConnector* は廃止されました。 このパラメーターは、例えば、サード パーティのスパム対策サービスにメッセージをルーティングできるコネクタを作成するのに使用されました。 現在では、通常、MX レコードの使用によりスパム対策サービスにメールをルーティングするので、リンクされたコネクタの動作は不要です。

*MaxMessageSize* パラメーターで指定される既定の最大メッセージ サイズは、10 MB から 25 MB へ拡大されました。送信コネクタのパラメーターの設定方法の詳細については、「[Set-SendConnector](https://technet.microsoft.com/ja-jp/library/aa998294\(v=exchg.150\))」を参照してください。

*TlsCertificateName* が追加されました。 これは、送信接続に使用するローカルの証明書を認証し、不正な証明書のリスクを最小化するために使用されます。

