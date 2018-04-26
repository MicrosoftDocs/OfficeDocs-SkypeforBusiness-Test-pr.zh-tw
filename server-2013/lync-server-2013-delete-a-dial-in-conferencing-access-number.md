---
title: 刪除電話撥入式會議存取號碼
TOCTitle: 刪除電話撥入式會議存取號碼
ms:assetid: 199c5d9c-0489-4ad5-a7f1-ca59fe0e6ac7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520956(v=OCS.15)
ms:contentKeyID: 49290235
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除電話撥入式會議存取號碼

 

_**上次修改主題的時間：** 2013-02-23_

遵循下列步驟，可刪除電話撥入式會議存取號碼。

## 刪除電話撥入式會議存取號碼

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限) 或指派給 CsServerAdministrator 或 CsAdministrator 角色的使用者帳戶，登入部署 Lync Server 2013 之網路上的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[會議\]，然後按一下 \[撥入存取號碼\]。

4.  在頁面中，按一下清單中要刪除的撥入號碼，按一下 **\[編輯\]**，再按一下 **\[刪除\]**。

5.  按一下 **\[確定\]**。

## 使用 Windows PowerShell Cmdlet 移除電話撥入式會議存取號碼

電話撥入式會議存取號碼也可以用 Windows PowerShell 和 **Remove-CsDialInConferencingAccessNumber** Cmdlet 來刪除。此 Cmdlet 可從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 移除特定電話撥入式會議存取號碼

  - 下列命令會刪除識別碼為 sip:RedmondDialInAccess@litwareinc.com 的電話撥入式會議存取號碼：
    
        Remove-CsDialInConferencingAccessNumber -Identity "sip:RedmondDialInAccess@litwareinc.com"

## 移除指派給特定地區的所有電話撥入式會議存取號碼

  - 下列命令會刪除與西北地區相關聯的所有電話撥入式會議存取號碼：
    
        Get-CsDialInConferencingAccessNumber -Region "Northwest" | Remove-CsDialInConferencingAccessNumber

## 根據主要語言移除電話撥入式會議存取號碼

  - 下列命令會刪除主要語言為義大利文的所有電話撥入式會議存取號碼：
    
        Get-CsDialInConferencingAccessNumber | Where-Object {$_.PrimaryLanguage -eq "it-IT"} | Remove-CsDialInConferencingAccessNumber

如需詳細資訊，請參閱＜[Remove-CsDialInConferencingAccessNumber](remove-csdialinconferencingaccessnumber.md)＞Cmdlet 的說明主題。

