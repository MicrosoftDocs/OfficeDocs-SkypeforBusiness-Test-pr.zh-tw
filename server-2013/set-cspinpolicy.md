---
title: Set-CsPinPolicy
TOCTitle: Set-CsPinPolicy
ms:assetid: f0e1afb9-4c71-45c5-8093-6cd12db3d697
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412997(v=OCS.15)
ms:contentKeyID: 49292759
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPinPolicy

 

_**上次修改主題的時間：** 2015-03-09_

修改一或多項現有的用戶端個人識別碼 (PIN) 原則。PIN 驗證讓使用者在存取 Lync Server 時只需提供 PIN 而無須提供使用者名稱與密碼。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsPinPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsPinPolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AllowCommonPatterns <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-MaximumLogonAttempts <UInt32>] [-MinPasswordLength <UInt32>] [-PINHistoryCount <UInt64>] [-PINLifetime <UInt64>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會修改指派給 Redmond 網站的 PIN 原則。在此案例中，命令會將 MinPasswordLength 屬性值變更為 10；這表示新的 PIN 至少必須包含 10 個數字。

    Set-CsPinPolicy -Identity site:Redmond -MinPasswordLength 10

## 範例 2

範例 2 會修改 Identity 為 RedmondUsersPinPolicy 之個別使用者 PIN 原則的兩個屬性：它會變更 MinPasswordLength 與 AllowCommonPatterns 屬性的值。

    Set-CsPinPolicy -Identity RedmondUsersPinPolicy -MinPasswordLength 10 -AllowCommonPatterns $True

## 範例 3

範例 3 所示的命令會變更設定供組織使用之所有 PIN 原則的 MinPasswordLength 值。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsPinPolicy** Cmdlet，以擷取所有現有 PIN 原則的集合。然後，此集合會以管線傳送到 **Set-CsPinPolicy** Cmdlet，這會修改集合中每個原則的 MinPasswordLength 屬性值。

    Get-CsPinPolicy | Set-CsPinPolicy -MinPasswordLength 10

## 詳細描述

Lync Server 可讓使用者連線至系統，或透過電話加入公用交換電話網路 (PSTN) 會議。一般說來，在登入系統或加入會議時，使用者必須輸入使用者名稱和密碼。然而很遺憾地，如果您使用的是沒有英數字元鍵盤的電話，輸入使用者名稱和密碼將會是一大難題。基於上述考量，Lync Server 可讓您將僅由數字組成的 PIN 提供給使用者。當出現提示時，使用者只要輸入 PIN 便能登入系統或加入會議，完全不需要使用者名稱和密碼。

Lync Server 使用用戶端 PIN 原則來管理 PIN 驗證屬性。例如，您可以指定 PIN 號碼的長度下限，以及決定是否將允許使用「共同模式」(例如，連續數字) 的 PIN (例如，像是 123456 的 PIN)。PIN 原則可以在全域、網站或個別使用者範圍設定；您可以使用 **Set-CsPinPolicy** Cmdlet 修改這些原則的屬性。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsPinPolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPinPolicy"}

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
<td><p><em>AllowCommonPatterns</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示是否允許在 PIN 中使用「共同模式」。共同模式包括重複的數字 (225577)、4 或多個連續的數字 (991234)，以及和使用者電話號碼或分機號碼相同的 PIN。如果設為 True ($True)，表示允許使用共同模式 (例如，包含連續數字的 PIN 碼 123456)；如果設為 False ($False)，表示不允許使用共同模式。預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓系統管理員提供隨附於 PIN 原則的其他文字。例如，Description 可包含應指派原則的使用者資訊。</p></td>
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
<td><p>建立原則時指派給原則的唯一識別碼。PIN 原則可以在全域、網站、個別使用者範圍內加以指派。若要參考全域執行個體，請使用下列語法：-Identity global。若要在網站範圍內參照原則，請使用類似下列的語法：-Identity site:Redmond。若要參考個別使用者原則，請使用類似下列的語法：-Identity RedmondPinPolicy。</p>
<p>若未指定 Identity，則 <strong>Set-CsPinPolicy</strong> Cmdlet 將會修改全域原則。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>UserPinPolicy 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaximumLogonAttempts</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>表示允許的連續登入失敗次數，超過此次數，就會自動鎖定使用者的 PIN。登入失敗會以下列兩種方式來計數：本機登入失敗和全域登入失敗。當使用者首次嘗試登入時，會開始一個新的 30 分鐘觀察期間；在那 30 分鐘期間執行的每一次登入失敗都會記錄為本機登入失敗和全域登入失敗。如果使用者在那 30 分鐘之觀察視窗執行期間到達 MaximumLogonAttempts，則系統將暫時鎖定該使用者一個小時；在此期間，即使使用者提供正確的 PIN，還是無法使用 PIN 驗證來登入。</p>
<p>當鎖定期間過期之後，使用者的本機登入嘗試次數將重設為 0。但是，使用者的全域登入嘗試次數將不會重設。如果使用者持續登入失敗，最後將會到達允許的全域登入嘗試次數上限。任何到達該點之使用者的 PIN 將遭到系統鎖定，在系統管理員解除鎖定該 PIN 之前，將無法使用 PIN 驗證。</p>
<p>允許的登入嘗試次數上限會根據 PIN 大小而有所不同；這就是為什麼 MaximumLogonAttempts 屬性不會在您執行 <strong>Get-CsPinPolicy</strong> Cmdlet 時顯示預設值。根據預設，若 PIN 長度為 4，可允許使用者進行 10 次本機登入嘗試和 100 次全域登入嘗試。若 PIN 長度為 5，則允許 25 次本機登入嘗試和 1000 次全域登入嘗試；若 PIN 長度大於 6，便允許 25 次本機嘗試和 5000 次全域嘗試。如果指定了 MaximumLogonAttempts 內容值，該值將用來做為本機登入嘗試次數的允許次數上限；但是，不論指派給 MaximumLogonAttempts 的值為何，全域登入值都不會變更。</p>
<p>每當使用者使用 PIN 驗證成功登入時，本機失敗的登入嘗試次數即會重設為 0。全域登入嘗試次數只有在系統管理員解除鎖定使用者的 PIN 時才會重設。</p>
<p>MaximumLogonAttempts 可以設為 1 和 999 (含) 之間的任何整數。但是建議您不要修改此屬性。設為 Null 值 (預設值) 時， Lync Server 2013會自動計算封鎖原則。這麼做通常可提供最高層級的安全性。</p></td>
</tr>
<tr class="even">
<td><p><em>MinPasswordLength</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>允許的 PIN 號碼長度下限 (即最少位數)。例如，如果將 MinPasswordLength 設為 8，則 PIN 號碼 1259 將會遭到拒絕，因為這個 PIN 只有 4 位數。PIN 長度至少必須有 4 位數，但不得大於 24 位數；預設值為 5。</p></td>
</tr>
<tr class="odd">
<td><p><em>PINHistoryCount</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt64</p></td>
<td><p>表示使用者能重複使用相同 PIN 的頻率。例如，如果將 PINHistoryCount 設為 3，則使用者在前三次重設 PIN 時都必須使用新的 PIN，在第四次重設時便能使用第一個 PIN (在第五次重設時能重述使用第二個 PIN，依此類推)。PIN 歷程記錄計數可以是任何介於 0 到 20 之間 (包括 0 和 20) 的整數；0 表示使用者能反覆使用相同的 PIN。根據預設，PINHistoryCount 設為 0。</p>
<p>如果將 PINLifetime 設為任何大於 0 的值，則 PINHistoryCount 也必須大於 0。例如，您無法將 PINLifetime 設為 30，但讓 PINHistoryCount 維持 0。</p></td>
</tr>
<tr class="even">
<td><p><em>PINLifetime</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt64</p></td>
<td><p>表示 PIN 的有效時間長度 (以天為單位)。當 PIN 存留期到期後，使用者必須先選取新的 PIN，才能使用 PIN 驗證取得系統的存取權限。您可以將 PINLifetime 設為任何介於 0 到 999 之間 (包括 0 和 999) 的整數。0 表示 PIN 永遠不會到期。根據預設，PIN 存留期設為 0 天。</p>
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

Microsoft.Rtc.Management.WritableConfig.Policy.UserPin.UserPolicy 物件。**Set-CsPinPolicy** Cmdlet 會接受 PIN 原則物件以管線傳送的資料。

## 傳回類型

**Set-CsPinPolicy** Cmdlet 不會傳回值或物件，而會設定一或多個 Microsoft.Rtc.Management.WritableConfig.Policy.UserPin.UserPolicy 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsPinPolicy](get-cspinpolicy.md)  
[Grant-CsPinPolicy](grant-cspinpolicy.md)  
[New-CsPinPolicy](new-cspinpolicy.md)  
[Remove-CsPinPolicy](remove-cspinpolicy.md)

