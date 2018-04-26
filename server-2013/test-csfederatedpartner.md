---
title: Test-CsFederatedPartner
TOCTitle: Test-CsFederatedPartner
ms:assetid: 1f56bf80-37b4-4520-b8a5-da0740a894a2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398281(v=OCS.15)
ms:contentKeyID: 49290297
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsFederatedPartner

 

_**上次修改主題的時間：** 2015-03-09_

驗證連線到同盟網域的能力。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsFederatedPartner -Domain <String> -TargetFqdn <String> [-Certificate <X509Certificate2>] [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-ProxyFqdn <String>]

## 範例

## 範例 1

範例 1 所示的命令會驗證本機存取 Proxy 伺服器 (accessproxy.litwareinc.com) 和同盟網域 Fabrikam.com 之間的連線。

    Test-CsFederatedPartner -TargetFqdn accessproxy.litwareinc.com -Domain fabrikam.com

## 範例 2

範例 2 顯示如何測試您的網域與 Lync Server 推播通知服務之間的連線。您必須已將此服務設定為主機供應商而且必須已將 push.lync.com 新增至您的允許網域清單，此測試才能成功。如需詳細資訊，請參閱[在 Lync Server 2013 中設定推播通知](lync-server-2013-configuring-for-push-notifications.md)。

    Test-CsFederatedPartner -TargetFqdn accessproxy.litwareinco.com -Domain push.lync.com -ProxyFqdn sipfed.online.lync.com

## 範例 3

在範例 3 中，會針對您允許網域清單中的所有網域驗證連線。為達此目的，命令會先使用 Get-CsAllowedDomain Cmdlet 擷取您的所有允許網域的集合。然後再將該集合管線傳送到 ForEach-Object Cmdlet。然後，ForEach-Object 會針對集合中的每個網域執行 Test-CsFederatedPartner Cmdlet。

    Get-CsAllowedDomain | ForEach-Object {Test-CsFederatedPartner -TargetFqdn accessproxy.litwareinc.com -Domain $_.Identity}

## 詳細描述

**Test-CsFederatedPartner** 會驗證您是否能夠連線到同盟協力廠商的網域。若要驗證網域的連線能力，該網域必須列在允許 (同盟) 網域的集合中。您可以使用 **New-CsAllowedDomain** Cmdlet 將網域新增至允許清單。

誰可以執行這個 Cmdlet：若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsFederatedPartner"}

## 參數


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>必要</th>
<th>類型</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Domain</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>同盟網域的完整網域名稱 (FQDN)。例如：-Domain &quot;fabrikam.com&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>組織用於同盟 SIP 流量的存取 Proxy 伺服器的 FQDN。TargetFqdn 必須指向同盟 SIP 流量流向的 Proxy 伺服器的內緣。</p></td>
</tr>
<tr class="odd">
<td><p><em>Certificate</em></p></td>
<td><p>選用</p></td>
<td><p>System.Security.Cryptography.X509Certificates.X509Certificate2</p></td>
<td><p>可讓您在連線至同盟網域時提供用於驗證的 X509 憑證。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。此變數包含兩個方法 (ToHTML 和 ToXML)，可用於將輸出儲存為 HTML 或 XML 檔案。</p>
<p>若要將輸出儲存在名為 $TestOutput 的記錄器變數中，請使用下列語法：</p>
<p>-OutLoggerVariable TestOutput</p>
<p>注意：指定變數名稱時，請勿在前面加上 $ 字元。若要將儲存在記錄器變數中的資訊儲存為 HTML 檔案，請使用類似下列的命令：</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>若要將儲存在記錄器變數中的資訊儲存為 XML 檔案，請使用類似下列的命令：</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="even">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。例如，您可使用下列語法，將輸出儲存於名為 $TestOutput 的變數中：</p>
<p>-OutVerboseVariable TestOutput</p>
<p>指定變數名稱時，請勿在前面加上 $ 字元。</p></td>
</tr>
<tr class="odd">
<td><p><em>ProxyFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>同盟組織使用的存取 Proxy 伺服器的 FQDN。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Test-CsFederatedPartner** 不接受管線傳送的輸入。

## 傳回類型

**Test-CsFederatedPartner** 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsAllowedDomain](get-csalloweddomain.md)

