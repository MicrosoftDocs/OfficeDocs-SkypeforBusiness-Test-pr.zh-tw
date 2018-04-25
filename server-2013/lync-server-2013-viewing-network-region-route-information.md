---
title: 檢視網路地區路由資訊
TOCTitle: 檢視網路地區路由資訊
ms:assetid: 34dd9fa3-e695-4680-b244-3019298b5009
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688021(v=OCS.15)
ms:contentKeyID: 49890019
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視網路地區路由資訊

 

_**上次修改主題的時間：** 2013-02-23_

通話許可控制 (CAC) 組態內的每個地區都必須要有辦法存取其他每個地區。地區連結會設定地區間連線的頻寬限制，也代表實體連結，而路由會決定從甲地連線到乙地時要採取的連結路徑。請使用下列程序來檢視 Lync Server 2013 控制台或 Lync Server 2013 管理命令介面中現有的網路地區路由。如需有關建立或修改網路地區路由的詳細資訊，請參閱＜[建立或修改網路地區路由](lync-server-2013-creating-or-modifying-network-region-routes.md)＞。

## 檢視 Lync Server 控制台中的網路地區路由資訊

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[網路組態\]** 和 \[地區路由\]。

4.  在 \[地區路由\] 頁面上，按一下要檢視的地區路由。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您一次只能檢視一個地區路由。</td>
    </tr>
    </tbody>
    </table>


5.  在 **\[編輯\]** 功能表上，按一下 \[顯示詳細資料\]。

## 使用 Lync Server PowerShell Cmdlet 檢視網路地區路由資訊

網路地區路由資訊也可以使用 Lync Server PowerShell 和 Get-CsNetworkInterRegionRoute Cmdlet 來檢視。這個 Cmdlet 可以從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 檢視網路地區路由資訊

  - 若要檢視有關您所有網路地區路由的資訊，請在 Lync Server 管理命令介面中輸入下列命令，然後按 ENTER：
    
        Get-CsNetworkInterRegionRoute
    
    即會傳回類似下列的資訊：
    
        Identity                  : TransAmericaRoute
        NetworkRegionLinks        : {NorthwestToNortheast}
        InterNetworkRegionRouteID : TransAmericaRoute
        NetworkRegionID1          : Pacific Northwest
        NetworkRegionID2          : Northeast

如需詳細資訊，請參閱適用於 [Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md) Cmdlet 的說明主題。

## 請參閱

#### 工作

[建立或修改網路地區路由](lync-server-2013-creating-or-modifying-network-region-routes.md)  
[刪除現有的網路地區路由](lync-server-2013-deleting-existing-network-region-routes.md)

