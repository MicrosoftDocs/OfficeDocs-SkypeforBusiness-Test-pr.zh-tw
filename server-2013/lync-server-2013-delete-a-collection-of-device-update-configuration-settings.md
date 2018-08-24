---
title: 刪除裝置更新組態設定的集合
TOCTitle: 刪除裝置更新組態設定的集合
ms:assetid: 1a649136-34a9-42a7-a5b3-a78bbfe93f36
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994019(v=OCS.15)
ms:contentKeyID: 52056061
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除裝置更新組態設定的集合

 

_**上次修改主題的時間：** 2013-02-20_

您也可以使用 Windows PowerShell 和 **Remove-CsdeviceUpdateConfiguration** Cmdlet 來刪除裝置更新組態設定。此 Cmdlet 可從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。


## 移除特定的裝置更新組態設定集合

  - 此命令會刪除套用至 Redmond 網站的裝置更新組態設定：
    
        Remove-CsDeviceUpdateConfiguration -Identity "site:Redmond"

## 移除所有套用至網站範圍的裝置更新組態設定

  - 此命令會刪除所有套用至網站範圍的裝置更新組態設定：
    
        Get-CsDeviceUpdateConfiguration -Filter "site:*" | Remove-CsDeviceUpdateConfiguration

## 根據 LogCleanUpInterval 屬性值來移除裝置更新組態設定

  - 下列命令會刪除所有裝置更新組態設定，且記錄清除間隔大於 10 天 (10.00:00:00)︰
    
        Get-CsDeviceUpdateConfiguration | Where-Object {$_.LogCleanUpInterval -gt "10.00:00:00" | Remove-CsDeviceUpdateConfiguration

如需詳細資訊，請參閱＜[Remove-CsDeviceUpdateConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsDeviceUpdateConfiguration)＞ Cmdlet 的說明主題。

