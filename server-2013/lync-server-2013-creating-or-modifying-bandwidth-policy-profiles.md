---
title: 建立或修改頻寬原則設定檔
TOCTitle: 建立或修改頻寬原則設定檔
ms:assetid: 08a2e18f-9b0d-4a2f-aa14-13bbf79ec745
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520945(v=OCS.15)
ms:contentKeyID: 49290014
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 建立或修改頻寬原則設定檔

 

_**上次修改主題的時間：** 2012-10-15_

頻寬原則為通話許可控制 (CAC) 的一部分，可用來定義某些形式的頻寬限制。在 Microsoft Lync Server 2013 中，只能指派音訊與視訊形式的頻寬限制。您可以設定整體頻寬限制和工作階段限制。您可以使用 Lync Server 控制台來建立、修改或刪除這些原則的容器設定檔。每個頻寬原則設定檔可以與一或多個網路網站產生關聯。請使用下列程序來建立或修改頻寬原則設定檔。若要刪除頻寬原則設定檔，請參閱＜[刪除網路頻寬原則設定檔](lync-server-2013-deleting-network-bandwidth-policy-profiles.md)＞。

## 若要建立新的頻寬原則設定檔

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[網路設定\]，然後按一下 \[頻寬原則\]。

4.  在「頻寬原則」頁面上，按一下 \[新增\]。

5.  在 **\[新增頻寬原則設定檔\]** 的 **\[名稱\]** 欄位中輸入名稱。在所有頻寬原則設定檔中，此名稱必須是唯一的。

6.  在 **\[音訊限制\]** 欄位中輸入數值。此值是要配置給所有音訊連線的最大頻寬數量 (以 kbps 表示)。

7.  在 **\[音訊工作階段限制\]** 欄位中輸入數值。此值是要配置給個別音訊連線的最大頻寬數量 (以 kbps 表示)。此值必須為 40 或更大。

8.  在 **\[視訊限制\]** 欄位中輸入數值。此值是要配置給所有視訊連線的最大頻寬數量 (以 kbps 表示)。

9.  在 **\[視訊工作階段限制\]** 欄位中輸入數值。此值是要配置給個別視訊連線的最大頻寬數量 (以 kbps 表示)。此值必須為 100 或更大。

10. (選用) 在 **\[描述\]** 欄位中輸入值，以提供更多有關此頻寬原則設定檔 (無法單獨以名稱表示) 的資訊。

11. 按一下 **\[認可\]**。
    
    > [!NOTE]  
    > 建立新的頻寬原則設定檔並不會自動強制頻寬限制。您必須先讓原則設定檔與網站產生關聯。如需有關如何讓原則設定檔與網站產生關聯的詳細資訊，請參閱＜<a href="lync-server-2013-creating-or-modifying-network-sites.md">建立或修改網站</a>＞。
    


## 若要修改頻寬原則設定檔

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[網路設定\]，然後按一下 \[頻寬原則\]。

4.  在「頻寬原則」頁面上，按一下您要修改的頻寬原則設定檔。

5.  在 **\[編輯\]** 功能表上，按一下 **\[顯示詳細資料\]**。

6.  在 **\[編輯頻寬原則設定檔\]** 頁面上，視需要修改欄位 (如需詳細資訊，請參閱本主題中前面的＜若要建立頻寬原則設定檔＞一節)。

7.  按一下 **\[認可\]**。
    
    > [!NOTE]  
    > 當您修改頻寬原則設定檔時，將會立即更新與此頻寬原則設定檔關聯的所有網路網站的頻寬限制。
    


## 請參閱

#### 工作

[刪除網路頻寬原則設定檔](lync-server-2013-deleting-network-bandwidth-policy-profiles.md)  

#### 其他資源

[在 Lync Server 2013 中設定通話許可控制](lync-server-2013-configure-call-admission-control.md)  
[New-CsNetworkBandwidthPolicyProfile](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsNetworkBandwidthPolicyProfile)  
[Set-CsNetworkBandwidthPolicyProfile](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsNetworkBandwidthPolicyProfile)  
[Get-CsNetworkBandwidthPolicyProfile](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkBandwidthPolicyProfile)

