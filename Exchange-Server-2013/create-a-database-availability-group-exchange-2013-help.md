---
title: 'データベース可用性グループを作成する: Exchange 2013 Help'
TOCTitle: データベース可用性グループを作成する
ms:assetid: d6b98299-e203-488b-af73-50753fe152c8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd351172(v=EXCHG.150)
ms:contentKeyID: 48270100
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# データベース可用性グループを作成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-07_

データベース可用性グループ (DAG) とは、データベース障害、サーバー障害、またはネットワーク障害からの自動的なデータベース レベルの回復を提供する、最大 16 の Microsoft Exchange Server 2013 メールボックス サーバーのセットのことです。メールボックス サーバーは DAG に追加されると、DAG の他のサーバーと連動して、データベース障害、サーバー障害、およびネットワーク障害からの自動的なデータベース レベルの回復を提供します。

DAG に関連する他の管理タスクについては、「[データベース可用性グループの管理](managing-database-availability-groups-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[高可用性とサイト復元のアクセス許可](high-availability-and-site-resilience-permissions-exchange-2013-help.md)」の「データベース可用性グループ」。

  - Windows Server 2012 を実行しているメールボックス サーバーを使用して DAG を作成する場合は、メンバーを DAG に追加する前にクラスター名オブジェクト (CNO) を事前に設定する必要があります。Windows Server 2012 R2 を実行しているメールボックス サーバーを使用して、管理用のアクセス ポイントがない DAG を作成する場合は、DAG に CNO を事前設定する必要はありません。詳細な手順については、「[データベース可用性グループのクラスター名オブジェクトを事前設定する](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md)」を参照してください。

  - DAG を作成するときに、その DAG の一意の名前を 15 文字以内で指定します。DAG の名前を指定することに加えて、DAG に 1 つ以上の IP アドレス (IPv4、または IPv4 と IPv6 の両方) を割り当てることも必要です。ただし、管理用のアクセス ポイントがない Windows Server 2012 R2 DAG を作成していて DAG に IP アドレスを割り当てない場合、その必要はありません。そうでない場合、割り当てる IP アドレスは、MAPI ネットワークの各サブネット上になければならず、使用可能である必要があります。1 つ以上の IPv4 アドレスを指定し、IPv6 を使用するようにシステムを構成している場合は、タスクでは、DAG に 1 つ以上の IPv6 アドレスも自動的に割り当てようとします。

  - DAG を作成する際には、監視サーバーおよび監視ディレクトリを任意に指定できます。ミラーリング監視サーバーを指定する場合は、メールボックス サーバーの役割がインストールされていないクライアント アクセス サーバーを使用することをお勧めします。これにより、Exchange 管理者は監視の可用性を把握することができ、ミラーリング監視サーバーを使用するために必要なすべてのセキュリティのアクセス許可が適用されます。
    
    以下のオプションと動作の組み合わせを使用できます。
    
      - DAG の名前のみを指定して、<strong>監視サーバー</strong> と <strong>監視ディレクトリ</strong> フィールドを空白のまま残すことができます。この場合、タスクでは、メールボックス サーバーの役割がインストールされていないクライアント アクセス サーバーが検索されます。また、そのクライアント アクセス サーバー上に既定の監視ディレクトリを自動的に作成して共有し、DAG を構成して、そのサーバーをミラーリング監視サーバーとして使用します。
    
      - DAG の名前、使用するミラーリング監視サーバー、およびミラーリング監視サーバーで作成して共有するディレクトリを指定できます。
    
      - DAG の名前および使用するミラーリング監視サーバーを指定して、<strong>監視ディレクトリ</strong> フィールドを空白のまま残すことができます。このシナリオでは、タスクは指定の監視サーバーに既定の監視ディレクトリを作成します。
    
      - DAG の名前を指定し、<strong>監視サーバー</strong> フィールドを空白のまま残して、ミラーリング監視サーバーで作成して共有するディレクトリを指定できます。この場合、ウィザードは、メールボックス サーバーの役割がインストールされていないクライアント アクセス サーバーを検索し、指定の監視ディレクトリをそのサーバーに自動的に作成してディレクトリを共有し、DAG を構成して、そのクライアント アクセス サーバーをミラーリング監視サーバーとして使用します。
    

    > [!IMPORTANT]
    > 指定するミラーリング監視サーバーが Exchange 2013 サーバーでも Exchange 2010 サーバーでもない場合、Exchange Trusted Subsystem ユニバーサル セキュリティ グループをミラーリング監視サーバー上のローカルの Administrators グループに追加する必要があります。必要に応じて、Exchange がディレクトリを作成し、ミラーリング監視サーバーで共有できることを確認するには、これらのセキュリティ アクセス許可が必要です。適切なアクセス許可が構成されていない場合、次のエラーが返されます。<BR><CODE>Error: An error occurred during discovery of the database availability group topology. Error: An error occurred while attempting a cluster operation. Error: Cluster API "AddClusterNode() (MaxPercentage=12) failed with 0x80070005. Error: Access is denied."</CODE>



  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してデータベース可用性グループを作成する

1.  EAC で、<strong>サーバー</strong> \> <strong>データベース可用性グループ</strong> に移動します。

2.  ![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックして、DAG を作成します。

3.      
    <strong>データベース可用性グループの新規作成</strong> ページで、DAG について次の情報を指定します。
    
      - <strong>データベース可用性グループ名</strong>   このフィールドを使用して、DAG の有効な一意の名前を 15 文字以内で入力します。名前はコンピューター名と同じで、その名前で対応する CNO が Active Directory に作成されます。この名前は DAG の名前と、基になるクラスターの名前の両方になります。
    
      - <strong>監視サーバー</strong>   このフィールドを使用して、DAG の ミラーリング監視サーバーを指定します。このフィールドを空白のまま残した場合、システムは、ミラーリング監視サーバーとして使用されるメールボックス サーバーと共に、コンピューター上にインストールされていない、ローカルの Active Directory サイトのクライアント アクセス サーバーを自動的に選択しようと試みます。
        

        > [!NOTE]
        > ミラーリング監視サーバーを指定している場合、ホスト名または完全修飾ドメイン名 (FQDN) のいずれかを使用する必要があります。IP アドレスやワイルドカード名の使用はサポートされていません。また、ミラーリング監視サーバーを DAG のメンバーにすることはできません。

    
      - <strong>監視ディレクトリ</strong>   このフィールドを使用して、監視データの格納に使用される監視サーバー上のディレクトリのパスを入力します。ディレクトリが存在しない場合、ミラーリング監視サーバーにディレクトリが作成されます。このフィールドを空白のまま残した場合は、既定のディレクトリ (%SystemDrive%\\DAGFileShareWitnesses\\\<DAG FQDN\>) が監視サーバー上に作成されます。
    
      - <strong>データベース可用性グループの IP アドレス</strong>   このフィールドを使用して、1 つ以上の静的 IPv4 アドレスを DAG に割り当てます。IPv4 アドレスを入力し、![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックして追加します。DAG が動的ホスト構成プロトコル (DHCP) を使用して必要な IPv4 アドレスを取得する場合は、このフィールドを空白のまま残します。オプションで、255.255.255.255 と入力して、IP アドレスやクラスター管理用のアクセス ポイントがない DAG を作成します。このオプションは、Windows Server 2012 R2 を実行しているメールボックス サーバーが含まれる DAG のみに適用されます。

4.  <strong>保存</strong> をクリックして DAG を作成します。

## シェルを使用してデータベース可用性グループを作成する

この例では、監視サーバー FILESRV1 を使用するように構成された DAG1 という DAG、およびローカル ディレクトリ C:\\DAG1 を作成します。また、DAG1 は、DAG の IP アドレスに DHCP を使用するように構成されています。

```powershell
New-DatabaseAvailabilityGroup -Name DAG1 -WitnessServer FILESRV1 -WitnessDirectory C:\DAG1
```

この例では、DAG2 という DAG を作成します。ローカル Active Directory サイトではメールボックス サーバーの役割に DAG の監視サーバーとしての役割が含まれておらず、クライアント アクセス サーバーがシステムにより自動的に選択されます。この例では、MAPI ネットワーク上のすべての DAG メンバーは同じサブネット上にあるので、DAG2 には 1 つの静的 IP アドレスが割り当てられます。

```powershell
New-DatabaseAvailabilityGroup -Name DAG2 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8
```

この例では、DAG3 という DAG を作成します。DAG3 は、監視サーバー MBX2 およびローカル ディレクトリ C:\\DAG3 を使用するように構成されています。複数の DAG メンバーが MAPI ネットワーク上の別々のサブネット上にあるので、DAG3 には複数の静的 IP アドレスが割り当てられます。

```powershell
New-DatabaseAvailabilityGroup -Name DAG3 -WitnessServer MBX2 -WitnessDirectory C:\DAG3 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8,192.168.0.8
```

この例では、DHCP を使用するように構成された DAG4 という DAG を作成します。また、ミラーリング監視サーバーはシステムによって自動的に選択され、既定の監視ディレクトリが作成されます。

```powershell
New-DatabaseAvailabilityGroup -Name DAG4
```

この例では、管理用のアクセス ポイントがない DAG5 という DAG を作成します (Windows Server 2012 R2 DAG でのみ有効)。さらに、DAG の監視サーバーとして MBX4 を使用し、既定の監視ディレクトリを作成します。

```powershell
New-DatabaseAvailabilityGroup -Name DAG5 -DatabaseAvailabilityGroupIPAddresses ([System.Net.IPAddress]::None) -WitnessServer MBX4
```

## 正常な動作を確認する方法

DAG が正常に作成されたことを確認するには、次のいずれかの手順を実行します。

  - EAC で、<strong>サーバー</strong> \> <strong>データベース可用性グループ</strong> に移動します。新しく作成された DAG が表示されます。

  - シェルで次のコマンドを実行して DAG が作成されたことを確認し、DAG のプロパティ情報を表示します。
    
    ```powershell
    Get-DatabaseAvailabilityGroup <DAGName> | Format-List
    ```

## 詳細情報

[データベース可用性グループ (DAG)](database-availability-groups-dags-exchange-2013-help.md)

[データベース可用性グループのプロパティを構成する](configure-database-availability-group-properties-exchange-2013-help.md)

[Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/ja-jp/library/dd297934\(v=exchg.150\))

[New-DatabaseAvailabilityGroup](https://technet.microsoft.com/ja-jp/library/dd351107\(v=exchg.150\))

[New-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/ja-jp/library/dd335225\(v=exchg.150\))

[Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/ja-jp/library/dd298049\(v=exchg.150\))

