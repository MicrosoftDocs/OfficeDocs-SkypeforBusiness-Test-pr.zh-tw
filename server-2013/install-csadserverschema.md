---
title: Install-CsAdServerSchema
TOCTitle: Install-CsAdServerSchema
ms:assetid: 86e13601-7e80-4276-b176-77d9c6e7d55a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398681(v=OCS.15)
ms:contentKeyID: 49291558
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Install-CsAdServerSchema

 

_**上次修改主題的時間：** 2015-03-09_

擴充 Active Directory 架構，以便於安裝 Lync Server。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Install-CsAdServerSchema [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Ldf <String>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會讀取登錄中的資訊來判斷 .LDF 檔案的位置，然後使用該檔案來更新 Active Directory 架構。

    Install-CsAdServerSchema

## 範例 2

範例 2 會使用取自架構更新檔案 (位於 C:\\Schemas 資料夾) 的資訊來更新 Active Directory 架構。使用 Ldf 參數可以指定此資料夾位置。

    Install-CsAdServerSchema -Ldf "C:\Schemas"

## 詳細描述

雖然 Lync Server 會將大部分的組態資訊儲存在自己的中央管理資料庫中，但軟體也需要使用 Active Directory 網域服務 做為儲存位置；例如使用者相關的資訊會儲存在該使用者的 Active Directory 帳戶中。為達此目的， Lync Server 必須將這些值儲存到不屬於一般 Active Directory 使用者帳戶的屬性中。亦即，您必須「展開」您的 Active Directory 架構，並修改該架構，以新增 Lync Server 所需的自訂屬性 (和其他項目)。

展開 Active Directory 架構最簡單的方法是使用 **Install-CsAdServerSchema** Cmdlet。 **Install-CsAdServerSchema** Cmdlet 通常會隨 Lync Server 安裝程序執行，但如有需要，系統管理員可以隨時執行此 Cmdlet。您可以在 Cmdlet 執行完成之後，接著使用 **Get-CsAdServerSchema** Cmdlet 確認架構是否更新，以及 Active Directory 網域服務是否已經能夠繼續安裝程序的下一個步驟。

請注意， **Install-CsAdServerSchema** Cmdlet 在執行時，必須可以存取架構主機 (管理 Active Directory 物件和屬性定義的操作主機角色)。如果您是在架構主機以外的電腦上執行 **Install-CsAdServerSchema** Cmdlet，裝載架構主機的電腦必須允許遠端電腦對其登錄的存取。若非如此，則您必須在架構主機上執行 **Install-CsAdServerSchema** Cmdlet。

**Install-CsAdServerSchema** Cmdlet 執行的功能與下列 Microsoft Office Communications Server 2007 R2 命令執行的功能類似：

Lcscmd.exe /forest /action:SchemaPrep /SchemaType:Server

誰可以執行這個 Cmdlet：您必須為根網域中的 Active Directory 架構系統管理員，以及架構主機電腦的本機系統管理員，才能在本機執行 **Install-CsAdServerSchema** Cmdlet。

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
<td><p>網域中通用類別目錄伺服器的完整網域名稱 (FQDN)。如果您執行 <strong>Install-CsAdServerSchema</strong> Cmdlet 的電腦帳戶是在您的網域中，就不需要此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>網域中網域控制站的 FQDN。如果您執行 <strong>Install-CsAdServerSchema</strong> Cmdlet 的電腦帳戶是在您的網域中，就不需要此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Ldf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>包含要匯入之 .LDF 檔案的資料夾路徑。.LDF (LDAP 資料交換格式) 檔案包含 Active Directory 架構所需的更新。若未加入此參數， <strong>Install-CsAdServerSchema</strong> Cmdlet 會從登錄中記錄的 Lync Server 安裝路徑尋找檔案。安裝路徑通常是：C:\Program Files\ Microsoft Lync Server 2010\Deployment\Setup。</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\ServerSchema.html&quot;</p></td>
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

無。**Install-CsAdServerSchema** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Install-CsAdServerSchema** Cmdlet 不會傳回任何值或物件。

## 請參閱

#### 其他資源

[Get-CsAdServerSchema](get-csadserverschema.md)

