---
title: Get-CsPublicProvider
TOCTitle: Get-CsPublicProvider
ms:assetid: c122505d-7209-4dcb-a888-5c73f58fa68a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412945(v=OCS.15)
ms:contentKeyID: 49292199
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPublicProvider

 

_**上次修改主題的時間：** 2015-03-09_

傳回為設定供組織使用之公用提供者的資訊。公用提供者是可以為大眾提供立即訊息、目前狀態及相關服務的組織。Lync Server 的出貨版本中設有 Yahoo、AIM (AOL) 及 Messenger (MSN) 三家公用提供者，但未加以啟用。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsPublicProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsPublicProvider [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定供組織使用之所有公用提供者的集合。呼叫不含任何其他參數的 **Get-CsPublicProvider** Cmdlet 會傳回完整的公用提供者集合。

    Get-CsPublicProvider

## 範例 2

範例 2 會傳回所有 Identity 為 Messenger 的公用提供者。由於身分識別必須是公用提供者 (和主機供應商) 之中唯一的，因此這個命令一律最多只會傳回單一項目。

    Get-CsPublicProvider -Identity "Messenger"

## 範例 3

範例 3 會傳回 Identity 開頭為字母 W 的所有公用提供者。作法是加入 Filter 參數搭配篩選值 "W\*"。

    Get-CsPublicProvider -Filter W*

## 範例 4

範例 4 所示的命令會傳回目前停用的所有公用提供者集合。為達成此目的，命令會先呼叫 **Get-CsPublicProvider** Cmdlet，以傳回設定供組織使用之所有公用提供者的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 Enabled 屬性等於 False 的提供者。

    Get-CsPublicProvider | Where-Object {$_.Enabled -eq $False}

## 範例 5

範例 5 會傳回 VerificationLevel 屬性設為 AlwaysUnverifiable 或 UseSourceVerification 的所有公用提供者 (驗證層級可設為 AlwaysUnverifiable、UseSourceVerification 或 AlwaysVerifiable)。為了執行此工作，命令會先呼叫 **Get-CsPublicProvider** Cmdlet，傳回設定供組織使用之所有公用提供者的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 VerificationLevel 屬性不等於 AlwaysVerifiable 的提供者。整體效果：只會選取 VerificationLevel 屬性設為 AlwaysUnverifiable 或 UseSourceVerification 的公用提供者。

    Get-CsPublicProvider | Where-Object {$_.VerificationLevel -ne "AlwaysVerifiable"}

## 詳細描述

同盟是兩個組織用來建立信任關係的方法，以促進兩個群組之間的溝通。建立同盟後，兩個組織的使用者便可互相傳送立即訊息、訂閱目前狀態通知，並使用如 Lync 2013 等 SIP 應用程式互相通訊。Lync Server 允許三種同盟：1) 您組織與其他組織之間的直接同盟；2) 您組織與公用提供者之間的同盟；3) 您組織與協力廠商主機服務提供者之間的同盟。

公用提供者是一家提供 SIP 通訊服務給一般大眾的組織。當您與公用提供者建立同盟關係時，實際上就等於和任何具有該提供者所提供帳戶的使用者建立同盟。例如，如果您與 Messenger (MSN) 結盟，您的使用者便能夠與任何具有 Messenger 立即訊息帳戶的使用者交換立即訊息和目前狀態資訊。

若要與公用提供者結盟，您需要建立及啟用新的公用提供者 (此外，公用提供者也將需要與您建立同盟關係)。**Get-CsPublicProvider** Cmdlet 讓您可以傳回為已設定用於您組織的公用提供者相關資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsPublicProvider** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPublicProvider"}

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
<td><p>讓您可以使用萬用字元傳回一或多個公用提供者。例如，若要傳回 Identity 是以字母 Y 開頭的所有公用提供者的集合，請使用下列語法：-Filter &quot;Y*&quot;。若要傳回 Identity 中有出現字串值 &quot;Windows&quot; 的公用提供者的集合，請使用下列語法：-Filter &quot;*Windows*&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要傳回的公用提供者的唯一識別碼。Identity 通常是提供服務的網站名稱 (例如，Yahoo!、AOL、MSN 等)。</p>
<p>您無法在指定 Identity 時使用萬用字元。若要使用萬用字元傳回一或多個公用提供者，請改用 Filter 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取公用提供者資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsPublicProvider** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

傳回 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider 物件的執行個體。

## 請參閱

#### 其他資源

[Disable-CsPublicProvider](disable-cspublicprovider.md)  
[Enable-CsPublicProvider](enable-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Remove-CsPublicProvider](remove-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

