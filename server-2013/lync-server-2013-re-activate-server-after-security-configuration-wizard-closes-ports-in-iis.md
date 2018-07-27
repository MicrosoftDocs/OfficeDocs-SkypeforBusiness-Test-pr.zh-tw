---
title: Lync Server 2013：在安全性設定精靈於 IIS 中關閉連接埠後重新啟動伺服器
TOCTitle: 在安全性設定精靈於 IIS 中關閉連接埠後重新啟動伺服器
ms:assetid: cb8e17cf-f8c1-4099-b63b-c242d656c26a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398851(v=OCS.15)
ms:contentKeyID: 49292334
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在安全性設定精靈於 IIS 中關閉連接埠後重新啟動伺服器

 

_**上次修改主題的時間：** 2012-10-01_

某些 Lync Server 2013 角色會在 Internet Information Services (IIS) 連接埠 4443 上執行 Web 服務。執行 Lync Server 部署精靈、Bootstrapper.exe 或使用 **Enable-CsComputer** Cmdlet 會在防火牆內建立例外狀況，並且開啟連接埠。如果您接著執行 Windows Server 2008 R2 \[安全性設定精靈\] (或其他增強指令碼)，連接埠 4443 將會被封鎖，而外部用戶端將無法連絡 Web 服務。若要重新開啟連接埠，您可以直接修改防火牆例外狀況，或重新啟動伺服器。

## 若要使用部署精靈重新啟動伺服器

1.  在 Lync Server 部署精靈頁面上，按一下 **\[執行\]** (位於 **\[步驟 2：安裝或移除 Lync Server 元件\]** 。

2.  在 **\[安裝 Lync Server 元件\]** 頁面上，按 **\[下一步\]** 。

3.  在 **\[執行命令\]** 頁面上，當工作狀態顯示為完成後，按一下 \[完成\] 。
    
    > [!NOTE]  
    > 您也可以使用 bootstrapper.exe 或 <strong>Enable-CsComputer</strong> 重新啟動伺服器。
    

