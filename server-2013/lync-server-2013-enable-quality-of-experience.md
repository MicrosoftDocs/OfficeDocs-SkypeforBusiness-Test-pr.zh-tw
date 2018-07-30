---
title: 啟用經驗品質
TOCTitle: 啟用經驗品質
ms:assetid: c8bb3c67-b324-4d94-8158-00c792c7ac42
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182583(v=OCS.15)
ms:contentKeyID: 49292303
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 啟用經驗品質

 

_**上次修改主題的時間：** 2013-02-23_

經驗品質 (QoE) 會記錄數字資料，指出有關通話與工作階段中所包含參與者、裝置名稱、驅動程式、IP 位址和端點類型的媒體品質和資訊。如需詳細資訊，請參閱規劃文件中的[Lync Server 2013 中的規劃監控](lync-server-2013-planning-for-monitoring.md)。

利用下列程序可啟用整個組織或組織中各網站的 QoE。

> [!NOTE]  
> 若要啟用 QoE，您必須先設定監控與監控後端資料庫。如需詳細資訊，請參閱<a href="lync-server-2013-deploying-monitoring.md">在 Lync Server 2013 中部署監控</a>。



## 使用 Lync Server 控制台啟用 QoE

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限) 或指派給 CsServerAdministrator 或 CsAdministrator 角色的使用者帳戶，登入部署 Lync Server 2013 之網路上的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[監控和封存\]，然後按一下 \[經驗品質資料\]。

4.  在 \[經驗品質資料\] 頁面上，依序按一下表格中的適當集合、\[動作\] 和 \[啟用 QoE\]。

## 使用 Windows PowerShell Cmdlet 啟用 QoE

您可以使用 Windows PowerShell和 **Set-CsQoEConfiguration** Cmdlet 啟用 QoE。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 針對單一位置啟用 QoE

  - 若要停用 QoE，請將 EnableQoE 參數設為 True ($True)。
    
        Set-CsQoEConfiguration -Identity "site:Redmond" -EnableQoE $True

## 針對單一位置停用 QoE

  - 若要停用 QoE，請將 EnableQoE 參數設為 False ($False)。這樣並不會解除安裝監控功能。它會暫停收集和儲存 QoE 資料。
    
        Set-CsQoEConfiguration -Identity "site:Redmond" -EnableQoE $False

## 使用單一命令在多個位置啟用 QoE

  - 此命令會對目前貴組織內使用的所有 QoE 組態設定啟用 QoE。
    
        Get-CsQoEConfiguration | Set-CsQoEConfiguration "site:Redmond" -EnableQoE $True

如需詳細資訊，請參閱 [Set-CsQoEConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsQoEConfiguration)。

## 請參閱

#### 其他資源

[Lync Server 2013 中的規劃監控](lync-server-2013-planning-for-monitoring.md)  
[在 Lync Server 2013 中部署監控](lync-server-2013-deploying-monitoring.md)

