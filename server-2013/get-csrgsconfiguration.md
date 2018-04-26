---
title: Get-CsRgsConfiguration
TOCTitle: Get-CsRgsConfiguration
ms:assetid: a3667917-cfbf-47c1-8b48-e936594b5357
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412762(v=OCS.15)
ms:contentKeyID: 49291869
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsRgsConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回回應群組應用程式的組態設定資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsRgsConfiguration -Identity <RgsIdentity>

## 範例

## 範例 1

範例 1 會傳回 ApplicationServer:atl-cs-001.litwareinc.com 服務的回應群組組態設定。由於每一個服務只能有一個設定集合，所以此命令絕不會傳回一個以上的單一項目。

    Get-CsRgsConfiguration -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com"

## 範例 2

範例 2 顯示的命令會針對在服務 ApplicationServer:atl-cs-001.litwareinc.com 上找到的回應群組組態設定，傳回單一屬性 DisableCallContext 的值。為達此目的，會先使用 **Get-CsRgsConfiguration** 擷取 ApplicationServer:atl-cs-001.litwareinc.com 的回應群組組態設定的所有屬性值。請注意，此命令以括號括住；如此可以確保 Windows PowerShell 在進行任何其他動作之前，會先傳回所有屬性值。

傳回所有屬性值之後，使用標準「點標記法」來顯示 DisableCallContext 的屬性值 (以及僅該屬性的值)。標準點標記法由物件構成，後面跟著句點 (點)，再跟著要顯示之屬性的名稱。例如，若要顯示 AgentRingbackGracePeriod 屬性的值 (以及僅該屬性的值)，您可以使用此命令：

(Get-CsRgsConfiguration -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com").AgentRingbackGracePeriod。

    (Get-CsRgsConfiguration -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com").DisableCallContext

## 範例 3

範例 3 所示的命令示範如何從執行應用程式服務的所有電腦 (主控回應群組應用程式執行個體)，傳回回應群組組態資訊。為達此目的，命令先使用 **Get-CsService** Cmdlet 和 ApplicationServer 參數傳回組織中執行應用程式服務的所有伺服器的資訊。接著，此集合傳送到 **Where-Object** Cmdlet，此 Cmdlet 只會挑出 Applications 內容中包含應用程式 "urn:application:RGS" 的伺服器；此值表示回應群組應用程式在伺服器上執行。

然後，這些伺服器會傳送到 **ForEach-Object** Cmdlet。**ForEach-Object** 接著取得集合中的每一部伺服器，然後使用 **Get-CsRgsConfiguration**，從每一部伺服器傳回回應群組組態資訊。

    Get-CsService -ApplicationServer | Where-Object {$_.Applications -contains "urn:application:RGS"} | ForEach-Object {Get-CsRgsConfiguration -Identity $_.Identity}

## 詳細描述

回應群組應用程式 能讓您將來電自動路由傳送到如服務台或客戶支援專線等實體。當某人撥打指定的電話號碼，可將該來電直接路由傳送到適當的回應群組代理集合。或者，來電可能會先路由傳送到互動語音回應 (IVR) 佇列。在該佇列中，向來電者詢問一連串問題 (例如，「您是否為了現有訂單來電？」)，然後依據這些問題的回答，再轉接給適當的回應群組佇列。

**Get-CsRgsConfiguration** Cmdlet 提供您傳回設定 回應群組應用程式 方式的資訊。請注意，根據預設，此 Cmdlet 一次只從回應群組應用程式的某個執行個體傳回資訊。例如，如果您已分別安裝 回應群組應用程式，一個在 ApplicationServer:atl-cs-001.litwareinc.com 上，一個在 ApplicationServer:dublin-cs-001.litwareinc.com 上，一般來說，您必須分別呼叫 **Get-CsRgsConfiguration**，才能傳回每一個回應群組執行個體的資訊。不過，本主題的＜範例＞一節會顯示解決此問題的方法。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsRgsConfiguration** Cmdlet：RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsRgsConfiguration"}

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
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>託管回應群組組態設定的服務名稱；例如：-Identity &quot;service:ApplicationServer:atl-cs-001.litwareinc.com&quot;。如果您沒有包含此參數，<strong>Get-CsRgsConfiguration</strong> 會提示您提供 Identity。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串。**Get-CsRgsConfiguration** 接受字串值，代表回應群組組態設定的 Identity。

## 傳回類型

**Get-CsRgsConfiguration** 會傳回 Microsoft.Rtc.Rgs.Management.WritableSettings.ServiceSettings 物件的執行個體。

## 請參閱

#### 其他資源

[Move-CsRgsConfiguration](move-csrgsconfiguration.md)  
[Set-CsRgsConfiguration](set-csrgsconfiguration.md)

