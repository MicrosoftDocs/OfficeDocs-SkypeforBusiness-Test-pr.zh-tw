---
title: 準備和安裝最佳做法分析程式
TOCTitle: 準備和安裝最佳做法分析程式
ms:assetid: 550613dd-dc08-482e-9980-a3fe187cd162
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg591347(v=OCS.15)
ms:contentKeyID: 49290944
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 準備和安裝最佳做法分析程式

 

_**上次修改主題的時間：** 2013-11-07_

您必須以 Administrators 群組成員登入，來執行本主題所說明的工作。

## 安裝最佳做法分析程式的系統需求

若要執行 Lync Server 2013 的最佳做法分析程式來掃描您的環境，該電腦必須執行下列其中一個作業系統的 64 位元版本：

  - Windows Server 2008 R2 (含 Service Pack 1 (SP1)) Standard 作業系統

  - Windows Server 2008 R2 (含 SP1) Enterprise 作業系統

  - Windows Server 2008 R2 (含 SP1) Datacenter 作業系統

  - Windows Server 2012 Datacenter 作業系統

  - Windows Server 2012 Standard 作業系統

  - Windows Server 2012 Enterprise 作業系統

  - Windows Server 2012 R2 Datacenter 作業系統

  - Windows Server 2012 R2 Standard 作業系統

  - Windows Server 2012 R2 Enterprise 作業系統

  - Windows 8 作業系統

  - Windows 7 作業系統

該電腦也必須執行下列程式：

  - Microsoft .NET Framework 4.5。針對 Lync Server 2013，您必須先在伺服器上手動安裝 64 位元版本的 Microsoft .NET Framework 4.5，才能安裝 Lync Server 2013。

  - Lync Server 2013、核心元件。

  - WMI 回溯相容性套件。如需詳細資訊，請參閱移轉文件中的[安裝 WMI 回溯相容性套件](install-wmi-backward-compatibility-package.md)。

  - Windows PowerShell 3.0。如需詳細資訊，請參閱部署文件中的[針對 Lync Server 2013 安裝 Windows PowerShell 3.0](lync-server-2013-installing-windows-powershell-3-0.md)。

您可以在含有支援作業系統的電腦上安裝最佳做法分析程式，這些電腦上並未執行 Lync Server 2013、核心元件或 WMI 回溯相容性套件，但是您可以在這些電腦上使用最佳做法分析程式，只檢視報告而不執行掃描。

## 選擇電腦進行安裝

建議您在專門用來進行 Lync Server 2013 管理的電腦上安裝 Lync Server 2013 的最佳做法分析程式。您可以在執行 Lync Server 2013 的伺服器上或在執行 Lync Server 2013 系統管理工具的系統管理電腦上安裝此工具。如果您在執行 Lync Server 的伺服器上安裝此工具，則建議您將其當成僅用來掃描該伺服器的工具。

## 安裝最佳做法分析程式

您可以下載 Lync Server 2013 的最佳做法分析程式，網址為 [http://go.microsoft.com/fwlink/?linkid=266539\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=266539%26clcid=0x404)。

若要安裝最佳做法分析程式，請在您要安裝此工具的電腦上啟動 Microsoft 安裝程式檔案 RtcBPA.msi，然後依照螢幕上的指示執行。安裝程式檔的預設位置為 *\<系統磁碟機\>*\\Program Files\\Lync Server 2013\\BPA。

