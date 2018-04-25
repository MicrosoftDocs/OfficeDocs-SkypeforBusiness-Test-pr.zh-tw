---
title: Remove-CsConfigurationStoreLocation
TOCTitle: Remove-CsConfigurationStoreLocation
ms:assetid: 141be225-c6e4-4377-913b-ba61528929d4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398214(v=OCS.15)
ms:contentKeyID: 49290170
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConfigurationStoreLocation

 

_**上次修改主題的時間：** 2015-03-09_

移除中央管理存放區的 Active Directory 服務控制點。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsConfigurationStoreLocation [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會移除 中央管理存放區 的 Active Directory 服務控制點。若要還原此 SCP (或建立新的 SCP)，您必須執行 **Set-CsConfigurationStoreLocation** Cmdlet。

    Remove-CsConfigurationStoreLocation

## 範例 2

範例 2 也移除了 中央管理存放區 的 Active Directory 服務控制點。除了刪除 SCP 外，此命令會將作業成功 (或失敗) 的資訊儲存在 C:\\Logs\\Store\_Location.html 記錄檔。為了建立此記錄檔，命令會使用 Report 參數，後面再加上應記錄資訊的記錄檔路徑。如果此檔案已存在，則當命令執行時會覆寫檔案的內容。如果檔案不存在，則當命令執行時會建立該檔案。

    Remove-CsConfigurationStoreLocation -Report C:\Logs\Store_Location.html

## 詳細描述

Active Directory 網域服務 會使用服務控制指標 (SCP) 來協助電腦尋找服務。例如，安裝 Lync Server 時，系統會建立 SCP，提供有關 中央管理存放區 的位置資訊，以保留 Lync Server 資料。需要存取資料庫的電腦會連線至 Active Directory，並使用 SCP 中包含的資訊來協助它們找到正確的電腦，以及正確的 SQL Server 執行個體。

如上所述，當您安裝 Lync Server 時，系統會自動為您建立中央管理存放區的 SCP。通常您不會刪除此 SCP，如果您刪除，電腦將無法找到該資料庫。但是，有時候您必須刪除 SCP (當疑難排解問題時或許需要刪除)。若要執行該作業，請使用 **Remove-CsConfigurationStoreLocation** Cmdlet。在刪除 SCP 後，您可以使用 **Set-CsConfigurationStoreLocation** Cmdlet 重新建立 SCP (或建立新的服務控制點)。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsConfigurationStoreLocation** Cmdlet：RTCUniversalServerAdmins。

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
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>儲存全域設定之網域控制器的完整網域名稱 (FQDN)。如果全域設定是儲存在 Active Directory 的系統容器內，則此參數必須導向根網域控制器。如果全域設定儲存在組態容器中，則會使用任何一個網域控制站，且會省略此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\ConfigurationStore.html&quot;</p></td>
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

無。**Remove-CsConfigurationStoreLocation** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Remove-CsConfigurationStoreLocation** Cmdlet 不會傳回任何物件或值。

## 請參閱

#### 其他資源

[Get-CsConfigurationStoreLocation](get-csconfigurationstorelocation.md)  
[Set-CsConfigurationStoreLocation](set-csconfigurationstorelocation.md)

