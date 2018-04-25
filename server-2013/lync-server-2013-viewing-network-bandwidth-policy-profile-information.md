---
title: 檢視網路頻寬原則設定檔資訊
TOCTitle: 檢視網路頻寬原則設定檔資訊
ms:assetid: eed453fc-04e9-4971-959c-6fad54bf1c96
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721931(v=OCS.15)
ms:contentKeyID: 49890381
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視網路頻寬原則設定檔資訊

 

_**上次修改主題的時間：** 2013-02-23_

頻寬原則為通話許可控制 (CAC) 的一部分，用於定義某些形式的頻寬限制。在 Microsoft Lync Server 2013 中，只會指派音訊與視訊形式的頻寬限制。您可以設定整體頻寬限制和工作階段限制。您可以使用 Lync Server 控制台建立或修改這些原則的容器設定檔。每個頻寬原則設定檔可以與一或多個網路網站建立關聯。請依照下列程序檢視頻寬原則設定檔。要建立或修改頻寬原則設定檔，請參閱＜[建立或修改頻寬原則設定檔](lync-server-2013-creating-or-modifying-bandwidth-policy-profiles.md)＞。

## 若要修改頻寬原則設定檔

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中按一下 \[網路設定\]，然後按一下 \[位置原則\]。

4.  在 \[頻寬原則\] 頁面上，按一下您要修改的頻寬原則設定檔。

5.  在 \[編輯\] 功能表上，按一下 \[顯示詳細資料\]。

## 使用 Lync Server PowerShell Cmdlet 檢視網路頻寬原則設定檔資訊

網路頻寬原則設定檔也可透過 Lync Server PowerShell 與 Get-CsNetworkBandwidthPolicyProfile Cmdlet 檢視。此 Cmdlet 可從 Lync Server 2013 管理命令介面或 Windows PowerShell 的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 檢視網路頻寬原則設定檔資訊

  - 要檢視所有網路頻寬原則設定檔相關資訊，請在 Lync Server 管理命令介面輸入下列命令，然後按下 ENTER：
    
        Get-CsNetworkBandwidthPolicyProfile
    
    這樣將傳回類似下列的資訊：
    
        Identity          : RedmondBandwidthPolicy
        BWPolicy          : {BWLimit=200;BWSessionLimit=200;
                            BWPolicyModality=Audio, 
                            BWLimit=1400;BWSessionLimit=500;
                            BWPolicyModality=Video}
        BWPolicyProfileID : RedmondBandwidthPolicy
        Description       :

如需詳細資訊，請參閱＜[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)＞Cmdlet 的說明主題。

## 請參閱

#### 工作

[建立或修改頻寬原則設定檔](lync-server-2013-creating-or-modifying-bandwidth-policy-profiles.md)  
[刪除網路頻寬原則設定檔](lync-server-2013-deleting-network-bandwidth-policy-profiles.md)  

#### 其他資源

[在 Lync Server 2013 中設定通話許可控制](lync-server-2013-configure-call-admission-control.md)

