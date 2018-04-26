---
title: 建立或修改網路地區
TOCTitle: 建立或修改網路地區
ms:assetid: bd08bb66-5976-4ece-b45c-7de19569f814
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182579(v=OCS.15)
ms:contentKeyID: 49292141
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 建立或修改網路地區

 

_**上次修改主題的時間：** 2012-11-01_

網路地區可將網路的不同部分跨多個地理區域互連。每個網路地區都必須與中央網站產生關聯。中央網站是資料中心網站，通話許可控制 (CAC) 頻寬原則服務會在其上執行。您可以使用 Lync Server 控制台來設定網路地區。網路地區包含的設定可判斷是否允許透過網際網路的替代路徑用於音訊和視訊連線。您可以從 Lync Server 控制台建立、修改或刪除網路地區。使用本主題可建立和修改網路地區。如需刪除現有網路地區的詳細資訊，請參閱＜[刪除現有網路地區](lync-server-2013-deleting-existing-network-regions.md)＞(可能為英文網頁)。

## 若要建立網路地區

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[網路設定\]，然後按一下 \[地區\]。

4.  在 **\[地區\]** 頁面上，按一下 \[新增\]。

5.  在 **\[新增地區\]** 頁面上，將值輸入 **\[名稱\]** 欄位中。此值在您的 Microsoft Lync Server 2013 部署中必須是唯一的。

6.  從 **\[中央網站\]** 下拉式清單中，選取此網路地區的中央網站。

7.  \[啟用音訊替代路徑\] 核取方塊預設為核取狀態。如果主要路徑中沒有足夠的頻寬，此欄位會判斷是否將透過替代路徑來路由傳送音訊通話。只有在您需要針對網際網路關閉卸載時，才取消選取此核取方塊。如果您的所有電話都是網際網路電話，必須選取此核取方塊，無論頻寬設定為何。

8.  \[啟用視訊替代路徑\] 核取方塊預設為核取狀態。如果主要路徑中沒有足夠的頻寬，此欄位會判斷是否將透過替代路徑來路由傳送視訊通話。只有在您需要針對網際網路關閉卸載時，才取消選取此核取方塊。如果您的所有電話都是網際網路電話，必須選取此核取方塊，無論頻寬設定為何。

9.  (選用) 在 **\[描述\]** 欄位中輸入值，以提供無法單用名稱表達之地區的詳細資訊。

10. 按一下 \[認可\]。

**\[關聯的網站\]** 表格不是用於建立網路地區。您會在建立或修改網站時，將網站與地區產生關聯。如需詳細資訊，請參閱[建立或修改網站](lync-server-2013-creating-or-modifying-network-sites.md)。

## 若要修改網路地區

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[網路設定\]，然後按一下 \[地區\]。

4.  在 **\[地區\]** 頁面上，按一下您要修改的地區。

5.  在 \[編輯\] 功能表上，按一下 \[顯示詳細資料\]。

6.  您可以在 **\[編輯地區\]** 頁面上，修改啟用或停用音訊和視訊替代路徑的設定，以及變更描述 (如需詳細資訊，請參閱本主題稍早的＜建立網路地區＞一節)。

7.  按一下 \[認可\]。

您無法在此頁面上修改 **\[關聯的網站\]**。關聯的網站清單是供您參考，讓您了解修改地區設定會影響哪些網站。

## 請參閱

#### 工作

[刪除現有網路地區](lync-server-2013-deleting-existing-network-regions.md)  
[在 Lync Server 2013 中設定 CAC 的網路區域](lync-server-2013-configure-network-regions-for-cac.md)  

#### 其他資源

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Set-CsNetworkRegion](set-csnetworkregion.md)  
[Remove-CsNetworkRegion](remove-csnetworkregion.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)

