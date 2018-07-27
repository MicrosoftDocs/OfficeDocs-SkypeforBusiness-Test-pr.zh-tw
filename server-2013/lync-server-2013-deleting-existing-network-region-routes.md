---
title: 刪除現有的網路地區路由
TOCTitle: 刪除現有的網路地區路由
ms:assetid: 6256ff80-5f1e-48b4-928b-24aeb3c1a0e7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688074(v=OCS.15)
ms:contentKeyID: 49890091
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除現有的網路地區路由

 

_**上次修改主題的時間：** 2012-11-01_

通話許可控制服務 (CAC) 組態內的每個地區，都必須要有辦法存取其他每個地區。地區連結會設定地區間連線的頻寬限制，也代表實體連結，路由則會決定從甲地連線到乙地時要周遊的連結路徑。您可以使用 Lync Server 控制台來設定網路地區路由。您也可以從 Lync Server 控制台建立、修改或刪除網路地區路由。若要刪除現有的網路地區路由，請利用本主題。如需有關建立或修改網路地區路由的詳細資訊，請參閱＜[建立或修改網路地區路由](lync-server-2013-creating-or-modifying-network-region-routes.md)＞。

## 刪除網路地區路由

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[網路設定\]** 和 **\[地區路由\]**。

4.  在 **\[地區路由\]** 頁面上，按一下您要刪除的地區路由。
    
    > [!NOTE]  
    > 您可以同時刪除多個地區路由。如果要執行這項作業，請按住 CTRL 鍵，然後選取多個地區路由。或者，若要選取所有地區路由，請按一下 <strong>[編輯]</strong> 功能表上的 <strong>[全選]</strong>。
    


5.  在 **\[編輯\]** 功能表中，按一下 **\[刪除\]**。

6.  按一下 **\[確定\]**。

## 請參閱

#### 工作

[建立或修改網路地區路由](lync-server-2013-creating-or-modifying-network-region-routes.md)  

#### 概念

[設定網路區域路由](https://technet.microsoft.com/zh-tw/library/gg133706\(v=ocs.15\))  

#### 其他資源

[New-CsNetworkInterRegionRoute](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsNetworkInterRegionRoute)  
[Set-CsNetworkInterRegionRoute](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsNetworkInterRegionRoute)  
[Remove-CsNetworkInterRegionRoute](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsNetworkInterRegionRoute)  
[Get-CsNetworkInterRegionRoute](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkInterRegionRoute)

