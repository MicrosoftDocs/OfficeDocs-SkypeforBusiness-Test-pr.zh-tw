---
title: Lync Server 2013：刪除外部使用者存取的網站或使用者原則
TOCTitle: 刪除外部使用者存取的網站或使用者原則
ms:assetid: 6d907507-825b-4354-9c03-337a459f72de
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg521013(v=OCS.15)
ms:contentKeyID: 49291237
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中刪除外部使用者存取的網站或使用者原則

 

_**上次修改主題的時間：** 2013-02-22_

您可以在 **\[外部存取原則\]** 頁面中，刪除 Lync Server 控制台中所列的任何網站或使用者原則。刪除全域原則並不是實際加以刪除，只是將它重設為不支援任何外部使用者存取選項的預設設定。如需重設全域原則的詳細資訊，請參閱＜ [在 Lync Server 2013 中重設外部使用者存取的全域原則](lync-server-2013-reset-the-global-policy-for-external-user-access.md)＞。

## 刪除外部使用者存取的網站或使用者原則

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  按一下 **\[外部使用者存取\]** ，並按一下 **\[外部存取原則\]** 。

4.  在 **\[外部存取原則\]** 索引標籤上，按一下想要刪除的網站或使用者原則，並按一下 **\[編輯\]** ，然後按一下 **\[刪除\]** 。

5.  系統提示確認刪除時，請按一下 **\[確定\]** 。

## 使用 Windows PowerShell Cmdlet 移除 PIN 原則

外部存取原則可使用 Windows PowerShell 與 Remove-CsExternalAccessPolicy Cmdlet 加以刪除。此 Cmdlet 可從 Lync Server 2013 管理命令介面 或從 Windows PowerShell 的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 若要移除特定外部存取原則

  - 此命令會移除套用至 Redmond 網站的外部存取原則：
    
        Remove-CsExternalAccessPolicy -Identity "site:Redmond"

## 若要移除套用至個別使用者範圍的所有外部存取原則

  - 此命令會移除在個別使用者範圍內設定的外部存取原則：
    
        Get-CsExternalAccessPolicy -Filter "tag:*" | Remove-CsExternalAccessPolicy

## 若要移除停用外部使用者存取的所有外部存取原則

  - 此命令會刪除已停用外部使用者存取的所有外部存取原則：
    
        Get-CsExternalAccessPolicy | Where-Object {$_.EnableOutsideAccess -eq $False} | Remove-CsExternalAccessPolicy

如需詳細資訊，請參閱 [Remove-CsExternalAccessPolicy](remove-csexternalaccesspolicy.md) Cmdlet 的說明主題。

