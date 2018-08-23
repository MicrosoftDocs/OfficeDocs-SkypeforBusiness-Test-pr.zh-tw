---
title: "Lync Server 2013：將使用者隸屬於 Survivable Branch Appliance 或 Survivable Branch 伺服器"
TOCTitle: 將使用者隸屬於 Survivable Branch Appliance 或 Survivable Branch Server
ms:assetid: faf1ebb9-6d7d-4a58-8ff7-801b7b31d3ba
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413066(v=OCS.15)
ms:contentKeyID: 49292896
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中將使用者隸屬於 Survivable Branch Appliance 或 Survivable Branch Server

 

_**上次修改主題的時間：** 2014-12-10_

將使用者隸屬於 Survivable Branch Appliance 或 Survivable Branch 伺服器 的程序，類似將使用者隸屬於 前端集區 的程序。在中央網站執行 Survivable Branch Appliance 或 Survivable Branch 伺服器 程序。

## 將使用者隸屬於 Survivable Branch Appliance 或 Survivable Branch Server

1.  將使用者移至 Survivable Branch 伺服器 之前，請開啟 Lync Server 管理命令介面，然後執行下列所有動作：
    
      - 執行 **Test-CsPstnOutboundCall** 以確認 Survivable Branch 伺服器 正在執行中，且 PSTN 連線能力已設定。如果您需要修改 PSTN 閘道內容，請使用 **Set-CsPstnGateway**。
    
      - 執行 **Get-CsVoicePolicy**，以確認使用者將隸屬於具有適當 VoIP 路由原則的 Survivable Branch 伺服器。如果您需要修改 VoIP 原則，請使用 **Set-CsVoicePolicy**。
    
      - 執行 **Get-CsVoicemailReroutingConfiguration**，以確認已設定語音信箱重新路由設定。如果您需要修改語音信箱重新路由設定，請使用 Cmdlet Set-CsVoicemailReroutingConfiguration。

2.  在 Lync Server 管理命令介面中，執行 Cmdlet **Move-CsUser** 以移動隸屬使用者。

> [!NOTE]  
> 您也可以使用 Lync Server 控制台 來確認先決條件並隸屬使用者。



## 請參閱

#### 其他資源

[Test-CsPstnOutboundCall](https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsPstnOutboundCall)  
[Get-CsVoicePolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsVoicePolicy)  
[Get-CsVoicemailReroutingConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsVoicemailReroutingConfiguration)  
[Move-CsUser](https://docs.microsoft.com/en-us/powershell/module/skype/Move-CsUser)

