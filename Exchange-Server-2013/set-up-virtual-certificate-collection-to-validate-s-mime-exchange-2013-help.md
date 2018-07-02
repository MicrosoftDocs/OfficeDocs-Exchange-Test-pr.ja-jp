---
title: 'S/MIME を検証するための仮想証明書コレクションをセットアップする: Exchange Online Help'
TOCTitle: S/MIME を検証するための仮想証明書コレクションをセットアップする
ms:assetid: 04a616e6-197c-490c-ae8c-c8d5f0f0b3dd
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn626155(v=EXCHG.150)
ms:contentKeyID: 61212676
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# S/MIME を検証するための仮想証明書コレクションをセットアップする

 

_**適用先:** Exchange Online, Exchange Server 2013_

テナント管理者は、S/MIME 証明書の検証に使用する仮想証明書コレクションを構成する必要があります。この仮想証明書コレクションは、SST ファイル名拡張子を持つ証明書ストア ファイルの種類としてセットアップされます。SST ファイルには、S/MIME 証明書の検証時に使用されるすべてのルート証明書と中間証明書が含まれます。

## SST を作成して保存する

この手順を実行するには、シェルを使用する必要があります。オンプレミスの Exchange 組織で Exchange 管理シェル を開く方法については、「[シェルを開く](https://technet.microsoft.com/ja-jp/library/dd638134\(v=exchg.150\))」を参照してください。 Windows PowerShell を使って Exchange Online に接続する方法については、「[Exchange Online PowerShell への接続](https://go.microsoft.com/fwlink/p/?linkid=396554)」を参照してください。

管理者は、`Export-Certificate` コマンドレットを使用して信頼できるコンピューターから証明書をエクスポートし、その種類を SST に設定することによって、この SST ファイルを作成できます。`Export-Certificate` コマンドレットの詳細については、「[Export-Certificate](https://technet.microsoft.com/ja-jp/library/hh848628.aspx)」を参照してください。

SST ファイルが生成されたら、`Set-Smimeconfig` コマンドレットと *-SMIMECertificateIssuingCA* パラメーターを使用して、そのファイルを仮想証明書ストアに保存します。例:`Set-SmimeConfig -SMIMECertificateIssuingCA (Get-Content filename.sst -Encoding Byte)`

## 証明書が有効なことを確認する

Exchange 2013 SP1 は、まず、SST ファイルをチェックして、証明書を検証します。検証が失敗した場合は、ローカル コンピューターの証明書ストアを調査して、証明書を検証します。この動作は、Exchange 2013 SP1 で変更されたもので、以前のバージョンの Exchange とは異なります。Exchange Online では、SST のみが検証に使用されます。

## 詳細情報

[S/MIME によるメッセージの署名と暗号化](s-mime-for-message-signing-and-encryption-exchange-2013-help.md)

[Get-SmimeConfig](https://technet.microsoft.com/ja-jp/library/dn554257\(v=exchg.150\))

