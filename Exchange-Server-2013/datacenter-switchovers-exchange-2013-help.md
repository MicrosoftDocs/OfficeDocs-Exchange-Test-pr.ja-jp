﻿---
title: 'データセンターの切り替え: Exchange 2013 Help'
TOCTitle: データセンターの切り替え
ms:assetid: ac208c12-04d0-4809-bacd-72478ff14983
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd351049(v=EXCHG.150)
ms:contentKeyID: 62523712
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# データセンターの切り替え

 

_**適用先:** Exchange Server 2013 SP1_

_**トピックの最終更新日:** 2016-03-17_

サイトの復元構成では、サイト レベルのエラーに対する自動回復が DAG 内で発生する場合があります。これにより、メッセージング システムは機能した状態のままになります。この設定では、DAG メンバーを 2 か所に展開し、DAG のミラーリング監視サーバーを残りの 1 か所に展開する必要があるため、少なくとも 3 つの場所が必要です。

3 つの場所が存在しない場合、または存在するものの、データセンター レベルの回復アクションを制御したい場合は、サイト レベルのエラーが発生した場合に備えて手動回復用に DAG を設定できます。その場合、*データセンター切り替え* と呼ばれるプロセスを実行します。多くの障害復旧シナリオと同様に、データセンター切り替えを事前に計画および準備すると、復旧プロセスを簡略化して停止期間を短縮できます。

第 2 データセンターをアクティブ化するための初期決定を行った後、4 つの基本手順に従ってデータセンター切り替えの実行を完了します。

1.  **部分実行データセンターの終了**   これは、プライマリ データセンターの Exchange のサービスを終了する手順です (実行中のサービスがある場合)。メールボックス サーバーの役割はアクティブ/パッシブの高可用性モデルを使用するため、メールボックス サーバーの役割には特に重要です。部分的に障害が発生したデータセンターでサービスを停止しないと、プライマリ データセンターに戻る時点で、部分的に障害が発生したデータセンターからの問題が、サービスに悪影響を及ぼす可能性があります。
    

    > [!IMPORTANT]
    > プライマリ データセンターの障害の結果としてネットワークまたは Active Directory インフラストラクチャの信頼性が危険にさらされた場合は、これらの依存関係が正常なサービスに復元されるまで、すべてのメッセージング サービスをオフにすることをお勧めします。



2.  **第 2 データセンターの前提条件を検証および確認する**   第 2 データセンターのインフラストラクチャ依存関係の正常性の検証は、最初のデータセンター サービスとほぼ独立に行われるため、この手順を手順 1 と並行して実行できます。各組織には通常、この手順を実行するための独自の方法が必要です。たとえば、この手順の完了を決定するには、インフラストラクチャ監視アプリケーションによって収集およびフィルタリングされた正常性情報を確認するか、組織のインフラストラクチャに固有のツールを使用できます。インフラストラクチャが正常でなく、不安定な状態のときに第 2 データセンターをアクティブ化すると、満足する結果が得られない可能性があるため、これは重要な手順です。

3.  **メールボックス サーバーをアクティブにする**   この手順で、第 2 データセンターのアクティブ化のプロセスを開始します。Microsoft Exchange サービスでデータベースの停止と回復を処理できるため、この手順を手順 4 と平行して実行できます。メールボックス サーバーのアクティブ化のプロセスでは、プライマリ データセンターからの障害のあるサーバーを利用できないようにマークし、第 2 データセンターのサーバーをアクティブ化します。メールボックス サーバーのアクティブ化プロセスは、DAG がデータベース アクティブ化調整 (DAC) モードであるかどうかによって異なります。データベース アクティブ化調整モードの詳細については、「[データセンター ライセンス認証調整モード](datacenter-activation-coordination-mode-exchange-2013-help.md)」を参照してください。
    
    DAG が DAC モードの場合、Exchange のサイト復元コマンドレットを使用して、部分的に障害が発生したデータセンターを停止 (必要な場合) し、メールボックス サーバーをアクティブ化できます。たとえば DAC モードでは、この手順を [Stop-DatabaseAvailabilityGroup](https://technet.microsoft.com/ja-jp/library/dd335133\(v=exchg.150\)) コマンドレットを使用して実行できます。場合によっては、サーバーを利用不可として 2 回マークする必要があります (データセンターごとに 1 回ずつ)。次に、[Restore-DatabaseAvailabilityGroup](https://technet.microsoft.com/ja-jp/library/dd351169\(v=exchg.150\)) コマンドレットを実行して第 2 データセンターのデータベース可用性グループ (DAG) の残りのメンバーを復元するため、DAG メンバーをまだ動作しているメンバーまで減らし、それによってクォーラムを再確立します。DAG が DAC モードにない場合は、Windows のフェールオーバー クラスター ツールを使用してメールボックス サーバーをアクティブ化する必要があります。いずれかのプロセスが完了すると、第 2 データセンターでパッシブであったデータベース コピーがアクティブになりマウントできます。この時点で、メールボックス サーバーの復旧は完了です。

4.  **クライアント アクセス サーバーをアクティブにする**   このプロセスでは、URL マッピング情報およびドメイン ネーム システム (DNS) 変更方法を使用して、すべての必要な DNS の更新を実行します。マッピング情報は、実行する DNS 変更について説明します。更新を完了するために必要な時間は、使用される方法および DNS レコードでの TTL (Time to Live) 設定 (および展開のインフラストラクチャが TTL を許可するかどうか) に依存します。

手順 3 および 4 を完了してしばらくしたら、ユーザーがメッセージング サービスにアクセスできるようになります。手順 3 および 4 については、後で詳しく説明します。

**目次**

部分的に障害が発生したデータセンターの終了

メールボックス サーバーのアクティブ化

クライアント アクセス サーバーのアクティブ化

サービスのプライマリ データセンターへの復元

サイトの復元の再確立

## 部分的に障害が発生したデータセンターの終了

障害が発生したデータセンターの DAG メンバーがまだ動作している場合は、サービスを終了する必要があります。

DAG が DAC モードの場合、プライマリ データセンターの残存 DAG メンバーを終了するための特定の操作は以下のとおりです。

1.  プライマリ データセンターの DAG メンバーは、プライマリ データセンターで停止としてマークされている必要があります。*停止*は、データベースのマウントを防止する アクティブ マネージャー の状態であり、障害が発生したデータセンター内の各サーバーの アクティブ マネージャー が、[Stop-DatabaseAvailabilityGroup](https://technet.microsoft.com/ja-jp/library/dd335133\(v=exchg.150\)) コマンドレットを使用することでこの状態に置かれます。このコマンドレットの *ActiveDirectorySite* パラメーターを使用すると、1 つのコマンドでプライマリ データセンター内のすべてのサーバーを停止としてマークすることができます。障害によっては、この手順を実行できない場合があります。この手順は、データセンターの状態が許す場合に実行する必要があります。**Stop-DatabaseAvailabilityGroup** コマンドレットは、プライマリ データセンター内のすべてのサーバーに対して実行する必要があります。プライマリ データセンターでメールボックス サーバーは使用できないが Active Directory が動作している場合は、**Stop-DatabaseAvailabilityGroup** コマンドを *ConfigurationOnly* パラメーター付きで、プライマリ データセンター内でこの状態にあるすべてのサーバーに対して実行する必要があります。またはメールボックス サーバーをオフにする必要があります。障害が発生したデータセンター内のメールボックス サーバーをオフにすることも、サーバーに対して **Stop-DatabaseAvailabilityGroup** コマンドを正常に実行することもできないと、2 つのデータセンターにわたってスプリット ブレイン現象が発生する可能性が生まれます。この要件を満たすには、パワー管理デバイスを通してコンピューターを個別にオフにする必要があります。

2.  どのプライマリ データセンターのサーバーが停止されているかを表すために第 2 データセンターを更新する必要があります。これを行うには、同じ *ActiveDirectorySite* パラメーターを使用して同じ **Stop-DatabaseAvailabilityGroup** コマンドを *ConfigurationOnly* パラメーター付きで実行し、障害が発生したプライマリ データセンターの Active Directory サイトの名前を指定します。この手順の目的は、第 2 データセンター内のサーバーに、サービスの復元時にどのメールボックス サーバーが使用できるかについて通知することです。

DAG が DAC モードではない場合、プライマリ データセンターの残存 DAG メンバーを終了するための特定の操作は以下のとおりです。

1.  プライマリ データセンターの DAG メンバーは、メンバーごとに次のコマンドを実行して、DAG の基になるクラスターから強制的に削除される必要があります。
    
    ```powershell
    net stop clussvc
    ```
    ```powershell
    cluster <DAGName> node <DAGMemberName> /forcecleanup
    ```

2.  この際、第 2 データセンター内の DAG メンバーを再起動して、第 2 データセンターからの削除プロセスを完了するために使用する必要があります。第 2 データセンター内の各 DAG メンバーで、メンバーごとに次のコマンドを実行してクラスター サービスを停止します。
    
    ```powershell
    net stop clussvc
    ```

3.  第 2 データセンター内の各 DAG メンバーで、次のコマンドを実行してクラスター サービスのクォーラム開始を強制します。
    
    ```powershell
    net start clussvc /forcequorum
    ```

4.  フェールオーバー クラスター管理ツールを開き、DAG の基になるクラスターに接続します。クラスターを展開し、<strong>ノード</strong> を展開します。プライマリ データセンターの各ノードを右クリックし、<strong>他の操作</strong> に続いて <strong>削除</strong> を選択します。プライマリ データセンターの DAG メンバーの削除を完了後、フェールオーバー クラスター管理ツールを閉じます。

ページのトップへ

## メールボックス サーバーのアクティブ化

データセンター切り替えの間にメールボックス サーバーをアクティブ化するために必要な手順もまた、DAG が DAC モードであるかどうかによって異なります。第 2 データセンター内の DAG メンバーをアクティブ化する前に、第 2 データセンターのインフラストラクチャ サービスでメッセージング サービスのアクティブ化の準備ができていることを検証することをお勧めします。

DAG が DAC モードである場合、第 2 データセンター内のメールボックス サーバーのアクティブ化を完了する手順は、次のとおりです。

1.  第 2 データセンターの各 DAG メンバーでクラスター サービスを停止する必要があります。**Stop-Service** コマンドレットを使用してサービス (たとえば、`Stop-Service ClusSvc`) を停止するか、または昇格されたコマンド プロンプトから `net stop clussvc` を使用できます。

2.  次に、[Restore-DatabaseAvailabilityGroup](https://technet.microsoft.com/ja-jp/library/dd351169\(v=exchg.150\)) コマンドレットを使用してスタンバイ データセンター内のメールボックス サーバーをアクティブにします。サービスの復元に使用するサーバーを識別し、DAG での代替監視サーバーの使用を構成するため、スタンバイ データセンターの Active Directory サイトが **Restore-DatabaseAvailabilityGroup** コマンドレットに渡されます。代替監視サーバーが構成されていない場合は、[Restore-DatabaseAvailabilityGroup](https://technet.microsoft.com/ja-jp/library/dd351169\(v=exchg.150\)) コマンドレットの *AlternateWitnessServer* パラメーターと *AlternateWitnessDirectory* パラメーターを使用して構成できます。このコマンドが成功した場合、クォーラム条件がスタンバイ データセンターのサーバーに縮小されます。データセンター内のサーバー数が偶数の場合、DAG は、DAG オブジェクトの設定によって識別されるように代替監視サーバーの使用に切り替えます。

3.  これで、データベースをアクティブ化できるようになります。組織が使用する特定の構成によっては、自動でない可能性があります。スタンバイ データセンター内のサーバーがアクティブ化ブロックの設定を持つ場合、システムは、データベースのプライマリ データセンターからスタンバイ データセンターへの自動フェールオーバーを実行しません。スタンバイ データセンター内のデータベース コピーに対してフェールオーバーの制限が存在しない場合、システムは、第 2 データセンターのコピーを正常であると仮定してアクティブ化します。データベースが、明示的な手動操作が必要なアクティブ化ブロック設定で構成されている場合、操作には 2 つの選択肢があります。
    
    1.  アクティブ化をブロックする設定をオフにします。これにより、システムが既定の動作に戻り、使用可能なコピーがアクティブ化されます。
    
    2.  設定を変更せずそのままにし、[Move-ActiveMailboxDatabase](https://technet.microsoft.com/ja-jp/library/dd298068\(v=exchg.150\)) コマンドレットを使用して、第 2 データセンターでデータベースのアクティブ化を完了します。アクティブ化ブロックが設定されているときに **Move-ActiveMailboxDatabase** コマンドレットを使用してこの手順を完了するには、移動の対象を明示的に識別する必要があります。

4.  最後の手順は、タスクからのすべてのエラーおよび警告メッセージを確認することです。表示された警告をフォローアップおよび修正する必要があります。これらのコマンドのタスク設計モデルでは、設計の基本的な目標を達成できない場合にのみ失敗するようになっています。たとえば、**Restore-DatabaseAvailabilityGroup** コマンドレットは、第 2 データセンター内のサーバーがクォーラムを停止させずにサービスを再開できるよう DAG のクォーラムを縮小できなかった場合に失敗します。ただし、各タスクの出力は、管理者のフォローアップを必要とする問題の識別にも使用されます。すべてのタスク出力を保存し、フォローアップ操作のために確認することを強くお勧めします。

DAG が DAC モードでない場合、第 2 データセンター内のメールボックス サーバーのアクティブ化を完了する手順は、次のとおりです。

1.  クォーラムは、第 2 データセンター内の DAG メンバー数に基づいて変更される必要があります。
    
    1.  DAG メンバー数が奇数である場合、次のコマンドを実行して、DAG クォーラム モデルをノードおよびファイル共有マジョリティ クォーラムからノード マジョリティ クォーラムに変更します。
        
        ```powershell
        cluster <DAGName> /quorum /nodemajority
        ```
    
    2.  DAG メンバー数が偶数である場合、Exchange 管理シェルで次のコマンドを実行して、監視サーバーおよびディレクトリを再構成します。
        
        ```powershell
        Set-DatabaseAvailabilityGroup <DAGName> -WitnessServer <ServerName>
        ```

2.  次のコマンドを実行して、第 2 データセンター内の残りの DAG メンバーでクラスター サービスを開始します。
    
    ```powershell
    net start clussvc
    ```

3.  サーバー切り替えを実行し、DAG メンバーごとに次のコマンドを実行して、DAG 内のメールボックス データベースをアクティブ化します。
    
    ```powershell
    Move-ActiveMailboxDatabase -Server <DAGMemberinPrimarySite> -ActivateOnServer <DAGMemberinSecondSite>
    ```

4.  次のコマンドを実行して、2 番目のサイトの DAG メンバーごとにメールボックス データベースをマウントします。
    
    ```powershell
    Get-MailboxDatabase <DAGMemberinSecondSite> | Mount-Database
    ```

ページのトップへ

## クライアント アクセス サーバーのアクティブ化

クライアントは、サービス エンドポイント (Outlook Web App、自動検出、Exchange ActiveSync、Outlook Anywhere、POP3、IMAP4、および RPC クライアント アクセス アレイなど) に接続し、Exchange のサービスとデータにアクセスします。したがって、クライアント アクセス サーバーをアクティブ化すると、これらのサービス エンドポイントの DNS レコードのマッピングが、プライマリ データセンターの IP アドレスから新しいサービス エンドポイントとして構成される第 2 データセンターの IP アドレスに変更されます。変更が必要な DNS レコードが同じ DNS ゾーンに存在するかどうかは、DNS 構成によって変わります。

## クライアント アクセス サーバーのアクティブ化

クライアントは、次の 2 つの方法のどちらかで新しいサービス エンドポイントに自動的に接続します。

  - クライアントは、引き続き接続を試みます。TTL が元の DNS エントリに対して期限切れになった後、およびエントリがクライアントの DNS キャッシュから期限切れになった後は自動的に接続します。ユーザーは、コマンド プロンプトから `ipconfig /flushdns` コマンドを実行して、その DNS キャッシュを手動でクリアすることもできます。

  - クライアントの起動または再起動では、スタートアップ時に DNS 参照を実行し、サービス エンドポイントの新しい IP アドレスを取得します。これは、第 2 データセンター内のクライアント アクセス サーバーまたはアレイです。

すべての適切な構成の変更が完了し、第 2 データセンターのサービスが、プライマリ データセンターのときと同様に機能するように定義および構成されていると仮定し、確立された DNS 構成が正しいと仮定すれば、クライアント アクセス サーバーをアクティブ化するためにこれ以上の変更は必要ありません。

## トランスポート サービスのアクティブ化

メッセージを送信するクライアントおよび他のサーバーは、通常、DNS を使用してこれらのサーバーを識別します。第 2 データセンター内のトランスポート サービスのアクティブ化では、第 2 データセンターのメールボックス サーバーの IP アドレスをポイントするように DNS レコードを変更します。クライアントおよび送信サーバーは、次の 2 つの方法のどちらかで第 2 データセンター内のサーバーに自動的に接続します。

  - クライアントは、引き続き接続を試みます。TTL が元の DNS エントリに対して期限切れになった後、およびエントリがクライアントの DNS キャッシュから期限切れになった後は自動的に接続します。ユーザーは、コマンド プロンプトから `ipconfig /flushdns` コマンドを実行して、その DNS キャッシュを手動でクリアすることもできます。

  - クライアントの起動または再起動は、スタートアップ時に DNS 参照を実行し、SMTP エンドポイントの新しい IP アドレスを取得します。これは、第 2 データセンター内のメールボックス サーバーです。

すべての適切な構成の変更が完了し、第 2 データセンターのサービスが、プライマリ データセンターのときと同様に機能するように定義および構成されていると仮定し、確立された DNS 構成が正しいと仮定すれば、トランスポート サービスをアクティブ化するためにこれ以上の変更は必要ありません。

## ユニファイド メッセージング サービスのアクティブ化

ユニファイド メッセージング (UM) サービスは、組織の PBX システムと電話回線に接続します。PBX システムとユニファイド メッセージング サービス間の論理接続は、IP ゲートウェイによって提供されます。IP ゲートウェイには高可用性機能が含まれ、障害が検出されたときに IP ゲートウェイは複数のユニファイド メッセージング サービス間で切り替わることができます。

第 2 データセンターにサイト復元ソリューション専用となっているため無効な状態にあったユニファイド メッセージング サービスがある場合、[Enable-UMService](https://technet.microsoft.com/ja-jp/library/jj552411\(v=exchg.150\)) コマンドレット (たとえば、`Enable-UMService EX4`) を使用してユニファイド メッセージング サービスを有効にすることができます。

IP ゲートウェイが DNS サーバーを使用してユニファイド メッセージング サービスに関連付けられていると仮定した場合、ユニファイド メッセージング ビスのアクティブ化では、第 2 データセンター内のユニファイド メッセージング サービス用に構成される新しい IP アドレスをポイントするように DNS レコードを変更します。すべての適切な構成の変更が完了し、第 2 データセンターのサービスが、プライマリ データセンターのときと同様に機能するように定義および構成されていると仮定し、確立された DNS 構成が正しいと仮定すれば、ユニファイド メッセージング サービスをアクティブ化するためにこれ以上の変更は必要ありません。

使用中の IP ゲートウェイが DNS 名を使用したユニファイド メッセージング サービスの解決をサポートしない場合は、IP ゲートウェイを第 2 データセンター内のユニファイド メッセージング サービスの IP アドレスに手動でポイントするための追加の構成手順が必要です。

## エッジ トランスポート サーバーのアクティブ化

エッジ トランスポート サーバーの役割をアクティブにするための手順は、特定の構成に応じて変化します。2 つのデータセンター内のエッジ トランスポート サーバーは、アクティブ/パッシブまたはアクティブ/アクティブ構成で構成できます。アクティブ/パッシブ構成では、第 2 データセンター内のエッジ トランスポート サーバーは、第 2 データセンターがアクティブになるまでアイドルです。アクティブ/アクティブ構成では、両方のデータセンター内のエッジ トランスポート サーバーが常にメールを配信しています。

アクティブ/アクティブ構成では、第 2 データセンターのエッジ トランスポート サーバーは既に動作しているので、エッジ トランスポート サーバーをアクティブにする手順は必要ありません。アクティブ/パッシブ構成では、各 SMTP ドメインの DNS MX リソース レコードを、プライマリ データセンターからスタンバイ データセンターへの切り替えの一部として更新する必要があります。アクティブ/アクティブ構成は単純なデータセンター切り替えソリューションを提供しますが、アクティブ/アクティブ構成には、データセンターの切り替え後に第 2 データセンター内のエッジ トランスポート サーバーが、プライマリ データセンター内のエッジ トランスポート サーバーが使用できなくなった結果として増加した負荷のフローをサポートするための十分な容量を提供できることを確認するため、負荷を注意深く監視する必要があるという欠点があります。

アクティブ/アクティブ構成を使用した場合でも、データセンターの切り替え中にエッジ トランスポート サーバーの MX リソース レコードを更新することが適切な場合もあります。障害が発生したデータセンターの MX リソース レコードで障害が発生したデータセンターをポイントし続けることを許可すると、データセンターが回復を開始したときに、そのエッジ トランスポート サーバーへの接続を試行し始める可能性があります。これは、エッジ トランスポート サービスが (たとえば、データセンター内の依存サービスが復元中のため) 不安定な状態のときに発生します。

DNS レコードが組織の制御下にあると仮定すると、エッジ トランスポート サーバーのアクティブ化では、サーバーによってホストされる各 SMTP ドメインの MX リソース レコードを更新します。


> [!NOTE]
> 組織によって使用される MX リソース レコードが組織の制御下にある DNS サーバーによってホストされていない場合は、MX リソース レコードの CNAME レコードを参照し、更新可能な組織の制御下の CNAME レコードを使用することを考慮する必要があります。



DNS 更新は着信トラフィックを有効にし、発信トラフィックが、機能するエッジ トランスポート サーバーを持つサイトでメールボックス データベースのアクティブ化によって処理されます。

  - 着信 SMTP 接続が更新済みの名前解決情報を使用して開始されると、SMTP クライアントが第 2 データセンター内のエッジ トランスポート サーバーに接続します。トラフィックがエッジ トランスポート サーバーによって適切にルーティングされ、これ以上の変更は必要ありません。

  - 発信 SMTP 接続が開始されると、ローカルで使用できるエッジ トランスポート サーバーを試み、これらのメッセージが、受信サーバーの状態に応じてキューに入れられるか、すぐに送信されます。

ページのトップへ

## サービスのプライマリ データセンターへの復元

一般に、データセンターの障害は一時的または永続的です。プライマリ データセンターの永続的な破壊を引き起こすイベントなど、永続的なエラーの場合、プライマリ データセンターがアクティブになる見込みはありません。しかし、一時的なエラー (たとえば、長時間の電力消失や広範囲に及ぶものの修理可能な破損) の場合、プライマリ データセンターが最終的に完全サービスに復元される見込みがあります。

以前に障害が発生したデータセンターにサービスを復元するプロセスを*スイッチバック*といいます。データセンターのスイッチバックの実行に使用する手順は、データセンターの切り替えの実行に使用する手順と似ています。主な違いは、データセンターのスイッチバックはスケジュールされており、停止期間が通常、はるかに短い点です。

Exchange のインフラストラクチャとの依存関係が再アクティブ化され、機能し、安定しており、検証されるまで、スイッチバックを実行しないことが重要です。これらの依存関係が使用できないか、または正常でない場合は、スイッチバック プロセスが必要な停止よりも長くなり、プロセスが完全に失敗する可能性があります。

## メールボックス サーバーの役割のスイッチバック

メールボックス サーバーの役割は、プライマリ データセンターにスイッチバックされる最初の役割である必要があります。次の手順で、メールボックス サーバーの役割のスイッチバック プロセスを詳しく示します。

1.  データセンターの切り替えプロセスの一部として、プライマリ データセンター内のメールボックス サーバーは停止状態に置かれました。環境 (プライマリ データセンター、Exchange 依存関係、ワイド エリア ネットワーク (WAN) 接続など) が整っている場合、最初の手順は、復元されたプライマリ データセンターのメールボックス サーバーを開始状態に置き、それらを DAG に組み込むことです。これを実行する方法は、DAG が DAC モードであるかどうかによって異なります。
    
    1.  DAG が DAC モードである場合、[Start-DatabaseAvailabilityGroup](https://technet.microsoft.com/ja-jp/library/dd335076\(v=exchg.150\)) コマンドレットを使用して、DAG メンバーをプライマリ サイトに再度組み込むことができます。次に、DAG で適切なクォーラム モデルが使用されていることを確認するために、DAG に対してパラメーターを指定せずに [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/ja-jp/library/dd297934\(v=exchg.150\)) コマンドレットを実行します。
    
    2.  DAG が DAC モードでない場合、[Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/ja-jp/library/dd298049\(v=exchg.150\)) コマンドレットを使用して、DAG メンバーを再度組み込むことができます。

2.  プライマリ データセンター内のメールボックス サーバーが DAG に組み込まれたら、データベース コピーを同期する必要があります。障害の性質、停止の長さ、停止中に管理者が行った操作に応じて、データベース コピーの再シードが必要になる場合があります。たとえば、停止中、第 2 データセンターの存続するアクティブなコピー用にログ ファイルの切り詰めを許可するため、障害が発生したプライマリ データセンターからデータベース コピーを削除する場合、再シードが必要になります。各データベースは、個別にこのポイントから前方に進むことができます。プライマリ データセンター内のレプリケートされるデータベース コピーが正常になったら、次の手順に進むことができます。
    

    > [!NOTE]
    > このプロセスでは、すべてのデータベースを同時に移動する必要はありません。組織の大部分のデータベースを一度に移動することをお勧めしますが、プライマリ データセンターにデータベース コピーに関連する問題がある場合は一部のデータベースを第 2 データセンターに残すことができます。



3.  プライマリ データセンターのデータベースの大部分が正常な状態になった後、スイッチバック停止をスケジュールできます。スケジュールされた時刻に達したときに、次の手順を実行する必要があります。
    
    1.  データセンターの切り替えプロセス中、DAG は代替監視サーバーを使用するように構成されました。DAG は、プライマリ データセンター内の監視サーバーを使用するように再構成する必要があります。プライマリ データセンターの停止前に使用していたものと同じ監視サーバーと監視ディレクトリを使用している場合は、`Set-DatabaseAvailabilityGroup -Identity DAGName` コマンドを実行できます。元の監視サーバーや監視ディレクトリとは別の監視サーバーまたは監視ディレクトリを使用する予定の場合は、[Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/ja-jp/library/dd297934\(v=exchg.150\)) コマンドを使用して、監視サーバーと監視ディレクトリのパラメーターを適切な値で構成します。
    
    2.  プライマリ データセンターで再アクティブ化するデータベースは、第 2 データセンターでマウント解除する必要があります。[Dismount-Database](https://technet.microsoft.com/ja-jp/library/bb124936\(v=exchg.150\)) コマンドレットを使用して、データベースのマウントを解除することができます。
    
    3.  データベースがマウント解除されたら、クライアント アクセス サーバーの URL を第 2 データセンターからプライマリ データセンターに移動する必要があります。これには、URL の DNS レコードを、プライマリ データセンター内のクライアント アクセス サーバーまたはアレイをポイントするように変更します。これにより、システムは、各データベースの移動中にデータベース フェールオーバーが発生したかのように動作します。
        

        > [!IMPORTANT]
        > クライアント アクセス サーバーの URL が移動され、DNS TTL およびキャッシュ エントリの期限が切れるまで、次の手順に進まないでください。クライアント アクセス サーバーの URL をプライマリ データセンターに移動する前にプライマリ データセンターのデータベースをアクティブにすると、構成が無効になります (たとえば、マウントされたデータベースの Active Directory サイトにクライアント アクセス サーバーがない)。

    
    4.  プライマリ データセンター内の各データベースは正常な状態であるため、データベースの切り替えを実行することでプライマリ データセンターでアクティブ化できます。これには、アクティブにする各データベースに対して [Move-ActiveMailboxDatabase](https://technet.microsoft.com/ja-jp/library/dd298068\(v=exchg.150\)) コマンドレットを使用します。
    
    5.  各データベースをプライマリ データセンターに移動したら、[Mount-Database](https://technet.microsoft.com/ja-jp/library/aa998871\(v=exchg.150\)) コマンドレットを使用してマウントできます。

1 つ以上のデータベースがアクティブになり、プライマリ データセンターにマウントされたら、他のサーバーの役割のスイッチバック手順を実行できます。

## クライアント アクセス サーバーのスイッチバック

切り替えプロセスの一部として、クライアント アクセス サーバー、トランスポートおよびユニファイド メッセージング サービス、エッジ トランスポート サーバーのサービス エンドポイントを解決するために、クライアント、他のサーバー、IP ゲートウェイによって使用される内部および外部 DNS レコードが、第 2 データセンターの対応するエンドポイントをポイントするように変更されました。他のサーバーの役割のスイッチバック プロセスでは、プライマリ データセンターの復元されたサービス エンドポイントをポイントするようにこれらのレコードを変更します。

第 2 データセンターへの切り替え中に行われた DNS 変更の場合と同様、クライアント、サーバー、IP ゲートウェイは、引き続き接続を試み、TTL が元の DNS エントリに対して期限切れになった後、およびエントリが DNS キャッシュから期限切れになった後は自動的に接続します。

ページのトップへ

## サイトの復元の再確立

プライマリ データセンターへのスイッチバックが正常に完了したら、第 2 データセンターで各メールボックス データベースのコピーの正常性と状態を確認することで、プライマリ データセンターのサイトの復元を再確立できます。さらに、第 2 データセンターのデータベース コピーのアクティブ化がもともとブロックされている場合は、この時点で設定を再構成できます。

ページのトップへ
