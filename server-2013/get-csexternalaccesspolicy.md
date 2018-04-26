---
title: Get-CsExternalAccessPolicy
TOCTitle: Get-CsExternalAccessPolicy
ms:assetid: 301403c8-aeb2-4501-a2ae-96eaa6ad68a4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425805(v=OCS.15)
ms:contentKeyID: 49290488
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsExternalAccessPolicy

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定供組織使用之外部存取原則的資訊。外部存取原則可指定使用者是否可以：1) 和同盟組織中用工作階段初始通訊協定 (SIP) 帳戶的使用者通訊；2) 和使用公用立即訊息 (IM) 提供者 (例如 Windows Live) 之SIP 帳戶的使用者通訊；以及 3) 直接從網際網路存取 Lync Server，而無須登入內部網路。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsExternalAccessPolicy [-Identity <XdsIdentity>] [[-ApplicableTo] <Object>] <COMMON PARAMETERS>

    Get-CsExternalAccessPolicy [-Filter <String>] [[-ApplicableTo] <Object>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 會傳回設定供組織使用之所有外部存取原則的集合。呼叫不含任何額外參數的 **Get-CsExternalAccessPolicy** Cmdlet 一律會傳回外部存取原則的完整集合。

    Get-CsExternalAccessPolicy

## 範例 2

範例 2 使用 Identity 參數傳回具有 Identity site:Redmond 的外部存取原則。因為存取原則 Identity 必須是唯一的，此命令絕不會傳回一個以上的項目。

    Get-CsExternalAccessPolicy -Identity site:Redmond

## 範例 3

範例 3 展示的命令使用 Filter 參數來傳回已在每個使用者範圍內設定的所有外部存取原則；參數值 "tag:\*" 可將傳回的資料限制為 Identity 開頭為字串值 "tag:" 的原則。根據定義，任何具有 Identity 開頭為 "tag:" 的原則都是已在每個使用者範圍設定的原則

    Get-CsExternalAccessPolicy -Filter tag:*

## 範例 4

在範例 4 中，**Get-CsExternalAccessPolicy** Cmdlet 和 **Where-Object** Cmdlet 可用來傳回授予使用者同盟存取的所有外部存取原則。為達成此目的，會先使用 **Get-CsExternalAccessPolicy** Cmdlet 傳回組織內目前所使用的所有外部存取原則集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 EnableFederationAccess 內容等於 True 的原則。

    Get-CsExternalAccessPolicy | Where-Object {$_.EnableFederationAccess -eq $True}

## 範例 5

範例 5 所示的命令傳回符合兩個準則的外部存取原則：允許同盟存取和公用雲端存取兩者。為了執行此工作，命令會先使用 **Get-CsExternalAccessPolicy** Cmdlet 傳回組織內使用中的所有存取原則集合。該集合便會管線傳送到 **Where-Object** Cmdlet，這會只挑出符合兩個準則的原則：EnableFederationAccess 屬性必須等於 True，且 EnablePublicCloudAccess 屬性必須也等於 True。只有 EnableFederationAccess 和 EnablePublicCloudAccess 都為 True 的原則會被傳回，並顯示在螢幕上。

若要傳回 EnableFederationAccess 或 EnablePublicCloudAccess 為 True 的原則清單，請使用 –or 運算子：

Where-Object {$\_.EnableFederationAccess -eq $True -or $\_.EnablePublicCloudAccess -eq $True}

    Get-CsExternalAccessPolicy | Where-Object {$_.EnableFederationAccess -eq $True -and $_.EnablePublicCloudAccess -eq $True} 

## 詳細描述

安裝 Lync Server 時，只允許使用者彼此交換立即訊息和目前狀態資訊：根據預設，他們只能與 Active Directory 網域服務 中具有 SIP 帳戶的其他人員通訊。此外，不允許使用者透過網際網路存取 Lync Server；而是在他們可以登入 Lync Server 之前，必須登入您的內部網路。

這可能足以符合您的通訊需求。如果不符合您的需求，您可以使用外部存取原則，擴充使用者通訊和共同作業的能力。外部存取原則可以授與 (或撤銷) 使用者執行下列任何或全部作業的能力：

1\. 與具有含同盟組織 SIP 帳戶的人員通訊。請注意，單獨啟用同盟將不提供使用者這項功能。而是您必須啟用同盟，然後指派使用者外部存取原則，給予他們與同盟使用者通訊的權限。

2\. 透過公用立即訊息服務 (例如 Windows Live) 與具有 SIP 帳戶的人員通訊。

3.透過網際網路存取 Lync Server，而不必先登入您的內部網路。這讓使用者可以使用 Lync，並從網路咖啡廳或其他遠端位置登入 Lync Server。

**Get-CsExternalAccessPolicy** Cmdlet 提供一種方法，可讓您傳回已設定供組織使用的所有外部存取原則資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsExternalAccessPolicy** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsExternalAccessPolicy"}

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
<td><p>System.Strkng</p></td>
<td><p>讓您可以用萬用字元搜尋外部存取原則。例如，若要在網站範圍尋找設定的所有原則，請使用下列 Filter：site:*。若要尋找個別使用者原則 Seattle、Seville 和 Saskatoon (皆以字母 &quot;S&quot; 為開頭)，請使用下列 Filter：&quot;S*&quot;。請注意，Filter 參數只適用於原則 Identity。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>在建立原則時要指派給它的唯一 Identity。可在全域、網站或每個使用者範圍上指派的外部存取原則。若要參考全域執行個體，請使用下列語法：-Identity global。若要參考網站範圍的原則，請使用以下的語法：-Identity site:Redmond。若要在每個使用者範圍上參考原則，請使用類似下列的語法：-Identity RedmondPolicy。</p>
<p>請注意，星號 (*) 之類的萬用字元不能與 Identity 參數一起使用。若要以萬用字元搜尋原則，請改用 Filter 參數。</p>
<p>若未指定 Identity 和 Filter 參數，則 <strong>Get-CsExternalAccessPolicy</strong> Cmdlet 會傳回設定供組織使用之所有外部存取原則的集合。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取外部存取原則資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsExternalAccessPolicy** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

傳回 Microsoft.Rtc.Management.WritableConfig.Policy.ExternalAccess.ExternalAccessPolicy 物件的執行個體。

## 請參閱

#### 其他資源

[Grant-CsExternalAccessPolicy](grant-csexternalaccesspolicy.md)  
[New-CsExternalAccessPolicy](new-csexternalaccesspolicy.md)  
[Remove-CsExternalAccessPolicy](remove-csexternalaccesspolicy.md)  
[Set-CsExternalAccessPolicy](set-csexternalaccesspolicy.md)

