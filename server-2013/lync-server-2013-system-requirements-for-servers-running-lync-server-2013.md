---
title: Lync Server 2013：執行 Lync Server 2013 之伺服器的系統需求
TOCTitle: 執行 Lync Server 2013 之伺服器的系統需求
ms:assetid: 781d487d-5958-416a-becb-904d9af3cc0a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398588(v=OCS.15)
ms:contentKeyID: 49291376
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 執行 Lync Server 2013 之伺服器的系統需求

 

_**上次修改主題的時間：** 2014-07-24_

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需有關硬體需求的詳細資訊，請參閱＜ <a href="lync-server-2013-server-hardware-platforms.md">Lync Server 2013 的伺服器硬體平台</a>＞。</td>
</tr>
</tbody>
</table>


Standard Edition 和 Enterprise Edition 伺服器具有相同的軟體需求。

執行 Lync Server 2013 Enterprise Edition 的伺服器適合供大型組織作為主要組織性的部署。Enterprise Edition Server 依設計最多可讓每個集區容納約 80,000 名使用者。執行 Lync Server 2013 Standard Edition 的伺服器則適合小型組織以及主要組織部署的遠端位置。一對 Standard Edition 伺服器最多可支援 5,000 名使用者。如需 Standard Edition Server 與 Enterprise Edition Server 之間差異的詳細資訊，請參閱＜ [Lync Server 2013 的部署概觀](lync-server-2013-deployment-overview.md)＞。

## 作業系統安裝

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync Server 2013 僅提供 64 位元版本，因此需要 64 位元硬體和 64 位元版本的 Windows Server 作業系統。這個版本未提供 32 位元版本的 Lync Server 2013。</td>
</tr>
</tbody>
</table>


Standard Edition 和 Enterprise Edition 伺服器可以使用下列任何一項：

  - Windows Server 2008 R2 SP1 或最新 Service Pack

  - Windows Server 2012

  - Windows Server 2012 R2

在 Standard Edition Server 或 Enterprise Edition 前端伺服器上安裝作業系統軟體。套用所有更新，讓作業系統具備最新更新和必要更新層級，以符合您組織的標準。如需有關作業系統的詳細資訊，請參閱支援文件中的 [Lync Server 2013 中的伺服器及工具作業系統支援](lync-server-2013-server-and-tools-operating-system-support.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果 Lync Server 2013 要在 Windows Server 2012 R2 上正常運作，您可能需要在 Windows Server 中變更登錄機碼的值。您可能必須進行此變更，憑證才能正常運作，用戶端也才能向 Survivable Branch Appliance 註冊。如需詳細資訊，請參閱 <a href="http://support.microsoft.com/kb/2901554" class="uri">http://support.microsoft.com/kb/2901554</a>。</td>
</tr>
</tbody>
</table>


## Lync Server 2013 其他軟體

除了作業系統所需的更新以外， Lync Server 2013 需要作業系統角色、功能和軟體才能運作。如需有關必須在發行拓撲和安裝 Lync Server 2013 前安裝的其他軟體的詳細資訊，請參閱規劃文件中的 [Lync Server 2013 的其他軟體需求](lync-server-2013-additional-software-requirements.md)。

## 所有伺服器角色所需的其他軟體

所有伺服器角色中，您也務必安裝 Windows PowerShell 命令列介面 3.0 與 Microsoft .NET Framework 4.5。

另外，任何您想要執行 Lync Server 系統管理工具的電腦，皆須具備 Windows PowerShell 命令列介面 3.0 與 Microsoft .NET Framework 4.5。

## Windows PowerShell 3.0

Lync Server 2013 要求您在每部電腦安裝 Windows PowerShell 3.0，且電腦將參與您的 Lync Server 拓撲。如需如何安裝 Windows PowerShell 3.0 的詳細資訊，請參閱＜ [針對 Lync Server 2013 安裝 Windows PowerShell 3.0](lync-server-2013-installing-windows-powershell-3-0.md)＞。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在具有 SP1 的 Windows Server 2008 R2 中，安裝 Microsoft .NET Framework 4.5 之前，無法安裝 Windows PowerShell 命令列介面 3.0。</td>
</tr>
</tbody>
</table>


## Microsoft .NET Framework 4.5

當您在將執行 Lync Server 2013 的 Windows Server 2012 或 Windows Server 2012 R2 伺服器上安裝 Microsoft .NET Framework 4.5 時，必須額外執行一個步驟。安裝 .NET Framework 4.5 後，請使用伺服器管理員安裝 HTTP 啟動。

**在 Windows Server 2012 或 Windows Server 2012 R2 上安裝 .NET 4.5 HTTP 啟動**

1.  從 **\[開始\]** 功能表，依序按一下 **\[程式集\]** 、 **\[系統管理工具\]** 和 **\[伺服器管理員\]**。

2.  在伺服器管理員的 **\[功能摘要\]** 下，請選擇 **\[新增功能\]**。

3.  展開 **\[.NET Framework 4.5\]**。

4.  如果尚未選取，請先選取 **\[WCF 啟動\]** ，然後選取 **\[HTTP 啟動\]**。

5.  按 **\[下一步\]** 並依照提示以完成安裝。

