---
title: 設定 Lync Server 2013 與 Office Web Apps Server 搭配使用
TOCTitle: 設定 Lync Server 2013 與 Office Web Apps Server 搭配使用
ms:assetid: 6231e519-9010-4ff9-b5a6-b5859c2b3e11
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204944(v=OCS.15)
ms:contentKeyID: 49291100
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定 Lync Server 2013 與 Office Web Apps Server 搭配使用

 

_**上次修改主題的時間：** 2013-04-22_

在設定 Lync Server 2013 以使用 Office Web Apps Server 之前，您必須先部署及設定 Office Web Apps Server。如需如何安裝及設定單一 Office Web Apps Server，或如何安裝及設定 Office Web Apps Server 陣列以取得高可用性的詳細資訊，請參閱**部署 Office Web Apps Server 與 Office Web Apps 指南**文件。

一旦成功安裝 Office Web Apps Server 並正確設定 Web 伺服陣列後，您必須設定 Lync Server 才能和新伺服器通訊；這項作業是透過將 Office Web Apps Server 探索 URL 新增至 Lync Server 拓撲完成。若要將 Office Web Apps Server 新增至拓撲，請完成下列步驟：

1.  依序按一下 **\[開始\]**、**\[所有程式\]**、**\[Microsoft Lync Server 2013\]**，然後按一下 **\[Lync Server 拓撲產生器\]**。

2.  在 **\[拓撲產生器\]** 對話方塊中，選取 **\[從現有的部署下載拓撲\]**，然後按一下 **\[確定\]**。

3.  在 **\[另存拓撲\]** 對話方塊的 **\[檔案名稱\]** 方塊中，鍵入拓撲文件的名稱 (例如 **PreWebAppsServerTopology**)，然後按一下 **\[儲存\]**。如果新拓撲之後發生問題，就可以擷取並重新發行此拓撲。

4.  在拓撲產生器中，依序展開 **\[Lync Server 2013\]**、網站名稱及 **\[Enterprise Edition 前端集區\]**，接著用滑鼠右鍵按一下其中一個集區的名稱，然後按一下 **\[編輯內容\]**。

5.  在 **\[編輯內容\]** 對話方塊的 **\[一般\]** 索引標籤上，尋找標題 **\[關聯 Office Web Apps Server\]**，然後按一下 **\[新增\]** (或從下拉式清單中選取現有的 Office Web Apps Server)。

6.  在 **\[定義新的 Office Web Apps Server\]** 對話方塊的 **\[Office Web Apps Server FQDN\]** 方塊中，鍵入 Office Web Apps Server 電腦的完整網域名稱 (FQDN)；執行此動作時，您的 Office Web Apps Server 探索 URL 應自動輸入至 **\[Office Web Apps Server 探索 URL\]** 方塊。
    
    如果 Office Web Apps Server 是以內部部署方式安裝，並與 Lync Server 2013 位於相同網路地區，則不應選取 **\[Office Web Apps Server 部署在外部網路 (亦即周邊/網際網路)\]** 選項。
    
    如果 Office Web Apps Server 部署在內部防火牆外，則選取 **\[Office Web Apps Server 部署在外部網路 (亦即周邊/網際網路\]** 選項。

7.  在 **\[定義新的 Office Web Apps Server\]** 對話方塊中，按一下 **\[確定\]**，然後按一下 **\[編輯內容\]** 對話方塊中的 **\[確定\]**。Office Web Apps 探索 URL 將會列為其中一個集區的關聯。

您必須對每個需要與 Office Web Apps Server 建立關聯的集區重複此程序。

在新增探索 URL 至拓撲後，必須發行此更新的拓撲。在拓撲產生器中執行此作業的步驟如下：

1.  按一下 **\[動作\]**，然後按一下 **\[發行拓撲\]**。

2.  在發行拓撲精靈的 **\[發行拓撲\]** 頁面上，按 **\[下一步\]**。

3.  在 **\[發行精靈完成\]** 頁面上，按一下 **\[完成\]**。

4.  關閉拓撲產生器。

