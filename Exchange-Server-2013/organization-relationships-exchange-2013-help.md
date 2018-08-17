---
title: '組織上の関係: Exchange 2013 Help'
TOCTitle: 組織上の関係
ms:assetid: 4c48db61-3370-462b-a3f8-2a6311c6e4ee
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657445(v=EXCHG.150)
ms:contentKeyID: 49896241
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 組織上の関係

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-02-20_

外部ビジネス パートナーと予定表の情報を共有するには、組織上の関係を設定します。Exchange 管理者は、Office 365 組織または別の Exchange 社内組織との組織上の関係を設定できます。予定表を社内の別の Exchange 組織と共有する必要がある場合は、両方の社内 Exchange 管理者が、クラウドとの認証関係 (「フェデレーション」とも呼ばれます) を設定し、最小ソフトウェア要件を満たす必要があります。

組織上の関係とは、各組織のユーザーに予定表の空き時間情報の表示を許可するための、ビジネス間の 1 対 1 の関係です。組織上の関係を設定する際には、自分の側の関係を設定し、外部組織のユーザーに表示を許可する情報のレベルを指定します。外部組織の側では、これと同じ設定にすることも、異なる設定にすることもできます。たとえば、Contoso が Tailspin Toys との組織上の関係を作成した場合、Tailspin Toys のユーザーは、Contoso のユーザーの電子メール アドレスを会議出席依頼に追加することで、Contoso のユーザーとの会議をスケジュールできます。出席を依頼する対象の Contoso ユーザーの空き時間情報は、Tailspin Toys ユーザーに表示されます。ただし、Tailspin Toys の管理者が Contoso との組織上の関係を設定するまでは、Contoso で Tailspin Toys ユーザーの空き時間情報を表示することはできません。

指定できるアクセス レベルは 3 つあります。

  - \[アクセス許可なし\]

  - 空き時間情報の時間へのアクセスのみ

  - 時間、件名、場所を含む空き時間情報へのアクセス


> [!NOTE]
> ユーザーが自分の空き時間情報を他のユーザーと共有したくない場合は、Outlook で既定のアクセス許可エントリを変更できます。それには、ユーザーが <STRONG>[予定表プロパティ]</STRONG> &gt; <STRONG>[アクセス許可]</STRONG> タブに移動して、<STRONG>[既定]</STRONG> アクセス許可を選択し、<STRONG>[アクセス許可レベル]</STRONG> リストから <STRONG>[なし]</STRONG> を選択します。ユーザーの空き時間情報は、組織上の関係が存在するとしても、内部ユーザーまたは外部ユーザーに表示されなくなります。そのユーザーが設定したアクセス許可が適用されます。



組織の共有の一部として組織上の関係を構成および管理するには、以下のトピックを参照してください。

[組織の関係を作成する](create-an-organization-relationship-exchange-2013-help.md)

[組織の関係の変更](modify-an-organization-relationship-exchange-2013-help.md)

[組織の関係を削除する](remove-an-organization-relationship-exchange-2013-help.md)

フェデレーション共有に関する詳細情報は、「[共有](sharing-exchange-2013-help.md)」を参照してください。

