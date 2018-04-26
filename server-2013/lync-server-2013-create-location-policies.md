---
title: 在 Lync Server 2013 中建立位置原則
TOCTitle: 在 Lync Server 2013 中建立位置原則
ms:assetid: f1878194-c756-4794-8fa1-15dd2118b4b3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413006(v=OCS.15)
ms:contentKeyID: 49292780
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立位置原則

 

_**上次修改主題的時間：** 2015-03-09_

在用戶端註冊期間，Lync Server 會使用「位置」原則來啟用 Lync 用戶端的 E9-1-1。「位置」原則包含定義 E9-1-1 實作方式的設定。

您可以編輯全域位置原則，並建立新的標記位置原則。當用戶端不是位在具有相關聯之位置原則的子網域內，或是沒有直接指派位置原則給用戶端時，用戶端便會取得全域原則。標記原則會指派給子網路或使用者。

若要建立位置原則，必須使用具有 RTCUniversalServerAdmins 群組成員或 CsVoice系統管理員 系統管理角色成員身分的帳戶，或是具有系統管理員權限的帳戶。

如需位置原則的完整描述，請參閱[針對 Lync Server 2013 定義位置原則](lync-server-2013-defining-the-location-policy.md)。此程序中的 Cmdlet 會使用以下列值定義的位置原則：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>項目</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EnhancedEmergencyServicesEnabled</p></td>
<td><p><strong>True</strong></p></td>
</tr>
<tr class="even">
<td><p>LocationRequired</p></td>
<td><p><strong>免責聲明</strong></p></td>
</tr>
<tr class="odd">
<td><p>EnhancedEmergencyServiceDisclaimer</p></td>
<td><p>根據貴公司的原則，您必須設定位置。如果不這麼做，緊急服務就無法在緊急時找到您。請設定位置。</p></td>
</tr>
<tr class="even">
<td><p>UseLocationForE911Only</p></td>
<td><p><strong>False</strong></p></td>
</tr>
<tr class="odd">
<td><p>PstnUsage</p></td>
<td><p><strong>EmergencyUsage</strong></p></td>
</tr>
<tr class="even">
<td><p>EmergencyDialString</p></td>
<td><p><strong>911</strong></p></td>
</tr>
<tr class="odd">
<td><p>EmergencyDialMask</p></td>
<td><p><strong>112</strong></p></td>
</tr>
<tr class="even">
<td><p>NotificationUri</p></td>
<td><p><strong>sip:security@litwareinc.com</strong></p></td>
</tr>
<tr class="odd">
<td><p>ConferenceUri</p></td>
<td><p><strong>sip:+14255550123@litwareinc.com</strong></p></td>
</tr>
<tr class="even">
<td><p>ConferenceMode</p></td>
<td><p><strong>twoway</strong></p></td>
</tr>
<tr class="odd">
<td><p>LocationRefreshInterval</p></td>
<td><p><strong>2</strong></p></td>
</tr>
</tbody>
</table>


如需使用位置原則的詳細資訊，請參閱 Lync Server 管理命令介面 文件中的下列 Cmdlet：

  - New-CsLocationPolicy

  - Get-CsLocationPolicy

  - Set-CsLocationPolicy

  - Remove-CsLocationPolicy

  - Grant-CsLocationPolicy

## 若要建立位置原則

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果 <strong>PstnUsage</strong> 的設定尚未在 PstnUsages 的全域清單中，則 CsLocationPolicy 會失敗。</td>
    </tr>
    </tbody>
    </table>


2.  您可以選擇執行下列 Cmdlet 來編輯全域位置原則：
    
        Set-CsLocationPolicy -Identity Global -EnhancedEmergencyServicesEnabled $true -LocationRequired "disclaimer" -EnhancedEmergencyServiceDisclaimer "Your company policy requires you to set a location. If you do not set a location emergency services will not be able to locate you in an emergency. Please set a location." -PstnUsage "emergencyUsage" -EmergencyDialString "911" -ConferenceMode "twoway" -ConferenceUri "sip:+14255550123@litwareinc.com" -EmergencyDialMask "112" NotificationUri "sip:security@litwareinc.com" -UseLocationForE911Only $true -LocationRefreshInterval 2

3.  執行下列 Cmdlet 以建立標記位置原則。
    
        New-CsLocationPolicy -Identity Tag:Redmond - EnhancedEmergencyServicesEnabled $true -LocationRequired "disclaimer" -EnhancedEmergencyServiceDisclaimer "Your company policy requires you to set a location. If you do not set a location emergency services will not be able to locate you in an emergency. Please set a location." -UseLocationForE911Only $false -PstnUsage "EmergencyUsage" -EmergencyDialString "911" -EmergencyDialMask "112" -NotificationUri "sip:security@litwareinc.com" -ConferenceUri "sip:+14255550123@litwareinc.com" -ConferenceMode "twoway" -LocationRefreshInterval 2

4.  執行下列 Cmdlet 以便將步驟 3 所建立的標記位置原則套用至使用者原則。
    
        (Get-CsUser | where { $_.Name -match "UserName" }) | Grant-CsLocationPolicy -PolicyName Redmond

