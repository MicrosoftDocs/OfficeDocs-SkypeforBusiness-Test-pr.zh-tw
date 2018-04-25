---
title: Lync Online：下載並安裝 Windows PowerShell 3.0
TOCTitle: 下載並安裝 Windows PowerShell 3.0
ms:assetid: 39ae065d-02d7-4ce3-9e6f-6ad550a1777e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362783(v=OCS.15)
ms:contentKeyID: 56269082
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Online 中下載並安裝 Windows PowerShell 3.0

 

_**上次修改主題的時間：** 2015-06-22_

如果您使用的是 Windows Server 2012、 Windows Server 2012 R2、Windows 8 或 Windows 8.1，應已擁有 Windows PowerShell 3.0。這是因為該應用程式預先安裝於這些作業系統中。

如果您執行的是 Windows 7 或 Windows Server 2008 R2，則可能也有執行 Windows PowerShell 3.0。不過，也有可能是執行這些作業系統原本隨附的版本 (即版本 2.0)。若要判定使用的 Windows PowerShell 版本，請在您的 Windows 7 或 Windows Server 2008 R2 電腦上執行下列操作：

1.  依序按一下 \[開始\]、\[所有程式\]、\[附屬應用程式\]、\[Windows PowerShell\] 和 \[Windows PowerShell\]。

2.  在 Windows PowerShell 主控台中，輸入下列命令並按下 ENTER：
    
        Get-Host | Select-Object Version

3.  主控台視窗接著應會顯示類似以下的資訊：
    
        Version
        -------
        3.0

若是傳回的版本號碼為 3.0，則您所執行的是 Windows PowerShell 3.0。若是傳回的版本號碼並非 3.0，則您將需要安裝 Windows PowerShell 3.0。您可以下載 Windows Management Framework 3.o，其中包括 Windows PowerShell 3.0，其位於 [Microsoft 下載中心](http://www.microsoft.com/en-us/download/details.aspx?id=34595)。

您確認已安裝 Windows PowerShell 3.0 後，必須確保 Windows PowerShell 已設定好執行遠端指令碼。若要這麼做，請以系統管理員的身分啟動 Windows PowerShell。在 Windows 7、Windows Server 2008 R2、 Windows Server 2012 或 Windows Server 2012 R2 中，執行下列操作：

1.  依序按一下 \[開始\]、\[所有程式\]、\[附屬應用程式\] 及 \[Windows PowerShell\]，以滑鼠右鍵按一下 \[Windows PowerShell\]，然後按一下 \[以系統管理員身分執行\]。

2.  若是出現 \[使用者帳戶控制\] 對話方塊，請按 \[是\] 以確認要以系統管理員認證執行 Windows PowerShell。

如果您執行的是 Windows 8，請改為執行下列程序：

1.  存取快速鍵列，按一下 \[搜尋\]，然後以滑鼠右鍵按一下 \[Windows PowerShell\]。若要在任何 Windows 8 電腦上快速存取快速鍵列 (無論是否為觸控螢幕)，請在按住 Windows 鍵的同時按下 C。

2.  在畫面下方的工具列中，按一下 \[以系統管理員身分執行\]。

3.  若是出現 \[使用者帳戶控制\] 對話方塊，請按 \[是\] 以確認要以系統管理員認證執行 Windows PowerShell。

在 Windows PowerShell 開始執行後，您必須變更執行原則以允許執行遠端指令碼。在 Windows PowerShell 主控台中，輸入下列命令並按下 ENTER：

    Set-ExecutionPolicy RemoteSigned -Force

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>執行上述命令時，您可能會收到下列錯誤訊息：<br />
Set-ExecutionPolicy : Access to the registry key'HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PowerShell\1\ShellIds\Micrsoft.PowerShell' is denied. (Set-ExecutionPolicy：存取登錄機碼 'HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PowerShell\1\ShellIds\Micrsoft.PowerShell' 遭拒。)<br />
此錯誤訊息通常會在您並非以系統管理員認證執行 Windows PowerShell 時出現。請關閉 Windows PowerShell 工作階段，然後以系統管理員身分啟動新工作階段。</td>
</tr>
</tbody>
</table>


若要確認執行原則是否正確設定，請於 Windows PowerShell 命令提示字元中輸入下列內容，然後按下 ENTER：

    Get-ExecutionPolicy

若是收到下列值，則一切均已正確設定。

    RemoteSigned

如果您目前執行的並非 Windows PowerShell 3.0，還需要從 Microsoft 下載中心下載並安裝 Windows Management Framework 3.0。此安裝套件包含 Windows PowerShell 3.0 與 Windows Remote Management (WinRM) 3.0。如果您執行的是 Windows 7 且尚未更新為 Windows PowerShell 3.0，可能需要使用此安裝套件。如果您執行的是 Windows Server 2012、 Windows Server 2012 R2、Windows 8 或 Windows 8.1，則無需安裝 Windows PowerShell 3.0。 Windows PowerShell 3.0 已預先安裝於這些作業系統中。

安裝 Windows Management Framework 3.0 之前：

  - 確認下載的是正確版本的安裝套件。若是執行 64 位元版本的 Windows 7，請下載 Windows6.1-KB2506143-x64.msu 檔案。若是執行 32 位元版本的 Windows 7，請下載 Windows6.1-KB2506143-x86.msu 檔案。

  - 若是您的電腦執行的是 Windows 7，請確認您已安裝 Windows 7 Service Pack 1。

若不確定執行的 Windows 版本為何或是否已安裝 Windows 7 Service Pack 1，請按一下 \[開始\]，以滑鼠右鍵按一下 \[電腦\]，然後按一下 \[內容\]。\[系統\] 對話方塊將會回報下列資訊：

![顯示設定的 \[系統\] 對話方塊](images/Dn362783.30bff2e8-2862-4dd7-828f-43732f4b9314(OCS.15).png "顯示設定的 [系統] 對話方塊")

若要安裝 Windows Management Framework 3.0，請執行下列程序：

1.  連按兩下 .MSU 安裝檔 ( **Windows6.1-KB2506143-x64.msu** 或 **Windows6.1-KB2506143-x86.msu**)。

2.  在 \[下載並安裝更新\] 精靈中，按一下 \[閱讀授權合約條款 (第 1 頁，共 1 頁)\] 頁面中的 \[我接受\]。

3.  安裝完成後，按一下 \[立即重新啟動\] 以重新啟動您的電腦。

電腦重新開機後，確認 Windows PowerShell 可以啟動，而且可以使用系統管理員認證執行應用程式。若要執行此操作：

1.  依序按一下 \[開始\]、\[所有程式\]、\[附屬應用程式\] 及 \[Windows PowerShell\]，以滑鼠右鍵按一下 \[Windows PowerShell\]，然後按一下 \[以系統管理員身分執行\]。

2.  若是顯示 \[使用者帳戶控制\] 對話方塊，按一下 \[是\] 以確認要以系統管理員認證執行 Windows PowerShell。

出現 Windows PowerShell 主控台後，接著應確認 WinRM 服務正在執行且設定正確。若要確認服務正在執行，請在 Windows PowerShell 命令提示字元中輸入下列命令並按下 ENTER：

    Get-Service winrm

隨即會顯示 WinRM 服務的相關資訊：

    Status   Name               DisplayName
    ------   ----               -----------
    Running  winrm              Windows Remote Management (WS-Manag...

若是服務的 Status 並非 "Running"，請輸入下列命令並按下 ENTER 以啟動 WinRM 服務：

    Start-Service winrm

服務啟動後，執行下列命令以確認 WinRM 使用的是 Basic 驗證：

    winrm set winrm/config/client/auth '@{Basic="True"}'

畫面將會顯示類似以下的資訊：

    Auth
        Basic = true
        Digest = true
        Kerberos = true
        Negotiate = true
        Certificate = true
        CredSSP = false

若是基本驗證設為 True，即表示已可使用 Windows PowerShell 連線至 商務用 Skype Online。

