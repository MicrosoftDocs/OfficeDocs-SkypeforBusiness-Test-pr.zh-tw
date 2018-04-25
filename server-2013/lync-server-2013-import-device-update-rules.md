---
title: 匯入裝置更新規則
TOCTitle: 匯入裝置更新規則
ms:assetid: 919e9c87-912b-4bc9-92e7-5998fc2e0bf0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994056(v=OCS.15)
ms:contentKeyID: 52056148
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 匯入裝置更新規則

 

_**上次修改主題的時間：** 2013-02-23_

裝置更新規則僅可使用 Windows PowerShell 和 **Import-CsDeviceUpdate** Cmdlet 來匯入。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行此 Cmdlet。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：<a href="http://go.microsoft.com/fwlink/p/?linkid=255876">http://go.microsoft.com/fwlink/p/?linkId=255876</a>。</td>
</tr>
</tbody>
</table>



## 將裝置更新規則匯入單一 Web 伺服器

  - 下列命令會將裝置更新規則匯入 Web 伺服器 atl-cs-001.litwareinc.com：
    
        Import-CsDeviceUpdate -Identity "service:WebServer:atl-cs-001.litwareinc.com" -FileName C:\Updates\UCUpdates.cab

## 將裝置更新規則匯入所有 Web 伺服器

  - 例如，裝置更新規則會匯入您的組織中所部署的所有 Web 伺服器。若要讓此命令成功運作，必須共用資料夾 \\\\atl-fs-001.litwareinc.com\\Updates，並提供給所有 Web 伺服器使用。
    
        Get-CsService -WebServer | ForEach-Object {Import-CsDeviceUpdate -Identity $_.Identity -FileName \\atl-fs-001.litwareinc.com\Updates\UCUpdates.cab}

如需詳細資訊，請參閱＜[Import-CsDeviceUpdate](import-csdeviceupdate.md)＞ Cmdlet 的說明主題。

## 請參閱

#### 工作

[檢視裝置更新規則的資訊](lync-server-2013-view-information-about-device-update-rules.md)  
[核准裝置更新規則](lync-server-2013-approve-a-device-update-rule.md)

