---
title: Get-CsPinPolicy
TOCTitle: Get-CsPinPolicy
ms:assetid: 1d627ba5-6333-466c-82a1-859deaf8d690
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398262(v=OCS.15)
ms:contentKeyID: 49290278
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPinPolicy

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定供組織使用之用戶端個人識別碼 (PIN) 原則的資訊。PIN 驗證讓使用者在存取 Lync Server 時只需提供 PIN 而無須提供使用者名稱與密碼。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsPinPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsPinPolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定供組織使用之所有 PIN 原則的集合。呼叫不含任何參數的 **Get-CsPinPolicy** Cmdlet 一律會傳回一組完整的 PIN 原則。

    Get-CsPinPolicy

## 範例 2

範例 2 會傳回單一 PIN 原則：Identity 為 site:Redmond 的原則。

    Get-CsPinPolicy -Identity "site:Redmond"

## 範例 3

範例 3 所示的命令會使用 Filter 參數傳回所有已在個別使用者範圍設定的原則。作法是使用篩選值 "tag:\*"，此值可指示 **Get-CsPinPolicy** Cmdlet 只傳回 Identity 開頭為字元 "tag:" 的原則。

    Get-CsPinPolicy -Filter "tag:*"

## 範例 4

範例 4 會傳回所有 AllowCommonPatterns 內容為 True 的 PIN 原則。此範例會先呼叫不含任何參數的 **Get-CsPinPolicy** Cmdlet，傳回設定供組織使用之所有 PIN 原則的集合。然後再將該集合傳遞至 **Where-Object** Cmdlet，這會只挑出 AllowCommonPatterns 屬性等於 True 的原則。

    Get-CsPinPolicy | Where-Object {$_.AllowCommonPatterns -eq $True}

## 範例 5

與範例 4 相同，範例 5 所示的命令會使用 **Where-Object** Cmdlet 傳回現有 PIN 原則的子集。在此範例中， **Where-Object** Cmdlet 只會擷取 PinLifetime 屬性大於 30 的原則。也就是說，只會傳回 PIN 到期時間大於 30 天的原則。

    Get-CsPinPolicy | Where-Object {$_.PinLifetime -gt 30}

## 詳細描述

Lync Server 可讓使用者連線至系統，或透過電話加入公用交換電話網路 (PSTN) 會議。一般說來，在登入系統或加入會議時，使用者必須輸入使用者名稱和密碼。然而很遺憾地，如果您使用的是沒有英數字元鍵盤的電話，輸入使用者名稱和密碼將會是一大難題。基於上述考量，Lync Server 可讓您將僅由數字組成的 PIN 提供給使用者。當出現提示時，使用者只要輸入 PIN 便能登入系統或加入會議，完全不需要使用者名稱和密碼。

Lync Server 使用 PIN 原則來管理 PIN 驗證屬性。例如，您可以指定 PIN 的長度下限，以及決定是否將允許使用「共同模式」(例如，連續數字) 的 PIN (例如，像是 123456 的 PIN)。您可以使用 **Get-CsPinPolicy** Cmdlet 擷取設定為目前要在組織內使用之 PIN 原則的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsPinPolicy** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPinPolicy"}

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
<td><p>System.Strkng</p></td>
<td><p>可讓您針對 PIN 原則進行萬用字元搜尋。例如，若要在網站範圍尋找設定的所有原則，請使用下列 Filter：site:*。若要尋找網站原則 Seattle、Seville 以及 Saskatoon (開頭皆為字母 &quot;S&quot;)，請使用此篩選：site:S*。請注意，此參數只能依據 Identity 內容來篩選。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>在建立原則時要指派給它的唯一 Identity。PIN 原則可以在全域、網站或個別使用者範圍指派。若要參考全域執行個體，請使用下列語法：-Identity global。若要參考網站範圍的原則，請使用以下的語法：-Identity site:Redmond。若要在每個使用者範圍上參考原則，請使用類似下列的語法：-Identity RedmondPolicy.</p>
<p>Identity 參數不能使用萬用字元，例如星號 (*)。若要以萬用字元搜尋原則，請改用 Filter 參數。</p>
<p>若未指定 Identity 或 Filter 參數， <strong>Get-CsPinPolicy</strong> Cmdlet 會傳回設定供組織使用之所有 PIN 原則的資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區的本機複本擷取 PIN 原則資料，而非從 中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsPinPolicy** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsPinPolicy** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Policy.UserPin.UserPinPolicy 物件的一或多個執行個體。

## 請參閱

#### 其他資源

[Grant-CsPinPolicy](grant-cspinpolicy.md)  
[New-CsPinPolicy](new-cspinpolicy.md)  
[Remove-CsPinPolicy](remove-cspinpolicy.md)  
[Set-CsPinPolicy](set-cspinpolicy.md)

