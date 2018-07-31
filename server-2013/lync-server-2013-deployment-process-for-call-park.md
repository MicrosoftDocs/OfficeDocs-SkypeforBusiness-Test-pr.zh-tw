---
title: Lync Server 2013：通話駐留的部署程序
TOCTitle: 通話駐留的部署程序
ms:assetid: 2000d672-a85f-4262-9d69-0bee9ae3709a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398283(v=OCS.15)
ms:contentKeyID: 49290307
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中通話駐留的部署程序

 

_**上次修改主題的時間：** 2015-03-09_

本節將概要說明部署 通話駐留應用程式的所需步驟。您必須先使用 企業語音部署 Enterprise Edition 或 Standard Edition，之後才能設定 通話駐留。 通話駐留需要的元件在您部署 企業語音時就會加以安裝和啟用。

### 通話駐留部署程序

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>階段</th>
<th>步驟</th>
<th>所需群組和角色</th>
<th>部署文件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>設定範圍表中的通話駐留範圍</p></td>
<td><p>使用 Lync Server 控制台或 <strong>New-CSCallParkOrbit</strong> Cmdlet，在通話駐留軌道範圍表中建立駐留範圍，並將其關聯至裝載 通話駐留應用程式的 應用程式服務。</p>
<div class="alert">

> [!NOTE]  
> 為了能與現有撥號對應表密切整合，駐留範圍通常設定為虛擬分機的區塊。不支援將直接向內撥號 (DID) 號碼指派為通話駐留範圍表中的範圍號碼。


</div></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsVoiceAdministrator</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-create-or-modify-a-call-park-orbit-range.md">在 Lync Server 2013 中建立或修改通話駐留軌道範圍</a></p></td>
</tr>
<tr class="even">
<td><p>進行 通話駐留設定</p></td>
<td><p>使用 <strong>Set-CsCpsConfiguration</strong> Cmdlet 來進行 通話駐留設定。建議您至少設定 <strong>OnTimeoutURI</strong> 選項，以設定駐留通話逾時後採用的後援目的地。您也可以設定下列各項：</p>
<ul>
<li><p>(選用) <strong>EnableMusicOnHold</strong> 可啟用或停用等候音樂。</p></li>
<li><p>(選用) <strong>MaxCallPickupAttempts</strong> 決定在將駐留通話轉接至後援統一資源識別項 (URI) 之前，駐留通話回撥接聽電話的次數。</p></li>
<li><p>(選用) <strong>CallPickupTimeoutThreshold</strong> 決定從駐留通話之後到回撥原先接聽來電的電話之前所經過的時間長度。</p></li>
</ul></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsVoiceAdministrator</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-configure-call-park-settings.md">在 Lync Server 2013 中設定通話駐留設定</a></p></td>
</tr>
<tr class="odd">
<td><p>(選用) 自訂等候音樂</p></td>
<td><p>(選用) 使用 <strong>Set-CsCallParkServiceMusicOnHoldFile</strong> Cmdlet 可自訂和上傳音訊檔案，以取代預設的等候音樂。</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsVoiceAdministrator</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-customize-call-park-music-on-hold.md">在 Lync Server 2013 中自訂通話駐留等候音樂</a></p></td>
</tr>
<tr class="even">
<td><p>設定語音原則，為使用者啟用 通話駐留</p></td>
<td><p>使用 Lync Server 控制台或 <strong>Set-CSVoicePolicy</strong> Cmdlet 搭配 <strong>EnableCallPark</strong> 選項，可在語音原則中為使用者啟用 通話駐留。</p>
<div class="alert">

> [!NOTE]  
> 根據預設，所有使用者的 通話駐留都是停用。


</div>
<div class="alert">

> [!NOTE]  
> 如果您有多個語音原則，請務必為每個語音原則設定 EnableCallPark 屬性，而非只是設定預設原則。


</div></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsVoiceAdministrator</p>
<p>CsUserAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-enable-call-park-for-users.md">在 Lync Server 2013 中為使用者啟用通話駐留</a></p></td>
</tr>
<tr class="odd">
<td><p>確認 通話駐留的正規化規則</p></td>
<td><p>通話駐留軌道不可正規化。確認您的正規化規則不包含任何駐留範圍。若有必要，可建立額外的正規化規則，用以防止範圍被正規化。</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsVoiceAdministrator</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-verify-normalization-rules-for-call-park.md">在 Lync Server 2013 中驗證通話駐留的正規化規則</a></p></td>
</tr>
<tr class="even">
<td><p>確認 通話駐留部署</p></td>
<td><p>測試撥打及擷取通話，確保您的設定運作符合預期。</p></td>
<td><p>-</p></td>
<td><p><a href="lync-server-2013-optional-verify-call-park-deployment.md">(選用) 在 Lync Server 2013 中驗證通話駐留部署</a></p></td>
</tr>
</tbody>
</table>

