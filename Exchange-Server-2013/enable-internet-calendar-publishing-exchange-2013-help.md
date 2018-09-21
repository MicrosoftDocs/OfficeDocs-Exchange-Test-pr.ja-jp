---
title: 'インターネット予定表の公開を有効にする: Exchange 2013 Help'
TOCTitle: インターネット予定表の公開を有効にする
ms:assetid: b4c71696-52bb-492c-8259-0e419acd0bbc
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ853046(v=EXCHG.150)
ms:contentKeyID: 50555857
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# インターネット予定表の公開を有効にする

 

_**適用先:** Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:** 2016-08-22_

**概要**:これらの手順を使用して、Exchange 2013 組織内の OWA ユーザーが予定表の空き時間情報を外部の組織と共有できるようにします。

Microsoft Exchange Server 2013 組織のユーザーは、Exchange 組織外のユーザーや、インターネットにアクセスできるその他の個人と、予定表の空き時間情報を共有できます。インターネット予定表の公開により柔軟性が向上し、予定表の空き時間情報を共有できるユーザーの数が増加します。

インターネット予定表の公開を有効にするには、一般的な 3 つの手順を実行します。

1.  メールボックス サーバーの Web プロキシ URL を構成します (この手順は、ユーザーの組織内に Web プロキシ URL が既に存在する場合にのみ必要です。それ以外の場合は手順 2 に進みます)。

2.  クライアント アクセス サーバーの仮想ディレクトリの公開を有効にします。

3.  インターネット予定表の公開のための専用の共有ポリシーを作成するか、または <strong>匿名</strong> ドメインをサポートするように既定の共有ポリシーを更新します。いずれかの方法により、Exchange 組織内のユーザーは、インターネットにアクセスできる他のユーザーを招待して、公開された URL にアクセスすることにより、予定表の空き時間情報を限定的に表示させることができます。


> [!IMPORTANT]
> 手順 3 を完了すると、ユーザーは Outlook から予定表を公開する必要があります。予定表の公開は、ユーザーが組織外の人に提供できる URL を作成します。URL の 1 つでは、受信者が Outlook または Outlook Web App を使用して予定表を登録できます。もう 1 つのURLでは、受信者は Web ブラウザーで予定表を表示できます。ユーザーはそれぞれ、別のユーザーがどの程度まで詳細に表示できるかを制御できます。



共有ポリシーに関連する追加の管理タスクについては、「[共有ポリシー](sharing-policies-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - このタスクの予想所要時間:15 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「予定表と共有のアクセス許可」。

  - Exchange 2013 クライアント アクセス サーバーが、ユーザーの予定表情報を共有する Exchange 組織内に存在する。

  - ユーザー メールボックスが、ユーザーの予定表情報を共有する Exchange 組織内の Exchange 2013 メールボックス サーバー上にある。

  - Outlook 2010 以降および Outlook Web App のユーザーのみが、共有への招待を作成できる。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 実行方法

## 手順 1: シェルを使用して、Web プロキシ URL を構成します。


> [!NOTE]
> この手順は、Web プロキシ URL が既にユーザーの組織内に存在する場合にのみ必要です。それ以外の場合は、手順 2 に進みます。<BR>Exchange 管理センター (EAC) を使用して、Web プロキシ URL を構成することはできません。



この例では、メールボックス サーバー MAIL01 の Web プロキシ URL を構成します。

```powershell
Set-ExchangeServer -Identity "MAIL01" -InternetWebProxy "<Webproxy URL>"
```

構文およびパラメーターの詳細については、「[Set-ExchangeServer](https://technet.microsoft.com/ja-jp/library/bb123716\(v=exchg.150\))」を参照してください。

## このステップの検証方法

Web プロキシ URL が正常に構成されたことを確認するには、次のシェル コマンドを実行し、*InternetWebProxy* パラメーターを確認します。

```powershell
Get-ExchangeServer | format-list
```

## 手順 2: シェルを使用して、仮想ディレクトリの公開を有効にします。


> [!NOTE]
> EAC を使用して、仮想ディレクトリの公開を有効にすることはできません。



この例では、クライアント アクセス サーバー CAS01 の仮想ディレクトリの公開を有効にします。

    Set-OwaVirtualDirectory -Identity "CAS01\owa (Default Web Site)" -ExternalUrl "<URL for CAS01>" -CalendarEnabled $true

ID `CAS01\owa (Default Web Site)` は、サーバー名と Outlook Web App 仮想ディレクトリになります。

構文およびパラメーターの詳細については、「[Set-OwaVirtualDirectory](https://technet.microsoft.com/ja-jp/library/bb123515\(v=exchg.150\))」を参照してください。

## このステップの検証方法

仮想ディレクトリの公開が正常に有効化されたことを確認するには、次のシェル コマンドを実行し、*ExternalURL* パラメーターを確認します。

```powershell
Get-OwaVirtualDirectory | format-list
```

## 手順 3: インターネット予定表の公開のための共有ポリシーを作成または構成する


> [!NOTE]
> 次に示す手順 3 のオプションは、Exchange Online 環境にのみ適用されます。



インターネット予定表の公開用に共有ポリシーを作成する (オプション 1) か、インターネット予定表の公開用に既定の共有ポリシーを構成する (オプション 2) か、いずれかを選択できます。どちらのオプションでも、EAC とシェルのどちらを使用するか選択できます。

## オプション 1:インターネット予定表の公開用に共有ポリシーを作成する

インターネット予定表の公開のための共有ポリシーを作成するには、次の手順を完了します。

## EAC を使用する

1.  <strong>組織</strong> \> <strong>共有</strong> に移動します。

2.  リスト ビューの <strong>個別共有</strong> で、<strong>新規作成</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

3.  <strong>共有ポリシー</strong> で、<strong>ポリシー名</strong> フィールドに共有ポリシーのフレンドリ名を入力します (たとえば、**Internet** など)。

4.  <strong>追加</strong> ![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックして、共有ポリシーの共有ルールを定義します。

5.  <strong>共有ルール</strong> で <strong>特定のドメインと共有</strong> をクリックし、対応するボックスに **Anonymous** を入力します。

6.  共有ポリシーに対して強制する予定表の共有レベルを指定するには、<strong>予定表フォルダーを共有する</strong> チェック ボックスをオンにし、次のいずれかを選択します。
    
      - <strong>時刻のみを指定して予定表の空き時間情報にアクセス</strong>
    
      - <strong>時間、件名、場所を含む予定表の空き時間情報</strong>
    
      - <strong>時刻、件名、場所、役職などの予定表のすべての予定情報</strong>

7.  共有ポリシーのルールを設定するには、<strong>\[保存\]</strong>をクリックします。

8.  <strong>共有ポリシー</strong> で、<strong>保存</strong> をクリックしてポリシーを作成します。

## シェルを使用する

この例では、Internet という名前のインターネット予定表の公開の共有ポリシーを作成し、空き時間情報のみを共有するようにポリシーを構成します。このポリシーは有効になっています。

    New-SharingPolicy -Name "Internet" -Domains 'Anonymous: CalendarSharingFreeBusySimple' -Enabled $true

この例では、共有ポリシー Internet をユーザーのメールボックスに追加します。

```powershell
Set-Mailbox -Identity <user name> -SharingPolicy "Internet"
```

この例では、共有ポリシー Internet を組織単位 (OU) に追加します。

```powershell
Set-Mailbox -OrganizationalUnit <OU name> -SharingPolicy "Internet"
```

構文およびパラメーターの詳細については、「[New-SharingPolicy](https://technet.microsoft.com/ja-jp/library/dd298186\(v=exchg.150\))」と「[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))」を参照してください。

## このステップの検証方法

共有ポリシーが正常に作成されたことを確認するには、次のシェル コマンドを実行して共有ポリシーの情報を確認します。

```powershell
Get-SharingPolicy <policy name> | format-list
```

## オプション 2:インターネット予定表の公開用に既定の共有ポリシーを構成する

インターネット予定表の公開のための既定の共有ポリシーを構成するには、次の手順を完了します。

## EAC を使用する

1.  <strong>組織</strong> \> <strong>共有</strong> に移動します。

2.  リスト ビューの <strong>個別共有</strong> で \[既定の共有ポリシー\] を選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>共有ポリシー</strong> で <strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックして、共有ポリシーをポリシーに追加します。

4.  <strong>共有ルール</strong> で <strong>特定のドメインと共有</strong> をクリックし、対応するボックスに **Anonymous** を入力します。

5.  共有ポリシーに対して強制する予定表の共有レベルを指定するには、<strong>予定表フォルダーを共有する</strong> チェック ボックスをオンにし、次のいずれかを選択します。
    
      - <strong>時刻のみを指定して予定表の空き時間情報にアクセス</strong>
    
      - <strong>時間、件名、場所を含む予定表の空き時間情報</strong>
    
      - <strong>時刻、件名、場所、役職などの予定表のすべての予定情報</strong>

6.  共有ポリシーのルールを設定するには、<strong>\[保存\]</strong>をクリックします。

7.  <strong>共有ポリシー</strong> で、<strong>保存</strong> をクリックして変更を保存します。

## シェルを使用する

この例では、\[既定の共有ポリシー\] を更新し、空き時間情報のみを共有するようにポリシーを構成します。このポリシーは有効になっています。

    Set-SharingPolicy -Name "Default Sharing Policy" -Domains 'Anonymous: CalendarSharingFreeBusySimple' -Enabled $true

構文およびパラメーターの詳細については、「[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))」を参照してください。

## このステップの検証方法

\[既定の共有ポリシー\] が正常に更新されたことを確認するには、次のシェル コマンドを実行して共有ポリシーの情報を確認します。

```powershell
Get-SharingPolicy <policy name> | format-list
```

