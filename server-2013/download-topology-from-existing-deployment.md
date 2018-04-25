---
title: 從現有部署下載拓撲
TOCTitle: 從現有部署下載拓撲
ms:assetid: e39065a2-d4b0-4f27-8c49-f56be78fa55b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721913(v=OCS.15)
ms:contentKeyID: 49890352
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 從現有部署下載拓撲

 

_**上次修改主題的時間：** 2012-09-29_

建立 Lync Server 2013 集區時，您會使用 Lync Server 2010 對應的中央管理存放區。若您在第一次使用與後續編輯工作階段中啟動拓撲產生器，系統會提示您輸入希望拓撲產生器載入目前組態文件的位置。因為您已有定義的 Lync Server 2010 拓撲，且已建立了中央管理存放區，您應該從現有的部署下載拓撲。拓撲產生器將會讀取資料庫並擷取目前定義。

**從現有的部署下載拓撲**

1.  開啟 \[Lync Server 部署精靈\] 。

2.  在 \[Lync Server 2013 – 部署精靈\] 頁面上，按一下 \[安裝系統管理工具\]。

3.  啟動拓撲產生器：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\]，然後按一下 \[Lync Server 拓撲產生器\]。

4.  選擇 \[從現有部署下載拓撲\] 。
    
    ![部署精靈拓撲產生器設定](images/JJ721913.d5b39fd9-3c13-422e-a06c-25d2568fe781(OCS.15).jpg "部署精靈拓撲產生器設定")

5.  選擇檔案名稱，然後依預設的 .tbxml 檔案類型儲存拓撲。

6.  展開 Lync Server 節點 (如圖所示)，顯示部署中的各種伺服器角色。
    
    ![拓撲產生器伺服器角色一般內容](images/JJ721913.af99ead3-676b-47fd-8369-5a5f9717383f(OCS.15).jpg "拓撲產生器伺服器角色一般內容")

