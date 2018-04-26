---
title: New-CsServerApplication
TOCTitle: New-CsServerApplication
ms:assetid: 045e6e65-8ad6-49af-8bfb-aa9045fa4dd8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398096(v=OCS.15)
ms:contentKeyID: 49289944
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsServerApplication

 

_**上次修改主題的時間：** 2015-03-09_

建立新的伺服器應用程式。伺服器應用程式是由 Lync Server 代管的應用程式。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsServerApplication -Name <String> -Parent <String> <COMMON PARAMETERS>

    New-CsServerApplication -Identity <XdsIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -Uri <String> [-Confirm [<SwitchParameter>]] [-Critical <$true | $false>] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Priority <Int32>] [-Script <String>] [-ScriptName <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會建立 Identity 為 EdgeServer:atl-edge-001.litwareinc.com/EdgeMonitor 的新伺服器應用程式。除了指定 Identity 之外，還會加上 Uri 和 Critical 參數；這些參數是用來指定應用程式 URI，並表示此應用程式不被視為關鍵。

    New-CsServerApplication -Identity "EdgeServer:atl-edge-001.litwareinc.com/EdgeMonitor" -Uri http://www.litwareinc.com/edgemonitor -Critical $False

## 範例 2

範例 2 所示的命令會示範如何建立一開始只存在於記憶體中的新伺服器應用程式。為達成此目的，第一個命令會呼叫 **New-CsServerApplication** Cmdlet 搭配下列兩個參數：Identity (指定應用程式的 Identity) 和 InMemory (表示新應用程式只應在記憶體中建立)，並將產生的伺服器應用程式物件儲存在變數 $x 中。

建立此虛擬伺服器應用程式後，命令 2 和 3 會分別用來修改 Uri 和 Critical 屬性的值。最後，命令 4 是用來將虛擬伺服器應用程式轉換為實際的伺服器應用程式。請注意，最後一個命令是必要項目。如果您沒有呼叫 **Set-CsServerApplication** Cmdlet，就不會為 EdgeServer:atl-edge-001.litwareinc.com/EdgeMonitor 設定應用程式，而且只要您一結束 Windows PowerShell 工作階段或刪除變數 $x，虛擬應用程式就會消失。

    $x = New-CsServerApplication -Identity "EdgeServer:atl-edge-001.litwareinc.com/EdgeMonitor" -InMemory
    $x.Uri = "http://www.litwareinc.com/edgemonitor"
    $x.Critical = $False
    Set-CsServerApplication -Instance $x

## 詳細描述

伺服器應用程式是指在 Lync Server 下執行的個別程式。**New-CsServerApplication** Cmdlet 可讓系統管理員設定新的伺服器應用程式。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsServerApplication** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsServerApplication"}

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
<td><p>要建立之伺服器應用程式的唯一識別碼。伺服器應用程式的 Identity 是由主控應用程式的服務加上應用程式名稱組成。例如，名稱為 QoEAgent 之伺服器應用程式的 Identity 會類似如下：service:Registrar:atl-cs-001.litwareinc.com/QoEAgent。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>服務的易記名稱。如果使用 Identity 參數，您就不需要在建立新服務時加入 Name 參數；Name 屬性會使用應用程式 Identity 的名稱部分填入。例如，如果建立 Identity 為 service:Registrar:atl-cs-001.litwareinc.com/TestService 的新應用程式，就會自動將該應用程式命名為 TestService。只有在使用 Parent 參數時，才需要 Name 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Parent</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>指定將主控新伺服器應用程式的服務。如果使用了 Identity 參數，您就不需要使用 Parent 或 Name 參數；那是因為應用程式 Identity 已結合了 Parent 和 Name 屬性的值。不過，您可以省略 Identity 參數，而改用 Parent 和 Name 參數。在該情況下，Parent 參數的外觀必須類似如下：-Parent &quot;Registrar:atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Uri</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>應用程式的唯一統一資源識別元 (URI)。例如，QoEAgent 應用程式的 URI 為 http://www.microsoft.com/LCS/QoEAgent。</p></td>
</tr>
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
<td><p>若設為 True，除非有問題的應用程式可以啟動，否則 Lync Server 將不會啟動。若為 False，無論應用程式能否啟動，Lync Server 一律會啟動。若未指定此參數，Critical 內容會設為 True。</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>將此值設為 True 可啟用應用程式。將此值設為 False 即可停用此應用程式。若未指定此參數，則 Enabled 內容會設為 False，並停用新應用程式。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>表示伺服器應用程式的執行順序。優先順序為 0 的應用程式會先啟動；優先順序為 1 的應用程式會第二個啟動，依此類推。請注意，主控伺服器應用程式的每個服務都有其自己唯一的一組優先順序。例如，登錄器服務可以主控對應到優先順序 0、1, 和 2 的三個應用程式。同樣地，Edge Server 服務可以有四個應用程式；這些應用程式的優先順序為 0、1、2 和 3。</p>
<p>如果您沒有指定優先順序，則會自動將應用程式新增至優先順序清單的底部。如果您新增或移除應用程式，其他應用程式的優先順序會依此調整。例如，如果您刪除優先順序為 0 的應用程式，則先前優先順序為 1 的應用程式會將其優先順序自動設為 0。</p></td>
</tr>
<tr class="odd">
<td><p><em>Script</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您關聯伺服器應用程式與指令碼。若要將指令碼加入伺服器應用程式，請使用類似下列的語法：</p>
<p>-Script &quot;Update.ps1&quot;</p>
<p>若要移除指令碼，只要將 Script 屬性設為 Null 值即可：</p>
<p>-Script $Null</p>
<p>每個伺服器應用程式只可關聯一個指令碼。</p></td>
</tr>
<tr class="even">
<td><p><em>ScriptName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>應用程式使用的 Microsoft SIP Processing Language (MSPL) 指令碼的路徑 (若適用的話)。MSPL 是用來篩選和轉送 SIP 訊息的指令碼語言。</p></td>
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

無。**New-CsServerApplication** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsServerApplication** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.ServerApplication.Application 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsServerApplication](get-csserverapplication.md)  
[Remove-CsServerApplication](remove-csserverapplication.md)  
[Set-CsServerApplication](set-csserverapplication.md)

