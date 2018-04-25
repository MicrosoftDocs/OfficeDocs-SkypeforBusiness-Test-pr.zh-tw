---
title: 安裝 WMI 回溯相容性套件
TOCTitle: 安裝 WMI 回溯相容性套件
ms:assetid: 38797fbd-06a0-4008-b099-158e7b5d7703
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204816(v=OCS.15)
ms:contentKeyID: 49290603
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 安裝 WMI 回溯相容性套件

 

_**上次修改主題的時間：** 2012-10-02_

若您未安裝 WMI 回溯相容性套件，而嘗試啟動 \[拓撲產生器合併精靈\]，您會看到下列錯誤：

![WMI 錯誤訊息](images/JJ204816.a007d2f2-fc85-430c-91eb-382b032469af(OCS.15).jpg "WMI 錯誤訊息")

若您未安裝 WMI 回溯相容性套件，而嘗試啟動 **Merge-CsLegacytopology** Cmdlet，您會看到下列錯誤：

![Windows PowerShell WMI 提供者錯誤](images/JJ204816.c510824e-1807-4c7e-bb28-c6cfea2eac1d(OCS.15).jpg "Windows PowerShell WMI 提供者錯誤")

安裝 WMI 回溯相容性套件

1.  在安裝媒體上，瀏覽至 \\SETUP\\AMD64\\SETUP\\OCSWMIBC.MSI。

2.  安裝 OCSWMIBC.MSI。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>OCSWMIBC.msi 必須安裝在執行 [拓撲產生器合併精靈] 的電腦上。然而，建議將 OCSWMIBC.msi 安裝在拓撲中的所有前端伺服器上。</td>
    </tr>
    </tbody>
    </table>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>凡位於安裝有 Lync Server 2013 核心元件及 Lync Server 2013 管理命令介面的網域中，並有權存取 Office Communications Server 2007 R2 拓撲 (WMI 提供者至 Active Directory 網域服務 (AD DS) 及 SQL Server) 的電腦，皆可安裝 OCSWMIBC.msi。</td>
    </tr>
    </tbody>
    </table>

