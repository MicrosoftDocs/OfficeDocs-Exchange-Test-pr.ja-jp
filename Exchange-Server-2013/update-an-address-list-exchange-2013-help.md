---
title: 'アドレス一覧を更新する: Exchange 2013 Help'
TOCTitle: アドレス一覧を更新する
ms:assetid: 163e7099-cf14-4bb0-a84c-1401e9db670e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa996375(v=EXCHG.150)
ms:contentKeyID: 49895267
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.UpdateAddressListWizardForm.ScheduleWizardPage
ms.translationtype: HT
---

# アドレス一覧を更新する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-14_

アドレス一覧は、受信者およびその他の Active Directory オブジェクトの集合です。アドレス一覧を適用するのは、アドレス一覧のフィルター ルールが編集された場合です。アドレス一覧のメンバーシップを更新して、新しい受信者を追加したり、フィルター条件を満たしていないメンバーを削除したりするには、アドレス一覧を適用する必要があります。

アドレス一覧に関連する追加の管理タスクについては、「[アドレス一覧の手順](address-list-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : アドレス一覧の受信者数によっては、このプロセスの完了に時間がかかる場合があります。

  - アドレス一覧には、組織の規模とアドレス一覧に追加するフィルターによっては、数千人から数万人の受信者を登録するものがあります。アドレス一覧の更新には、多くのコンピューターリソースを消費する場合があります。したがって、アドレス一覧は、通常、オフピーク時に行います。

  - アドレス一覧の受信者数が 3,000 人を超える場合、Exchange 管理シェルによるアドレス一覧の更新をお勧めします。

このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EAC を使用してアドレス一覧を更新する

1.  <strong>組織</strong> \> <strong>アドレス一覧</strong> に移動します。

2.  リスト ビューで、更新するアドレス一覧を選択します。

3.  \[詳細\] ウィンドウで、<strong>更新</strong> をクリックします。

## シェルを使用してアドレス一覧を更新する

この例では、アドレス一覧 Washington State を更新します。

    Update-AddressList "Washington State"

同じ名前で複数のアドレス一覧が存在する場合、更新するアドレス一覧への完全パスを指定する必要があります。たとえば、North America の下のアドレス一覧 Sales を更新する場合に、Europe の下にも Sales アドレス一覧が存在する場合、次のコマンドを使用します。

    Update-AddressList "North America\Sales"

構文およびパラメーターの詳細については、「[Update-AddressList](https://technet.microsoft.com/ja-jp/library/aa997982\(v=exchg.150\))」を参照してください。

