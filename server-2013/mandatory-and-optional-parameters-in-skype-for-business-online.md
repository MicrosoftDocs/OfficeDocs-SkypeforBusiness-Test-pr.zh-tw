---
title: 強制參數與選擇性參數
TOCTitle: 強制參數與選擇性參數
ms:assetid: e766362f-e2e9-4598-a595-fdf5eedd9ad6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362851(v=OCS.15)
ms:contentKeyID: 56269162
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 強制參數與選擇性參數

 

_**上次修改主題的時間：** 2015-06-22_

Windows PowerShell 參數可分為兩大類：強制參數或選擇性參數。「強制參數」 是指在執行命令時必須加入的參數。例如 [Remove-CsUserAcp](remove-csuseracp.md) Cmdlet 用於將先前指派給使用者的音訊會議提供者取消指派。執行 **the Remove-CsUserAcp** Cmdlet 時，您必須加上 Identity 參數。該參數可告知 Cmdlet 哪些使用者的音訊會議提供者必須移除。正如您所預期，執行下列命令卻未加上任何參數將沒有任何意義：

    Remove-CsUserAcp

在此情況下，此 Cmdlet 將不清楚要移除哪個使用者的音訊會議提供者。您必須改為指定使用者的身分識別：

    Remove-CsUserAcp -Identity "Ken Myer"

一般來說，Windows PowerShell 會在您省略強制參數而嘗試執行命令時提示您。例如，您可能在輸入下列內容後就按下 ENTER：

    Remove-CsUserAcp

倘若如此，Windows PowerShell 並不會執行這個不完整的命令，而是會提示您輸入遺失的強制參數：

    cmdlet Remove-CsUserAcp 在命令管線位置 1
    請提供下列參數的值:
    識別:

若是在輸入有效的 Identity 參數後按下 ENTER，Windows PowerShell 將執行 **Remove-CsUserAcp** Cmdlet 並移除音訊會議提供者。若您改變心意而決定不要執行命令，請按 Ctrl-C 以終止命令。

這並非防呆系統，而 Windows PowerShell 也不一定都能提示您提供必要參數。例如，部分 Cmdlet 的設定為 參數 A 或參數 B (但非兩者同時存在) 為強制參數。Windows PowerShell 可能會提示您輸入參數 A 與參數 B；然而，您的命令將會失敗，因為您無法在命令中同時使用參數 A 與參數 B。由於諸如此類的情況，執行命令前最好先加上所有必要參數，而非依賴 Windows PowerShell 提示您所需資訊。

另請注意，參數值的格式化程序有時可能並非直覺性的操作。例如，加入包含空格的參數值時，您將需要為該值加上雙引號：

    -Identity "Ken Myer"

然而，只有在所要執行的命令中輸入參數與參數值時，才需要使用雙引號。若是嘗試執行 **Remove-CsUserAcp** Cmdlet，但不慎省略 Identity 參數，則 Windows PowerShell 將提示您輸入使用者的身分識別：

    cmdlet Remove-CsUserAcp 在命令管線位置 1
    請提供下列參數的值:
    識別:

接著您輸入 Ken Myer，並為 Identity 參數加上雙引號：

    cmdlet Remove-CsUserAcp 在命令管線位置 1
    請提供下列參數的值:
    識別:"Ken Myer"

若是執行此操作，命令將會失敗，並出現下列錯誤訊息：

    Remove-CsUserAcp : 找不到識別 ""Ken Myer"" 的管理物件。

在此情況下，搜尋的是 Identity 為 "Ken Myer" 的使用者，其中雙引號也包含為 Identity 參數的一部分。若是系統提示您輸入參數值，請勿包含雙引號：

    cmdlet Remove-CsUserAcp 在命令管線位置 1
    請提供下列參數的值:
    識別:Ken Myer

相較之下，「選擇性參數」恰如其名稱所述：Cmdlet 無需輸入參數即可執行。例如，Remove-CsUserAcp 具有選擇性參數 Name。若是 Name 參數包含在命令中，則僅會移除指定的音訊會議提供者。下列命令會移除名稱為 Fabrikam ACP 的音訊會議提供者但不會移除其他指派給 Ken Myer 的任何音訊會議提供者：

    Remove-CsUserAcp -Identity "Ken Myer" -Name "Fabrikam ACP"

若是省略選擇性參數，命令仍會執行。然而，在此情況下，Remove-CsUserAcp 將刪除所有指派給 Ken Myer 的音訊會議提供者：

    Remove-CsUserAcp -Identity "Ken Myer"

## 請參閱

#### 概念

[Windows PowerShell 與 Lync Online 的簡介](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

