---
title: Remove-CsPrivacyConfiguration
TOCTitle: Remove-CsPrivacyConfiguration
ms:assetid: 32052c51-953d-4278-9425-306245d297ed
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425821(v=OCS.15)
ms:contentKeyID: 49290517
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPrivacyConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的隱私權組態設定集合。隱私權組態設定可指定使用者所能使用的資訊量。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsPrivacyConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會傳回指派給 Redmond 網站的隱私權組態設定。在刪除這些設定後，Redmond 網站中的使用者會自動繼承全域隱私權組態設定。

    Remove-CsPrivacyConfiguration -Identity site:Redmond

## 範例 2

在範例 2 中，會刪除網站範圍所指派的所有隱私權組態設定。為達成此目的，命令會先呼叫 **Get-CsPrivacyConfiguration** Cmdlet 搭配 Filter 參數；篩選值 "site:\*" 可確保只會傳回 Identity 的開頭為 "site" 字元的設定。然後再將篩選後的集合管線傳送到 **Remove-CsPrivacyConfiguration** Cmdlet，以移除集合中的每一個項目。

    Get-CsPrivacyConfiguration -Filter "site:*" | Remove-CsPrivacyConfiguration

## 範例 3

範例 3 所示的命令會刪除所有隱私權模式已停用的隱私權組態設定。為執行此工作，命令會先呼叫不含任何參數的 **Get-CsPrivacyConfiguration** Cmdlet，以傳回組織目前所使用之所有隱私權組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 EnablePrivacyMode 屬性等於 False 的設定。接著將篩選後的集合管線傳送到 **Remove-CsPrivacyConfiguration** Cmdlet，以刪除集合中的每個項目。

    Get-CsPrivacyConfiguration | Where-Object {$_.EnablePrivacyMode -eq $False} | Remove-CsPrivacyConfiguration

## 詳細描述

Lync Server 可以提供使用者與其他人共用大量目前狀態資訊的機會：他們可以發佈自己的照片、提供詳細的位置資訊，並將自己的目前狀態資訊自動提供給組織內的每一個人 (而不是只將此資訊提供給其連絡人清單上的人)。

有些使用者很高興有這個機會能將此資訊提供給他們的同事，但也有一些使用者不願意分享此資料(例如，許多人對於將他們的照片放在目前狀態資料中會有疑慮)。一般而言，使用者可控制是否分享哪些資訊，例如使用者可勾選或取消勾選核取方塊，來控制是否要與他人分享其位置資訊。此外，隱私權組態 Cmdlet 可讓系統管理員管理使用者的隱私權設定。在某些情況下，系統管理員可啟用或停用設定。例如，如果將 AutoInitiateContacts 內容設為 True，則會將小組成員自動新增至每個使用者的連絡人清單中；如果設為 False，則不會將小組成員自動新增至每個使用者的連絡人清單中。

在其他狀況下，系統管理員可在 Lync Server 中設定預設值，同時仍讓使用者有權利變更這些值。例如會預設發佈使用者的位置資料，但使用者有權利停止發佈位置。透過將 PublishLocationDataByDefault 屬性設為 False，系統管理員可變更此行為：在此狀況下，預設不會發佈位置資料，但使用者仍有權利選擇發佈此資料。

隱私權組態設定會套用在全域範圍、網站範圍與服務範圍 (雖然僅適用於 User Server 服務)。**Remove-CsPrivacyConfiguration** Cmdlet 讓您能夠刪除已在網站範圍或服務範圍設定的設定，例如如果您對在網站範圍所設定的設定執行此 Cmdlet，則會刪除那些設定，且該網站內的使用者會讓隱私權設定由全域集合管理。此外也會對全域集合執行 **Remove-CsPrivacyConfiguration** Cmdlet，但不會刪除全域集合。而是該集合中所有的該屬性皆會重設為預設值。例如，假設您先前已將 EnablePrivacyMode 屬性變更為 True。如果您現在「刪除」全域集合，則 EnablePrivacyMode 會回復成預設值 False。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsPrivacyConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPrivacyConfiguration"}

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
<td><p>要移除之隱私權組態設定的唯一識別碼。若要移除在此網站範圍設定的設定，請使用類似下列的語法：-Identity site:Redmond。若要移除該服務層級的設定，請使用下列語法：-Identity service:UserServer:atl-cs-001.litwareinc.com。</p>
<p>此外也會對全域的設定集合執行 <strong>Remove-CsPrivacyConfiguration</strong> Cmdlet。但此狀況下不會刪除全設定，而是將該集合中的所有屬性重設為預設值。</p></td>
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
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要刪除隱私權組態設定之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行此命令來傳回每位租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PrivacyConfiguration 物件。**Remove-CsPrivacyConfiguration** Cmdlet 接受隱私組態物件的管線傳送輸入。

## 傳回類型

無。反之，**Remove-CsPrivacyConfiguration** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PrivacyConfiguration 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsPrivacyConfiguration](get-csprivacyconfiguration.md)  
[New-CsPrivacyConfiguration](new-csprivacyconfiguration.md)  
[Set-CsPrivacyConfiguration](set-csprivacyconfiguration.md)

