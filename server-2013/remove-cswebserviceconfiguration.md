---
title: Remove-CsWebServiceConfiguration
TOCTitle: Remove-CsWebServiceConfiguration
ms:assetid: 1df2f881-6594-4de7-9762-8d64b2243355
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398266(v=OCS.15)
ms:contentKeyID: 49290277
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsWebServiceConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除一或多個 Web 服務組態設定的集合。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsWebServiceConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會移除 Redmond 網站的 Web 服務組態設定。

    Remove-CsWebServiceConfiguration -Identity site:Redmond

## 範例 2

在範例 2 中會移除在網站範圍設定的所有 Web 服務設定。為了執行此工作，命令會先呼叫 **Get-CsWebServiceConfiguration** Cmdlet 搭配 Filter 參數；篩選值 "site:\*" 可確保只會傳回 Identity 開頭為字元為 "site:" 的設定。然後將篩選後的集合管線傳送到 **Remove-CsWebServiceConfiguration** Cmdlet，以刪除集合中的每個項目。

    Get-CsWebServiceConfiguration -Filter "site:*" | Remove-CsWebServiceConfiguration

## 範例 3

範例 3 所示的命令會刪除所有已停用群組擴充的 Web 服務組態設定。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsWebServiceConfiguration** Cmdlet，以傳回組織中使用之所有 Web 服務組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 EnableGroupExpansion 屬性等於 False 的設定。接著將篩選後的集合管線傳送到 **Remove-CsWebServiceConfiguration** Cmdlet，以刪除集合中的每個項目。

    Get-CsWebServiceConfiguration | Where-Object {$_.EnableGroupExpansion -eq $False} | Remove-CsWebServiceConfiguration

## 詳細描述

許多 Lync Server 元件為 Web 元件：這些元件使用 Web 服務或網頁來執行工作。例如，使用者利用 Web 服務搜尋通訊錄的新連絡人，或使用群組擴充來檢視通訊群組的個別成員。同樣地，從電話撥入式會議到 Lync Server 控制台等元件都是使用網頁做為 Lync Server 和使用者之間的介面。

**CsWebServiceConfiguration** Cmdlet 可讓系統管理員管理整個組織的 Web 服務 組態設定。其中包括管理群組擴充、憑證設定以及允許的驗證方法。因為您可以在全域、網站和服務範圍 (僅限 Web Services 服務) 設定不同設定，您可以針對不同使用者和不同位置來自訂 Web 服務功能。

如果您在網站或服務範圍建立自訂 Web 服務組態設定，稍後可以使用 **Remove-CsWebServiceConfiguration** Cmdlet 來移除這些設定。請注意，您也可以對 Web 服務設定的全域集合執行 **Remove-CsWebServiceConfiguration** Cmdlet。但是，在該情況下將不會移除全域集合；那是因為 Lync Server 不允許您移除全域設定，而是將全域集合中的所有屬性還原為其預設值。例如，假設您已將 MaxGroupSizeToExpand 值變更為 500。因為此屬性的預設值為 100，因此，「移除」全域集合會將 MaxGroupSizeToExpand 屬性的值重設為 100。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsWebServiceConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsWebServiceConfiguration"}

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
<td><p>要移除之 Web 服務 組態設定的唯一識別碼。若要移除在網站範圍設定的設定，請使用類似下列的語法：-Identity &quot;site:Redmond&quot;。若要移除在服務範圍設定的設定，請使用類似下列的語法：-Identity &quot;service:WebServer:atl-cs-001.litwareinc.com&quot;。</p>
<p>也可以針對全域集合執行 <strong>Remove-CsWebServiceConfiguration</strong> Cmdlet。不過，在該情況下將不會移除全域集合；而是將該集合中的所有屬性重設為預設值。若要重設全域集合，請使用下列語法：-Identity global。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Web.WebServiceSettings 物件。 **Remove-CsWebServiceConfiguration** Cmdlet 接受管線傳送的 Web 服務設定物件輸入。

## 傳回類型

無。反之， **Remove-CsWebServiceConfiguration** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Settings.Web.WebServiceSettings 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsWebServiceConfiguration](get-cswebserviceconfiguration.md)  
[New-CsWebServiceConfiguration](new-cswebserviceconfiguration.md)  
[Set-CsWebServiceConfiguration](set-cswebserviceconfiguration.md)

