---
title: Lync Server 2013：其他軟體需求
TOCTitle: 其他軟體需求
ms:assetid: 87b318e3-03ae-41f7-af5e-29bb294f6af0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398686(v=OCS.15)
ms:contentKeyID: 49291565
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的其他軟體需求

 

_**上次修改主題的時間：** 2014-06-20_

除了伺服器平台的硬體和作業系統需求， Lync Server 2013 還需要您部署的伺服器上已安裝其他軟體。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需執行 Lync Server 的伺服器平台需求的詳細資訊，請參閱＜ <a href="lync-server-2013-server-hardware-platforms.md">Lync Server 2013 的伺服器硬體平台</a>＞及＜ <a href="lync-server-2013-server-and-tools-operating-system-support.md">Lync Server 2013 中的伺服器及工具作業系統支援</a>＞。如需用戶端電腦和裝置的系統需求詳細資訊，請參閱規劃文件中的＜ <a href="lync-server-2013-planning-for-clients-and-devices.md">規劃 Lync Server 2013 中的用戶端和裝置</a>＞。如需系統管理工具的軟體需求詳細資訊，請參閱＜ <a href="lync-server-2013-administrative-tools-software-requirements.md">Lync Server 2013 中的系統管理工具軟體需求</a>＞。</td>
</tr>
</tbody>
</table>


## 所有內部伺服器角色都需要的其他軟體

本節列出所有內部伺服器角色 (Edge Server 除外的所有 Lync Server 伺服器角色) 的必要軟體。Edge Server 和 Edge 集區 的需求列示於本主題中 **Edge Server 的其他軟體** 一節。

## Windows PowerShell 3.0

每一部執行 Lync Server 2013 的伺服器必須安裝正確的 Windows PowerShell 3.0 版本。如需詳細資訊，請參閱＜ [針對 Lync Server 2013 安裝 Windows PowerShell 3.0](lync-server-2013-installing-windows-powershell-3-0.md)＞。

## Microsoft .NET Framework 4.5

Lync Server 在所有內部伺服器角色，及將執行 Lync Server 系統管理工具或 Microsoft Lync Server 2013 規劃工具 的任何電腦上，都需要 Microsoft .NET Framework 4.5。若為 Lync Server 2013，您必須在安裝 Lync Server 2013 之前於伺服器上手動安裝 64 位元版本的 Microsoft .NET Framework 4.5。若要手動安裝，請從 Microsoft 下載中心下載 Microsoft .NET 4.5 Framework，網址為 [http://go.microsoft.com/fwlink/p/?LinkId=268529](http://go.microsoft.com/fwlink/p/?linkid=268529)

## 在執行 Windows Server 2012 的伺服器上安裝 Microsoft .NET Framework 4.5

當您在執行 Lync Server 2013 與 Windows Server 2012 伺服器上安裝 Microsoft .NET Framework 4.5 時，必須額外執行一個步驟。安裝 .NET Framework 4.5 後，請使用伺服器管理員安裝 HTTP 啟動。

**在 Windows Server 2012 上安裝 .NET 4.5 HTTP 啟動**

1.  從 **\[開始\]** 功能表，依序按一下 **\[程式集\]** 、 **\[系統管理工具\]** 和 **\[伺服器管理員\]** 。

2.  在伺服器管理員的 **\[功能摘要\]** 下，請選擇 **\[新增功能\]** 。

3.  展開 **\[.NET Framework 4.5\]** 。

4.  如果尚未選取，請先選取 **\[WCF 啟動\]** ，然後選取 **\[HTTP 啟動\]** 。

5.  按 **\[下一步\]** 並依照提示以完成安裝。

## Windows Identity Foundation

Lync Server 2013 中的 **Windows Identity Foundation** 需要安裝 Windows Identity Foundation 以支援伺服器對伺服器驗證案例。 Windows Server 2008 R2 和 Windows Server 2012 需要不同的程序來安裝 Windows Identify Foundation。從下列清單選取您的伺服器作業系統：

  - Windows Server 2008 R2   若為 Windows Server 2008 R2，請檢查是否已安裝於電腦上。若要執行此動作，請前往 \[新增/移除程式\] 、\[檢視已安裝的更新\] ，查看 \[Windows\] 之下的項目 \[Windows Identity Foundation (KB974405)\] 。如需安裝 Windows Identity Foundation 的詳細資訊，請參閱 <http://go.microsoft.com/fwlink/?linkid=204657>。

  - Windows Server 2012   若為 Windows Server 2012，請使用 \[伺服器管理員\] 安裝 Windows Identity Foundation。在 \[伺服器管理員\] 的 \[新增角色及功能精靈\] 中，選取 \[功能\] 。從清單中選取 \[Windows Identity Foundation 3.5\] 。按 \[下一步\] ，然後按一下 \[安裝\] 。

## 所有前端伺服器和 Standard Edition Server 需要的其他軟體

所有前端伺服器和 Standard Edition Server 也必須執行含特定模組的 Internet Information Services (IIS)。此外，所有將部署會議、 通話駐留應用程式、宣告或回應群組的前端伺服器和 Standard Edition Server 都必須執行 Windows Media Format Runtime。

## Internet Information Services (IIS)

前端伺服器和 Standard Edition Server 必須執行含有下列模組的 Internet Information Services (IIS)：

  - 靜態內容

  - 預設文件

  - HTTP 錯誤

  - ASP.NET

  - .NET 擴充性

  - 網際網路伺服器 API (ISAPI) 延伸模組

  - ISAPI 篩選器

  - HTTP 記錄

  - 記錄工具

  - 追蹤

  - Windows 驗證

  - 要求篩選

  - 靜態內容壓縮

  - 動態內容壓縮

  - IIS 管理主控台

  - IIS 管理指令碼及工具

  - 匿名驗證 (安裝 IIS 時預設會安裝此模組)

  - 用戶端憑證對應驗證

## Windows Media Format Runtime 和 Windows Desktop Experience

**Windows Desktop Experience** 所有將部署會議的前端伺服器和 Standard Edition Server 都必須安裝 Windows Media Format Runtime， Windows Server 2012 則是在 Windows Desktop Experience 中安裝。 Windows Server 2012 需要 Microsoft Media Foundation。需要有 Windows Media Format Runtime， 通話駐留、宣告和回應群組應用程式才能執行 Windows Media Audio (.wma) 檔案來播放宣告和音樂。 UNRESOLVED\_TOKEN\_VAL()

在安裝 Lync Server 2013 之前，建議您先安裝 Windows 桌面體驗。如果 Lync Server 2013 在伺服器上找不到這個軟體，就會提示您進行安裝，然後您就必須重新啟動伺服器來完成安裝。

## 執行 Windows Server 2012 的 Edge Server 和 Standard Edition Server 需要的其他軟體

前端伺服器 需要 .NET 3.5，但是 Windows Server 2012 預設未安裝。若要安裝，請將 Windows Server 2012 安裝媒體放入磁碟機 D，並如下輸入：

    Add-WindowsFeature RSAT-ADDS, Web-Server, Web-Static-Content, Web-Default-Doc, Web-Http-Errors, Web-Asp-Net, Web-Net-Ext, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Http-Logging, Web-Log-Libraries, Web-Request-Monitor, Web-Http-Tracing, Web-Basic-Auth, Web-Windows-Auth, Web-Client-Auth, Web-Filtering, Web-Stat-Compression, Web-Dyn-Compression, NET-WCF-HTTP-Activation45, Web-Asp-Net45, Web-Mgmt-Tools, Web-Scripting-Tools, Web-Mgmt-Compat, Desktop-Experience, Telnet-Client, BITS -Source D:\sources\sxs

如需在執行 Windows Server 2012 的伺服器上安裝 .NET 3.5 的詳細資訊，請參閱＜Microsoft .NET Framework 3.5 Deployment Considerations＞，網址為 <http://go.microsoft.com/fwlink/?linkid=275032>。

## Director 需要的其他軟體

Director 必須執行含有下列模組的 Internet Information Services (IIS)：

  - 靜態內容

  - 預設文件

  - HTTP 錯誤

  - ASP.NET

  - .NET 擴充性

  - 網際網路伺服器 API (ISAPI) 延伸模組

  - ISAPI 篩選器

  - HTTP 記錄

  - 記錄工具

  - 追蹤

  - Windows 驗證

  - 要求篩選

  - 靜態內容壓縮

  - IIS 管理主控台

  - IIS 管理指令碼及工具

  - 匿名驗證 (安裝 IIS 時預設會安裝此模組)

  - 用戶端憑證對應驗證

## 常設聊天室前端伺服器的其他軟體

常設聊天室前端伺服器必須執行訊息佇列 (也稱為 MSMQ)，這是 Windows Server 的元件。

如需啟用 MSMQ 的詳細資訊，[請按一下這裡。](http://technet.microsoft.com/en-us/library/cc771474.aspx)

## Edge Server 的其他軟體

Edge Server 需要以下軟體：

  - 每一部執行 Lync Server 2013 的伺服器必須安裝正確的 Windows PowerShell 3.0 版本。如需詳細資訊，請參閱＜ [針對 Lync Server 2013 安裝 Windows PowerShell 3.0](lync-server-2013-installing-windows-powershell-3-0.md)＞。

  - Lync Server 需要 Microsoft .NET Framework 4.5。若為安裝在 Windows Server 2008 R2 上的 Lync Server 2013，您必須在安裝 Lync Server 2013 之前於伺服器上手動安裝 64 位元版本的 Microsoft .NET Framework 4.5。若要手動安裝，請從 Microsoft 下載中心下載 Microsoft .NET 4.5 Framework，網址為 <http://go.microsoft.com/fwlink/?linkid=268529>

  - Lync Server 2013 中的 **Windows Identity Foundation** 需要安裝 Windows Identity Foundation 以支援伺服器對伺服器驗證案例。 Windows Server 2008 R2 和 Windows Server 2012 需要不同的程序來安裝 Windows Identify Foundation。從下列清單選取您的伺服器作業系統：
    
      - Windows Server 2008 R2   若為 Windows Server 2008 R2，請檢查是否已安裝於電腦上。若要執行此動作，請前往 \[新增/移除程式\] 、\[檢視已安裝的更新\] ，查看 \[Windows\] 之下的項目 \[Windows Identity Foundation (KB974405)\] 。如需安裝 Windows Identity Foundation 的詳細資訊，請參閱 <http://go.microsoft.com/fwlink/?linkid=204657>。
    
      - Windows Server 2012   若為 Windows Server 2012，請使用 \[伺服器管理員\] 安裝 Windows Identity Foundation。在 \[伺服器管理員\] 的 \[新增角色及功能精靈\] 中，選取 \[功能\] 。從清單中選取 \[Windows Identity Foundation 3.5\] 。按 \[下一步\] ，然後按一下 \[安裝\] 。

## 不要在媒體伺服器上安裝 Layered Socket Provider

在任何前端伺服器或獨立式媒體伺服器上，請不要安裝任何 Microsoft Internet Security and Acceleration (ISA) Server 用戶端軟體，或其他任何 Winsock Layered Service Provider (LSP) 軟體。安裝此軟體會造成媒體流量效能降低。

## 請參閱

#### 概念

[Lync Server 2013 中的系統管理工具軟體需求](lync-server-2013-administrative-tools-software-requirements.md)

