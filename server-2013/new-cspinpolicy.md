---
title: New-CsPinPolicy
TOCTitle: New-CsPinPolicy
ms:assetid: d64fb0f9-1cdc-4497-992a-d002abafe92e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398935(v=OCS.15)
ms:contentKeyID: 49292473
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPinPolicy

 

_**上次修改主題的時間：** 2015-03-09_

建立新的用戶端個人識別碼 (PIN) 原則。PIN 驗證讓使用者在存取 Lync Server 時只需提供 PIN 而無須提供使用者名稱與密碼。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsPinPolicy -Identity <XdsIdentity> [-AllowCommonPatterns <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-MaximumLogonAttempts <UInt32>] [-MinPasswordLength <UInt32>] [-PINHistoryCount <UInt64>] [-PINLifetime <UInt64>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會使用 **New-CsPinPolicy** Cmdlet，來建立 Identity 為 site:Redmond 的新 PIN 原則。此命令只包含一個選用參數 MinPasswordLength，此參數可用來將 MinPasswordLength 屬性設為 10。所有剩餘的原則屬性將會使用預設值來設定。

    New-CsPinPolicy -Identity "site:Redmond" -MinPasswordLength 10

## 範例 2

範例 2 所示的命令會建立 Identity 為 site:Redmond 的新原則。此命令使用 MinPasswordLength、PINHistory 及 PINLifetime 等參數，明確地為新原則設定三個不同的內容值。

    New-CsPinPolicy -Identity "site:Redmond" -MinPasswordLength 10 -PINHistoryCount 10 -PINLifetime 30

## 範例 3

範例 3 所示的命令示範如何只在記憶體內建立新的 PIN 原則、修改該原則的屬性值，然後使用 **Set-CsPinPolicy** Cmdlet，將這個只建立於記憶體內的原則轉換成實際的 PIN 原則。在上述命令的第一行中， **New-CsPinPolicy** Cmdlet 搭配 InMemory 參數會用來在記憶體內建立 Identity 為 site:Redmond 的原則；此原則會儲存於變數 $x 中。若未將該原則指派給變數，它便只會建立於記憶體內，當命令完成時，它也會隨即消失。

將虛擬原則指派給變數 $x 後，即會使用後續的三個命令來修改該原則的屬性值。例如，第 2 行會將 MinPasswordLength 屬性值設為 10。完成所有屬性的設定後，會使用 **Set-CsPinPolicy** Cmdlet 來建立 Identity 為 site:Redmond 的實際原則。作法是使用 Instance 參數並傳遞變數 $x 做為參數值。呼叫 **Set-CsPinPolicy** Cmdlet 後，就能使用 **Get-CsPinPolicy** Cmdlet 來檢視原則及其屬性值。

    $x = New-CsPinPolicy -Identity "site:Redmond" -InMemory
    $x.MinPasswordLength = 10
    $x.PINHistoryCount = 10
    $x.PINLifetime = 30
    Set-CsPinPolicy -Instance $x

## 範例 4

範例 4 使用的命令會建立新的 PIN 原則 (site:Paris)，這個新的 PIN 原則會使用可現有原則 site:Redmond 中找到的其中一個屬性值。為達成此目的，第一個命令會使用 **Get-CsPinPolicy** Cmdlet 來擷取 PIN 原則 site:Redmond；然後將針對此原則擷取到的資訊儲存於變數 $x 中。

第二個命令會使用 **New-CsPinPolicy** Cmdlet 來建立原則 site:Paris。此外，MinPasswordLength 參數可用來指定 MinPasswordLength 屬性值。但是，此命令不會使用硬式編碼的數值，而是使用 $x.MinPasswordLength 做為參數值。如此一來，會指示 **New-CsPinPolicy** Cmdlet，將密碼長度下限設為在 site:Redmond 原則中找到的 MinPasswordLength 屬性值。整體效果是將現有原則 site:Redmond 中的 MinPasswordLength 屬性值複製到新原則 site:Paris 中。

    $x = Get-CsPinPolicy -Identity "site:Redmond"
    New-CsPinPolicy -Identity "site:Paris" -MinPasswordLength $x.MinPasswordLength 

## 詳細描述

Lync Server 可讓使用者透過電話連接系統或加入公用交換電話網路 (PSTN) 會議。使用者在登入系統或加入會議時通常會輸入使用者名稱和密碼；但是，如果您使用的是沒有英數字元鍵盤的電話，則輸入使用者名稱和密碼將會是一大難題。基於上述考量， Lync Server 可讓您為使用者提供僅由數字組成的 PIN；出現提示時，使用者只要輸入 PIN 便能登入或加入會議，而不需輸入使用者名稱和密碼。

Lync Server 使用 PIN 原則來管理 PIN 驗證屬性。例如，您可以指定 PIN 的長度下限，以及決定是否將允許使用「共同模式」(例如，連續數字) 的 PIN (例如，像是 123456 的 PIN)。您可以使用 **New-CsPinPolicy** Cmdlet 來建立新的 PIN 驗證原則，可以在網站範圍或個別使用者範圍內設定這些新原則 (除了上述原則之外，還有一個全域 PIN 原則。不過您不能建立第二個全域 PIN 原則，只能修改現有的全域原則)。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsPinPolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPinPolicy"}

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
<td><p>表示要指派給原則的唯一 Identity。您可以在網站範圍或個別使用者範圍內建立 PIN 原則。若要建立網站範圍的原則，請使用類似下列的語法：-Identity site:Redmond。若要在個別使用者範圍建立原則，請使用類似下列的語法：-Identity RedmondPinPolicy。</p></td>
</tr>
<tr class="even">
<td><p><em>AllowCommonPatterns</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示是否允許在 PIN 中使用「共同模式」。共同模式包括重複的數字 (222222)；四或多個連續的數字 (123456)，以及和使用者電話號碼或分機號碼相同的 PIN。如果設為 True，表示允許使用共同模式 (例如，包含連續數字的 PIN 456789)；如果設為 False，表示不允許使用共同模式。預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓系統管理員提供隨附於 PIN 原則的說明文字。例如，Description 可包含被指派原則的使用者相關資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaximumLogonAttempts</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>表示允許的連續登入失敗次數，超過此次數，就會自動鎖定使用者的 PIN。登入失敗會以下列兩種方式來計數：本機登入失敗和全域登入失敗。當使用者首次嘗試登入時，會開啟一個新的 30 分鐘觀察視窗；在那 30 分鐘之視窗執行期間的每一次登入失敗都會記錄為本機登入失敗和全域登入失敗。如果使用者在那 30 分鐘之觀察視窗執行期間到達 MaximumLogonAttempts，則系統將暫時鎖定該使用者一個小時；在此期間，即使使用者提供正確的 PIN，還是無法使用 PIN 驗證來登入。</p>
<p>當鎖定期間過期之後，使用者的本機登入嘗試次數將重設為 0。但是，使用者的全域登入嘗試次數將不會重設。如果使用者持續登入失敗，最後將會到達允許的全域登入嘗試次數上限。任何到達該點之使用者的 PIN 將遭到系統鎖定，在系統管理員解除鎖定該 PIN 之前，將無法使用 PIN 驗證。</p>
<p>允許的登入嘗試次數上限會根據 PIN 大小而有所不同；這就是為什麼 MaximumLogonAttempts 內容不會在您執行 Get-CsPinPolicy 時顯示預設值。根據預設，若 PIN 長度為 4，可允許使用者進行 10 次本機登入嘗試和 100 次全域登入嘗試。若 PIN 長度為 5，則允許 25 次本機登入嘗試和 1000 次全域登入嘗試；若 PIN 長度大於 6，便允許 25 次本機嘗試和 5000 次全域嘗試。如果指定了 MaximumLogonAttempts 內容值，該值將用來做為本機登入嘗試次數的允許次數上限；但是，不論指派給 MaximumLogonAttempts 的值為何，全域登入值都不會變更。</p>
<p>每當使用者使用 PIN 驗證成功登入時，本機失敗的登入嘗試次數即會重設為 0。全域登入嘗試次數只有在系統管理員解除鎖定使用者的 PIN 時才會重設。</p>
<p>MaximumLogonAttempts 可以設為 1 和 999 (含) 之間的任何整數。但是建議您不要修改此屬性。設為 Null 值 (預設值) 時， Lync Server 2013會自動計算封鎖原則。這麼做通常可提供最大的安全性。</p></td>
</tr>
<tr class="even">
<td><p><em>MinPasswordLength</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>允許的 PIN 長度下限 (即最少位數)。例如，如果將 MinPasswordLength 設為 8，則 PIN 1259 將會遭到拒絕，因為這個 PIN 只有 4 位數。PIN 長度至少必須有 4 位數，但不得大於 24 位數；預設值為 5。</p></td>
</tr>
<tr class="odd">
<td><p><em>PINHistoryCount</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt64</p></td>
<td><p>表示使用者能重複使用相同 PIN 的頻率。例如，如果將 PINHistoryCount 設為 3，則使用者在前三次重設 PIN 時都必須使用新的 PIN，在第四次重設時便能使用第一個 PIN (在第五次重設時能重複使用第二個 PIN，依此類推)。PIN 歷程記錄計數可以是任何介於 0 到 20 之間 (包括 0 和 20) 的整數；0 表示使用者能反覆使用相同的 PIN 號碼。根據預設，PINHistoryCount 設為 0。</p>
<p>如果將 PINLifetime 設為任何大於 0 的值，則 PINHistoryCount 也必須大於 0。例如，您無法將 PINLifetime 設為 30，但讓 PINHistoryCount 維持 0。</p></td>
</tr>
<tr class="even">
<td><p><em>PINLifetime</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt64</p></td>
<td><p>表示 PIN 的有效時間長度 (以天為單位)。當 PIN 存留期到期後，使用者必須先選取新的 PIN 號碼，才能使用 PIN 驗證取得系統的存取權限。您可以將 PINLifetime 設為任何介於 0 到 999 之間 (包括 0 和 999) 的整數。0 表示 PIN 號碼永遠不會到期。根據預設，PIN 存留期設為 0 天。</p>
<p>如果您將 PINLifetime 設為大於 0 的值，則也必須將 PINHistoryCount 設為大於 0 的值。</p></td>
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

無。**New-CsPinPolicy** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Policy.UserPin.UserPolicy 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsPinPolicy](get-cspinpolicy.md)  
[Grant-CsPinPolicy](grant-cspinpolicy.md)  
[Remove-CsPinPolicy](remove-cspinpolicy.md)  
[Set-CsPinPolicy](set-cspinpolicy.md)

