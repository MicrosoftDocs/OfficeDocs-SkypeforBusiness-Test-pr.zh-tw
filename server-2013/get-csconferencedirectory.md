---
title: Get-CsConferenceDirectory
TOCTitle: Get-CsConferenceDirectory
ms:assetid: 2b7927ab-c6b3-42ce-9c27-9825cd47fd77
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425771(v=OCS.15)
ms:contentKeyID: 49290435
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConferenceDirectory

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定供組織使用之會議目錄的資訊。會議目錄可協助電話撥入式會議使用者尋找會議資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsConferenceDirectory [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsConferenceDirectory [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定為在組織中使用之所有會議目錄的資訊。

    Get-CsConferenceDirectory

## 範例 2

範例 2 會傳回 Identity 為 2 的會議目錄相關資訊。由於 Identity 必須是唯一的，因此此命令絕不會傳回一個以上的會議目錄。

    Get-CsConferenceDirectory -Identity 2

## 範例 3

範例 3 會傳回存放於 UserServer:atl-cs-001.litwareinc.com 服務上的所有會議目錄。為達成此目的，此命令會先呼叫未含任何參數的 **Get-CsConferenceDirectory** Cmdlet，以傳回組織中找到的所有會議目錄集合。然後再將此集合管線傳送至 **Where-Object** Cmdlet，這會只選取 ServiceID 符合 "UserServer:atl-cs-001.litwareinc.com" 字串值的目錄。

    Get-CsConferenceDirectory | Where-Object {$_.ServiceID -match "UserServer:atl-cs-001.litwareinc.com"}

## 詳細描述

建立電話撥入式會議統一資源識別元 (URI) 時，會指派唯一 SIP 位址給這些 URI。不過，無法辨識 SIP 的裝置很難轉譯 SIP 位址；例如，公用交換電話網路 (PSTN) 電話無法轉譯 SIP 位址。有鑑於此，Lync Server 便會使用會議目錄來做為協助這些裝置尋找、連接及撥入會議的方法。完成此作業的方法是，建立與每個電話撥入式會議 URI 相關聯的 SIP 會議目錄，並以非 SIP URI 的整數值來識別。PSTN 電話和其他裝置在連線到會議時可以使用這些號碼 (而不是 SIP URI)；使用者連線到電話撥入式會議時所輸入的 PSTN 會議識別中包含目錄號碼。

**Get-CsConferenceDirectory** Cmdlet 可讓您傳回設定供組織使用之所有會議目錄的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsConferenceDirectory** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsConferenceDirectory"}

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
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您使用萬用字元指定要擷取之會議目錄的 Identity。由於目錄 Identity 是數值，因此此參數可能是最小的值。不過，此語法將傳回 Identity 開頭為數字 3: -Filter &quot;3*&quot; 的所有會議目錄。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要傳回之會議目錄的數值識別碼 (例如 7)。如果省略此參數，則 <strong>Get-CsConferenceDirectory</strong> Cmdlet 會傳回用於組織之所有會議目錄的資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取會議目錄資料，而非從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsConferenceDirectory** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsConferenceDirectory** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.PstnConf.ConferenceDirectories 物件的執行個體。

## 請參閱

#### 其他資源

[Move-CsConferenceDirectory](move-csconferencedirectory.md)  
[New-CsConferenceDirectory](new-csconferencedirectory.md)  
[Remove-CsConferenceDirectory](remove-csconferencedirectory.md)

