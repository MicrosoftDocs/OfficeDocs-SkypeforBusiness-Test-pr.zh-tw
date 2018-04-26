---
title: Lync Server 2013：系統管理工具軟體需求
TOCTitle: 系統管理工具軟體需求
ms:assetid: 2fb172c3-7b84-4e49-981c-2a17e7a00a29
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg195653(v=OCS.15)
ms:contentKeyID: 49290480
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的系統管理工具軟體需求

 

_**上次修改主題的時間：** 2013-11-07_

本主題說明安裝以及使用 Lync Server 2013 系統管理工具時，除了作業系統之外所需的軟體。

## Microsoft .NET Framework 4.5

Lync Server 2013 需要 Microsoft .NET Framework 4.5 的 64 位元版本。

## Windows PowerShell 3.0

執行所有 Microsoft Lync Server 2013 的元件皆需要 Windows PowerShell 3.0。如需詳細資訊，請參閱＜ [針對 Lync Server 2013 安裝 Windows PowerShell 3.0](lync-server-2013-installing-windows-powershell-3-0.md)＞。

## Windows Installer 4.5 版

Lync Server 2013 採用 Windows Installer 技術來安裝、解除安裝和維護各種伺服器角色。Windows Installer 4.5 版是以 Windows Server 作業系統適用的可轉散發元件形式提供。Windows Installer 4.5 隨附 Windows Server 2012 R2、Windows Server 2012 和 Windows Server 2008 R2，這代表您不需要為任何執行 Lync Server 2013 的電腦下載公用程式。( Lync Server 2013 僅能安裝在執行 Windows Server 2012 R2、Windows Server 2012 或 Windows Server 2008 R2 的電腦上。)

不過，如果您想要在管理員工作站安裝 Lync Server 管理命令介面 或 Lync Server 拓撲產生器，可能需要下載 Windows Installer 4.5。該公用程式隨附於 Windows 7 和 Windows 2008 R2，但未隨附於任何舊版 Windows 作業系統。您可以從 Microsoft 下載中心 <http://go.microsoft.com/fwlink/p/?linkid=197395> 下載 Windows Installer 4.5。

## Microsoft Silverlight 5 瀏覽器外掛程式

Lync Server 2013 控制台是一種 Web 工具，會要求您安裝最新版的 Microsoft Silverlight 5 瀏覽器外掛程式。當您啟動 Lync Server 2013 控制台 時，如果未安裝此軟體，或者安裝的是舊版， Lync Server 2013 控制台會提示您安裝所需的版本。

## 請參閱

#### 概念

[Lync Server 2013 中的伺服器及工具作業系統支援](lync-server-2013-server-and-tools-operating-system-support.md)  

#### 其他資源

[Lync Server 2013 中的系統管理工具基礎結構需求](lync-server-2013-administrative-tools-infrastructure-requirements.md)  
[設定和管理 Lync Server 2013 所需的系統管理員權限](lync-server-2013-administrator-rights-and-permissions-required-for-setup-and-administration.md)

