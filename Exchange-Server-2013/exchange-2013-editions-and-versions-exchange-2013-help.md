---
title: 'Exchange 2013: エディションとバージョン: Exchange 2013 Help'
TOCTitle: 'Exchange 2013: エディションとバージョン'
ms:assetid: b563b543-fb3f-4465-9a54-cbfd680aee1f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb232170(v=EXCHG.150)
ms:contentKeyID: 50555859
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013: エディションとバージョン

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

Microsoft Exchange Server 2013 は、Standard Edition と Enterprise Edition の 2 つのサーバーのエディションで使用できます。Enterprise Edition は、RTM (Release to Manufacturing) 版と累積更新プログラム 1 (CU1) 版ではサーバーあたり 50 マウント済みデータベースまで、累積更新プログラム 2 (CU2) 以降ではサーバーあたり 100 マウント済みデータベースまで拡張できます。Standard Edition ではサーバーあたり 5 マウント済みデータベースまでに制限されています。マウント済みデータベースとは使用中のデータベースのことです。マウント済みデータベースは、クライアントで使用するためにマウントされたアクティブ メールボックス データベース、またはログのレプリケーションと再生の回復時にマウントされたパッシブ メールボックス データベースのいずれかです。上記制限を上回る数のデータベースを作成することはできますが、指定された最大数までしかマウントできません。回復データベースはこの制限には含まれません。

これらのライセンス エディションは、プロダクト キーによって定義されます。有効なライセンスのプロダクト キーを入力すると、サーバーのサポートされているエディションが設定されます。プロダクト キーは同じエディションのキーの切り替えおよびアップグレードにのみ使用でき、ダウングレードには使用できません。有効なプロダクト キーを使用して、Exchange 2013 の評価版から Standard Edition と Enterprise Edition のいずれかに移行できます。また、有効なプロダクト キーを使用して、Standard Edition から Enterprise Edition に移行することもできます。

同じエディションのプロダクト キーを使用して、サーバーのライセンスを変更することもできます。たとえば、2 台の Standard Edition サーバーと 2 つのキーがあるときに、誤って同じキーを両方のサーバーに使用した場合は、一方のキーを発行済みの別のキーに変更できます。この作業を行うときに、再インストールや再構成は必要ありません。プロダクト キーを入力して Microsoft Exchange Information Store service サービスを再起動すると、プロダクト キーに対応するエディションが反映されます。

評価版の有効期限が切れても機能は失われないので、Exchange 2013 を再インストールすることなく、120 日を超えてテスト、デモンストレーション、トレーニング、およびその他の非運用環境を維持することができます。

前述したように、プロダクト キーを使用して、Enterprise Edition から Standard Edition にダウングレードしたり、評価版に戻したりすることはできません。このようなダウングレードを実行するには、Exchange 2013 をアンインストールし、Exchange 2013 を再インストールして、適切なプロダクト キーを入力する必要があります。

## Exchange 2013 バージョン

Exchange 2013 バージョンの一覧と、Exchange 2013 の最新バージョンのダウンロードおよびアップグレードの方法については、以下のトピックを参照してください。

  - [Exchange Server 更新プログラム: ビルド番号とリリース日](https://technet.microsoft.com/ja-jp/library/hh135098\(v=exchg.150\))

  - [Exchange 2013 から最新の累積更新プログラムまたは Service Pack へのアップグレード](upgrade-exchange-2013-to-the-latest-cumulative-update-or-service-pack-exchange-2013-help.md)

実行している Exchange 2013 バージョンのビルド番号を表示するには、Exchange 管理シェルで次のコマンドを実行します。

```powershell
Get-ExchangeServer | fl name,edition,admindisplayversion
```

## Exchange 2013 ライセンスの種類

Exchange 2010 のライセンス方法と同様に、Exchange 2013 はサーバー/クライアント アクセス ライセンス (CAL) モデルとしてライセンスされます。ライセンスの種類は、次のとおりです。

  - **サーバー ライセンス**   実行されているサーバー ソフトウェアのインスタンスごとに、1 つのライセンスを割り当てる必要があります。サーバー ライセンスは、Standard Edition と Enterprise Edition の 2 つのサーバーのエディションで使用できます。

  - **クライアント アクセス ライセンス (CAL)**   Exchange 2013 にも、Standard CAL と Enterprise CAL と呼ばれる 2 つのクライアント アクセス ライセンス (CAL) エディションが用意されています。サーバー エディションと CAL タイプは混在させることができます。たとえば、Enterprise CAL を Exchange 2013 Standard Edition で使用できます。同様に、Standard CAL を Exchange 2013 Enterprise Edition で使用できます。

Exchange ライセンス タイプの詳細については、「[ライセンス](https://go.microsoft.com/fwlink/p/?linkid=392675)」を参照してください。

