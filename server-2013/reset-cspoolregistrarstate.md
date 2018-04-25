---
title: Reset-CsPoolRegistrarState
TOCTitle: Reset-CsPoolRegistrarState
ms:assetid: 1bdbd5d7-cc72-46c5-ac20-ddc0d5723fe0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ619172(v=OCS.15)
ms:contentKeyID: 49290257
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Reset-CsPoolRegistrarState

 

_**上次修改主題的時間：** 2015-03-09_

重設指定登錄器集區的登錄器與 Windows 虛擬環境服務。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Reset-CsPoolRegistrarState -PoolFqdn <Fqdn> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-MachineFqdn <Fqdn>] [-NoReStart <SwitchParameter>] [-ResetLocalDatabases <SwitchParameter>] [-ResetType <ServiceReset | QuorumLossRecovery | FullReset | MachineStateRemoved>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會針對登錄器集區 atl-cs-001.litwareinc.com 執行服務重設。請注意，發出此命令之後，系統會提示您確認是否要繼續進行服務重設。

    Reset-CsPoolRegistrarState -PoolFqdn "atl-cs-001.litwareinc.com" -ResetType ServiceReset

## 範例 2

範例 2 也會針對登錄器集區 atl-cs-001.litwareinc.com 執行服務重設。但在此情況下，會包含 Confirm 參數並搭配參數值 $False (-Confirm:$False)。這樣會隱藏在呼叫 **Reset-CsPoolRegistrarState** Cmdlet 時，通常會顯示的確認提示。因此，系統將不會提示您確認是否要繼續進行服務重設，而是在您按 ENTER 後立即執行該命令。

    Reset-CsPoolRegistrarState -PoolFqdn "atl-cs-001.litwareinc.com" -ResetType ServiceReset -Confirm:$False

## 範例 3

範例 3 的仲裁遺失復原重設是在集區 atl-cs-001.litwareinc.com 中執行。當集區內使用中的前端伺服器數目低於仲裁狀態時 (也就是集區內目前使用中的前端伺服器少於總數的 85%)，通常就會重設仲裁遺失復原。請注意，只有處於仲裁遺失狀態下的服務，才必須從備份存放區重新載入使用者資料。其他服務將不受此命令影響。

    Reset-CsPoolRegistrarState -PoolFqdn "atl-cs-001.litwareinc.com" -ResetType QuorumLossRecovery

## 範例 4

範例 4 的完整重設是針對集區 atl-cs-001.litwareinc.com 進行。完整重設時，會停止前端服務及 Windows Fabric 服務，並移除一組項目 (包括 LyncServer-MachineSet.xml 及 Settings.xml 檔案)。移除這些項目之後，就會重新啟動前端服務及 Windows Fabric 服務。

請注意，嘗試重新啟動集區時，如果使用 FullReset 選項，有時會導致失敗，且集區不會確實重新啟動。因為這個原因，建議您先使用其中一個其他 ResetType 選項嘗試重新啟動集區。如果還是失敗，請先洽詢 Microsoft 支援人員，再使用 FullReset 選項。

    Reset-CsPoolRegistrarState -PoolFqdn "atl-cs-001.litwareinc.com" -ResetType FullReset

## 範例 5

範例 5 是範例 4 所示的命令的變化。不過，在此情況下，會包含 NoReStart 參數；這樣可防止 **Reset-CsPoolRegistrarState** Cmdlet 重新啟動已在集區重設時停止的服務 (例如 Windows Fabric 服務)。管理員可決定是否要手動重新啟動這些服務。

如範例 4 所述，嘗試重新啟動集區時，如果使用 FullReset 選項，有時會導致失敗，且集區不會確實重新啟動。因為這個原因，建議您先使用其中一個其他 ResetType 選項嘗試重新啟動集區。如果還是失敗，請先洽詢 Microsoft 支援人員，再使用 FullReset 選項。

    Reset-CsPoolRegistrarState -PoolFqdn "atl-cs-001.litwareinc.com" -ResetType FullReset -NoReStart

## 詳細描述

**Reset-CsPoolRegistrarState** Cmdlet 可讓您重設登錄器集區的 Windows 虛擬環境服務 (FabricHostSvc) 與 Lync Server 登錄器服務 (RtcSrv)；如果集區沒有回應或是無法啟動 (那通常表示登錄器服務將維持停留在「啟動擱置」狀態)，才需要這樣做。根據預設，執行此 Cmdlet 會停止該狀態，然後重新啟動集區上的所有相關服務。但是，您可以使用 NoReStart 參數，不需要將那些服務重新啟動，就能讓 **Reset-CsPooRegistrarState** Cmdlet 停止那些服務。接著，您可以選擇手動重新啟動所有 (或部分) 前述服務。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Reset-CsPoolRegistrarState"}

**Lync Server 控制台：** **Reset-CsPoolRegistrarState** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p><em>PoolFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>重設之登錄器集區的完整網域名稱。例如：</p>
<p>-PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
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
<td><p><em>MachineFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>要從集區中移除之電腦的完整網域名稱。只有在執行 MachineStateRemoved 重設時，才能使用這個參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>NoReStart</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指定時，就不會重新啟動在 Cmdlet 執行時處於停止的服務 (例如 RtcSrv 與 FabricHostSvc)。</p></td>
</tr>
<tr class="even">
<td><p><em>ResetLocalDatabases</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指定時，除了本機 Lync Server 服務之外，本機 Lync Server 資料庫也會在停止後重新啟動。</p></td>
</tr>
<tr class="odd">
<td><p><em>ResetType</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Hadr.ResetPoolFabricStateCmdlet+PoolResetType</p></td>
<td><p>要執行的重設類型。允許的值為：</p>
<p>* <strong>ServiceReset</strong> – RtcSrv 與 fabricHostSvc 服務停止並重新啟動。如果未指定 <code>ResetType</code>，就會執行服務重設。</p>
<p>* <strong>QuorumLossRecovery</strong> – 針對任何目前處於仲裁遺失狀態的路由群組從備份存放區重新載入使用者資料。(當資料庫或其複本均無法使用時，就會發生仲裁遺失)。當您執行此重設類型時，可能會遺失尚未寫入資料庫的資料。</p>
<p><code>QuorumLossRecovery</code> 選項可協助您的集區從複製層級仲裁遺失復原，但若要其成功運作，集區不能處於集區層級仲裁遺失更嚴重的層級。如需更多資訊，請參閱<a href="lync-server-2013-topologies-and-components-for-front-end-servers-instant-messaging-and-presence.md">Lync Server 2013 中的前端伺服器、立即訊息及顯示狀態的拓撲和元件</a>。</p>
<p>* <strong>FullReset</strong> – 與 <code>QuorumLossRecovery</code> 執行的重設類型相同，此外還會重新建立本機 Lync Server 資料庫。此重設類型可能會花費很長的時間並佔用大量資源。只有在您將集區中 前端伺服器 的數字變更為像是 2-to-Any、1-to-Any、Any-to-2，或 Any-to-1 時，才使用此選項.. <strong>請勿使用此選項來疑難排解或解決服務啟動問題。</strong></p>
<p>請注意，如果將此 cmdlet 用在 ServiceReset 或 FullReset 選項，將會影響已登入的使用者，不過使用 QuorumLossRecovery 選項則不會影響到使用者。</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>嘗試重新啟動集區時使用 FullReset 選項有時會造成失敗，使得集區無法確實重新啟動。因為這個原因，建議您先使用其中一個其他 ResetType 選項嘗試重新啟動集區。如果還是失敗，請先洽詢 Microsoft 支援人員，再使用 FullReset 選項。通常 FullReset 只有在將拓撲從單一前端伺服器集區變更為多前端伺服器集區時使用。</td>
</tr>
</tbody>
</table>

</div>
<p><code>* MachineStateRemoved</code> -- 從集區中移除指定的伺服器。只有在有問題的伺服器 (或其資料庫) 永久遺失時，才能使用此重設類型。</p></td>
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

無。 **Reset-CsPoolRegistrarState** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

字串值。 **Reset-CsPoolRegistrarState** Cmdlet 不會傳回物件。

## 請參閱

#### 其他資源

[Get-CsPoolFabricState](get-cspoolfabricstate.md)

