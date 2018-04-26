---
title: Lync Server 管理命令介面
TOCTitle: Lync Server 管理命令介面
ms:assetid: 674b523b-c0b7-4ed6-9e67-afa6e8ac7e12
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398474(v=OCS.15)
ms:contentKeyID: 49291163
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 管理命令介面

 

_**上次修改主題的時間：** 2012-06-20_

與 Microsoft Office Communications Server 2007 R2 中可用的功能相較之下，Microsoft Lync Server 2010 引進一大組的新功能及改良功能。其中一項改良功能是管理實作的方式。例如，新的使用者介面 (稱為 Lync Server 控制台) 對於大部分習慣使用 Microsoft Management Console 的使用者即是一大轉變。其他對管理性的主要改良是納入 Windows PowerShell。

Windows PowerShell 可讓您從命令列管理 Microsoft 應用程式。它包括命令列環境、產品特定命令，以及完整指令碼語言。Windows PowerShell 一開始是在 2006 年年底引進為 Windows 作業系統的可下載版本，而且併入為用於管理 Microsoft Exchange Server 2007 的命令列介面。它從那時持續成長，而且已併入大部分的 Microsoft Server 產品，其中最新的是 Microsoft Lync Server 2013。Lync Server 2010 引進近 550 個產品特定的 Cmdlet，可用來管理部署的每個層面。

下列各節包含 Cmdlet 及其描述的清單。此資訊也可以直接從命令列取得。只要在 Lync Server 管理命令介面命令提示字元中輸入下列命令即可：

    Get-Help <cmdlet name> -Full

例如，若要從命令提示字元擷取 **New-CsVoicePolicy** Cmdlet 的說明，請輸入下列命令：

    Get-Help New-CsVoicePolicy -Full

Lync Server 2013 中的 Windows PowerShell 須知事項：

  - 若要執行 Lync Server Cmdlet，請開啟 Lync Server 管理命令介面。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您開啟 Windows PowerShell 視窗，而非 Lync Server 管理命令介面，則預設無法執行 Lync Server Cmdlet。若要從 Windows PowerShell 執行 Lync Server Cmdlet，請先在 Windows PowerShell 命令提示字元中鍵入下列命令：<br />
    Import-Module Lync</td>
    </tr>
    </tbody>
    </table>


  - Lync Server 管理命令介面會自動安裝在每部 Lync Server Enterprise Edition 前端伺服器或 Standard Edition Server 上。

  - 關於新增和更新資訊、範例指令碼以及開始使用與深入了解 Windows PowerShell 和 Microsoft Lync Server 2013 Cmdlet 的說明，請參閱 Lync Server Windows PowerShell 部落格 [http://go.microsoft.com/fwlink/?linkid=203150\&clcid=0x404 (英文)](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x404)。

