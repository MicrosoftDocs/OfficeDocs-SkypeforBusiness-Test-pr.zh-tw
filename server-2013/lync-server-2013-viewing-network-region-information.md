---
title: 檢視網路地區資訊
TOCTitle: 檢視網路地區資訊
ms:assetid: 665740d0-a3ed-460f-8337-5ed945f90589
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688076(v=OCS.15)
ms:contentKeyID: 49890095
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視網路地區資訊

 

_**上次修改主題的時間：** 2013-02-23_

網路地區會與跨多個地理區域的網路不同部分交互連線。每個網路地區都必須與中央網站產生關聯。中央網站是執行通話許可控制服務 (CAC) 頻寬原則服務的資料中心網站。您可以使用 Lync Server 控制台來檢視網路地區。網路地區包含的設定可決定是否允許透過網際網路的替代路徑進行音訊和視訊連線。請使用本主題檢視現有的網路地區。如需建立或修改現有網路地區的詳細資訊，請參閱＜[建立或修改網路地區](lync-server-2013-creating-or-modifying-network-regions.md)＞。

## 利用 Lync Server 控制台檢視網路地區的資訊

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[網路設定\]** 和 **\[地區\]**。

4.  在 **\[地區\]** 頁面上，按一下您要檢視的區域。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您一次僅可檢視一個區域。</td>
    </tr>
    </tbody>
    </table>


5.  在 **\[編輯\]** 功能表上，按一下 **\[顯示詳細資料\]**。

## 使用 Windows PowerShell Cmdlet 檢視網路地區資訊

使用 Windows PowerShell 和 **Get-CsNetworkRegion** Cmdlet 可以檢視網路地區資訊。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 檢視網路區域資訊

  - 若要檢視所有網路地區的資訊，請在 Lync Server 管理命令介面中鍵入下列命令，然後按 ENTER 鍵：
    
        Get-CsNetworkRegion
    
    如此將傳回類似以下的資訊：
    
        Identity         : Pacific Northwest
        Description      :
        BypassID         : 3b232b84-2c1d-4da2-8181-e9330bafebe9
        CentralSite      : Site:Redmond1
        BWAlternatePaths : {BWPolicyModality=Audio;AlternatePath=True, 
                           BWPolicyModality=Video;AlternatePath=True}
        NetworkRegionID  : Pacific Northwest

如需詳細資訊，請參閱 [Get-CsNetworkRegion](get-csnetworkregion.md) Cmdlet 的說明主題。

## 請參閱

#### 工作

[建立或修改網路地區](lync-server-2013-creating-or-modifying-network-regions.md)  
[刪除現有網路地區](lync-server-2013-deleting-existing-network-regions.md)

