---
title: Remove-CsClientVersionPolicy
TOCTitle: Remove-CsClientVersionPolicy
ms:assetid: 2fd9ca4c-8b4f-41f0-b051-5b486376008c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425801(v=OCS.15)
ms:contentKeyID: 49290483
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsClientVersionPolicy

 

_**上次修改主題的時間：** 2015-03-09_

移除指定的用戶端版本原則。用戶端版本原則可讓您指定可以登入您 Lync Server 系統的用戶端 (例如 Microsoft Office Communicator 2007 R2)。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsClientVersionPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會刪除 Redmond 網站的用戶端版本原則。

    Remove-CsClientVersionPolicy -Identity site:Redmond

## 範例 2

在範例 2 中，會刪除在個別使用者範圍設定的所有用戶端版本原則。為達成此目的，命令會先呼叫 **Get-CsClientVersionPolicy** Cmdlet 搭配 Filter 參數；篩選值 "tag:\*" 可將傳回的資料限制在個別使用者範圍所設定的原則。然後再將篩選後的集合管線傳送到 **Remove-CsClientVersionPolicy** Cmdlet，以刪除集合中的每個項目。

    Get-CsClientVersionPolicy -Filter tag:* | Remove-CsClientVersionPolicy

## 詳細描述

用戶端版本原則代表用戶端版本規則的集合；而用戶端版本規則用於決定允許登入 Lync Server 的用戶端應用程式。當使用者嘗試登入 Lync Server 時，該使用者的用戶端應用程式會傳送 SIP 標頭給伺服器，這個標頭包含與應用程式本身有關的詳細資訊，包括軟體的主要版本和組建編號。然後系統會根據用戶端版本規則的集合，檢查 SIP 標頭所含的版本資訊，查看是否有任何規則要套用至該特定應用程式。如果有這樣的規則，Lync Server 就會採取此規則指定的行動。例如，規則可能會告知 Lync Server 允許登入、封鎖登入，或允許登入，但是會以無訊息方式將用戶端應用程式升級為最新版本 (例如，將 Communicator 2007 R2 升級到 Lync 2013)。

用戶端版本原則 (可套用至全域範圍、網站範圍、服務範圍 (僅登錄器服務)，或個別使用者範圍)，可讓您在決定哪些用戶端應用程式可用來存取系統時，擁有彈性。例如，一般而言，您可能想防止使用者使用 Communicator 2007 R2 登入 Lync Server，因為 Communicator 2007 R2 與 Lync 2013 所支援的功能和特性並不同。但是，由於硬體或軟體衝突，您可能有一群不能升級為 Lync 2013 的使用者。在該情況下，您可以建立個別的規則 (以及個別的用戶端版本原則)，允許那些使用者從 Communicator 2007 R2 登入。

您可以使用 **New-CsClientVersionPolicy** 建立新的原則。稍後，您可以透過執行 **Remove-CsClientVersionPolicy** 來移除這些自訂原則。當您移除用戶端版本原則時，先前由該原則所管理的使用者將自動繼承管理階層中的下一個原則。例如，如果您刪除個別使用者原則，將自動由適當的服務原則來管理使用者。如果沒有服務原則，則將由適當的網站原則管理使用者。如果沒有網站原則，則將由全域原則管理使用者。

請注意，全域原則一定會存在，也就是說，任何使用者都會由用戶端版本原則管理。雖然您可以針對全域原則執行 **Remove-CsClientVersionPolicy** Cmdlet，但該原則實際上並不會遭到刪除，而是將所有原則規則重設為其預設值。

請注意，用戶端版本原則不適用於同盟使用者；而是同盟使用者受到本身組織中使用的用戶端版本原則所約束。例如，假設某位同盟使用者使用用戶端 A (此為同盟組織所允許的用戶端)。只要同盟組織允許使用用戶端 A，這個使用者就可以使用該用戶端與您的組織通訊。即使您的用戶端版本原則會封鎖使用用戶端 A，此情況也成立。在您組織中強制執行的用戶端版本原則不會覆寫同盟組織中使用者的用戶端版本原則。

誰可以執行這個 Cmdlet：根據預設，會授權下列群組的成員執行 **Remove-CsClientVersionPolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsClientVersionPolicy\\b"}

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
<td><p>要刪除之原則的唯一識別碼。若要移除已設定於網站範圍內的原則，可使用類似下列的語法：-Identity &quot;site:Redmond&quot;。若要移除已設定於服務範圍內的原則，可使用類似下列的語法：-Identity &quot;Registrar:atl-cs-001.litwareinc.com&quot;。登錄程式服務是唯一可以主控用戶端版本原則的服務。</p>
<p>在個別使用者範圍也可以移除原則。若要移除個別使用者原則，請使用類似下列的語法：-Identity &quot;SalesDepartmentPolicy&quot;。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionPolicy 物件。 **Remove-CsClientVersionPolicy** Cmdlet 接受管線傳送的用戶端版本原則物件執行個體。

## 傳回類型

**Remove-CsClientVersionPolicy** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionPolicy 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsClientVersionPolicy](get-csclientversionpolicy.md)  
[Grant-CsClientVersionPolicy](grant-csclientversionpolicy.md)  
[New-CsClientVersionPolicy](new-csclientversionpolicy.md)  
[Set-CsClientVersionPolicy](set-csclientversionpolicy.md)

