---
title: 刪除網路子網路
TOCTitle: 刪除網路子網路
ms:assetid: c1850f38-40a3-48c9-b6f1-f181c5e63b6b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721873(v=OCS.15)
ms:contentKeyID: 49890293
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除網路子網路

 

_**上次修改主題的時間：** 2013-02-21_

您可以使用下列程序刪除子網路。從 Lync Server 控制台可以建立、修改或刪除網路子網路。如需關於建立或修改網路子網路的詳細資訊，請參閱[建立或修改網路子網路](lync-server-2013-create-or-modify-network-subnets.md)

在已實作通話許可控制 (CAC) 的大多數 Microsoft Lync Server 2013 部署中，通常有大量子網路。因此，最好是從 Lync Server 管理命令介面設定子網路。您可以從該處呼叫 **New-CsNetworkSubnet** 並搭配 Windows PowerShell Cmdlet **Import-CSV**。您可以同時使用這兩個 Cmdlet，一次從逗點分隔值 (.csv) 檔案讀入子網路設定並建立多個子網路。如需如何從 .csv 檔案建立子網路的範例，請參閱 [New-CsNetworkSubnet](new-csnetworksubnet.md)。

## 刪除網路子網路

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[網路設定\] 再按一下 \[子網路\]。

4.  在 \[子網路\] 頁面中，按一下您要刪除的子網路。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可以一次刪除一個以上的子網路。若要這麼做，請按住 CTRL 鍵，然後選取一個以上的子網路。或者，若要選取所有子網路，請按一下 [編輯] 功能表上的 [全選]。</td>
    </tr>
    </tbody>
    </table>


5.  在 \[編輯\] 功能表中，按一下 \[刪除\]。

6.  按一下 \[確定\]。

## 請參閱

#### 工作

[建立或修改網路子網路](lync-server-2013-create-or-modify-network-subnets.md)

