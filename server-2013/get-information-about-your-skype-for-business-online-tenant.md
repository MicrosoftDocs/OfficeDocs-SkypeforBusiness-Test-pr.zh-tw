---
title: 取得 Lync Online 租用戶的相關資訊
TOCTitle: 取得 Lync Online 租用戶的相關資訊
ms:assetid: 06467515-9114-45bb-8d09-26a915c3fc4d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362768(v=OCS.15)
ms:contentKeyID: 56269064
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 取得 Lync Online 租用戶的相關資訊

 

_**上次修改主題的時間：** 2015-06-22_

若要傳回 商務用 Skype Online 租用戶的相關資訊，請呼叫 [Get-CsTenant](get-cstenant.md) Cmdlet，無需加入任何額外參數：

    Get-CsTenant

若是僅要傳回租用戶名稱與識別碼 (執行 [Set-CsTenantPublicProvider](set-cstenantpublicprovider.md) 與 [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) 等 Cmdlet 需要有 TenantID 參數值)，請使用以下命令：

    Get-CsTenant | Select-Object Name, TenantID

## 請參閱

#### 概念

[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

