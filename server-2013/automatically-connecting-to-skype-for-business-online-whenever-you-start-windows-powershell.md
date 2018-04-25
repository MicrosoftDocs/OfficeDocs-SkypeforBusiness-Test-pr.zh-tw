---
title: 啟動 Windows PowerShell 時自動連線至 Lync Online
TOCTitle: 啟動 Windows PowerShell 時自動連線至 Lync Online
ms:assetid: 68f76c36-5dd6-48ea-b19a-d65593199e4c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362799(v=OCS.15)
ms:contentKeyID: 56269102
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 啟動 Windows PowerShell 時自動連線至 Lync Online

 

_**上次修改主題的時間：** 2015-06-22_

若是記不住連線至 商務用 Skype Online 所需的所有命令，您可以事先進行設定，如此只要連按兩下捷徑檔並輸入 商務用 Skype Online 密碼，即可連線至 商務用 Skype Online。

若要執行此操作，首先請開啟記事本 (或任何其他文字編輯器)，然後貼上下列命令，將您的 商務用 Skype Online 帳戶名稱取代為 kenmyer@litwareinc.com：

    $credential = Get-Credential "kenmyer@litwareinc.com"
    $session = New-CsOnlineSession -Credential $credential 
    Import-PSSession $session

以 .PS1 為副檔名儲存檔案 (例如 C:\\Scripts\\LyncOnline.ps1)。

儲存檔案後，執行下列程序以建立可啟動 Windows PowerShell 並在啟動時執行指令碼的桌面捷徑：

1.  以滑鼠右鍵按一下桌面，按一下 \[新增\]，然後按一下 \[捷徑\]。

2.  在 \[建立捷徑\] 精靈中，在 \[輸入項目的位置\] 方塊中輸入以下內容並按一下 \[下一步\] (記得使用剛建立的指令碼的路徑)：
    
        powershell.exe -noexit C:\Scripts\LyncOnline.ps1

3.  在 \[輸入這個捷徑的名稱\] 方塊中，輸入捷徑名稱 (例如 商務用 Skype Online)，然後按一下 \[完成\]。

4.  之後要使用 Windows PowerShell 管理 商務用 Skype Online 時，只要連按兩下新捷徑並輸入密碼，指令碼將進行連線並設定新遠端工作階段。

這項新工作階段通常不會儲存在變數 $session，而是會將其工作階段識別碼指定為 1。這不會對您的工作階段有任何影響，起碼到關閉工作階段之前均是如此。若要執行此操作，您將需要在呼叫 **Remove-PSSession** Cmdlet 時參照工作階段識別碼：

    Remove-PSSession 1

若要確認指定給您的 商務用 Skype Online 工作階段的識別碼為何，請從 Windows PowerShell 命令提示字元中執行下列命令：

    Get-PSSession

## 請參閱

#### 概念

[設定您的電腦以進行 Lync Online 管理](configuring-your-computer-for-skype-for-business-online-management.md)

