---
title: 刪除網路頻寬原則設定檔
TOCTitle: 刪除網路頻寬原則設定檔
ms:assetid: 4d6beda8-6aa5-4d5e-8a07-363598f0e0c8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688050(v=OCS.15)
ms:contentKeyID: 49890057
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除網路頻寬原則設定檔

 

_**上次修改主題的時間：** 2012-11-01_

頻寬原則為通話許可控制 (CAC) 的一部分，用於定義某些形式的頻寬限制。在 Microsoft Lync Server 2013 中，只會指派音訊與視訊形式的頻寬限制。您可以設定整體頻寬限制和工作階段限制。您可以使用 Lync Server 控制台建立、修改或刪除這些原則的容器設定檔。請使用下列程序來刪除網路頻寬原則設定檔。如需有關建立或修改網路頻寬原則設定檔的詳細資訊，請參閱＜[建立或修改頻寬原則設定檔](lync-server-2013-creating-or-modifying-bandwidth-policy-profiles.md)＞。

## 刪除頻寬原則設定檔

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[網路設定\]**，再按一下 **\[頻寬原則\]**。

4.  在 **\[頻寬原則\]** 頁面上，按一下您要刪除的頻寬原則設定檔。
    
    > [!NOTE]  
    > 您可以一次刪除一個以上的設定檔。若要這麼做，請按住 CTRL 鍵並同時選取多個設定檔。或者，若要選取所有設定檔，請按一下 <strong>[編輯]</strong> 功能表上的 <strong>[全選]</strong>。
    


5.  在 **\[編輯\]** 功能表上，按一下 **\[刪除\]**。
    
    > [!WARNING]
    > 您無法刪除與網站關聯的頻寬原則設定檔。您必須先移除與網站的關聯，才可以刪除設定檔。如需有關如何修改網站的詳細資訊，請參閱＜<a href="lync-server-2013-creating-or-modifying-network-sites.md">建立或修改網站</a>＞。


## 請參閱

#### 工作

[建立或修改頻寬原則設定檔](lync-server-2013-creating-or-modifying-bandwidth-policy-profiles.md)  
[檢視網路頻寬原則設定檔資訊](lync-server-2013-viewing-network-bandwidth-policy-profile-information.md)  

#### 其他資源

[在 Lync Server 2013 中設定通話許可控制](lync-server-2013-configure-call-admission-control.md)  
[Remove-CsNetworkBandwidthPolicyProfile](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsNetworkBandwidthPolicyProfile)

