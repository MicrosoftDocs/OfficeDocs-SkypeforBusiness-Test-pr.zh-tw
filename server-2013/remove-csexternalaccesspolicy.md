---
title: Remove-CsExternalAccessPolicy
TOCTitle: Remove-CsExternalAccessPolicy
ms:assetid: eae27b8f-0c25-4723-95e9-435e36f06a79
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399057(v=OCS.15)
ms:contentKeyID: 49292704
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsExternalAccessPolicy

 

_**上次修改主題的時間：** 2015-03-09_

可讓您移除現有的外部存取原則。外部存取原則可指定使用者是否可以：1) 和同盟組織中用工作階段初始通訊協定 (SIP) 帳戶的使用者通訊；2) 與具有公用即時訊息 (IM) 供應商 (如 MSN) SIP 帳戶的使用者通訊；以及 3) 直接從網際網路存取 Lync Server，而無須登入內部網路。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsExternalAccessPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

於範例 1 中，Identity 為 site:Redmond 的外部存取原則會遭到刪除。在移除原則後，Redmond 網站中的使用者會使用全域原則來控制外部存取權限。

    Remove-CsExternalAccessPolicy -Identity site:Redmond

## 範例 2

範例 2 會刪除在網站範圍設定的所有外部存取原則。為了執行此工作，命令會先使用 **Get-CsExternalAccessPolicy** Cmdlet 搭配 Filter 參數，以傳回在網站範圍設定的原則集合；篩選值 "site:\*" 可將傳回的資料限制在 Identity 開頭為字串值 "site:" 的外部存取原則。然後再將篩選後的集合以管線傳送到 **Remove-CsExternalAccessPolicy** Cmdlet，以刪除集合中的每一個原則。

    Get-CsExternalAccessPolicy -Filter site:* | Remove-CsExternalAccessPolicy 

## 範例 3

於範例 3 中，會刪除允許同盟存取的所有外部存取原則。為達成此目的，命令會先呼叫 **Get-CsExternalAccessPolicy** Cmdlet 以傳回設定供組織使用之所有外部存取原則的集合。然後，此集合會以管線傳送到 **Where-Object** Cmdlet，這只會挑出 EnableFederationAcces 屬性等於 True 的原則。接著將篩選後的集合以管線傳送到 **Remove-CsExternalAccessPolicy** Cmdlet，以刪除集合中的每一個原則。

    Get-CsExternalAccessPolicy | Where-Object {$_.EnableFederationAccess -eq $True} | Remove-CsExternalAccessPolicy 

## 範例 4

範例 4 會刪除至少符合這兩項準則中其中一項的所有外部存取原則：允許同盟存取、允許公用 Cloud 存取，或兩者皆允許。為了執行此工作，命令會先使用 **Get-CsExternalAccessPolicy** Cmdlet，以傳回設定供組織使用之所有外部存取原則的集合。然後，此集合會以管線傳送到 **Where-Object** Cmdlet，這樣只會選取符合下列準則的原則：EnableFederationAccess 等於 True，和/或 EnablePublicCloudAccess 等於 True。接著將符合這些準則其中一項 (或兩者) 的原則以管線傳送到 **Remove-CsExternalAccessPolicy** Cmdlet 加以移除。

若要在呼叫 **Where-Object** Cmdlet 時刪除 EnableFederationAccess 與 EnablePublicCloudAccess 皆為 True 的所有原則：

Where-Object {$\_.EnableFederationAccess -eq $True -and $\_.EnablePublicCloudAccess -eq $True}

    Get-CsExternalAccessPolicy | Where-Object {$_.EnableFederationAccess -eq $True -or $_.EnablePublicCloudAccess -eq $True} | Remove-CsExternalAccessPolicy 

## 詳細描述

安裝 Lync Server 時，只允許使用者彼此交換立即訊息和目前狀態資訊：根據預設，他們只能與 Active Directory 網域服務 中具有 SIP 帳戶的其他人員通訊。此外，不允許使用者透過網際網路存取 Lync Server；他們必須先登入您的內部網路，才可以登入 Lync Server。

1\. 這可能足以符合您的通訊需求。如果不符合您的需求，您可以使用外部存取原則，擴充使用者通訊和共同作業的能力。外部存取原則可以授與 (或撤銷) 使用者執行下列任何或全部作業的能力：

2\. 與具有含同盟組織 SIP 帳戶的人員通訊。請注意，單獨啟用同盟將不提供使用者這項功能。而是您必須啟用同盟，然後指派使用者外部存取原則，給予他們與同盟使用者通訊的權限。

3\. 透過公用立即訊息服務 (例如 Windows Live) 與具有 SIP 帳戶的人員通訊。

透過網際網路存取 Lync Server，而不必先登入您的內部網路。這讓使用者可以使用 Lync，並從網路咖啡廳或其他遠端位置登入 Lync Server。

當您安裝 Lync Server 時，系統會自動為您建立全域外部存取原則。除了全域原則外，您可以使用 **New-CsExternalAccessPolicy** Cmdlet 建立在網站範圍或個別使用者範圍所設定的外部存取原則。

**Remove-CsExternalAccessPolicy** Cmdlet 可讓您刪除任何使用 **New-CsExternalAccessPolicy** Cmdlet 建立的原則；這表示您可以刪除指派給網站範圍或個別使用者範圍的任何原則。您也可以對全域外部存取原則執行 **Remove-CsExternalAccessPolicy** Cmdlet。但在該狀況下，將無法刪除全域原則；根據設計，全域原則無法刪除。而只會將全域原則的屬性重設為其預設值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsExternalAccessPolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsExternalAccessPolicy"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要移除之外部存取原則的唯一識別碼。您可以在全域、網站或個別使用者範圍內設定外部存取原則。若要「移除」全域原則，請使用這個語法：-Identity global。(請注意，無法實際移除全域原則。而是將全域原則中的所有屬性重設為其預設值)。若要移除網站原則，請使用類似下列的語法：-Identity site:Redmond。若要移除個別使用者原則，請使用類似下列的語法：-Identity SalesAccessPolicy。</p>
<p>請注意，指定 Identity 時不得使用萬用字元。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.ExternalAccess.ExternalAccessPolicy 物件。**Remove-CsExternalAccessPolicy** Cmdlet 會接受外部存取原則物件以管線傳送的資料。

## 傳回類型

無。 **Remove-CsExternalAccessPolicy** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Policy.ExternalAccess.ExternalAccessPolicy 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsExternalAccessPolicy](get-csexternalaccesspolicy.md)  
[Grant-CsExternalAccessPolicy](grant-csexternalaccesspolicy.md)  
[New-CsExternalAccessPolicy](new-csexternalaccesspolicy.md)  
[Set-CsExternalAccessPolicy](set-csexternalaccesspolicy.md)

