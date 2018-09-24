---
title: 'フォレスト間のトポロジの空き時間情報サービスを構成する: Exchange 2013 Help'
TOCTitle: フォレスト間のトポロジの空き時間情報サービスを構成する
ms:assetid: f1e7d407-f0d3-47a7-8cc3-03c5980445d5
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb125182(v=EXCHG.150)
ms:contentKeyID: 52057873
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# フォレスト間のトポロジの空き時間情報サービスを構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-10-22_

可用性サービスは、セキュリティで保護された、一貫性のある、最新の空き時間情報を MicrosoftOutlook を実行しているクライアントに提供することで、インフォメーション ワーカーの空き時間情報データを向上させます。既定では、このサービスは Exchange Server 2013 と共にインストールされます。接続しているすべてのクライアントが Outlook を実行しているフォレスト間のトポロジでは、空き時間情報を取得するには、空き時間情報サービスが唯一の方法です。シェルを使用して、フォレスト間のトポロジの空き時間情報サービスを構成することはできません。


> [!NOTE]
> EAC を使用して、フォレスト間トポロジの可用性サービスを構成することはできません。



## 信頼されているフォレストと信頼されていないフォレストにおける可用性サービスの使用

空き時間情報サービスは、信頼されているフォレストまたは信頼されていないフォレストを経由するフォレスト間のトポロジで使用できます。利用できる空き時間情報の種類は、使用しているフォレストが信頼されているか、信頼されていないかによって異なります。

**信頼されているフォレスト**   信頼されているフォレストでは、可用性サービスが空き時間情報をユーザー単位で取得するように構成できます。空き時間情報サービスが空き時間情報をユーザー単位で取得できるように構成すると、サービスは特定ユーザーの代わりにフォレスト間の要求を実行します。これにより、リモート フォレストのユーザーが別のフォレストのユーザーの詳細な空き時間情報を取得できます。

**信頼されていないフォレスト**   信頼されていないフォレストでは、可用性サービスが空き時間情報を組織全体で取得するようにのみ構成できます。空き時間情報サービスが組織レベルで空き時間情報のフォレスト間要求を行うと、空き時間情報は組織の各ユーザーについて返されます。信頼されていないフォレストでは、ユーザー単位で返された空き時間情報のレベルを制御することはできません。

## フォレスト間トポロジ用の Windows の構成

既定では、グローバル アドレス一覧 (GAL) には単一のフォレストに属するメール受信者が含まれます。フォレスト間の環境がある場合、Microsoft Identity Lifecycle Manager (ILM) 2007 Feature Pack 1 (FP1) を使用して、任意のフォレストの GAL に他のフォレストに属するメール受信者を含めるようにすることをお勧めします。ILM 2007 FP1 により、他のフォレストに属する受信者を表すメール ユーザーが作成されます。ユーザーは GAL でそれらを参照してメールを送信できます。たとえば、フォレスト A のユーザーは、フォレスト B ではメール ユーザーとして表示されます。また、その逆の場合も同様です。送信先フォレスト内のユーザーは、他のフォレストの受信者を表すメール ユーザー オブジェクトを選択してメールを送信できます。

GAL 同期を有効にするには、メールが有効なユーザー、連絡先、およびグループを、指定された Active Directory サービスから集中メタディレクトリにインポートする管理エージェントを作成します。メタディレクトリでは、メールが有効なオブジェクトはメール ユーザーとして表されます。グループはメンバーシップが関連付けられていない連絡先として表されます。次に、管理エージェントは、指定された同期先フォレストの組織単位にこれらのメール ユーザーをエクスポートします。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「空き時間情報サービスのアクセス許可」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## シェルを使用して、信頼されているフォレスト間のトポロジでユーザー単位の空き時間情報を構成する

この例では、空き時間情報サービスがターゲット フォレストのメールボックス サーバー上でユーザー単位の空き時間情報を取得するように構成します。

```powershell
Get-MailboxServer | Add-ADPermission -Accessrights Extendedright -Extendedrights "ms-Exch-
EPI-Token-Serialization" -User "<Remote Forest Domain>\Exchange servers"
```

この例では、ソース フォレストのローカル メールボックス サーバー上で空き時間情報サービスが使用する、空き時間のアクセス方法を定義します。ローカルのメールボックス サーバーは、フォレスト ContosoForest.com からユーザー単位で空き時間情報にアクセスするように構成されています。この例では、サービス アカウントを使用して空き時間情報を取得します。

```powershell
Add-AvailabilityAddressSpace -Forestname ContosoForest.com -AccessMethod PerUserFB -UseServiceAccount:$true
```


> [!NOTE]
> 双方向のフォレスト間の可用性を構成するには、同期先フォレストでこれらの手順を繰り返します。



信頼されたフォレストとフォレスト間の空き時間情報を構成し、組織全体またはユーザー単位の資格情報を指定する代わりにサービス アカウントを使用する場合は、「シェルを使用して、サービス アカウントを使用した信頼されているフォレスト間の空き時間情報を構成する」セクションの例で示すように、アクセス許可を拡張する必要があります。その手順をターゲット フォレストで実行することにより、ソース フォレストのメールボックス サーバーに対して、元のユーザー コンテキストをシリアル化するためのアクセス許可が付与されます。

## シェルを使用して、サービス アカウントを使用した信頼されているフォレスト間の空き時間情報を構成する

この例では、サービス アカウントを使用する信頼されたフォレスト間の可用性を構成します。

```powershell
Get-MailboxServer | Add-ADPermission -Accessrights Extendedright -Extendedright "ms-Exch-EPI-Token-Serialization" -User "<Remote Forest Domain>\Exchange servers"
```

構文およびパラメーターの詳細については、以下のトピックを参照してください。

  - [Get-MailboxServer](https://technet.microsoft.com/ja-jp/library/bb123539\(v=exchg.150\))

  - [Add-ADPermission](https://technet.microsoft.com/ja-jp/library/bb124403\(v=exchg.150\))

  - [Add-AvailabilityAddressSpace](https://technet.microsoft.com/ja-jp/library/bb124122\(v=exchg.150\))

  - [Set-AvailabilityConfig](https://technet.microsoft.com/ja-jp/library/bb124103\(v=exchg.150\))

## シェルを使用して、信頼されていないフォレスト間のトポロジで組織全体の空き時間情報を構成する

この例では、空き時間情報構成オブジェクトの組織全体のアカウントを設定して、ターゲット フォレストの空き時間情報のアクセス レベルを構成します。

```powershell
Set-AvailabilityConfig -OrgWideAccount "Contoso.com\User"
```

この例では、ソース フォレストの空き時間情報アドレス空間構成オブジェクトを追加します。

```powershell
$a = Get-Credential (Enter the credentials for organization-wide user in Contoso.com domain)
Add-AvailabilityAddressspace -Forestname Contoso.com -Accessmethod OrgWideFB -Credential:$a
```

