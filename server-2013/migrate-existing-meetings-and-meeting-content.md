---
title: 移轉現有的會議與會議內容
TOCTitle: 移轉現有的會議與會議內容
ms:assetid: 30516731-2ae1-4a6d-a7e1-d3f05778c954
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688011(v=OCS.15)
ms:contentKeyID: 49890004
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移轉現有的會議與會議內容

 

_**上次修改主題的時間：** 2013-02-22_

當使用者帳戶從 Lync Server 2010 移至 Lync Server 2013 伺服器時，下列資訊會隨之移動：

  - **使用者已排定的會議**。包含移動會議目錄及會議資料。

  - **使用者的個人識別碼 (PIN)**。直到過期或使用者要求新 PIN 前，使用者目前的 PIN 都持續有效。

下列使用者帳戶資訊不會移到新的伺服器。

  - **會議內容**。若要移動會議期間分享的內容。例如 PowerPoint、白板、附件或投票資料，請在 **Move-CsUser** Cmdlet 中使用 **-MoveConferenceData** 參數。

