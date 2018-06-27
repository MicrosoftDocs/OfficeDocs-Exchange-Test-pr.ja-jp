---
title: '管理者監査ログの構造: Exchange 2013 Help'
TOCTitle: 管理者監査ログの構造
ms:assetid: 87e259c9-c884-4d53-bd78-d13f2300d73e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff459251(v=EXCHG.150)
ms:contentKeyID: 50555824
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理者監査ログの構造

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-03-09_

管理者監査ログには、Exchange 管理シェルおよび Exchange 管理センター (EAC) で実行されたコマンドレットおよびパラメーターがすべて記録されます。管理者監査ログは、EAC で管理者監査ログ レポートを実行したとき、またはシェルで **New-AdminAuditLogSearch** コマンドレットを実行したときに、オンデマンドで作成されます。監査ログの詳細については、「[管理者監査ログ](administrator-audit-logging-exchange-2013-help.md)」を参照してください。

監査ログは XML ファイルで、監査ログには複数の監査ログ エントリを含むことができます。次の表に、各 XML タグおよび関連付けられている属性ついての説明を示します。

管理者監査ログに関連する管理タスクについては、「[管理者監査ログの管理](manage-administrator-audit-logging-exchange-2013-help.md)」を参照してください。

### 監査ログ XML タグと属性

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
<th>属性</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;</code></p>
<p></p></td>
<td><p><code>N/A</code></p></td>
<td><p>これは、XML ドキュメントの宣言タグです。この宣言タグはすべての監査ログ XML ファイルに含まれており、この宣言タグには XML バージョン番号と文字のエンコード値が含まれます。</p></td>
</tr>
<tr class="even">
<td><p><code>SearchResults</code></p></td>
<td><p><code>N/A</code></p></td>
<td><p>このタグには、XML ファイル内のすべての監査ログ エントリが含まれています。<code>Event</code> タグは、このタグの子です。</p>
<p>XML ファイルごとに <code>SearchResults</code> タグが 1 つのみあります。</p></td>
</tr>
<tr class="odd">
<td><p><code>Event</code></p></td>
<td><p><code> </code></p></td>
<td><p>このタグには、各コマンドレッドの監査ログ エントリが含まれます。このタグには、<code>Caller</code>、<code>Cmdlet</code>、<code>ObjectModified</code>、<code>RunDate</code>、<code>Succeeded</code>、<code>Error</code>、および <code>OriginatingServer</code> の属性が含まれます。<code>CmdletParameters</code> と <code>ModifiedProperties</code> タグは、このタグの子です。</p>
<p>各監査ログ エントリごとに <code>Event</code> タグが 1 つあります。</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>Caller</code></p></td>
<td><p>この属性には、<code>Cmdlet</code> 属性内のコマンドレットを実行したユーザーのユーザー アカウントが含まれます。</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>Cmdlet</code></p></td>
<td><p>この属性には、<code>Caller</code> 属性内のユーザーによって実行されたコマンドレットの名前が含まれます。</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>ObjectModified</code></p></td>
<td><p>この属性には、<code>Cmdlet</code> 属性で指定したコマンドレットによって変更されたオブジェクトが含まれます。<code>ModifiedProperties</code> タグは、このオブジェクトで変更されたプロパティを示します。</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>RunDate</code></p></td>
<td><p>この属性には、<code>Cmdlet</code> 属性内のコマンドレットが実行された日時が含まれます。</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>Succeeded</code></p></td>
<td><p>この属性は、<code>Cmdlet</code> 属性内のコマンドレットが正常に実行されたかどうかを示します。値は、<code>True</code> または <code>False</code> のどちらかです。</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>Error</code></p></td>
<td><p>この属性には、<code>Cmdlet</code> 属性内のコマンドレットが正常に完了できなかった場合に生成されるエラー メッセージが含まれます。エラーが発生しなかった場合、値は <code>None</code> に設定されます。</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>OriginatingServer</code></p></td>
<td><p>この属性には、<code>Cmdlet</code> 属性内で指定されたコマンドレットが実行されたサーバーが含まれます。</p></td>
</tr>
<tr class="odd">
<td><p><code>CmdletParameters</code></p></td>
<td><p><code>N/A</code></p></td>
<td><p>このタグには、コマンドレットが実行されたときに指定されるすべてのパラメーターが含まれます。<code>Parameter</code> タグは、このタグの子です。</p>
<p><code>Event</code> タグごとに <code>CmdletParameters</code> タグが 1 つあります。</p></td>
</tr>
<tr class="even">
<td><p><code>Parameter</code></p></td>
<td><p><code> </code></p></td>
<td><p>このタグには、コマンドレットが実行されたときに指定された各パラメーターが含まれます。このタグには、<code>Name</code> および <code>Value</code> 属性が含まれます</p>
<p><code>CmdletParameters</code> タグごとに、<code>Parameter</code> タグを複数含めることができます。</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>Name</code></p></td>
<td><p>この属性には、実行されたコマンドレットで指定されたパラメーターの名前が含まれます。</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>Value</code></p></td>
<td><p>この属性には、<code>Name</code> 属性で指定されたパラメーターに対して提供された値が含まれます。</p></td>
</tr>
<tr class="odd">
<td><p><code>ModifiedProperties</code></p></td>
<td><p><code>N/A</code></p></td>
<td><p>このタグには、実行されたコマンドレットによって変更されたすべてのプロパティが含まれます。<code>Property</code> タグは、このタグの子です。</p>
<p><code>Event</code> タグごとに <code>ModifiedProperties</code> タグが 1 つあります。</p>

> [!IMPORTANT]
> このタグは、<STRONG>Set-AdminAuditLogConfig</STRONG> コマンドレットの <EM>LogLevel</EM> パラメーターが <CODE>Verbose</CODE> に設定されている場合にのみ指定されます。


</td>
</tr>
<tr class="even">
<td><p><code>Property</code></p></td>
<td><p><code> </code></p></td>
<td><p>このタグには、コマンドレットが実行されたときに指定された各プロパティが含まれます。このタグには、<code>Name</code>、<code>OldValue</code>、および <code>NewValue</code> 属性が含まれます。</p>
<p><code>ModifiedProperties</code> タグごとに、<code>Property</code> タグを複数含めることができます。</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>Name</code></p></td>
<td><p>この属性には、コマンドレットが実行されたときに変更されたプロパティの名前が含まれます。</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>OldValue</code></p></td>
<td><p>この属性には、<code>Name</code> 属性で指定されたプロパティが変更される前に、このプロパティに含まれていた値が含まれます。</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>NewValue</code></p></td>
<td><p>この属性には、<code>Name</code> 属性のプロパティが変更された値が含まれます。</p></td>
</tr>
</tbody>
</table>


## 監査ログ エントリの例

以下に、一般的な監査ログ エントリの例を示します。マイクロソフトでは、ログ エントリ内の情報に基づいて以下が発生していることを認識しています。

  - 10/18/2012 3:48 P.M. 太平洋夏時間 (UTC-7) に、ユーザー `Administrator` が **Set-Mailbox** コマンドレットを実行しました。

  - **Set-Mailbox** コマンドレットを実行した際、次の 2 つのパラメーターが指定されていました。
    
      - *Identity* には、値 `david`
    
      - *ProhibitSendReceiveQuota* には、値 `10GB`

  - オブジェクト `david` に対する次の 2 つのプロパティが変更されました。
    

    > [!NOTE]
    > この例では、<CODE>Set-AdminAuditLogConfig</CODE> コマンドレットの <EM>LogLevel</EM> パラメーターが <CODE>Verbose</CODE> に設定されていたため、変更されたプロパティは監査ログに保存されます。

    
      - *ProhibitSendReceiveQuota* には新しい値 `10GB` が指定され、古い値 `35GB` と置き換えられました。

  - 操作は、エラーなしで正常に完了しました。

<!-- end list -->

    <?xml version="1.0" encoding="utf-8"?>
    <SearchResults>
    
      <Event Caller="corp.e15a.contoso.com/Users/Administrator" Cmdlet="Set-Mailbox" ObjectModified="corp.e15a.contoso.com/Users/david" RunDate="2012-10-18T15:48:15-07:00" Succeeded="true" Error="None" OriginatingServer="WIN8MBX (15.00.0516.032)">
        <CmdletParameters>
          <Parameter Name="Identity" Value="david" />
          <Parameter Name="ProhibitSendReceiveQuota" Value="10 GB (10,737,418,240 bytes)" />
        </CmdletParameters>
        <ModifiedProperties>
          <Property Name="ProhibitSendReceiveQuota" OldValue="35 GB (37,580,963,840 bytes)" NewValue="10 GB (10,737,418,240 bytes)" />
        </ModifiedProperties>
      </Event>
    </SearchResults>

