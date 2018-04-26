---
title: Set-CsServerApplication
TOCTitle: Set-CsServerApplication
ms:assetid: b0f75629-b6c3-4958-b466-6c8a2f104819
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412850(v=OCS.15)
ms:contentKeyID: 49292037
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsServerApplication

 

_**上次修改主題的時間：** 2015-03-09_

修改現有伺服器應用程式的屬性值。伺服器應用程式是由 Lync Server 代管的應用程式。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsServerApplication [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsServerApplication [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Critical <$true | $false>] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-Priority <Int32>] [-Script <String>] [-ScriptName <String>] [-Uri <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會啟用 Identity 為 Registrar:atl-cs-001.litwareinc.com/ExumRouting 的伺服器應用程式。由於識別身分必須是唯一的，因此這個命令只會啟用一個伺服器應用程式。

    Set-CsServerApplication -Identity "Registrar:atl-cs-001.litwareinc.com/ExumRouting" -Enabled $True

## 範例 2

範例 2 會啟用所有目前停用的伺服器應用程式。為達成此目的，命令會先呼叫 **Get-CsServerApplication** Cmdlet，以傳回組織目前使用的所有伺服器應用程式集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 Enabled 屬性等於 False 的應用程式。接著將篩選後的集合管線傳送到 **Set-CsServerApplication** Cmdlet，以取得集合中的每一個項目，並將 Enabled 屬性設為 True。

    Get-CsServerApplication | Where-Object {$_.Enabled -eq $False} | Set-CsServerApplication -Enabled $True

## 詳細描述

伺服器應用程式會參考 Lync Server 下所執行的個別程式。**Set-CsServerApplication** Cmdlet 提供多種方法讓系統管理員可以修改 Lync Server 中所執行之任何應用程式的內容值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsServerApplication** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsServerApplication"}

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
<td><p><em>Critical</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果設為 True (預設值)，除非上述的應用程式可以啟動，否則 Lync Server 將不會啟動。如為 False，不管此應用程式可不可以啟動，Lync Server 都會啟動。</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>將此值設為 True 即可啟用此應用程式。將此值設為 False 即可停用此應用程式。</p></td>
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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改之伺服器應用程式的唯一識別碼。伺服器應用程式 Identity 由託管應用程式的服務和應用程式名稱組成。例如，名為 QoEAgent 的伺服器應用程式可能會有如下的 Identity：Registrar:atl-cs-001.litwareinc.com/QoEAgent。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>ServerApplication.Application 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>Priority</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>指出伺服器應用程式的執行順序。優先順序 0 的應用程式會先啟動，優先順序 1 的應用程式第二個啟動，依此類推。請注意，每個裝載伺服器應用程式的服務都有一組自己的獨特優先順序。例如，登錄器服務可以主控對應到優先順序 0、1, 和 2 的三個應用程式。同樣地，Edge Server 服務可以有四個應用程式；這些應用程式的優先順序為 0、1、2 和 3。</p>
<p>如果您沒有指定優先順序，系統會自動將應用程式加到優先順序清單的最底部。如果您新增或移除應用程式，其他應用程式的優先順序將跟著調整。例如，如果刪除優先順序 0 的應用程式，則原本優先順序 1 的應用程式的優先順序將自動設為 0。</p></td>
</tr>
<tr class="even">
<td><p><em>Script</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您關聯伺服器應用程式與指令碼。若要將指令碼新增至伺服器應用程式，請使用類似下列的語法：</p>
<p>-Script &quot;Update.ps1&quot;</p>
<p>若要移除指令碼，只要將 Script 屬性設為 Null 值即可：</p>
<p>-Script $Null</p>
<p>每個伺服器應用程式只可關聯一個指令碼。</p></td>
</tr>
<tr class="odd">
<td><p><em>ScriptName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指向應用程式所使用之 Microsoft SIP Processing Language (MSPL) 指令碼的路徑。MSPL 是用來篩選和轉送 SIP 訊息的指令碼語言。</p></td>
</tr>
<tr class="even">
<td><p><em>Uri</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>應用程式的唯一統一資源識別元 (URI)。例如，QoEAgent 應用程式的 URI 是 http://www.microsoft.com/LCS/QoEAgent。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.ServerApplication.Application 物件。**Set-CsServerApplication** Cmdlet 接受伺服器應用程式物件管線傳送的執行個體。

## 傳回類型

**Set-CsServerApplication** Cmdlet 不會傳回值或物件，而是會設定 Microsoft.Rtc.Management.WritableConfig.Settings.ServerApplication.application 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsServerApplication](get-csserverapplication.md)  
[New-CsServerApplication](new-csserverapplication.md)  
[Remove-CsServerApplication](remove-csserverapplication.md)

