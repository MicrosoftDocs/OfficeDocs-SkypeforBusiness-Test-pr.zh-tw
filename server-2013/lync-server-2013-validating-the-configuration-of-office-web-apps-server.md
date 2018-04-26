---
title: 驗證 Office Web Apps Server 的設定
TOCTitle: Validating the Configuration of Office Web Apps Server
ms:assetid: f6e8ecbf-305d-4a13-92d0-b61dbd82b0ea
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205393(v=OCS.15)
ms:contentKeyID: 49292844
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 驗證 Office Web Apps Server 的設定

 

_**上次修改主題的時間：** 2014-04-22_

將 Office Web Apps Server 新增至拓撲後，以及在發佈拓撲後，您應會在 Lync Server 事件日誌中看到兩個新日誌事件。首先，應已新增 LS Data MCU 事件 (事件識別碼 41034)；此事件會回報是否已發現 Office Web Apps Server：

**已發現 Web 會議伺服器 WAC，已啟用 PowerPoint 內容。**

除此之外，應該還會看到另一個回報 Office Web Apps Server URL 的 LS Data MCU 事件 (事件識別碼 41032)。例如類似下列的內容：

**Web 會議伺服器 WAS 的發現已成功。**

**WAC 內部準備者頁面：https://atl-officewebapps-001.litwareinc.com/m/Presenter.aspx?a=0\&embed=**

**WAC 內部出席者頁面：https://atl-officewebapps-001.litwareinc.com/m/ParticipantFrame.aspx?a=0\&embed=true&=**

**WAC 外部簡報者頁面：https://atl-officewebapps-001.litwareinc.com/m/Presenter.aspx?a=0\&embed**

**WAC 內部出席者頁面：https://atl-officewebapps-001.litwareinc.com/m/ParticipantFrame.aspx?a=0\&embed=true&**

如果您看報事件識別碼為 41033 的 LS Data MCU 事件，表示 Office Web Apps Server 的發現已失敗。在這種情況下，Microsoft Lync Server 2013 會視您的需要盡量嘗試發現新設定的 Office Web Apps Server。如果發生程序一再發生失敗，您應從拓撲部署中移除 Office Web Apps Server、發佈更新的拓撲，以及在解決連線問題後，嘗試將 Office Web Apps Server 新增回拓撲。

如果 Office Web Apps Server 已正確設定，發現程序也已辨識此伺服器，即可在配對的 Microsoft Lync 2013 用戶端之間共用 PowerPoint 簡報，以驗證 Office Web Apps Server 是否預期般正常運作。如果「使用者 A」可載入與顯示 PowerPoint 簡報，且如果「使用者 B」可接著加入會議並查看簡報，則表示 Office Web Apps Server 正常運作。

即使 Office Web Apps Server 看起來已正確設定，當您嘗試共用 PowerPoint 簡報時，可能還是會收到錯誤訊息「因為伺服器連線問題，無法使用部分共用功能。」。如果收到該錯誤訊息，應重新啟動與新 Office Web Apps Server 相關聯的前端伺服器(或伺服器)。

