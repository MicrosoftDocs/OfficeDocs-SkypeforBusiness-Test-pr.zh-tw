---
title: 啟用詳細通話記錄
TOCTitle: 啟用詳細通話記錄
ms:assetid: 3b28e432-596f-45a5-a070-577d6fa748d9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520980(v=OCS.15)
ms:contentKeyID: 49290642
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 啟用詳細通話記錄

 

_**上次修改主題的時間：** 2013-02-23_

詳細通話記錄 (CDR) 會記錄對等活動 (包括立即訊息、VoIP 電話、應用程式共用、檔案傳輸和會議) 的使用方式與診斷資訊。使用方式資料可以用來計算投資報酬率 (ROI)，而診斷資料則可用來排解對等活動和會議的疑難問題。

使用下列程序來為整個組織或組織內的個別網站啟用 CDR。

> [!NOTE]  
> 如要啟用 CDR，您必須設定監控及監控資料庫。如需詳細資訊，請參閱＜<a href="lync-server-2013-deploying-monitoring.md">在 Lync Server 2013 中部署監控</a>＞。



## 使用 Lync Server 控制台啟用 CDR

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限) 或指派給 CsServerAdministrator 或 CsAdministrator 角色的使用者帳戶，登入部署 Lync Server 2013 之網路上的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[監控和封存\]**，然後按一下 **\[詳細通話記錄\]**。

4.  在 **\[詳細通話記錄\]** 頁面上，依序按一下表格中的適當網站、**\[動作\]** 和 **\[啟用 CDR\]**。
    
    > [!NOTE]  
    > 預設會啟用 CDR。
    


## 使用 Lync Server 管理命令介面 Cmdlet 啟用 CDR

也可以使用 Windows PowerShell 及 **Set-CsCdrConfiguration** Cmdlet 來啟用 CDR。可從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段來執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 針對單一位置啟用 CDR

  - 如要停用 CDR，請將 EnableCDR 參數設為 True ($True)。
    
        Set-CsCdrConfiguration -Identity "site:Redmond" -EnableCDR $True

## 針對單一位置停用 CDR

  - 如要停用 CDR，請將 EnableCDR 參數設為 False ($False)。這樣不會解除安裝監控，只會暫停收集和儲存 CDR 資料。
    
        Set-CsCdrConfiguration -Identity "site:Redmond" -EnableCDR $False

## 使用單一命令啟用多個位置的 CDR

  - 以下命令會啟用組織中所有目前正在使用之 CDR 組態設定的 CDR。
    
        Get-CsCdrConfiguration | Set-CsCdrConfiguration "site:Redmond" -EnableCDR $True

如需詳細資訊，請參閱 [Set-CsCdrConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsCdrConfiguration) Cmdlet 的說明主題。

## 請參閱

#### 其他資源

[Lync Server 2013 中的規劃監控](lync-server-2013-planning-for-monitoring.md)  
[在 Lync Server 2013 中部署監控](lync-server-2013-deploying-monitoring.md)

