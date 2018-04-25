---
title: Set-CsRgsConfiguration
TOCTitle: Set-CsRgsConfiguration
ms:assetid: 259cec4c-0152-4c8f-8aa6-51cefc1b55c9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425728(v=OCS.15)
ms:contentKeyID: 49290363
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsRgsConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改回應群組應用程式的組態設定。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsRgsConfiguration -Identity <RgsIdentity> [-AgentRingbackGracePeriod <Int16>] [-DefaultMusicOnHoldFile <AudioFile>] [-DisableCallContext <$true | $false>] <COMMON PARAMETERS>

    Set-CsRgsConfiguration -Instance <ServiceSettings> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會修改在 ApplicationServer:atl-cs-001.litwareinc.com 服務上找到的 回應群組應用程式 組態設定的 AgentRingbackGracePeriod 屬性。在此範例中，AgentRingbackGracePeriod 設為 30 秒。

    Set-CsRgsConfiguration -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -AgentRingbackGracePeriod 30

## 範例 2

範例 2 修改組織中所有回應群組組態設定的 AgentRingbackGracePeriod。為達此目的，命令會先使用 **Get-CsService** Cmdlet 搭配 ApplicationServer 參數，以傳回組織中執行應用程式服務的所有電腦的資訊。然後再將傳回的集合管線傳送到 **Where-Object** Cmdlet，以選取 Applications 內容中包含應用程式 "urn:application:RGS" 的電腦 (此值表示回應群組應用程式在伺服器上執行)。

然後，這些電腦會傳送到 **ForEach-Object** Cmdlet。**ForEach-Object** 接著取得集合中的每一台電腦，並使用 **Set-CsRgsConfiguration** 將電腦回應群組組態設定 r 的 AgentRingbackGracePeriod 值設為 30 秒。

    Get-CsService -ApplicationServer | Where-Object {$_.Applications -contains "urn:application:RGS"} | ForEach-Object {Set-CsRgsConfiguration -Identity $_.Identity -AgentRingbackGracePeriod 30}

## 範例 3

範例 3 所示的命令會匯入音訊檔 (C:\\Media\\WhileYouWait.wav)，然後將該檔案指派給 DefaultMusicOnHoldFile 內容。為了執行這項作業，第一個命令會使用 **Import-CsRgsAudioFile** 將音訊匯入到 ApplicationServer:atl-cs-001.litwareinc.com 上找到的 回應群組應用程式。除了 Identity 參數 (指出服務位置) 外，也會使用 FileName 參數指定要匯入檔案的檔案名稱。

同樣重要的還有 Content 參數，此參數用於匯入音訊檔。執行檔案匯入的做法為呼叫 **Get-Content**，程式後面要加上匯入檔案的路徑。**Get-Content** 也必須將編碼類型設為位元組，將 ReadCount 設定 0 (將 ReadCount 設為 0 可確保以單一作業能讀取整個檔案)。匯入的檔案會儲存在名為 $x 的變數中。

匯入檔案之後，呼叫 **Set-CsRgsConfiguration** 以便將 DefaultMusicOnHoldFile 屬性設為 $x 中儲存的音訊檔。

    $x = Import-CsRgsAudioFile -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -FileName "WhileYouWait.wav" -Content (Get-Content C:\Media\WhileYouWait.wav -Encoding byte -ReadCount 0)
    
    Set-CsRgsConfiguration -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -DefaultMusicOnHoldFile $x

## 詳細描述

回應群組應用程式 能讓您將來電自動路由傳送到如服務台或客戶支援專線等實體。當某人撥打指定的電話號碼，可將該來電自動路由傳送到適當的回應群組代理集合。或者，來電可能會路由傳送到互動語音回應 (IVR) 佇列。在該佇列中，系統會詢問來電者一系列問題 (例如「您是否為了現有訂單來電？」)，然後依據這些問題的回答給予要求的資訊，或路由傳送到回應群組代理。

**Set-CsRgsConfiguration** Cmdlet 讓您能夠修改 回應群組應用程式 執行個體的屬性。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsRgsConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsRgsConfiguration"}

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
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>託管回應群組組態設定的服務名稱。例如：-Identity &quot;service:ApplicationServer:atl-cs-001.litwareinc.com.&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.ServiceSettings</p></td>
<td><p>要修改之回應群組組態設定的物件參考。物件參考通常是使用 <strong>Get-CsRgsConfiguration</strong> Cmdlet 擷取，並將傳回的值指派給變數；例如，此命令會將在 ApplicationServer:atl-cs-001.litwareinc.com 服務上找到的物件參考傳回至組態設定，並將該物件參考儲存在名為 $x 的變數中：</p>
<p>$x = Get-CsRgsConfiguration -Identity service:ApplicationServer:atl-cs-001.litwareinc.com</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>AgentRingbackGracePeriod</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int16</p></td>
<td><p>如果代理拒絕接聽來電，AgentRingbackGracePeriod 會表示來電轉回至相同代理前的等待時間 (以秒為單位)。寬限期間可設為介於 30 到 600 秒 (含) (10 分鐘) 的任何整數。預設值為 60 秒。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultMusicOnHoldFile</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.AudioFile</p></td>
<td><p>表示保留來電者電話時隨時可播放的預設音樂。只有在回應群組工作流程未定義自己的保留音樂時，才會播放預設的音樂。</p>
<p>DefaultMusicOnHoldFile 屬性必須使用 <strong>Import-CsRgsAudioFile</strong> Cmdlet 建立的物件參考來設定。</p>
<p>如果 DefaultMusicOnHold 等於 Null 值 (預設值)，且如果工作流程未定義自訂等候音樂，則每當保留來電者時，就會播放您安裝 Lync Server 時所自動設定的預設等候音樂。</p></td>
</tr>
<tr class="even">
<td><p><em>DisableCallContext</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果設為 False (預設值)，每當接聽來電時，每個代理都能夠看到來電內容 (例如來電者等待時間，或工作流程問題與回覆等資訊) (從 Lync 可看見此資訊)。如果設為 True，則當接聽來電時，來電內容資訊不會轉送給代理。</p>
<p>請注意，來電內容僅搭配 IVR 佇列一起使用。</p></td>
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

Microsoft.Rtc.Rgs.Management.WritableSettings.ServiceSettings 物件。**Set-CsRgsConfiguration** 接受管線傳送的回應群組應用程式設定物件執行個體。

## 傳回類型

**Set-CsRgsConfiguration** 不會傳回任何物件或值，而會設定現有的 Microsoft.Rtc.Rgs.Management.WritableSettings.ServiceSettings 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsRgsConfiguration](get-csrgsconfiguration.md)  
[Move-CsRgsConfiguration](move-csrgsconfiguration.md)

