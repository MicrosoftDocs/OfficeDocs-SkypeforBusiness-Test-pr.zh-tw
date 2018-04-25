---
title: Set-CsLisServiceProvider
TOCTitle: Set-CsLisServiceProvider
ms:assetid: 3fe2878c-6ad2-4b7f-a844-e978c263163f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425911(v=OCS.15)
ms:contentKeyID: 49290707
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsLisServiceProvider

 

_**上次修改主題的時間：** 2015-03-09_

建立或修改增強型 9-1-1 (E9-1-1) 網路路由提供者所提供用於驗證位置之 Web 服務的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsLisServiceProvider -CertFileName <String> -Password <SecureString> -ServiceProviderName <String> -ValidationServiceUrl <String> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

用於建立 E9-1-1 網路路由提供者 Web 服務項目的其中一個必要參數為包含存取憑證檔所需之密碼的安全字串。因此，此範例中的第一行是呼叫 **Read-Host** Cmdlet。**Read-Host** Cmdlet 會提示使用者進行輸入。我們指定的參數 AsSecureString 會將輸入顯示為星號 (\*)。我們已將此命令的結果指派給變數 $p。結果會是一個安全字串，此字串為使用者輸入的加密版本。換句話說，執行此命令會提示您輸入 Web 服務的密碼，並將該密碼以變數 $p 儲存。

既然有了密碼，我們就可以建立會存取 Web 服務的物件。作法是呼叫 **Set-CsLisServiceProvider** Cmdlet。我們會將數個參數傳遞到此 Cmdlet。第一個是提供者的名稱，在此範例中為 E911Provider。下一個提供的是 ValidationServiceUrl 的值，也就是 https://www.911contoso.com/validation/。請注意，這必須是「安全的網站」，其首碼為 https 而非 http。接下來，我們輸入包含用於安全地存取此 Web 服務之憑證的檔案名稱，亦即 C:\\MS-Contoso-Cert.pfx。最後，我們將變數 $p (包含具有 Web 服務密碼的安全字串) 傳遞到 Password 參數。

    $p = Read-Host -AsSecureString
    Set-CsLisServiceProvider -ServiceProviderName E911Provider -ValidationServiceUrl https://www.911contoso.com/validation/ -CertFileName C:\MS-Contoso-Cert.pfx -Password $p

## 詳細描述

在啟用 E9-1-1 的 Enterprise Voice 實作中，系統必須先透過 E9-1-1 網路路由提供者來路由傳送緊急通話，以確保將通話路由傳送至合適的公眾安全回應點 (PSAP) (PSAP 是在美國的一個機構，這個機構會將來電導向至最近的緊急服務，例如警察、消防以及救護車服務)。為了完成這項作業，提供者必須先取得組織周圍的位置清單，然後再比對位置清單和主要街道地址指南中的內容，以確保所有位置的有效性。此 Cmdlet 會建立或修改關於提供者的資訊，包括提供者的名稱、組織將用於傳送位置之 Web 服務的 URL，以及安全 Web 服務的憑證和密碼。

您無法為指定的 E9-1-1 實作定義一個以上的服務提供者。除非此 Cmdlet 可以解析 Web 服務的 URL 和安全性資訊，否則將無法成功。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsLisServiceProvider** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsLisServiceProvider"}

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
<td><p><em>CertFileName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>憑證檔的名稱 (和完整路徑)。此檔案的副檔名必須是 PFX。</p></td>
</tr>
<tr class="even">
<td><p><em>Password</em></p></td>
<td><p>必要</p></td>
<td><p>System.Security.SecureString</p></td>
<td><p>在受密碼保護的檔案中包含存取憑證所需之密碼的安全字串。使用 <strong>ConvertTo-SecureString</strong> Cmdlet 或 <strong>Read-Host</strong>  Cmdlet 搭配 AsSecureString 參數，可以建立安全字串。</p></td>
</tr>
<tr class="odd">
<td><p><em>ServiceProviderName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>E9-1-1 網路路由提供者的名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>ValidationServiceUrl</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>Web 服務的 URL。這必須是安全 URL，其首碼為 https://。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

接受管線傳送之位置資訊伺服器 (LIS) 服務提供者物件的輸入。

## 傳回類型

此 Cmdlet 會建立或修改 System.Management.Automation.PSCustomObject 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsLisServiceProvider](remove-cslisserviceprovider.md)  
[Get-CsLisServiceProvider](get-cslisserviceprovider.md)

