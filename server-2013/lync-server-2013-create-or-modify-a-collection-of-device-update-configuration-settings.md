---
title: 建立或修改裝置更新組態設定的集合
TOCTitle: 建立或修改裝置更新組態設定的集合
ms:assetid: 3e8ce95f-a8c8-417c-b1f7-0f759a567aff
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994029(v=OCS.15)
ms:contentKeyID: 52056093
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 建立或修改裝置更新組態設定的集合

 

_**上次修改主題的時間：** 2013-02-23_

您可以使用 Windows PowerShell 和 **New-CsDeviceUpdateConfiguration** Cmdlet 建立裝置更新組態設定 (只在網站範圍)，以及使用 **Set-CsDeviceUpdateConfiguration** Cmdlet 進行修改。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行這些 Cmdlet。

> [!NOTE]  
> 如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：<a href="http://go.microsoft.com/fwlink/p/?linkid=255876">http://go.microsoft.com/fwlink/p/?linkId=255876</a>。




## 使用預設值建立裝置更新組態設定

  - 此命令會針對 Redmond 網站建立一組新的裝置更新組態設定：
    
        New-CsDeviceUpdateConfiguration -Identity "site:Redmond"
    
    由於上述的命令除了指定必要的 Identity 參數以外，並未指定其他任何參數，因此新組態設定集合的所有屬性都將使用預設值。

## 在建立裝置更新組態設定時變更單一屬性值

  - 若要建立使用不同屬性值的設定，只需加入適當的參數和參數值即可。例如，若要建立裝置更新組態設定的集合，並且預設為每 21 天刪除舊的記錄檔，則可以使用下列命令：
    
        New-CsDeviceUpdateConfiguration -Identity "site:Redmond" -LogCleanupInterval "21.00:00:00"

## 在建立裝置更新組態設定時變更多個屬性值

  - 包含多個參數即可修改多個屬性值。例如，此命令會將記錄清除間隔設為 21 天，並將記錄排清間隔設為 30 分鐘︰
    
        New-CsDeviceUpdateConfiguration -Identity "site:Redmond" -LogCleanupInterval "21.00:00:00" -LogFlushInterval "00:30:00"

如需修改現有裝置組態設定的詳細資訊，請參閱 [Set-CsDeviceUpdateConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsDeviceUpdateConfiguration) Cmdlet 的說明主題。如需建立組態設定集合的詳細資訊，請參閱＜[New-CsDeviceUpdateConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsDeviceUpdateConfiguration)＞ Cmdlet 的說明主題。

