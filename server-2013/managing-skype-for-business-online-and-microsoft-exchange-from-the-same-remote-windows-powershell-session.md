---
title: 以相同的遠端 Windows PowerShell 工作階段管理 Lync Online 與 Microsoft Exchange
TOCTitle: 以相同的遠端 Windows PowerShell 工作階段管理 Lync Online 與 Microsoft Exchange
ms:assetid: 4eb4b5f0-f407-46bd-a2ac-a7ccbc387d51
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362787(v=OCS.15)
ms:contentKeyID: 56269087
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 以相同的遠端 Windows PowerShell 工作階段管理 Lync Online 與 Microsoft Exchange

 

_**上次修改主題的時間：** 2015-06-22_

若是訂閱 Office 365，不僅可存取 商務用 Skype Online，另外亦可存取 Exchange Online。您可以使用 Windows PowerShell 遠端工作階段管理 商務用 Skype Online，也可以使用 Windows PowerShell 遠端工作階段管理 Exchange。然而，商務用 Skype Online 與 Exchange Online 並未共用相同的 URI，連線方式也不同。這表示您需要使用個別的工作階段管理 商務用 Skype Online 與 Exchange。或者是有方法可使用單一 Windows PowerShell 遠端工作階段同時管理兩項產品？

結果您會發現不僅可以使用相同的 Windows PowerShell 執行個體同時管理兩項產品，而且設定雙重管理工作階段的方法相當簡單。首先，按照一般方式啟動 Windows PowerShell 並連線至 商務用 Skype Online：先建立認證物件，然後建立連線至 商務用 Skype Online 的新工作階段：

    $credential = Get-Credential "kenmyer@litwareinc.com"
    $lyncSession = New-CsOnlineSession -Credential $credential

接著，使用類似程序連線至 Exchange Online。請注意，您無需建立新的認證物件。您可以持續使用在登入 商務用 Skype Online 時所使用的相同物件 ($credential)：

    $exchangeSession = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri "https://outlook.office365.com/powershell-liveid/" -Credential $credential -Authentication "Basic" -AllowRedirection

無論您的 Office 365 URI 為何，應一律使用 URI https://outlook.office365.com/powershell-liveid/ 連線至 Exchange Online。在您通過驗證後，系統會將您自動重新導向至適當的 URI，因此加上 AllowRedirection 參數特別重要。若是省略此參數，您仍可通過驗證，但重新導向將會失敗，而您將無法連線至 Exchange Online：

    New-PSSession : [ps.outlook.com] The WinRM service cannot process the request because the request needs to be sent to a different machine. Use the redirect information to send the request to a new machine.  Redirect location reported: https://pod51043psh.outlook.com/powershell-liveid?PSVersion=3.0 . To automatically connect to the redirected URI, verify  MaximumConnectionRedirectionCount" property of session preference variable "PSSessionOption" and use "AllowRedirection" parameter on the cmdlet.

此時，您的電腦上應執行兩個不同的遠端工作階段。若要確認此操作，請在 Windows PowerShell 命令提示字元中輸入下列命令：

    Get-PSSession

畫面應會顯示類似下列的資訊：

    Id Name      ComputerName  State   ConfigurationName     Availability
    -- ----      ------------  -----   -----------------     ------------
     1 Session1  pod510w43...  Opened  Microsoft.PowerShell     Available
     2 Session2  up02921vd...  Opened  Microsoft.Exchange       Available

您現在已有一對遠端工作階段可匯入至您的 Windows PowerShell 本機工作階段。為執行此操作，請執行下列兩項命令：

    Import-PSSession $lyncSession
    Import-PSSession $exchangeSession

此時您將可使用 商務用 Skype Online 與 Exchange Online Cmdlet。若要確認，請執行下列命令，然後確認是否收到使用者資訊：

    Get-CsOnlineUser -ResultSize 1

接著執行下列 Exchange 命令，並確認是否收到信箱資訊：

    Get-Mailbox -ResultSize 1

若要結束管理工作階段，請務必關閉兩項遠端工作階段：

    Remove-PSSession $lyncSession
    Remove-PSSession $exchangeSession

## 請參閱

#### 概念

[設定您的電腦以進行 Lync Online 管理](configuring-your-computer-for-skype-for-business-online-management.md)

