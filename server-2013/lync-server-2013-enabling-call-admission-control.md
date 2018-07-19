---
title: 啟用通話許可控制
TOCTitle: 啟用通話許可控制
ms:assetid: 015f5c8f-2f90-4b9e-8149-b33767e90582
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520942(v=OCS.15)
ms:contentKeyID: 49289896
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 啟用通話許可控制

 

_**上次修改主題的時間：** 2012-11-01_

通話許可控制 (CAC) 是由地區、網站和子網路所構成的網路，可讓您根據可用頻寬來限制音訊和視訊傳輸。在您設定 CAC 網路之後，您必須啟用 CAC 以強制實施頻寬限制。您可以使用 Lync Server 控制台執行這項作業。

## 從 Lync Server 控制台 啟用 CAC

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[網路設定\]**，然後按一下 **\[全域\]**。

4.  在 **\[全域\]** 頁面上，按一下 **\[全域\]** 設定。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>任何 Microsoft Lync Server 2013 部署都只能設定一個網路，所以清單中絕不會有一個以上的網路設定。您無法重新命名 [全域] 設定。</td>
    </tr>
    </tbody>
    </table>


5.  在 **\[編輯\]** 功能表上，按一下 **\[顯示詳細資料\]**。

6.  在 **\[編輯通用設定\]** 頁面上，選取 **\[啟用通話許可控制\]** 核取方塊，然後按一下 **\[認可\]**。

當您按一下 **\[認可\]** 時，便會執行設定的測試。**\[編輯通用設定\]** 對話方塊隨即關閉，您會回到 **\[全域\]** 頁面。如果在網路設定中發現任何會使網路無法正常運作 (例如，每個區域未透過區域間路由彼此連線) 的錯誤或不一致情形，您將會收到警告。

如果您變更了網路設定，您可以開啟 \[全域\] 設定並按一下 **\[認可\]**，再次執行驗證檢查。您不需要先停用 CAC：使核取方塊保持已勾選狀態並按一下 **\[認可\]**。您可以隨時這麼做，而不需進行任何設定變更。

## 請參閱

#### 概念

[Lync Server 2013 中的通話許可控制概觀](lync-server-2013-overview-of-call-admission-control.md)  

#### 其他資源

[在 Lync Server 2013 中規劃通話許可控制](lync-server-2013-planning-for-call-admission-control.md)  
[在 Lync Server 2013 中設定通話許可控制](lync-server-2013-configure-call-admission-control.md)  
[Get-CsNetworkConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkConfiguration)  
[Set-CsNetworkConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsNetworkConfiguration)  
[Remove-CsNetworkConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsNetworkConfiguration)

