---
title: 檢視網站資訊
TOCTitle: 檢視網站資訊
ms:assetid: 24a97d98-b168-4016-81bf-c2c478092b87
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ687996(v=OCS.15)
ms:contentKeyID: 49889981
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視網站資訊

 

_**上次修改主題的時間：** 2013-02-23_

網路網站是設定在通話許可控制 (CAC) 或增強型 9-1-1 部署之每一個地區內部的辦公室或位置。您可在 Lync Server 2013 控制台或 Lync Server 管理命令介面中檢視網路網站資訊。如需建立或修改網路網站的詳細資訊，請參閱＜[建立或修改網站](lync-server-2013-creating-or-modifying-network-sites.md)＞。

## 若要在 Lync Server 控制台中檢視網路網站資訊

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 \[網路設定\] 和 \[網站\]。

4.  在 \[網站\] 頁面上，按一下您要檢視的網站。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您一次僅可檢視一個網站的網站資訊。</td>
    </tr>
    </tbody>
    </table>


5.  在 \[編輯\] 功能表上，按一下 \[顯示詳細資料\]。

## 若要使用 Lync Server 管理命令介面 Cmdlet 來檢視網路網站資訊

您也可以使用 Get-CsNetworkSite Cmdlet 來檢視網路網站資訊。此 Cmdlet 可從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 若要檢視網路網站資訊

  - 若要檢視網路網站的相關資訊，請在 Lync Server 管理命令介面中輸入下列命令，然後按 ENTER 鍵：
    
        Get-CsNetworkSite
    
    這會傳回類似如下的資訊：
    
        Identity          : Redmond
        NetworkSiteID     : Redmond
        Description       :
        NetworkRegionID   : Pacific Northwest
        BypassID          : 3b232b84-2c1d-4da2-8181-e9330bafebe9
        BWPolicyProfileID :
        LocationPolicy    :

如需詳細資訊，請參閱＜[Get-CsNetworkSite](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkSite)＞Cmdlet 的說明主題。

## 請參閱

#### 工作

[建立或修改網站](lync-server-2013-creating-or-modifying-network-sites.md)  
[刪除現有的網站](lync-server-2013-deleting-an-existing-network-site.md)

