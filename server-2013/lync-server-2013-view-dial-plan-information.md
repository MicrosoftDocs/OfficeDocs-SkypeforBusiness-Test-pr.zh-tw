---
title: 檢視 Lync Server 2013 中的撥號對應表資訊
TOCTitle: 檢視 Lync Server 2013 中的撥號對應表資訊
ms:assetid: 25ed0112-a8a7-418a-8c2c-580081be692a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ687997(v=OCS.15)
ms:contentKeyID: 49889983
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視 Lync Server 2013 中的撥號對應表資訊

 

_**上次修改主題的時間：** 2012-11-01_

若要檢視現有撥號對應表的相關資訊，請執行下列程序中的步驟，如果您想要建立新的撥號對應表，請參閱＜[在 Lync Server 2013 中建立撥號對應表](lync-server-2013-create-a-dial-plan.md)＞。

## 若要從 Lync Server 控制台來檢視撥號對應表的相關資訊

1.  以 RTCUniversalServerAdmins 群組成員或者 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 角色成員的身分登入電腦。如需詳細資料，請參閱[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 \[語音路由\] 和 \[撥號對應表\]。

4.  在 \[撥號對應表\] 頁面上，按兩下撥號對應表名稱。
    
    > [!NOTE]  
    > 您一次僅可檢視一個撥號對應表。
    


## 使用 Windows PowerShell Cmdlet 來檢視撥號對應表

  - 您也可以使用 Windows PowerShell 命令列介面和 **Get-CsDialPlan** Cmdlet 來檢視撥號對應表，此 Cmdlet 可從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。
    
    若要檢視撥號對應表的相關資訊，請在 Lync Server 管理命令介面中輸入下列命令，然後按 ENTER 鍵：
    
        Get-CsDialPlan
    
    此命令會傳回類似如下的資訊：
    
        Identity                 : Global
        Description              :
        DialinConferencingRegion :
        NormalizationRules       : {Description=;
                                   Pattern=^(\d+)$;Translation=$1;Name=
                                   KeepAll;IsInternalExtension=False}
        CountryCode              :
        State                    :
        City                     :
        ExternalAccessPrefix     :
        SimpleName               : DefaultProfile
        OptimizeDeviceDialing    : False

## 請參閱

#### 工作

[在 Lync Server 2013 中建立撥號對應表](lync-server-2013-create-a-dial-plan.md)  
[在 Lync Server 2013 中修改撥號對應表](lync-server-2013-modify-a-dial-plan.md)

