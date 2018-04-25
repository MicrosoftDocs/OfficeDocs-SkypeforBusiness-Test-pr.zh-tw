---
title: 適用於通訊錄管理的 New-CsWebServiceConfiguration
TOCTitle: 適用於通訊錄管理的 New-CsWebServiceConfiguration
ms:assetid: 49e4ecc5-aa3e-4dd4-a32c-b0dea3758fab
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg429703(v=OCS.15)
ms:contentKeyID: 49290823
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 適用於通訊錄管理的 New-CsWebServiceConfiguration

 

_**上次修改主題的時間：** 2012-11-01_

誰可以執行這個 Cmdlet：根據預設，會授權下列群組的成員在本機執行 New-CsWebServiceConfiguration Cmdlet：RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中輸入下列命令：

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "New-CsWebServiceConfiguration"}

New-CsWebServiceConfiguration 這個 Cmdlet 會為組織中的 Web 服務定義新的組態。Web 服務組態的範圍只能在網站或服務層級。無法在全域層級建立新的 Web 服務組態。對電話簿而言特別重要的是 EnableGroupExansion 屬性。如果設為 True，則 Web 服務可以回應群組擴充的要求。

例如：

    New-CsWebServiceConfiguration -Identity site:Redmond -EnableGroupExpansion $False -UseCertificateAuth $True

如需完整命令的詳細說明，請參閱主要 Lync Server Windows PowerShell RTCCmdlets 參考中的下列項目。

## 請參閱

#### 其他資源

[New-CsWebServiceConfiguration](new-cswebserviceconfiguration.md)

