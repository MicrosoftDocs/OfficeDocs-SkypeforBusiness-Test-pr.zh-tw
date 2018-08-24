---
title: 將會議裝置移至新的登錄器集區
TOCTitle: 將會議裝置移至新的登錄器集區
ms:assetid: 26e02ca3-e881-4f90-8bf0-b13649108100
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994025(v=OCS.15)
ms:contentKeyID: 52056077
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將會議裝置移至新的登錄器集區

 

_**上次修改主題的時間：** 2013-02-20_

您可以使用 **Move-CsMeetingRoom** Cmdlet，將會議裝置從一個登錄器集區移至另一個登錄器集區。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行此 Cmdlet。

> [!NOTE]  
> 如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：<a href="http://go.microsoft.com/fwlink/p/?linkid=255876">http://go.microsoft.com/fwlink/p/?linkId=255876</a>。




## 將會議裝置移至新的登錄器集區

  - 若要移動會議裝置，您必須指定要移動之會議室的身分識別，然後將 Target 參數設為裝置要移至之登錄器集區的完整網域名稱 (FQDN)。例如︰
    
        Move-CsMeetingRoom -Target "atl-cs-001.litwareinc.com" -Identity "Room 14"

如需詳細資訊，請參閱＜[Move-CsMeetingRoom](https://docs.microsoft.com/en-us/powershell/module/skype/Move-CsMeetingRoom)＞ Cmdlet 的說明主題。

