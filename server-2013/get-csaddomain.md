---
title: Get-CsAdDomain
TOCTitle: Get-CsAdDomain
ms:assetid: 64554035-3ba5-4aa7-b5d3-91277f107275
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398453(v=OCS.15)
ms:contentKeyID: 49291130
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAdDomain

 

_**上次修改主題的時間：** 2015-03-09_

傳回指出 Active Directory 網域服務設定是否正確的資訊，以便於安裝 Lync Server。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsAdDomain [-Domain <Fqdn>] [-DomainController <Fqdn>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>]

## 範例

## 範例 1

範例1 會傳回與本機 Active Directory 網域之目前狀態相關的資訊。如果您的網域設定是最新的，且網域已準備好裝載 Lync Server，則會傳回 LC\_DOMAIN\_SETTINGS\_STATE\_READY 值。

    Get-CsAdDomain

## 範例 2

範例 2 的命令會傳回特定網域的目前狀態：fabrikam.com。在多網域環境中，您可以藉由包含 Domain 參數來傳回指定網域的資訊。

    Get-CsAdDomain -Domain "fabrikam.com" 

## 範例 3

範例 3 會擷取您 Active Directory 網域的目前狀態，同時還會將狀態的資訊寫入名為 C:\\Logs\\DomainReport.html 的檔案中。這個檔案會詳列 **Get-CsAdDomain** Cmdlet 採取了哪些步驟來判定網域的準備狀態。這些步驟包括驗證 Active Directory 群組是否存在，以及檢查各種 Active Directory 容器權限設定等工作。

    Get-CsAdDomain -Report "C:\Logs\DomainReport.html"

## 詳細描述

在安裝 Lync Server 前，您必須先將網域準備好，包括擴充 Active Directory 架構以允許新增 Lync Server 特定的屬性，以及將所需的存取控制項目指派給用於管理與操作 Lync Server 的萬用群組。 **Get-CsAdDomain** Cmdlet 會傳回單一值，告訴您是否可在網域上安裝 Lync Server。如果 **Get-CsAdDomain** Cmdlet 傳回 LC\_DOMAINSETTINGS\_STATE\_READY 值，表示您可以將 Lync Server 安裝在該網域。如果 Cmdlet 傳回 LC\_DOMAINSETTINGS\_STATE\_NOT\_READY，則您必須先將網域正確地準備好，再嘗試安裝 Lync Server。

**Get-CsAdDomain** Cmdlet 會隨著安裝精靈執行。如果精靈判定網域未正確地準備好，會顯示錯誤訊息並停止安裝。但在嘗試安裝 Lync Server 之前，您可以在安裝精靈之外單獨執行 **Get-CsAdDomain** Cmdlet，以確認網域的狀態。

**Get-CsAdDomain** Cmdlet 執行的功能與下列 Microsoft Office Communications Server 2007 R2 命令相同：

Lcscmd.exe /domain /action:CheckDomainPrepState

誰可以執行這個 Cmdlet：根據預設，任何擁有 Active Directory 之讀取權限的使用者均可執行 **Get-CsAdDomain** Cmdlet。一般來說，所有網域成員均擁有此權限。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAdDomain"}

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
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>要檢查之網域的完整網域名稱 (FQDN)，例如：-Domain &quot;litwareinc.com&quot;。若未指定此參數，則會檢查本端網域。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>讓系統管理員指定執行 <strong>Get-CsAdDomain</strong> Cmdlet 時所使用之網域控制站的 FQDN。若未指定，該 Cmdlet 會使用第一個可用的網域控制站。</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>網域中通用類別目錄伺服器的 FQDN。如果是在電腦上以您網域中的帳戶執行 <strong>Get-CsAdDomain</strong> Cmdlet，則不需要此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>儲存全域設定之網域控制站的 FQDN。如果全域設定是儲存在 Active Directory 的系統容器內，則此參數必須導向根網域控制器。如果全域設定儲存在組態容器中，則會使用任何一個網域控制站，且會省略此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\DomainPrep.html&quot;</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsAdDomain** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsAdDomain** Cmdlet 會傳回 Microsoft.Rtc.Management.Deployment.LcDomainSettingsState 物件的執行個體。

## 請參閱

#### 其他資源

[Disable-CsAdDomain](disable-csaddomain.md)  
[Enable-CsAdDomain](enable-csaddomain.md)

