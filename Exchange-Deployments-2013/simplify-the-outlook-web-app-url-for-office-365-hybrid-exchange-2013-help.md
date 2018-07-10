---
title: 'Office 365 ハイブリッドの Outlook Web App の URL を簡略化する: Exchange 2013 Help'
TOCTitle: Office 365 ハイブリッドの Outlook Web App の URL を簡略化する
ms:assetid: 19449aee-3796-4298-90c6-c7579b8d2f7a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Mt791749(v=EXCHG.150)
ms:contentKeyID: 74259165
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Office 365 ハイブリッドの Outlook Web App の URL を簡略化する

 

_<strong>トピックの最終更新日:</strong>2016-11-11_

ハイブリッド環境のクラウド メールボックスのユーザーのために Web 上の Outlook (Outlook Web App) の URL を構成する方法について説明します。

オンプレミスの Exchange から Office 365 に移動する組織にとって主な懸念事項は、ユーザーの操作性です。メールボックスをいつどこに移動したかにかかわらず、ユーザーが中断なくメールボックスにアクセスできなければなりません。これをふまえて、Web 上の Outlook (旧称 Outlook Web App) の共存のストーリーが重要になります。

次のシナリオをご検討ください。ある会社でハイブリッド展開を使用して、メールボックスの一部をオンプレミスの Exchange から Office 365 へ移動します。移動前の金曜日には、ユーザーは https://mail.contoso.com/owa という URL を使用して、オンプレミスのメールボックスにアクセスしていました。移動後の月曜日には、同じユーザーが、その URL を使用してメールボックスにアクセスしようとするとエラーが発生するようになります。

影響を受けるユーザーが Web 上の Outlook を使用してメールボックスに接続できるようにするには、2 つのオプションがあります。

  - **新しい URL (例: https://outlook.com/owa/contoso.com) をユーザーに伝える**   このオプションの懸念事項:
    
      - URL が複雑。
    
      - 影響を受けるユーザーにとって、操作性がシームレスでない。

  - **組織上の関係の TargetOWAUrl 設定を構成する**   このオプションの懸念事項:
    
      - クラウド メールボックスのエンドポイントが外部になる (ユーザーが予期するドメイン内にない)。
    
      - エンドポイントに URL 内のドメインが必要 (Office 365 ビジネス製品と outlook.com のコンシューマー製品を区別するため)。
    
      - エンドポイントにより、ユーザーに対し証明書の不一致の警告が表示される。

クラウド メールボックスのユーザーのこれらの懸念事項を排除するには、次の手順に従います。

1.  **DNS に mail.office365.com を指す CNAME レコードを作成する (例: cloudowa.contoso.com)**
    
      - ユーザーは内部または外部のインターネット接続から接続している可能性があるので、この CNAME レコードは必ず内部と外部 (パブリック) の DNS に作成します。
    
      - この例では、要求に contoso.com のドメインが使用されています (cloudowa の部分は削除)。つまり、URL 内のドメインを指定する必要はありません。

2.  **オンプレミスの組織上の関係において Web 上の Outlook リダイレクトを構成する**   これを行うには、オンプレミスの Exchange の Exchange 管理シェル で次の構文を使用します。
    
        Set-OrganizationRelationship -TargetOWAUrl http://<CNAME value>/owa
    
    たとえば、手順 1 で作成した CNAME レコードが cloudowa.contoso.com の場合は、次のコマンドを実行します。
    
        Set-OrganizationRelationship -TargetOWAUrl http://cloudowa.contoso.com/owa
    
    **メモ:** 
    
      - http を使い、https は使いません。
    
      - 組織上の関係では、末尾の値 /owa が必要ですが、ユーザーが URL に /owa を入力する必要はありません。

## 複数の認証プロンプト

以下の点に応じて、複数の認証プロンプトがユーザーに表示される場合があります。

  - どこから接続しているか (内部または外部のインターネット接続)。

  - コンピューターがドメインに参加しているか、いないか。

  - ハイブリッド環境で、ID フェデレーションを使用しているかどうか。

予測されるユーザーの認証プロンプト エクスペリエンスを、次の表で説明します。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>認証方法</th>
<th>クライアント コンピューター</th>
<th>認証プロンプト エクスペリエンス</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ID フェデレーション</p></td>
<td><p>内部インターネット接続</p></td>
<td><p>単一のプロンプト</p></td>
</tr>
<tr class="even">
<td><p>ID フェデレーション</p></td>
<td><p>外部インターネット接続</p></td>
<td><p>二重のプロンプト</p></td>
</tr>
<tr class="odd">
<td><p>ID フェデレーションなし</p></td>
<td><p>ドメイン参加 (内部または外部)</p></td>
<td><p>二重のプロンプト</p></td>
</tr>
<tr class="even">
<td><p>ID フェデレーションあり、またはなし</p></td>
<td><p>ドメイン不参加 (内部または外部)</p></td>
<td><p>二重のプロンプト</p></td>
</tr>
</tbody>
</table>


**注**:ID フェデレーションを行うには AD FS のエンドポイントを Internet Explorer のイントラネット ゾーンで構成すること (<https://go.microsoft.com/fwlink/p/?linkid=834460> のトピックを参照)、また AD FS を一般的な Office 365 ガイダンスに従って構成することが必要です。

