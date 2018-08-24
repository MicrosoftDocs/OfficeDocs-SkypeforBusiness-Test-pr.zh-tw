---
title: 用於通訊錄管理的 Remove-CsWebServiceConfiguration
TOCTitle: 用於通訊錄管理的 Remove-CsWebServiceConfiguration
ms:assetid: 91947cad-5cdd-41b9-83e1-650703c55879
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg429713(v=OCS.15)
ms:contentKeyID: 49291670
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 用於通訊錄管理的 Remove-CsWebServiceConfiguration

 

_**上次修改主題的時間：** 2012-11-01_

誰可以執行這個 Cmdlet：根據預設，下列群組成員已獲得授權，可在本機執行 Remove-CsWebServiceConfiguration Cmdlet：RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中輸入下列命令：

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Remove-CsWebServiceConfiguration"}

Remove-CsWebServiceConfiguration Cmdlet 可讓系統管理員移除先前建立的 Web 服務設定。此 Cmdlet 無法移除全域 Web 服務設定。

例如：

    Remove-CsWebServiceConfiguration -Identity site:Redmond

如需完整命令的詳細說明，請參閱主要 Lync Server Windows PowerShell RTCCmdlets 參考中的下列項目。

## 請參閱

#### 其他資源

[Remove-CsWebServiceConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsWebServiceConfiguration)

