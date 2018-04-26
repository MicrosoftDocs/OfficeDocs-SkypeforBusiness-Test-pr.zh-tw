---
title: 下載並安裝 Lync Online Connector 模組
TOCTitle: 下載並安裝 Lync Online Connector 模組
ms:assetid: a0c87219-b642-4201-85d4-a85c2163d1eb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362829(v=OCS.15)
ms:contentKeyID: 56269134
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 下載並安裝 Lync Online Connector 模組

 

_**上次修改主題的時間：** 2015-06-22_

商務用 Skype Online Connector 模組包含 **New-CsOnlineSession** Cmdlet，可讓您建立連線至 商務用 Skype Online 的 Windows PowerShell 遠端工作階段。此模組僅受 64 位元電腦支援 (請參閱＜[設定您的電腦以進行 Lync Online 管理](configuring-your-computer-for-skype-for-business-online-management.md)＞以取得更多資訊)，並可透過 Microsoft 下載中心進行下載：[http://go.microsoft.com/fwlink/?LinkId=294688](http://go.microsoft.com/fwlink/?linkid=294688)。請下載 LyncOnlinePowershell.exe 檔，然後完成下列程序：

1.  連按兩下 **LyncOnlinePowershell.exe** 檔案。

2.  在 商務用 Skype Online 租用戶 PowerShell 安裝精靈中，選取 \[Microsoft Software License Terms 頁面中的 \[I accept the terms in the License Agreement\]，然後按下 \[Install\]。若是出現 \[User Account Control\] 對話方塊，請按一下 \[Yes\] 以繼續安裝。

3.  在 \[Completed the Microsoft Lync Online, Tenant PowerShell Setup\] 頁面中，按一下 \[Finish\]。

安裝程式會將 商務用 Skype Online Connector 模組 (與 **New-CsOnlineSession** Cmdlet) 複製至您的本機電腦。若要存取模組，請以系統管理員認證啟動 Windows PowerShell 工作階段，然後執行下列命令：

    Import-Module LyncOnlineConnector

若是不想在每次啟動 Windows PowerShell 時均需輸入此命令，您可以將命令新增至您的 Windows PowerShell 設定檔。若要執行此操作，請在 Windows PowerShell 命令提示字元中輸入下列命令並按下 ENTER：

    notepad.exe $profile

在 \[記事本\] 出現時，將下行新增至設定檔中已存在的命令 (如有的話) 下方：

    Import-Module LyncOnlineConnector

儲存檔案。下次啟動 Windows PowerShell 時，商務用 Skype Online Connector 模組將自動匯入。請注意，若是您並非以系統管理員認證執行 Windows PowerShell，您將收到錯誤訊息，且模組將無法載入。

除了安裝 商務用 Skype Online Connector 模組外，LyncOnlinePowershell.exe 還會安裝兩個額外元件：.NET Framework 4.5 與 Microsoft Visual C++ 2012 可轉散發套件 (x64) (版本 11.0.50727)。.NET Framework 4.5 可提供用於建置與執行 .NET 應用程式的基礎結構，包括 Windows PowerShell。Visual C++ 可轉散發套件則會針對並未安裝 Microsoft Visual Studio 2012 的電腦安裝 Visual C++ 執行階段元件。

## 請參閱

#### 概念

[設定您的電腦以進行 Lync Online 管理](configuring-your-computer-for-skype-for-business-online-management.md)

