---
title: 檢視網路地區連結資訊
TOCTitle: 檢視網路地區連結資訊
ms:assetid: 7b6b2ea2-83d8-4376-afb2-70e5d2cf6444
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688102(v=OCS.15)
ms:contentKeyID: 49890128
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視網路地區連結資訊

 

_**上次修改主題的時間：** 2013-02-23_

您可以透過通話許可控制 (CAC) 檢視兩個網路地區之間的連結。網路中的地區是透過實體廣域網路 (WAN) 連線相連結。您可以使用 Lync Server 控制台檢視兩個網路地區之間現有的連結。如需關於建立或修改網路地區連結的詳細資訊，請參閱＜[設定網路區域連結](lync-server-2013-configuring-network-region-links.md)＞。

## 在 Lync Server 控制台中檢視網路地區

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  按一下左導覽列中的 \[網路設定\]，然後按一下 \[地區連結\]。

4.  在 \[區域連結\] 頁面中，按一下要檢視的區域連結。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>一次只能檢視一個區域的資訊。</td>
    </tr>
    </tbody>
    </table>


5.  從 \[編輯\] 功能表中，選取 \[顯示詳細資料\]。

## 使用 Lync Server 管理命令介面 Cmdlet 檢視網路地區連結資訊

您可以使用 Lync Server 管理命令介面和 **Get-CsNetworkRegionLink** Cmdlet 檢視網路地區連結。您可以從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 檢視網路地區連結資訊

  - 若要檢視所有網路地區連結的資訊，請在 Lync Server 管理命令介面中輸入下列命令，然後按下 ENTER 鍵：
    
        Get-CsNetworkRegionLink
    
    此命令將傳回類似下列所示的資訊：
    
        Identity            : NorthwestToCalifornia
        BWPolicyProfileID   :
        NetworkRegionLinkID : NorthwestToCalifornia
        NetworkRegionID1    : Pacific Northwest
        NetworkRegionID2    : California

如需詳細資訊，請參閱 [Get-CsNetworkRegionLink](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkRegionLink)。

## 請參閱

#### 工作

[設定網路站台連結](lync-server-2013-configuring-network-site-links.md)

