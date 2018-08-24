---
title: 還原監控資料和封存資料
TOCTitle: 還原監控資料和封存資料
ms:assetid: 60118526-13bb-4b03-803e-6ffae219d436
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh202175(v=OCS.15)
ms:contentKeyID: 52056115
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 還原監控資料和封存資料

 

_**上次修改主題的時間：** 2013-02-18_

失敗後並不需要還原監控及封存資料來讓 Lync Server 啟動並執行。然而，如果監控及封存資料對組織很重要，則在重新建立資料庫之後，建議您還原資料。

下列程序說明如何使用 SQL Server Management Studio 還原封存或監控資料。

## 從備份檔還原監控或封存資料

1.  以本機電腦 Administrators 群組成員或具有相等使用者權限的群組成員身分，登入您要還原的伺服器。

2.  開啟 SQL Server Management Studio：依序按一下 \[開始\] 和 \[所有程式\]，再按一下 \[Microsoft SQL Server 2012\] 或 \[Microsoft SQL Server 2008 R2\]，然後按一下 \[SQL Server Management Studio\]。

3.  在 \[連線至伺服器\] 中，至少提供伺服器的名稱及驗證資訊，以連線至 SQL Server 執行個體。

4.  在 \[物件總管\] 中，以滑鼠右鍵按一下 \[資料庫\]，然後按一下 \[還原資料庫\]。

5.  在 \[選取頁面\] 底下，按一下 \[一般\]，然後在 \[目的地資料庫\] 中，選取資料庫名稱，如下所示：
    
      - 若為 封存資料庫，請選取 \[LcsLog\]。
    
      - 若為詳細通話記錄 (CDR) 資料庫，請選取 \[LcsCDR\]。
    
      - 若為經驗品質 (QoE) 資料庫，請選取 \[QoEMetrics\]。

6.  按一下 \[來源裝置\]。

7.  在 \[選取要還原的備份組\] 底下，按一下備份檔，然後按一下 \[還原\]。

8.  在 \[選取頁面\] 底下，按一下 \[選項\]，確認資料檔案路徑及記錄檔路徑在正確的資料夾中，然後按一下 \[確定\]。

## 確定存取控制清單 (ACL) 正確

1.  依序展開 \[資料庫\]、封存或監控資料庫、\[安全性\] 及 \[使用者\]。

2.  確認網域群組 RTCComponentUniversalServices 以使用者身分存在。

3.  如果 \[使用者\] 底下不存在 RTCComponentUniversalServices，請執行下列動作：
    
    1.  以滑鼠右鍵按一下 \[使用者\]，然後按一下 \[新增使用者\]。
    
    2.  在 \[登入名稱\] 中，輸入遺失的群組名稱 RTCComponentUniversalServices。
    
    3.  在 \[資料庫角色成員資格\] 底下，選取 \[ServerRole\] 權限，然後按一下 \[確定\]。
    
    > [!NOTE]  
    > 您不需要重新啟動封存或監控服務。
    

