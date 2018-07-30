---
title: 修改現有 PIN 原則
TOCTitle: 修改現有 PIN 原則
ms:assetid: 517caaee-3349-4fa6-8d86-e4da3258a445
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520993(v=OCS.15)
ms:contentKeyID: 49290911
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 修改現有 PIN 原則

 

_**上次修改主題的時間：** 2012-06-19_

您可以使用 **\[PIN 原則\]** 索引標籤，向以 IP 電話連線至 Lync 2013 的使用者提供個人識別碼 (PIN) 驗證。若要使用 PIN 驗證，請確定 \[Web 服務\] 設定中已選取 **\[啟用 PIN 驗證\]**。如需詳細資訊，請參閱＜[修改現有 Web 服務組態設定](lync-server-2013-modify-existing-web-service-configuration-settings.md)＞。

請遵循下列步驟來修改使用者層級或網站層級的 PIN 原則。

## 若要修改現有的 PIN 原則

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限) 或指派給 CsServerAdministrator 或 CsAdministrator 角色的使用者帳戶，登入部署 Lync Server 2013 之網路上的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[安全性\]** 和 **\[PIN 原則\]**。

4.  在 **\[PIN 原則\]** 頁面上，依序按一下原則、**\[編輯\]** 和 **\[顯示詳細資料\]**。

5.  在 **\[編輯 PIN 原則\]** 的 **\[最小 PIN 長度\]** 中，輸入或選取您要允許的最小 PIN 長度。預設的最小長度為五位數。

6.  若要能夠指定使用者遭鎖定前可嘗試登入的次數上限，請選取 **\[指定登入嘗試次數上限\]** 核取方塊。若未選取此選項，則會根據 PIN 長度自動指定允許的嘗試次數上限。依預設會自動指定嘗試次數上限。

7.  如果您選取了 **\[指定登入嘗試次數上限\]** 核取方塊，請在 **\[登入嘗試次數上限\]** 中輸入或選取您所要允許的登入嘗試次數上限。

8.  若要讓 PIN 有期限，請選取 **\[啟用 PIN 到期\]** 核取方塊。若未選取此選項，PIN 將永不過期。根據預設，PIN 永遠不會過期。

9.  如果您選取了 **\[啟用 PIN 到期\]** 核取方塊，請在 **\[PIN 於下列日數後到期\]** 中輸入或選取 PIN 將在幾天之後到期。

10. 在 **\[PIN 碼歷程記錄計數\]** 中，輸入使用者必須在建立多少個 PIN 之後才可重複使用 PIN。根據預設，使用者可重複使用其 PIN。

11. 若要允許在 PIN 中使用共同模式的數字 (如連續數字與重複數字組)，請選取 **\[允許共同模式\]** 核取方塊。若未選取此選項，則只會允許複合模式的數字。依預設只會允許複合模式的數字。
    
    > [!IMPORTANT]  
    > 建議您不要允許共同模式。
    


12. 按一下 **\[認可\]**。

