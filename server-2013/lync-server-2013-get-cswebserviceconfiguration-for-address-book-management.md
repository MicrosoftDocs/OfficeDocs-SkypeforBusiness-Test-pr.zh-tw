---
title: 適用於通訊錄管理的 Get-CsWebServiceConfiguration
TOCTitle: 適用於通訊錄管理的 Get-CsWebServiceConfiguration
ms:assetid: 0b223733-5224-47d1-9b47-2109e6f135c9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg429692(v=OCS.15)
ms:contentKeyID: 49290045
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 適用於通訊錄管理的 Get-CsWebServiceConfiguration

 

_**上次修改主題的時間：** 2012-11-01_

誰可以執行這個 Cmdlet：根據預設，會授權下列群組的成員在本機執行 Get-CsWebServiceConfiguration Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中輸入下列命令：

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Get-CsWebServiceConfiguration"}

Get-CsWebServiceConfiguration 會傳回目前貴組織中使用的 Web 服務組態資訊。通訊群組清單延伸功能的狀態對於通訊錄服務有益。如果 EnableGroupExpansion 屬性為 True，則您的組織目前可允許群組延伸。

例如：

    Get-CsWebServiceConfiguration -Identity site:Redmond

如需完整命令的詳細說明，請參閱主要 Lync Server Windows PowerShell RTCCmdlets 參考中的下列項目。

## 請參閱

#### 其他資源

[Get-CsWebServiceConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsWebServiceConfiguration)

