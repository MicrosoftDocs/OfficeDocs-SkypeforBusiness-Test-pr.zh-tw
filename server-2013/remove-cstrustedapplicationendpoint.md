---
title: Remove-CsTrustedApplicationEndpoint
TOCTitle: Remove-CsTrustedApplicationEndpoint
ms:assetid: c9b96690-d8c2-47f7-bff3-706dbf68d75a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398837(v=OCS.15)
ms:contentKeyID: 49292298
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsTrustedApplicationEndpoint

 

_**上次修改主題的時間：** 2015-03-09_

移除信任的應用程式端點。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsTrustedApplicationEndpoint -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會移除 Identity (在此案例中為顯示名稱) 為 Endpoint 1 的端點連絡人。由於 Identity 必須是唯一的，因此這個命令最多只會移除一個端點。

    Remove-CsTrustedApplicationEndpoint -Identity "Endpoint 1"

## 範例 2

此範例會移除所有和應用程式 tapp2 相關聯之信任的應用程式端點。為了完成此工作，可先呼叫 **Get-CsTrustedApplicationEndpoint** Cmdlet，接著將識別碼 tapp2 傳遞到 ApplicationId 參數。如此將傳回和 tapp2 信任的應用程式相關聯的端點集合。然後，此集合會管線傳送到 **Remove-CsTrustedApplicationEndpoint** Cmdlet，以移除集合中的每一個端點。請記住，這個對 **Get-CsTrustedApplicationEndpoint** Cmdlet 的呼叫會從多重集區擷取應用程式識別碼為 tapp2 的端點，以產生此命令，來從多重集區移除信任的應用程式端點。

    Get-CsTrustedApplicationEndpoint -ApplicationId tapp2 | Remove-CsTrustedApplicationEndpoint

## 詳細描述

信任的應用程式端點是 Active Directory 連絡人物件，可讓呼叫路由傳送至信任的應用程式。此 Cmdlet 移除 Active Directory 網域服務 中現有的端點連絡人物件。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsTrustedApplicationEndpoint** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsTrustedApplicationEndpoint"}

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
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>要移除之應用程式端點的 Identity (連絡人的辨別名稱)、SIP 位址或顯示名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.ADConnect.Schema.OCSADApplicationContact 物件。接受管線傳送的受信任應用程式端點物件輸入。

## 傳回類型

此 Cmdlet 不會傳回值，而會移除 Microsoft.Rtc.Management.ADConnect.Schema.OCSADApplicationContact 類型的物件。

## 請參閱

#### 其他資源

[New-CsTrustedApplicationEndpoint](new-cstrustedapplicationendpoint.md)  
[Set-CsTrustedApplicationEndpoint](set-cstrustedapplicationendpoint.md)  
[Get-CsTrustedApplicationEndpoint](get-cstrustedapplicationendpoint.md)

