---
title: 結合 Lync Online Cmdlet 與其他 Windows PowerShell Cmdlet
TOCTitle: 結合 Lync Online Cmdlet 與其他 Windows PowerShell Cmdlet
ms:assetid: 8bb8800a-f966-4570-8c8b-db87a91ad783
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362816(v=OCS.15)
ms:contentKeyID: 56269119
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 結合 Lync Online Cmdlet 與其他 Windows PowerShell Cmdlet

 

_**上次修改主題的時間：** 2015-06-22_

使用 Windows PowerShell 連線至 商務用 Skype Online 後，約有 40 個 商務用 Skype Online Cmdlet 可供使用。然而，在管理 商務用 Skype Online 時並非只能使用這 40 個 Cmdlet。除了 商務用 Skype Online Cmdlet，您還可以使用電腦上所安裝的任何其他 Windows PowerShell Cmdlet。(安裝 Windows PowerShell 3.0 後，同時也會安裝數百個核心 Windows PowerShell Cmdlet。) 您的命令可混合搭配 商務用 Skype Online Cmdlet 以及電腦上可用的任何其他 Cmdlet。

雖然 Windows PowerShell 3.0 的完整課程已超出本文涵蓋範圍，以下仍有幾個範例可為您說明混合搭配 Cmdlet 的原因。首先，任何 商務用 Skype Online Cmdlet 均無包含「列印」命令，而 Windows PowerShell 主控台也沒有提供該命令。那麼要如何列印 Cmdlet 所擷取的資訊呢？其中一種方式是在擷取資訊後，將該資訊傳送至 **Out-Printer** Cmdlet：

    Get-CsTenant | Out-Printer

因為未加入任何額外參數，所以 **the Out-Printer** Cmdlet 所傳回的所有資訊將列印至預設印表機。

同樣地，任何 商務用 Skype Online Cmdlet 均無包含可讓您將資料儲存至檔案的參數。但沒關係：以下命令會使用 **Out-File** Cmdlet 將傳回資訊儲存至文字檔 C:\\Logs\\Tenants.txt：

    Get-Tenant | Out-File -FilePath "C:\Logs\Tenants.txt"

而下列命令會使用 **Select-Object** Cmdlet 限制傳回並顯示於畫面上的資料。在此範例中，[Get-CsOnlineUser](get-csonlineuser.md) Cmdlet 會擷取所有 商務用 Skype Online 使用者的相關資訊，然後 **Select-Object** Cmdlet 則用於將顯示資料限制為使用者的身分識別值以及其封存原則：

    Get-CsOnlineUser | Select-Object Identity, ArchivingPolicy

因為您的電腦上有數百個 Cmdlet 可供使用，您可能會無法判斷何者為 商務用 Skype Online Cmdlet。若要傳回 商務用 Skype Online Cmdlet 清單 (且僅限 商務用 Skype Online Cmdlet)，您必須先判定包含所有 商務用 Skype Online Cmdlet 的暫時 Windows PowerShell 模組名稱。若要執行此操作，請從 Windows PowerShell 命令提示字元中執行下列命令：

    Get-Module

畫面將會出現類似以下資訊：

    ModuleType Name                 ExportedCommands
    ---------- ----                 ----------------
    Manifest   Microsoft.PowerS...  {Add-Computer, Add-Content, A...}
    Script     tmp_5astd3uh.m5v     {Disable-CsMeetingRoom, Enabl...}

ModuleType 為 Script 的模組即為包含 商務用 Skype Online Cmdlet 的模組。若要傳回該類 Cmdlet 的清單，請以 Script 為模組名稱執行 **Get-Command** Cmdlet：

    Get-Command -Module tmp_5astd3uh.m5v

您可能有數個模組是以 Script 作為 ModuleType。在此情況下，您可以執行下列命令以尋找包含 **Get-CsTenant** Cmdlet 的模組：

    Get-Command Get-CsTenant

**Get-CsTenant** Cmdlet 所傳回的模組即為包含所有 商務用 Skype Online Cmdlet 的模組：

    CommandType     Name                                               ModuleName
    -----------     ----                                               ----------
    Function        Get-CsTenant                                       tmp_5astd3uh.m5v

## 請參閱

#### 概念

[Windows PowerShell 與 Lync Online 的簡介](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

