---
title: Lync Server 2013：將使用者移轉到整合的連絡人存放區
TOCTitle: 將使用者移轉到整合的連絡人存放區
ms:assetid: 215a8ec1-d63e-4fdf-b73d-75aeb9dddb43
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204737(v=OCS.15)
ms:contentKeyID: 49290324
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中將使用者移轉到整合的連絡人存放區

 

_**上次修改主題的時間：** 2012-10-15_

當使用者滿足下列條件時，其連絡人就會自動移轉至 Exchange 2013：

  - 已指派了 UcsAllowed 設為 True 的使用者服務原則。

  - 已佈建了 Exchange 2013 信箱，並已登入信箱至少一次。

  - 使用 Lync 2013 豐富型用戶端登入。

若使用者是利用 Lync 2010 或舊版用戶端來登入，或使用者未連線至 Exchange 2013 伺服器，系統就會忽略使用者服務原則，且使用者的連絡人就會持續保留在 Lync Server中。

您可使用下列方法之一，來判斷使用者的連絡人是否已移轉：

  - 檢查用戶端電腦上的下列登錄機碼：
    
    HKEY\_CURRENT\_USER\\Software\\Microsoft\\Office\\15.0\\Lync\\\<SIP URL\>\\UCS
    
    若使用者的連絡人是儲存在 Exchange 2013 中，登錄機碼就會包含 InUCSMode 值 (其值為 2165)。

  - 執行 **Test-CsUnifiedContactStore** Cmdlet。在 Lync Server 管理命令介面命令列中輸入：
    
        Test-CsUnifiedContactStore -UserSipAddress "sip:kenmyer@litwareinc.com" -TargetFqdn "atl-cs-001.litwareinc.com"
    
    若 **Test-CsUnifiedContactStore** 成功，使用者的連絡人就已移轉至整合連絡人存放區。

