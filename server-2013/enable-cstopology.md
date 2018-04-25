---
title: Enable-CsTopology
TOCTitle: Enable-CsTopology
ms:assetid: 5aedffa0-9ca1-4aec-b4ad-c3e409c0ffb2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398398(v=OCS.15)
ms:contentKeyID: 49291026
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Enable-CsTopology

 

_**上次修改主題的時間：** 2015-03-09_

啟用最近發佈的 Lync Server 拓撲。您如有變更拓撲，必須發佈這些變更並加以啟用，變更才會生效。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Enable-CsTopology [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-SkipPrepareCheck <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會啟用最近發佈的拓撲。

    Enable-CsTopology

## 詳細描述

安裝 Lync Server 後，您最終必須變更基礎結構。例如，您可能需要新增網站、刪除現有的登錄器集區或新增其他封存伺服器。您必須使用拓撲產生器完成這些基礎結構變更。在拓撲產生器中完成變更後，接下來便能使用相同的工具來發佈及啟用變更。後面的這兩個步驟相當重要：儘管您可以使用拓撲產生器視需求做出修改，不過在發佈及啟用新拓撲之前這些修改並不會生效，而您的基礎結構也不會變更。

雖然在發佈變更時，系統會將新資訊 (例如，新網站或新伺服器角色) 寫入中央管理存放區。不過這些新物件 (或新修改的物件) 並不會立即加入您的拓撲中，而是必須等到更新過的拓撲啟用後才會加入。如果您在拓撲產生器中選取 \[發佈\] 選項，會同時執行下列這兩個步驟：發佈變更 (寫入中央管理存放區)，然後再啟用新拓撲。

不過，有時候您可能會想要以單獨的步驟發佈變更並啟用拓撲；這樣做可讓您在將新物件導入拓撲前，有機會確認部署是否已成功。若要分別發佈然後啟用拓撲變更，您必須執行下列步驟：

發佈在拓撲產生器中修改過的拓撲 (由於太晚進行產品變更，我們建議您一律使用拓撲產生器進行發佈)。

使用 **Enable-CsTopology** Cmdlet 使發佈後的變更生效。

有時候，您可能也需要呼叫 **Enable-CsTopology** Cmdlet，才能啟用在拓撲產生器之外所做的變更。例如，在您使用 CsKerberosAccountAssignment Cmdlet 修改 Kerberos Web 驗證之後，必須執行該 Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Enable-CsTopology** Cmdlet：RTCUniversalServerAdmins。但是，如果尚未委派安裝權限，則您必須是網域管理員才能執行該 Cmdlet。為了授與 RTCUniversalServerAdmins 實際使用 **Enable-CsTopology** Cmdlet 的權限，您必須針對包含執行 Lync Server 服務之電腦的每個 Active Directory 容器執行 **Grant-CsSetupPermission** Cmdlet。請注意，此限制也適用於透過拓撲產生器啟用拓撲。如果您尚未使用 **Grant-CsSetupPermission** Cmdlet 委派權限，則只有網域管理員才能透過拓撲產生器啟用拓撲。

此外，您必須在要建立 Lync Server 檔案共用的任何電腦上具有本機系統管理員身分，才能對共用資料夾設定必要的安全性權限。或者，如果您擁有檔案共用的完整控制權，則可執行 **Enable-CsTopology** Cmdlet。如此可讓該 Cmdlet 建立共用資料夾，並設定共用層級的安全性權限。但是，接下來本機系統管理員必須新增共用層級的安全性權限。

若要驗證已指派的安裝權限，請針對包含執行 Lync Server 服務之電腦的任何 Active Directory 容器執行 **Test-CsSetupPermission** Cmdlet。

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
<td><p><em>GlobalCatalog</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>網域中通用類別目錄伺服器的完整網域名稱 (FQDN)。如果您執行 <strong>Enable-CsTopology</strong> Cmdlet 的電腦帳戶是在您的網域中，就不需要此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>儲存全域設定之網域控制站的 FQDN。如果全域設定是儲存在 Active Directory 網域服務 的系統容器內，則此參數必須導向根網域控制器。如果全域設定儲存在組態容器中，則會使用任何一個網域控制站，且會省略此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\Enable_Topology.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>SkipPrepareCheck</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果設為 True ($True)，則 <strong>Enable-CsTopology</strong> Cmdlet 會略過其初始準備檢查。</p></td>
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

無。**Enable-CsTopology** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。反之，**Enable-CsTopology** Cmdlet 會啟用 Microsoft.Rtc.Management.Deploy.Internal.DefaultTopology 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsTopology](get-cstopology.md)  
[Grant-CsSetupPermission](grant-cssetuppermission.md)  
[Publish-CsTopology](publish-cstopology.md)  
[Test-CsSetupPermission](test-cssetuppermission.md)  
[Test-CsTopology](test-cstopology.md)

