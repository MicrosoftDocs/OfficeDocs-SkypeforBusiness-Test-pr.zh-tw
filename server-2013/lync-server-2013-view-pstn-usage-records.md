---
title: Lync Server 2013：檢視 PSTN 使用方式記錄
TOCTitle: 檢視 PSTN 使用方式記錄
ms:assetid: 65025c78-c263-472c-9ff9-e170588f10b5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398458(v=OCS.15)
ms:contentKeyID: 49291132
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中檢視 PSTN 使用方式記錄

 

_**上次修改主題的時間：** 2013-02-22_

公用交換電話網路 (PSTN) 使用方式記錄會指定組織內的各個使用者或使用者群組可以進行的通話等級 (如內線、當地或長途電話)。如需詳細資訊，請參閱規劃文件中的 [Lync Server 2013 中的 PSTN 使用方式記錄](lync-server-2013-pstn-usage-records.md)。

## 使用 Lync Server 控制台 檢視 PSTN 使用方式記錄

1.  以 RTCUniversalServerAdmins 群組成員或者 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 角色成員的身分登入電腦。如需詳細資料，請參閱[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[語音路由\]** ，然後按一下 **\[PSTN 使用方式\]** 。

4.  在 **\[PSTN 使用方式\]** 頁面上，反白想要檢視的 PSTN 使用方式記錄，並按一下 **\[編輯\]** ，然後按一下 **\[顯示詳細資料\]** 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>所選取 PSTN 使用方式記錄的唯讀頁面顯示相關聯的路由及相關聯的語音原則。</td>
    </tr>
    </tbody>
    </table>


## 使用 Windows PowerShell Cmdlet 檢視 PSTN 使用資訊

您也可以使用 Windows PowerShell 及 **Get-CsPstnUsage** Cmdlet 來檢視 PSTN 使用狀況。可以從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段來執行此 Cmdlet。 如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 使用 Windows PowerShell Cmdlet 檢視 PSTN 使用狀況資訊

  - 若要檢視所有 PSTN 使用狀況的資訊，請在 Lync Server 管理命令介面中輸入下列命令，然後按 ENTER 鍵：
    
        Get-CsPstnUsage
    
    此命令會傳回與下列相似的資訊：
    
        Identity : Global
        Usage    : {Internal, Local, Long Distance}

如需詳細資訊，請參閱＜[Get-CsPstnUsage](get-cspstnusage.md)＞。

## 請參閱

#### 工作

[在 Lync Server 2013 中建立語音原則和設定 PSTN 使用方式記錄](lync-server-2013-create-a-voice-policy-and-configure-pstn-usage-records.md)  
[在 Lync Server 2013 中修改語音原則和設定 PSTN 使用方式記錄](lync-server-2013-modify-a-voice-policy-and-configure-pstn-usage-records.md)

