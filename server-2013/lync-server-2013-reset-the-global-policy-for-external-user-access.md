---
title: Lync Server 2013：重設外部使用者存取的全域原則
TOCTitle: 重設外部使用者存取的全域原則
ms:assetid: 8207e1b1-de9e-461f-975f-fcc5c526849a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182545(v=OCS.15)
ms:contentKeyID: 49291508
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中重設外部使用者存取的全域原則

 

_**上次修改主題的時間：** 2013-02-22_

您無法完全刪除全域原則。使用全域原則的 **\[刪除\]** 選項只會將全域原則重設為預設設定，而預設設定不包含對任何外部使用者存取選項的支援。

## 若要將全域原則重設為預設設定

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[外部使用者存取\]** 和 **\[外部存取原則\]** 。

4.  在 **\[外部存取原則\]** 索引標籤上，依序按一下全域原則、 **\[編輯\]** 和 **\[刪除\]** 。

5.  系統提示確認刪除時，請按一下 \[確定\] 。頁面頂端會出現一則訊息，通知您已將全域原則重設。

## 使用 Windows PowerShell Cmdlet 重設全域外部存取原則

使用 Windows PowerShell 和 Remove-CsExternalAccessPolicy Cmdlet 也可重設全域外部存取原則。可從 Lync Server 2013 管理命令介面 或從遠端工作 Windows PowerShell 執行這個 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 重設全域外部存取原則

  - 這個命令可重設全域外部存取原則：
    
        Remove-CsExternalAccessPolicy -Identity "global"

如需詳細資訊，請參閱 [Remove-CsExternalAccessPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsExternalAccessPolicy) Cmdlet 的說明主題。

