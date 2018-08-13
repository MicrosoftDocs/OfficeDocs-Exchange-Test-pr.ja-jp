---
title: 'UM の証明書をインポートまたはエクスポートする: Exchange 2013 Help'
TOCTitle: UM の証明書をインポートまたはエクスポートする
ms:assetid: ee688c33-2e08-47e7-95fc-04ba10238341
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn205143(v=EXCHG.150)
ms:contentKeyID: 54652994
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM の証明書をインポートまたはエクスポートする

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2013-12-18_

EAC またはシェルを使って、自己署名型内部公開キー基盤 (PKI) またはサードパーティーの商用証明書をインポートまたはエクスポートすることができます。ユニファイド メッセージング (UM) の場合、Microsoft Exchange ユニファイド メッセージング サービスと Microsoft Exchange ユニファイド メッセージング呼び出しルータ サービスに対して、上記証明書のいずれかを使用できます。両方のサービスに対して同じ証明書を使うことも、サービスごとに異なる証明書を使うこともできます。

Exchange 用の証明書のインポートは、以下の場合に便利なことがあります。

  - あるファイルにエクスポートされた証明書をインポートする。

  - 内部証明機関によって生成された PKI 証明書ファイルをインポートする。

  - サード パーティの商用証明書をインポートする。

ローカル Exchange サーバー上の証明書ストアからの既存の証明書のエクスポートは、以下の場合に便利なことがあります。

  - 別の Exchange サーバーにインポートするためにエクスポートする。

  - VoIP ゲートウェイ、IP PBX、または SIP 対応 PBX にインポートするために証明書を エクスポートする

  - 証明書とその秘密キーをバックアップするために、証明書をエクスポートする。

ユニファイド メッセージングの証明書の管理に関するその他の管理タスクについては、「[UM の証明書の展開手順](deploying-certificates-for-um-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間:5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[Exchange およびシェル インフラストラクチャのアクセス許可](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)」の「証明書管理」と「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM サービス」。コンピューターのローカルの Administrators グループのメンバーであるアカウントを使用してログオンしていることを確認する必要があります。

  - 証明書をエクスポートする前に、**Get-ExchangeCertificate** コマンドレットを使用して、証明書の *PrivateKeyExportable* 属性が `$true` に設定されていることを確認します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して証明書をエクスポートする

1.  EAC で **\[サーバー\]** \> **\[証明書\]** \> **\[その他のオプション\]**![\[その他のオプション\] アイコン](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "[その他のオプション] アイコン") とクリックし、**\[Exchange 証明書のエクスポート\]** をクリックします。

2.  **\[Exchange 証明書のエクスポート\]** ページの **\[エクスポートするファイル\]** テキスト ボックスに証明書ファイルの名前を入力します。

3.  **\[パスワード\]** ボックスに、秘密キーを保護するために使用するパスワードを入力し、**\[OK\]** をクリックします。

## シェルを使用して証明書をエクスポートする

この例では、ユーザー名とパスワードを求めるプロンプトが表示された後、拇印が Thumbprint A36DE2B9B62980A717EBD0C3052F5F0B08FBFFCC の証明書をファイルにエクスポートします。

    $file = Export-ExchangeCertificate -Thumbprint A36DE2B9B62980A717EBD0C3052F5F0B08FBFFCC -BinaryEncoded:$true -Password (Get-Credential).password

この例では、次のことが行われます。

1.  **Get-ExchangeCertificate** コマンドレットを使用して、エクスポートする証明書を検索する。

2.  **Export-ExchangeCertificate** コマンドレットを使用して、証明書のパスワードを設定する。

3.  ユーザー名とパスワードを入力した後、証明書をファイルへ出力する。

<!-- end list -->
  ```
  $file = Get-ExchangeCertificate -DomainName umcorp.northwindtraders.com | Export-ExchangeCertificate -BinaryEncoded:$true -Password (Get-Credential).password
  ```
  ```
  Set-Content -Path "d:\umcerts\selfsigned.pfx" -Value $file.FileData =Encoding Byte
  ```

## EAC を使用して証明書をインポートする

1.  EAC で **\[サーバー\]** \> **\[証明書\]** \> **\[その他のオプション\]**![\[その他のオプション\] アイコン](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "[その他のオプション] アイコン") とクリックし、**\[Exchange 証明書のインポート\]** をクリックします。

2.  **\[Exchange 証明書のインポート\]** ページの **\[インポートするファイル\]** テキスト ボックスに証明書ファイルの共有フォルダー パスと名前を入力します。証明書がパスワードで保護されている場合、**\[パスワード\]** ボックスにパスワードを入力し、**\[次へ\]** をクリックします。

3.  **\[追加\]** ![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックして、証明書を適用するサーバーを選択し、**\[OK\]** をクリックします。サーバーをリスト ビューから削除するには、**\[削除\]**![\[削除\] アイコン](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[削除] アイコン") をクリックして **\[完了\]** をクリックします。

## シェルを使用して証明書をインポートする

この例では、ユーザー名とパスワードを入力した後、d:\\certificates\\exchange\\SelfSignedUMCert.pfx 証明書ファイルから証明書をインポートします。

    Import-ExchangeCertificate -FileData ([Byte[]]$(Get-Content -Path d:\certificates\exchange\SelfSignedUMCert.pfx -Encoding Byte -ReadCount 0)) -Password:(Get-Credential).password

