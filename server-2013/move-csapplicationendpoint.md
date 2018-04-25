---
title: Move-CsApplicationEndpoint
TOCTitle: Move-CsApplicationEndpoint
ms:assetid: 0f5a5b7a-aca5-4672-b712-d47683e28caf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398188(v=OCS.15)
ms:contentKeyID: 49290108
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Move-CsApplicationEndpoint

 

_**上次修改主題的時間：** 2015-03-09_

將端點移至不同的登錄器集區。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Move-CsApplicationEndpoint -Identity <UserIdParameter> -TargetApplicationPool <Fqdn> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-IgnoreBackendStoreException <SwitchParameter>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例將 SIP 位址為 endpoint1@litwareinc.com 的應用程式端點連絡人物件移至信任的登錄器集區 TrustPoolA.litwareinc.com。共存之後，使用此命令將 UCMA 2.0 應用程式升級至 Lync Server 應用程式。

    Move-CsApplicationEndpoint -Identity sip:endpoint1@litwareinc.com -TargetApplicationPool TrustPoolA.litwareinc.com

## 範例 2

此範例將 SIP 位址為 endpoint2@litwareinc.com 的應用程式端點連絡人物件移至信任的登錄器集區 TrustPoolA.litwareinc.com。此範例不同於範例 1，因為此命令包含 Force 參數。使用此命令以就地移轉 UCMA 2.0 應用程式，或針對單純的 Lync Server 部署來直接部署 UCMA 2.0 應用程式。這樣會以必要屬性更新 Active Directory 中現有的物件，以透過 Lync Server 登錄器進行路由。

    Move-CsApplicationEndpoint -Identity sip:endpoint2@litwareinc.com -TargetApplicationPool TrustPoolA.litwareinc.com -Force

## 詳細描述

此 Cmdlet 會將 Active Directory 網域服務中現有端點連絡人物件從 Microsoft Office Communications Server 2007 R2 應用程式集區移至 Lync Server 應用程式集區，或從某個 Lync Server 應用程式集區移至另一個應用程式集區。與指定端點相關聯的應用程式必須存在目標集區上。若要判斷與端點相關聯的應用程式，請執行 **Get-CsTrustedApplicationEndpoint** Cmdlet 或 **Get-CsDialInConferencingAccessNumber** Cmdlet。

當針對 Office Communications Server 2007 R2 部署的應用程式以 Lync Server 重定目標時，此 Cmdlet 也用來升級 Active Directory 連絡人物件屬性。請注意，在此情況下，來源和目標應用程式集區相同。另外，如果原本設計以 Office Communications Server 2007 R2 為對象的應用程式直接針對 Lync Server 部署，則此 Cmdlet 必須搭配 Force 旗標，才能升級 Active Directory 連絡人物件內容。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Move-CsApplicationEndpoint** Cmdlet：RTCUniversalUserAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Move-CsApplicationEndpoint"}

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
<td><p>您要移動之端點連絡人的 SIP 位址或辨別名稱 (DN)。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetApplicationPool</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>正在向其移動端點之集區的完整網域名稱 (FQDN)。目標集區必須具有登錄器服務相依性。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓您指定網域控制站。若未指定網域控制站，則會使用第一個可用的網域控制站。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如果您將 Microsoft Unified Communications Managed API (UCMA) 2.0 連絡人物件移至相同集區，但在 Lync Server 部署上，則此為必要旗標。這樣會強制透過 Lync Server 登錄器進行路由。</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreBackendStoreException</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，會指示電腦忽略後端資料庫可能發生的任何錯誤，並嘗試移動應用程式端點，而不管那些錯誤。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指定此參數會在物件移動後，傳回應用程式端點物件。</p></td>
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

字串。接受管線傳送的字串值，代表應用程式端點的 Identity。

## 傳回類型

搭配 PassThru 參數使用時，傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSADApplicationContact 類型的物件。

## 請參閱

#### 其他資源

[Get-CsApplicationEndpoint](get-csapplicationendpoint.md)

