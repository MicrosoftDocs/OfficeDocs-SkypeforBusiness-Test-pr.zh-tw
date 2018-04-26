---
title: 移轉撥入存取號碼
TOCTitle: 移轉撥入存取號碼
ms:assetid: 568a94b7-a697-4ab2-9008-dc9ecc1c87c8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204898(v=OCS.15)
ms:contentKeyID: 49290961
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移轉撥入存取號碼

 

_**上次修改主題的時間：** 2012-09-26_

移轉電話撥入式存取號碼需要兩個步驟：執行 **Import-CsLegacyConfiguration** Cmdlet (先前已在 [匯入原則與設定](import-policies-and-settings.md)中完成) 來移轉撥號對應表與其他電話撥入存取號碼設定，以及執行 **Move-CsApplicationEndpoint** Cmdlet 來移轉連絡人物件。

## 移轉撥入存取號碼

1.  開啟 Office Communications Server 2007 R2 系統管理工具。

2.  在主控台樹狀目錄中，以滑鼠右鍵按一下樹系節點，並依序按一下 **\[內容\]** 和 **\[會議服務員內容\]** 。

3.  在 **\[存取電話號碼\]** 索引標籤上，按一下 **\[由集區服務\]** ，依據其相關聯的集區排序存取電話號碼，並識別所移轉之集區的所有存取號碼。

4.  若要識別每個存取號碼的 SIP URI，請按兩下存取號碼來開啟 **\[編輯會議服務員號碼\]** 對話方塊，然後查看 **\[SIP URI\]** 下方的內容。

5.  開啟 Lync Server 管理命令介面。

6.  將每個撥入存取號碼移至 Lync Server 2013 上所裝載的集區，然後執行：
    
        Move-CsApplicationEndpoint -Identity <SIP URI of the access number to be moved> -Target <FQDN of the pool to which the access number is moving>

7.  在 Office Communications Server 2007 R2 系統管理工具的 **\[存取電話號碼\]** 索引標籤上，確認所移轉的 Office Communications Server 2007 R2 集區中已無任何撥入存取號碼。

