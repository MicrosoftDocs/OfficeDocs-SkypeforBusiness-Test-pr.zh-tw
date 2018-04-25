---
title: 更新 Outlook 啟用清單
TOCTitle: 更新 Outlook 啟用清單
ms:assetid: 5db120dc-52f9-4dde-acb9-3824ae245086
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ215438(v=OCS.15)
ms:contentKeyID: 49291059
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 更新 Outlook 啟用清單

 

_**上次修改主題的時間：** 2013-01-07_

透過建立原則，將 Microsoft Lync 2013 的線上會議增益集包含在 Outlook 的增益集管理清單中，可以確保它對使用者一律保持啟用狀態。「增益集管理清單」原則包含在「群組原則管理主控台」的 Office 系統管理範本檔案中。它會在 HKCU\\Software\\Policies\\Microsoft\\Office\\15.0\\Outlook15\\Resiliency\\AddinList 下建立登錄機碼。您可以將 ucaddin.dll 的值新增至此機碼，然後設定 ucaddin.dll 值，使其一律保持啟用狀態，讓使用者無法手動停用它。

## 新增 ucaddin.dll 至 Outlook 增益集清單

  - 對位於 HKCU\\Software\\Policies\\Microsoft\\Office\\15.0\\Outlook15\\Resiliency\\AddinList 下的 AddinList 登錄機碼，新增下列的值︰
    
      - 登錄類型 = REG\_SZ
    
      - 名稱 = ucaddin.dll
    
      - 值 = 1 (指定增益集一律啟用，而且使用者無法管理)

