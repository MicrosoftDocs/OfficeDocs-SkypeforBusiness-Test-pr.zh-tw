---
title: 檢視網路子網路資訊
TOCTitle: 檢視網路子網路資訊
ms:assetid: 46f165f2-efe3-4cc1-9fee-a78b7f2ed41e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688044(v=OCS.15)
ms:contentKeyID: 49890044
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視網路子網路資訊

 

_**上次修改主題的時間：** 2013-02-23_

您可以使用下列程序來檢視網路子網路。您可以從 Lync Server 控制台來建立、修改或刪除網路子網路。如需建立或修改網路子網路的詳細資訊，請參閱＜[建立或修改網路子網路](lync-server-2013-create-or-modify-network-subnets.md)＞。

## 檢視網路子網路

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[網路設定\]** 和 **\[子網路\]**。

4.  在 **\[子網路\]** 頁面上，按一下您要檢視的子網路。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您一次只能檢視一個子網路。</td>
    </tr>
    </tbody>
    </table>


5.  在 **\[編輯\]** 功能表上，按一下 **\[顯示詳細資料...\]**。

## 使用 Lync Server PowerShell Cmdlet 檢視網路子網路設定資訊

您也可以使用 Lync Server PowerShell 和 Get-CsNetworkSubnet Cmdlet 來檢視網路子網路資訊。這個 Cmdlet 可以從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段來執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 檢視網路子網路資訊

  - 如果要檢視您所有網路子網路的資訊，請在 Lync Server 管理命令介面中輸入下列命令，然後按 ENTER 鍵：
    
        Get-CsNetworkSubnet
    
    這樣就會傳回類似下面的資訊：
    
        Identity      : 172.11.15.0
        MaskBits      : 28
        Description   :
        NetworkSiteID : Redmond
        SubnetID      : 172.11.15.0

如需詳細資訊，請參閱 [Get-CsNetworkSubnet](get-csnetworksubnet.md) Cmdlet 的說明主題。

## 請參閱

#### 工作

[建立或修改網路子網路](lync-server-2013-create-or-modify-network-subnets.md)  
[刪除網路子網路](lync-server-2013-deleting-network-subnets.md)

