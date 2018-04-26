---
title: 檢視公共區域電話資訊
TOCTitle: 檢視公共區域電話資訊
ms:assetid: e652240c-6a3f-4be7-a083-32f24c08e655
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994081(v=OCS.15)
ms:contentKeyID: 52056244
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視公共區域電話資訊

 

_**上次修改主題的時間：** 2013-02-20_

您可以使用 **Get-CsCommonAreaPhone** Cmdlet 檢視有關設定供組織使用之公共區域電話的資訊。如果沒有使用任何參數，此 Cmdlet 會傳回有關您所有公共區域電話的資訊。選用的參數則提供讓您篩選資訊的各種方法，例如，您可以傳回所有在指定組織單位 (OU) 中具有連絡人物件的公共區域電話，或所有位於某指定建築物中的連絡人物件。如需 **Get-CsCommonAreaPhone** 參數的詳細資訊，請參閱＜[Get-CsCommonAreaPhone](get-cscommonareaphone.md)＞。

從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行 **Get-CsCommonAreaPhone**。


## 檢視有關您所有公共區域電話的資訊

  - 若要檢視有關您所有公共區域電話的資訊，請在 Lync Server 管理命令介面中輸入下列命令，然後按 Enter：
    
        Get-CsCommonAreaPhone
    
    您會收到類似以下的資訊：
    
        Identity           : CN=Building 14 Lobby,OU=Redmond,
                             DC=litwareinc,DC=com
        RegistrarPool      : atl-cs-001.litwareinc.com
        Enabled            : True
        SipAddress         : sip:4714e34b-9781-421d-b07a-
                             52056b5b4a56@litwareinc.com
        ClientPolicy       :
        PinPolicy          :
        VoicePolicy        :
        MobilityPolicy     :
        GroupChatPolicy    :
        ConferencingPolicy :
        LineURI            : tel:+14255550712
        DisplayNumber      : 1-425-555-0712
        DisplayName        : Building 14 Lobby
        Description        :
        ExUmEnabled        : False

如需詳細資訊，請參閱＜[Get-CsCommonAreaPhone](get-cscommonareaphone.md)＞ Cmdlet 的說明主題。

