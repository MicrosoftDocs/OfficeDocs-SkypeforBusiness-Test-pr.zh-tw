---
title: Enable-CsHostingProvider
TOCTitle: Enable-CsHostingProvider
ms:assetid: 0ba76785-6c6d-4ee6-9418-5c77b2cbaedf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398166(v=OCS.15)
ms:contentKeyID: 49290053
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Enable-CsHostingProvider

 

_**上次修改主題的時間：** 2015-03-09_

啟用供組織使用的主機供應商。主機供應商是第三方組織，可提供立即訊息、目前狀態，以及您要結為同盟之網域相關的服務。主機供應商 (例如 Microsoft Lync Online 2010) 不同於公用提供者 (例如 Yahoo\!、MSN 和 AOL)，其服務對象不是一般大眾。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Enable-CsHostingProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Enable-CsHostingProvider [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會啟用 Identity 為 Fabrikam.com 的主機供應商以供使用。請注意，如果已經啟用 Fabrikam.com 以供使用，則此命令將會傳回錯誤。

    Enable-CsHostingProvider -Identity Fabrikam.com

## 範例 2

範例 2 會示範如何啟用目前已停用的所有主機供應商。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsHostingProvider** Cmdlet，以傳回目前設定供組織使用之所有主機供應商的集合。然後再將此集合管線傳送至 **Where-Object** Cmdlet，以選取 Enabled 屬性等於 False 的任何提供者；根據定義，這是目前停用的任何提供者。接著將篩選後的集合管線傳送到 **Enable-CsHostingProvider** Cmdlet，以啟用集合中的每一個供應商

    Get-CsHostingProvider | Where-Object {$_.Enabled -eq $False} | Enable-CsHostingProvider

## 範例 3

範例 3 會啟用在「分割網域」設定中使用之所有主機供應商以供使用 (分隔網域表示您的某些 Lync Server 帳戶為內部維護，而其他帳戶則是由主機供應商維護)。為了執行此工作，命令會先使用 **Get-CsHostingProvider** Cmdlet 傳回目前設定之所有主機提供者的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取符合下列兩個準則的供應商：1) EnabledSharedAddressSpace 屬性等於 True；且 2) Enabled 屬性等於 False。接著將篩選後的集合管線傳送到 **Enable-CsHostingProvider** Cmdlet，以啟用集合中的每個供應商。

    Get-CsHostingProvider | Where-Object {$_.EnabledSharedAddressSpace -eq $True -and $_.Enabled -eq $False} | Enable-CsHostingProvider

## 詳細描述

「同盟」是兩個組織可建立信任關係的一種方法，此信任關係會簡化兩個團體之間的通訊。建立同盟後，兩個組織的使用者便可互相傳送立即訊息、訂閱目前狀態通知，並使用如 Lync 2013 等 SIP 應用程式互相通訊。Lync Server 允許三種同盟：1) 您的組織與其他組織之間的直接同盟；2) 您的組織與公用提供者之間的同盟；以及 3) 您的組織與協力廠商主機供應商之間的同盟。

主機供應商是一種為其他組織提供 SIP 通訊服務的組織，例如 Fabrikam Hosting，Inc. 可能託管 Contoso、Northwind Traders、Wingtip Toys 等組織的使用者。當您與主機供應商建立同盟關係時，實際上是與由該供應商提供主機服務的任何組織建立同盟。例如，如果您與 Fabrikam Hosting 同盟，您的使用者便能夠與 Contoso、Northwind Traders 及 Wingtip Toys 的使用者交換立即訊息和目前狀態的資訊。

主機供應商也可以用於分割網域案例。在分隔網域的案例中，您的部分 Lync Server 使用者會擁有在內部主控的帳戶 (也就是在 Lync Server 的本機實作上進行主控)。其他使用者的帳戶由第三方主機供應商在外部部署維護。與主機供應商同盟可讓內部部署使用者與外部部署使用者互相通訊。

為了與第三方主機供應商同盟，您必須建立並啟用新的主機供應商。(此外，該第三方供應商也必須與您建立同盟關係)。您可以在建立主機供應商時啟用該供應商；或者，也可以事後使用 **Enable-CsHostingProvider** Cmdlet 來啟用該供應商。

請注意，如果您的 Edge Server 設定為使用預設路由，而非網域名稱系統 (DNS) 伺服器路由，則您無法與主機供應商同盟。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Enable-CsHostingProvider** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Enable-CsHostingProvider"}

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
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要啟用之主機供應商的唯一識別碼。Identity 可能是主機供應商的完整網域名稱 (FQDN) (例如，fabrikam.com)，也可能是提供服務之公司的名稱 (Fabrikam，Inc.)。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>DisplayHostingProvider 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayHostingProvider 物件。**Enable-CsHostingProvider** Cmdlet 接受管線傳送的主機供應商物件執行個體。

## 傳回類型

無。反之，此 Cmdlet 會啟用 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayHostingProvider 物件的執行個體。

## 請參閱

#### 其他資源

[Disable-CsHostingProvider](disable-cshostingprovider.md)  
[Get-CsHostingProvider](get-cshostingprovider.md)  
[New-CsHostingProvider](new-cshostingprovider.md)  
[Remove-CsHostingProvider](remove-cshostingprovider.md)  
[Set-CsHostingProvider](set-cshostingprovider.md)

