---
title: 建立或修改網路子網路
TOCTitle: 建立或修改網路子網路
ms:assetid: 1ba8c4e3-fbc7-4758-88ac-d651fef17bed
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520957(v=OCS.15)
ms:contentKeyID: 49290251
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 建立或修改網路子網路

 

_**上次修改主題的時間：** 2013-02-21_

為了判斷屬於此子網路的主機地理位置，網路子網路必須與網路網站相關聯。您可以使用 Lync Server 控制台設定子網路。從 Lync Server 控制台可以建立、修改或刪除網路子網路。如需刪除網路子網路的詳細資訊，請參閱＜[刪除網路子網路](lync-server-2013-deleting-network-subnets.md)＞

在已實作通話許可控制 (CAC) 的大多數 Microsoft Lync Server 2013 部署中，通常有大量子網路。因此，最好是從 Lync Server 管理命令介面設定子網路。您可以從該處呼叫 **New-CsNetworkSubnet** 並搭配 Windows PowerShell Cmdlet **Import-CSV**。您可以同時使用這兩個 Cmdlet，一次從逗點分隔值 (.csv) 檔案讀入子網路設定並建立多個子網路。如需如何從 .csv 檔案建立子網路的範例，請參閱 ＜[New-CsNetworkSubnet](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsNetworkSubnet)＞。

## 建立網路子網路

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[網路設定\]** 再按一下 **\[子網路\]**。

4.  在 **\[子網路\]** 頁面上，按一下 **\[新增\]**。

5.  在 **\[新增子網路\]** 中，於 **\[子網路 ID\]** 欄位輸入值。此 ID 必須是 IP 位址 (例如 174.11.12.0)，而且必須是子網路定義之 IP 位址範圍中的第一個位址。

6.  在 **\[遮罩\]** 欄位中，輸入 1 至 32 的數值。
    
    > [!NOTE]  
    > 這個值是要套用至所建立之子網路的位元遮罩。
    


7.  在 \[網路網站 ID\] 中，選取此子網路所屬的網站。

8.  (選用) 在 **\[描述\]** 欄位輸入值，提供名稱不足以描述的子網路其他相關資訊。

9.  按一下 **\[認可\]**。

## 修改網路子網路

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[網路設定\]** 再按一下 **\[子網路\]**。

4.  在 **\[子網路\]** 頁面中，按一下您要修改的子網路。

5.  在 **\[編輯\]** 功能表上，按一下 **\[顯示詳細資料\]**。

6.  在 **\[編輯子網路\]** 頁面中，修改位元遮罩、相關網路網站或說明。如果修改位元遮罩，請記住子網路 ID 必須仍是子網路定義之 IP 位址範圍中的第一個位址。

7.  按一下 **\[認可\]**。

## 請參閱

#### 工作

[刪除網路子網路](lync-server-2013-deleting-network-subnets.md)  

#### 概念

[關於 Lync Server 2013 中的網路區域、網站和子網路](lync-server-2013-about-network-regions-sites-and-subnets.md)  

#### 其他資源

[New-CsNetworkSubnet](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsNetworkSubnet)  
[Set-CsNetworkSubnet](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsNetworkSubnet)  
[Remove-CsNetworkSubnet](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsNetworkSubnet)  
[Get-CsNetworkSubnet](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkSubnet)

