---
title: 'Exchange 2013 でのマルチテナント機能: Exchange 2013 Help'
TOCTitle: Exchange 2013 でのマルチテナント機能
ms:assetid: df09257d-dd98-4f59-b830-1818cedda15c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ862352(v=EXCHG.150)
ms:contentKeyID: 50555886
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 でのマルチテナント機能

 

_**適用先:** Exchange Online, Exchange Server, Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

マルチテナントの (ホストされている) Exchange 2013 展開は、電子メール、データ、ユーザー、グローバル アドレス リスト (GAL) などの一般的な Exchange オブジェクトを通常は一切共有していない複数の個別の組織または部署 (テナント) をホストするように Exchange 組織が構成されている状態と定義されます。ハードウェア、ソフトウェア、およびリソースの (すべてが同時にテナント間の論理的な分離を維持しながらの) この共有により、組織は、標準 Exchange 展開の簡潔さを活かしながら、ホスティングのニーズを満たすマルチテナント機能とサービスを提供できます。

## Exchange 2013 組織におけるマルチテナンシー

Exchange 2013 では、Exchange 2010 Service Pack 2 (SP2) で使用されているアプローチによく似た、標準的なオンプレミスの Exchange インストールを使用することで引き続きホスティングがサポートされます。Microsoft は、`/hosting` モード スイッチを廃止し、アドレス帳ポリシー (ABP) を、独立ソフトウェア ベンダー (ISV) が提供するホスティング管理ソリューションおよび自動化ツールと組み合わせて使用するように強調しています。これらのソリューションは、Microsoft 承認の構成ガイドラインとプラクティスのフレームワーク上に構築され、Exchange 組織にホスティング サービスと機能をより簡単、より堅牢に提供する方法を提供します。

Exchange 2013 は、次のプライマリ コンポーネントと機能を活用してマルチテナンシーをサポートします。

  - **Active Directory**   マルチテナント Exchange 組織内の部署ごとに独立した *ExchangeOrganization* Active Directory コンテナーを備えるのではなく、単一の *ExchangeOrganization* Active Directory コンテナーを使用することで、Exchange 2013 マルチテナンシーがサポートされます。これにより、Active Directory 構造がさらに簡素化され、Active Directory に関わるアクセス許可の問題の発生確率を下げることができます。
    
    Exchange 2013 での Active Directory 変更の詳細については、[Active Directory](active-directory-exchange-2013-help.md) を参照してください。

  - **アドレス帳ポリシー (ABP)**   ABP は、Exchange 2010 SP2 で導入され、Exchange 2013 では、Exchange 組織におけるアドレス一覧、グローバル アドレス一覧 (GAL)、およびオフライン アドレス帳 (OAB) へのユーザー アクセスの制御に使用されます。ABP は、これらさまざまな Active Directory オブジェクトを、個々のユーザーに割り当てることができる単一の仮想オブジェクトにまとめます。これにより、マルチテナント組織の構造に合わせて、これらのリソースの論理グループを作成することができます。Exchange 2013 での ABP の機能は、Exchange 2010 SP2 での機能とほぼ同じです。
    
    Exchange 2013 での ABP の詳細については、[アドレス帳ポリシー](https://docs.microsoft.com/ja-jp/exchange/address-books/address-book-policies/address-book-policies) を参照してください。

  - **ホスティング管理ソリューション**   Exchange 2013 を使用してホストされた Exchange ソリューションを提供する管理者の一部は、ホスティング管理のカスタマイズされたアプローチを使用し、その利点を活かしています。Exchange 管理センター (EAC) にはいくつかの制限事項があるため、Microsoft はサードパーティ ベンダーとの連携を深め、ホストされた Exchange 2013 組織のガイドラインと承認済みフレームワークに準拠する、コントロール パネルおよび自動化ソリューションに関してベンダーによる開発を支援しています。ホストされた Exchange ソリューションを構成する組織がこれらのツールを活用し、必要に応じてホストされた組織を管理することをお勧めします。
    
    承認済みソリューション ベンダーを含む、ホストされた管理ソリューションの詳細については、「[Exchange Server 2013 hosting and multi-tenancy solutions and guidance](https://go.microsoft.com/fwlink/?linkid=275036)」(Exchange Server 2013のホスティングおよびマルチテナント ソリューションとガイダンス) を参照してください。

