---
title: 在 Lync Server 2013 中設定 E9-1-1 語音路由
TOCTitle: 在 Lync Server 2013 中設定 E9-1-1 語音路由
ms:assetid: 6933b840-0e7b-4509-ae43-bc9065677547
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398496(v=OCS.15)
ms:contentKeyID: 49291198
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定 E9-1-1 語音路由

 

_**上次修改主題的時間：** 2012-09-17_

若要部署 E9-1-1，您需要先設定緊急電話語音路由。如需建立語音路由的詳細資訊，請參閱＜[在 Lync Server 2013 中建立語音路由](lync-server-2013-create-a-voice-route.md)＞。例如，如果您的部署包括主要及次要 SIP 主幹，則可以定義多個路由。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要在 E9-1-1 INVITE 中包括位置資訊，則必須先設定連線至 E9-1-1 服務提供者的 SIP 主幹以透過閘道路由傳送緊急電話。若要進行這項作業，請將 <strong>set-cstrunkconfiguration</strong> Cmdlet 上的 EnablePIDFLOSupport 旗標設定為 True。EnablePIDFLOSupport 的預設值是 False。例如：<code>set-cstrunkconfiguration Service:PstnGateway:192.168.0.241 -EnablePIDFLOSupport $true.</code><br />
不需要啟用接收後援公用交換電話網路 (PSTN) 閘道的位置，也不需啟用緊急位置識別號碼 (ELIN) 閘道的位置。</td>
</tr>
</tbody>
</table>


如需使用語音路由的詳細資訊，請參閱下列 Cmdlet 的 Lync Server 管理命令介面文件：

  - **Set-CsPstnUsage**

  - **Get-CsPstnUsage**

  - **New-CsVoiceRoute**

  - **Get-CsVoiceRoute**

  - **Set-CsVoiceRoute**

  - **Remove-CsVoiceRoute**

## 設定 E9-1-1 語音路由

1.  使用屬於 RTCUniversalServerAdmins 群組成員或 CsVoiceAdministrator 系統管理角色成員的帳戶登入電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  執行下列 Cmdlet 來建立新的 PSTN 使用方式記錄。
    
    這必須是用於 \[位置原則\] 中 **PSTN** 設定的相同名稱。雖然部署會有多筆電話使用方式記錄，下列範例會將「緊急使用方式」新增至目前可用的 PSTN 使用方式清單。如需詳細資訊，請參閱＜[在 Lync Server 2013 中設定用於授權撥號功能和權限的語音原則和 PSTN 使用方式記錄](lync-server-2013-configuring-voice-policies-and-pstn-usage-records-to-authorize-calling-features-and-privileges.md)＞。
    
        Set-CsPstnUsage -Usage @{add='EmergencyUsage'}

4.  執行下列 Cmdlet，使用上個步驟中所建立的 PSTN 使用方式記錄來建立新的語音路由。
    
    數字模式必須是位置原則的**緊急撥號字串**設定中所使用的相同數字模式。因為 Lync 會在緊急電話中加上 “+”，所以需要 “+” 符號。"Co1-pstngateway-1" 是 E9-1-1 服務提供者或 ELIN 閘道服務 ID 的 SIP 主幹服務 ID。下列範例會使用“EmergencyRoute”作為語音路由的名稱。
    
        New-CsVoiceRoute -Name "EmergencyRoute" -NumberPattern "^\+911$" -PstnUsages @{add="EmergencyUsage"} -PstnGatewayList @{add="co1-pstngateway-1"}

5.  建議您針對 SIP 主幹連線選擇執行下列 Cmdlet，建立不是由 E9-1-1 伺服器提供者的 SIP 主幹所處理之通話的本機路由。如果與 E9-1-1 服務提供者的連線無法使用，則會使用此路由。
    
    下列範例假設使用者的語音原則有「本機」使用方式。
    
        New-CsVoiceRoute -Name "LocalEmergencyRoute" -NumberPattern "^\+911$" -PstnUsages @{add="Local"} -PstnGatewayList @{add="co1-pstngateway-2"}

