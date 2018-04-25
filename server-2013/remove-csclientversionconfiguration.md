---
title: Remove-CsClientVersionConfiguration
TOCTitle: Remove-CsClientVersionConfiguration
ms:assetid: 42065d1d-a0ef-4fa4-826b-d65b14b343c9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425925(v=OCS.15)
ms:contentKeyID: 49290729
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsClientVersionConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除指定的用戶端版本組態設定集合。用戶端版本組態設定可指定 Lync Server 是否要檢查登入系統之每個用戶端應用程式的版本號碼。如有啟用用戶端版本篩選，則該用戶端應用程式能否存取系統，將由相關用戶端版本原則中設定決定。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsClientVersionConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會刪除 Identity 為 "site:Redmond" 的用戶端版本組態設定。

    Remove-CsClientVersionConfiguration -Identity site:Redmond

## 範例 2

範例 2 會刪除在網站範圍套用的所有用戶端版本組態設定。為達成此目的，命令會先呼叫 **Get-CsClientVersionConfiguration** Cmdlet 搭配 Filter 參數；篩選值 "site:\*" 可確保只會傳回 Identity 開頭為字串值 "site:" 的用戶端版本組態設定。然後再將篩選後的集合管線傳送到 **Remove-CsClientVersionConfiguration** Cmdlet，以刪除集合中的每一個項目。

    Get-CsClientVersionConfiguration -Filter site:* | Remove-CsClientVersionConfiguration

## 範例 3

在範例 3 中，所有目前停用的用戶端版本組態設定皆會刪除。為達成此目的，命令會先使用 **Get-CsClientVersionConfiguration** Cmdlet 傳回組織目前使用之所有用戶端版本組態設定的集合。傳回此資料後，再將該集合管線傳送到 **Where-Object** Cmdlet，這會只挑出 Enabled 屬性等於 False 的設定。接著將篩選後的集合管線傳送到 **Remove-CsClientVersionConfiguration** Cmdlet，以刪除集合中的每個項目。

    Get-CsClientVersionConfiguration | Where-Object {$_.Enabled -eq $False} | Remove-CsClientVersionConfiguration

## 詳細描述

Lync Server 讓系統管理員有相當大的彈性空間可指定使用者用來登入系統的用戶端軟體 (以及同樣重要的該軟體版本號碼)。例如，沒有任何技術上的原因非要使用者使用 Lync Server 登入 Lync，也沒有任何一種技術可讓使用者無法使用 Microsoft Office Communicator 2007 R2 登入。

然而，也可能是一些非技術上的原因造成您不想要使用者使用 Office Communicator 2007 R2 登入。例如，Office Communicator 2007 R2 並不支援 Lync 中所有的功能，因此使用 Office Communicator 2007 R2 登入的使用者其使用經驗，會與使用 Lync 登入的使用者不同。這會對您的使用者造成一些困擾；也對服務台人員造成困擾，因為他們必須支援許多不同的用戶端應用程式。

您的組織如有此問題，可以運用用戶端版本篩選功能，指定可用於登入 Lync Server 的用戶端應用程式。當您安裝 Lync Server 時，會安裝並啟用一組全域用戶端版本組態設定。除了全域設定之外，也會在網站範圍套用用戶端版本組態設定。

任何您建立的網站設定日後皆可使用 **Remove-CsClientVersionConfiguration** Cmdlet 加以刪除。請注意，您也可以對全域設定執行 **Remove-CsClientVersionConfiguration** Cmdlet。在此狀況下不會移除全域設定，而是將全域範圍屬性重設為預設值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsClientVersionConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsClientVersionConfiguration"}

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
<td><p>要移除之用戶端版本組態設定集合的唯一識別碼。若要移除全域集合，請使用下列語法：-Identity global。(請記住，全域設定並不是真正的移除，而是將全域範圍屬性全部重設回其預設值)。若要移除網站集合，請使用類似下列的語法：-Identity site:Redmond。請注意，如有指定 Identity，即無法使用萬用字元。</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration 物件。**Remove-CsClientVersionConfiguration** Cmdlet 接受用戶端版本組態物件管線傳送的執行個體。

## 傳回類型

無。反之，此 Cmdlet 會刪除 Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsClientVersionConfiguration](get-csclientversionconfiguration.md)  
[New-CsClientVersionConfiguration](new-csclientversionconfiguration.md)  
[Set-CsClientVersionConfiguration](set-csclientversionconfiguration.md)

