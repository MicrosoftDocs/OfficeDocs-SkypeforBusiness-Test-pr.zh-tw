---
title: Get-CsHostingProvider
TOCTitle: Get-CsHostingProvider
ms:assetid: fd493022-eb53-4084-aa81-213cb5e959fc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413078(v=OCS.15)
ms:contentKeyID: 49292912
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsHostingProvider

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定供組織使用之主機供應商的資訊。主機供應商是第三方組織，可提供立即訊息、目前狀態，以及您要結為同盟之網域相關的服務。主機供應商 (如 Microsoft Lync Online 2010) 與公用提供者 (例如 Yahoo\!、MSN 與 AOL) 不同，其服務對象不是一般大眾。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsHostingProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsHostingProvider [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 會傳回設定供組織使用的所有主機供應商集合。呼叫不含任何參數的 **Get-CsHostingProvider** Cmdlet 會傳回主機供應商的完整集合。

    Get-CsHostingProvider

## 範例 2

範例 2 傳回 Identity 為 Fabrikam.com 的主機供應商。由於 Identity 在主機供應商之間必須是唯一的，因此，此命令絕對不會傳回一個以上的項目。

    Get-CsHostingProvider -Identity Fabrikam.com

## 範例 3

範例 3 所示的命令會傳回 Identity 以字串值 ".org" 結束 (例如，fabrikam.org 和 contoso.org) 的所有主機供應商集合。

    Get-CsHostingProvider -Filter *.org

## 範例 4

範例 4 會傳回目前已啟用為可供使用的所有主機供應商。為達成此目的，會先呼叫 **Get-CsHostingProvider** Cmdlet 傳回目前設定供組織使用之所有主機供應商的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 Enabled 屬性等於 True 的供應商。

    Get-CsHostingProvider | Where-Object {$_.Enabled -eq $True}

## 範例 5

範例 5 會傳回具有共用位址空間和主控 Lync Server 使用者的所有主機供應商；根據定義，這表示命令會傳回隸屬於「分隔網域」設定一部分的所有主機供應商 (簡單來說，分隔網域代表您的部分 Lync Server 帳戶是在內部維護，而其他帳戶是由主機供應商所維護)。為達成此目的，命令會先使用 **Get-CsHostingProvider** Cmdlet 傳回目前所設定之所有主機供應商的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取符合下列兩個準則的供應商：1) Enabled 屬性等於 True；且 2) EnabledSharedAddressSpace 屬性等於 True。

    Get-CsHostingProvider | Where-Object {$_.Enabled -eq $True -and $_.EnabledSharedAddressSpace -eq $True}

## 範例 6

範例 6 所示的命令會顯示設定供組織使用之所有主機供應商的屬性值。根據預設，當您執行 **Get-CsHostingProvider** 時，EnabledSharedAddressSpace 和 HostsOCSUsers 的屬性值並不會顯示。為能查看這些屬性值，會將 **Get-CsHostingProvider** Cmdlet 傳回的資訊管線傳送到 **Select-Object** Cmdlet (萬用字元 (\*) 會指示 **Select-Object** Cmdlet 顯示所有屬性及傳回項目的屬性值)。

    Get-CsHostingProvider | Select-Object *

## 詳細描述

同盟是兩個組織用來建立信任關係的方法，以促進兩個群組之間的溝通。建立同盟後，兩個組織的使用者便可互相傳送立即訊息、訂閱目前狀態通知，並使用如 Lync 等 SIP 應用程式互相通訊。Lync Server 允許三種同盟：1) 您組織與其他組織之間的直接同盟；2) 您組織與公用提供者之間的同盟；3) 您組織與第三方主機供應商之間的同盟。

主機供應商是為其他組織提供 SIP 通訊服務的組織；例如 Fabrikam，Inc. 可能為 Contoso、Northwind Traders、Wingtip Toys 的使用者提供主機服務。當您與主機供應商建立同盟關係時，便能夠有效率地與該供應商所託管的任何組織建立同盟關係。例如，如果您與 Fabrikam Hosting 同盟，您的使用者便能夠與 Contoso、Northwind Traders 及 Wingtip Toys 的使用者交換立即訊息和目前狀態的資訊。

主機供應商也用於分割網域案例。在分隔網域的案例中，您的部分 Lync Server 使用者會擁有在內部主控的帳戶 (也就是在 Lync Server 的本機實作上進行主控)。其他使用者的帳戶由第三方主機供應商在外部部署維護。與主機供應商同盟可讓內部部署使用者與外部部署使用者互相通訊。

**Get-CsHostingProvider** Cmdlet 會為您提供一個方式，來傳回已設定為供組織使用的所有主機供應商相關資訊。

請注意，如果您的 Edge Server 設定為使用預設路由，而非網域名稱系統 (DNS) 伺服器路由，則您無法與主機供應商同盟。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsHostingProvider** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsHostingProvider"}

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
<td><p>讓您能夠使用萬用字元值，傳回一或多個主機供應商。例如，若要傳回 Identity 是以字串值 &quot;.com&quot; 結尾的所有主機供應商，請使用下列語法：-Filter &quot;*.com&quot;。若要傳回 Identity 是以字串 &quot;Fabri&quot; 開頭的所有主機供應商，請使用下列語法：-Filter &quot;Fabri*&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要傳回之主機供應商的唯一識別碼。Identity 可能是主機供應商的完整網域 (FQDN) 名稱 (例如 fabrikam.com)，或者可能是提供服務的公司名稱 (Fabrikam，Inc.)。</p>
<p>若未指定此參數，<strong>Get-CsHostingProvider</strong> Cmdlet 將傳回已設定為供組織使用的所有主機供應商的集合。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區 的本機複本擷取主機供應商資料，而非從 中央管理存放區 本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsHostingProvider** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

傳回 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayHostingProvider 物件的執行個體。

## 請參閱

#### 其他資源

[Disable-CsHostingProvider](disable-cshostingprovider.md)  
[Enable-CsHostingProvider](enable-cshostingprovider.md)  
[New-CsHostingProvider](new-cshostingprovider.md)  
[Remove-CsHostingProvider](remove-cshostingprovider.md)  
[Set-CsHostingProvider](set-cshostingprovider.md)

