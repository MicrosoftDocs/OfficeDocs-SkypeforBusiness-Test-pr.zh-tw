---
title: 使用 PowerShell 管理集中式記錄服務組態設定
TOCTitle: 使用 PowerShell 管理集中式記錄服務組態設定
ms:assetid: f455c3aa-0061-413d-bdfb-a3e78f82723d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721938(v=OCS.15)
ms:contentKeyID: 49890507
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用 PowerShell 管理集中式記錄服務組態設定

 

_**上次修改主題的時間：** 2012-11-01_

將命令傳送至個別電腦 集中記錄服務 代理程式 (CLSAgent) 的 集中記錄服務 控制器 (CLSController) 所建立與使用的設定值與參數，會控制與設定 集中記錄服務。代理程式會處理傳送來的命令 (在使用 Start 命令的情況)，並使用案例的設定、提供者、日誌大小、追蹤期間以及旗標，根據提供的設定資訊開始收集追蹤日誌。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>並非所有列出的 集中記錄服務Windows PowerShell Cmdlet 均適用於 Lync Server 2013 的內部部署。雖然看起來似乎可行，但下列 Cmdlet 並非針對與 Lync Server 2013 內部部署共用而設計：
<ul>
<li><p><strong>CsClsRegion Cmdlet：</strong> <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsClsRegion">Get-CsClsRegion</a>、<a href="https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClsRegion">Set-CsClsRegion</a>、<a href="https://docs.microsoft.com/en-us/powershell/module/skype/New-CsClsRegion">New-CsClsRegion</a> 及 <a href="https://docs.microsoft.com/en-us/powershell/module/skype/New-CsClsRegion">Remove-CsClsRegion</a>。</p></li>
<li><p><strong>CsClsSearchTerm Cmdlet：</strong> <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsClsSearchTerm">Get-CsClsSearchTerm</a> 與 <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClsSearchTerm">Set-CsClsSearchTerm</a>。</p></li>
<li><p><strong>CsClsSecurityGroup Cmdlet：</strong> <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsClsSecurityGroup">Get-CsClsSecurityGroup</a>、<a href="https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClsSecurityGroup">Set-CsClsSecurityGroup</a>、<a href="https://docs.microsoft.com/en-us/powershell/module/skype/New-CsClsSecurityGroup">New-CsClsSecurityGroup</a> 及 <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsClsSecurityGroup">Remove-CsClsSecurityGroup</a>。</p></li>
</ul>
這些 Cmdlet 中定義的設定，不會妨礙或引發任何反作用，但它們是針對與 Microsoft Office 365 共用而設計，因此在內部部署中不會產生預期的結果。這並不表示這些 Cmdlet 在內部部署中毫無用處，只是本文件並未探討其用途的進階主題。</td>
</tr>
</tbody>
</table>


## 本章節內容

本節主題是定義 集中記錄服務 的設定選項、參數及設定值。如何設定 集中記錄服務、如何擷取設定值、建立實例、管理 集中記錄服務 的安全性群組、搜尋以及更多內容的相關資訊，均包含於下列主題。

  - [管理電腦、網站及全域集中式記錄服務組態](lync-server-2013-managing-computer-site-and-global-centralized-logging-service-configuration.md)

  - [設定集中式記錄服務的提供者](lync-server-2013-configuring-providers-for-centralized-logging-service.md)

  - [設定集中式記錄服務的案例](lync-server-2013-configuring-scenarios-for-the-centralized-logging-service.md)

## 請參閱

#### 概念

[集中式記錄服務概觀](lync-server-2013-overview-of-the-centralized-logging-service.md)  
[Centralized Logging Cmdlet](lync-server-2013-centralized-logging-cmdlets.md)

