---
title: Move-CsManagementServer
TOCTitle: Move-CsManagementServer
ms:assetid: bcead113-fbd2-4fcf-ae01-6a312511ceef
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412921(v=OCS.15)
ms:contentKeyID: 49292139
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Move-CsManagementServer

 

_**上次修改主題的時間：** 2015-03-09_

在集區之間移動 中央管理伺服器。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Move-CsManagementServer [-ConfigurationFileName <String>] [-LisConfigurationFileName <String>] [-TargetFqdn <Fqdn>] <COMMON PARAMETERS>

    Move-CsManagementServer [-TargetFqdn <Fqdn>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將 中央管理伺服器從原本的集區移動到新集區。若要執行此即時移轉 (亦即移動連線且可使用的 中央管理伺服器)，必須從伺服器將移至的集區中的電腦上執行命令。

    Move-CsManagementServer

## 範例 2

範例 2 是在災害復原的案例中移動 中央管理伺服器；也就是在現有管理伺服器已離線或無法使用的狀況下。若要執行此類移轉，必須從伺服器將移至的集區中的電腦上執行前述的命令。此外，您必須使用 ConfigurationFileName 參數匯入您先前儲存的組態備份檔案；使用 LisConfigurationFileName 參數匯入您先前儲存的 E9-1-1 備份檔案 (若您使用 E9-11)；以及 Force 參數在即使無法與現有伺服器連線的狀況下強制移轉 中央管理伺服器。

    Move-CsManagementServer -ConfigurationFileName "C:\CsConfiguration.zip" -LisConfigurationFileName "C:\CsLisConfiguration.zip" -Force

## 詳細描述

**Move-CsManagementServer** Cmdlet 讓系統管理員可將 中央管理伺服器 (及其隨附的 中央管理存放區) 從一個集區移動到另一個集區。因為在移動 中央管理伺服器時資料隨時可能遺失 (更別說服務中斷)，建議您不要進行這項移動，除非：

1\. 您必須淘汰現有的管理集區，而這麼做之前必須移轉 中央管理伺服器。

2\. 您遇到災害復原的案例，現有 中央管理伺服器已無法再使用。

在您移動 中央管理伺服器之前，必須執行下列作業：

1\. 確認已建立新的 中央管理存放區。作法是執行 **Install-CsDatabase** Cmdlet 搭配 CentralManagementDatabase 參數。

2\. 如果您要將 中央管理伺服器移至 Standard Edition 伺服器，請確認您已使用本機設定來執行 \[準備 Standard Edition 伺服器\] 選項。您必須進行這項事先準備作業以新增防火牆規則，這類規則將允許 Windows PowerShell 遠端存取新的 中央管理存放區。

3\. 確認要執行 **Move-CsManagementServer** Cmdlet 以容納 中央管理伺服器的電腦上有足夠的可用磁碟空間。

4\. 確認執行 **Move-CsManagementServer** Cmdlet 的電腦上已安裝前端伺服器服務。如果尚未安裝此服務，而又執行此 Cmdlet，則移動將會失敗。

5\. 確認您可以在將執行 **Move-CsManagementServer** Cmdlet 的電腦上成功執行 **Enable-CsTopology** Cmdlet。如果 **Enable-CsTopology** Cmdlet 無法在該電腦上執行，則移動將會失敗，而您將無法擁有正常運作的 中央管理存放區。

完成這些步驟之後，要將 中央管理伺服器從集區 A 移至集區 B，只需要登入集區 B 的電腦，然後呼叫不含任何其他參數的 **Move-CsManagementServer** Cmdlet：

Move-CsManagementServer

當您這麼做時， **Move-CsManagementServer** Cmdlet 會查閱拓撲以判斷 中央管理伺服器原先的位置 (集區 A)，然後將 中央管理伺服器和 中央管理存放區移轉到目前的集區 (集區 B)。

如果移動成功， **Move-CsManagementServer** Cmdlet 會在螢幕上顯示一份電腦清單。為了完成移動，您必須在列出的每一部電腦上執行本機設定。集區 A 中的電腦仍會繼續執行 中央管理服務的非使用中版本；執行本機設定將刪除該服務。在集區 B 中，已將 中央管理伺服器移至其上的電腦將會執行 中央管理服務；但集區中的其他電腦則不會執行。在這些電腦上執行本機設定將會安裝 中央管理服務。

若要在災害復原案例中移轉 中央管理伺服器，理想的狀況下您應該已經使用 **Export-CsConfiguration** Cmdlet 和 **Export-CsLisConfiguration** Cmdlet，分別建立 Lync Server 組態和增強型 9-1-1 (E9-1-1) 組態的備份檔案 (因為災害總是無預警發生，所以您應該定期執行這些 Cmdlet 並製作組態設定的備份檔案)。呼叫 **Move-CsManagementServer** Cmdlet 時，應該同時加上 ConfigurationFileName 和 LisConfigurationFileName 參數，以便讀取這些備份檔案。

每當您試圖移動離線或無法存取的 中央管理伺服器時，也必須加上 Force 參數。當您呼叫 **Move-CsManagementServer** Cmdlet 時，Cmdlet 會在移動 中央管理存放區前，將它暫時設為唯讀；這樣有助於保護資料以防遺失。但是，在災害復原案例中，無法將 中央管理存放區標示為唯讀。Force 參數會指示 Cmdlet 移動 中央管理存放區，即使並未將它設為唯讀也一樣。

如果 **Move-CsManagementServer** Cmdlet 失敗，則您可能會發現自己正處於 中央管理伺服器無法正常運作的狀況。若要還原 中央管理伺服器，您需要修正導致 **Move-CsManagementServer** Cmdlet 失敗的問題，然後重新執行此 Cmdlet。這次的重新執行可在新集區或舊集區上執行。如果您在舊集區上執行 **Move-CsManagementServer** Cmdlet，將能有效取消移動，並保留原來的組態。

請注意， **Move-CsManagementServer** Cmdlet 必須在本機執行，無法從遠端管理工作階段呼叫。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Move-CsManagementServer** Cmdlet：RTCUniversalServerAdmins。您也必須是執行此 Cmdlet 之電腦上的本機系統管理員。

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
<td><p><em>ConfigurationFileName</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>執行 <strong>Export-CsConfiguration</strong> Cmdlet 所建立的 Lync Server 組態備份檔案的完整路徑。只有在災害復原的案例才使用此參數。</p></td>
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
<td><p>強制 中央管理伺服器移動，即使現有存放區已離線；在災害復原的案例中必須使用此參數。請注意，當您強制移動 中央管理伺服器，隨時都有遺失資料的可能性。</p>
<p>如果您先前嘗試呼叫 <strong>Move-CsManagementServer</strong> Cmdlet 失敗，那麼也可以使用 Force 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>LisConfigurationFileName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>執行 <strong>Export-CsLisConfiguration</strong> Cmdlet 所建立的 E9-1-1 備份檔案的完整路徑。只有在災害復原的案例才使用此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\MoveManagementServer.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>TargetFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>管理伺服器應移至之目的地集區的完整網域名稱。</p></td>
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

無。 **Move-CsManagementServer** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。 **Move-CsManagementServer** Cmdlet 不會傳回任何物件。

## 請參閱

#### 其他資源

[Set-CsManagementServer](set-csmanagementserver.md)

