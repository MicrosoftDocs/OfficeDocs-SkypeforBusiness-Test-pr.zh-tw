---
title: 檢視位置原則資訊
TOCTitle: 檢視位置原則資訊
ms:assetid: 14e41bcb-ea0a-49c2-99b3-1f61fc34416d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520954(v=OCS.15)
ms:contentKeyID: 49290186
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視位置原則資訊

 

_**上次修改主題的時間：** 2012-11-01_

在 Lync Server 2013 中，您可以使用位置原則來套用與增強型 9-1-1 (E9-1-1) 功能和使用者或連絡人的位置設定相關的設定。位置原則會判斷使用者是否已啟用 E9-1-1，如果是，則會決定緊急電話的行為。例如，您可以使用位置原則來定義組成緊急電話的數字 (例如，在美國為 911)、是否應自動告知公司的安全部門，以及應如何路由傳送來電。

您可以從 Lync Server 2013 控制台中的 \[網路設定\] 群組來設定位置原則。您可以從 Lync Server 控制台檢視、建立、修改或刪除位置原則。請使用下列程序來檢視位置原則的相關資訊。如需建立或修改位置原則的詳細資訊，請參閱＜[建立或修改位置原則](lync-server-2013-creating-or-modifying-a-location-policy.md)＞。

## 檢視位置原則的相關資訊

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中按一下 **\[網路設定\]**，然後按一下 **\[位置原則\]**。

4.  在 **\[位置原則\]** 頁面上，選取您要修改的位置原則。

5.  在 **\[編輯\]** 功能表上，按一下 **\[顯示詳細資料\]**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您一次只能檢視一個位置原則的相關資訊。</td>
    </tr>
    </tbody>
    </table>


依預設會有名為「通用」的單一原則存在，且無法刪除或重新命名。但您可以修改全域原則。若您未建立網站原則或個別使用者原則，則所有使用者與連絡人都會套用此原則。特定的使用者必須套用個別使用者原則。

## 請參閱

#### 工作

[建立或修改位置原則](lync-server-2013-creating-or-modifying-a-location-policy.md)  
[在 Lync Server 2013 中建立位置原則](lync-server-2013-create-location-policies.md)  
[在 Lync Server 2013 中建立或修改網站](lync-server-2013-create-or-modify-a-network-site.md)  

#### 其他資源

[New-CsLocationPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsLocationPolicy)  
[Set-CsLocationPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsLocationPolicy)  
[Remove-CsLocationPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsLocationPolicy)  
[Get-CsLocationPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsLocationPolicy)

