---
title: 指派原則給公共區域電話
TOCTitle: 指派原則給公共區域電話
ms:assetid: f0554fd1-b237-49b3-9eb4-26f4b91f5604
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994082(v=OCS.15)
ms:contentKeyID: 52056257
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 指派原則給公共區域電話

 

_**上次修改主題的時間：** 2013-02-20_

為公共區域電話建立原則之後 (如需詳細資訊，請參閱＜[在 Lync Server 2013 中建立語音原則和設定 PSTN 使用方式記錄](lync-server-2013-create-a-voice-policy-and-configure-pstn-usage-records.md)＞)，您可以使用 Windows PowerShell 和適當的 **Grant-Cs** Cmdlet 將原則指派至公共區域電話。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行這些 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。


## 將原則指派至單一公共區域電話

  - 下列命令可將個別使用者語音原則 RedmondVoice 指派至識別為 “Building 14 Lobby” 的公共區域電話。
    
        Grant-CsVoicePolicy -Identity "Building 14 Lobby" -PolicyName "RedmondVoicePolicy"

## 將原則指派至多個公共區域電話

  - 在此範例中，個別使用者原則 RedmondVoice 會指派至所有設定供組織使用的公共區域電話。
    
        Get-CsCommonAreaPhone | Grant-CsVoicePolicy  -PolicyName "RedmondVoicePolicy"

如需詳細資訊，請參閱＜[Grant-CsVoicePolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Grant-CsVoicePolicy)＞的說明主題。

## 請參閱

#### 其他資源

[Get-CsCommonAreaPhone](get-cscommonareaphone.md)

