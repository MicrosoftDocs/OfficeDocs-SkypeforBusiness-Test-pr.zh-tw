---
title: Windows PowerShell Cmdlet、參數，以及參數值
TOCTitle: Windows PowerShell Cmdlet、參數，以及參數值
ms:assetid: 04615700-099f-4ac5-a801-ddeffccb9e4f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362765(v=OCS.15)
ms:contentKeyID: 56269065
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Windows PowerShell Cmdlet、參數，以及參數值

 

_**上次修改主題的時間：** 2015-06-22_

若是您已熟悉各個 Windows 版本的命令視窗 (或熟悉 MS-DOS)，則您在學習如何使用 Windows PowerShell 方面已有個不錯的開始。您在命令視窗中輸入命令並按下 ENTER，電腦會執行命令或可執行檔以作為回應。例如，若要傳回目前目錄中的所有檔案與資料夾的相關資訊，您需要在命令提示字元中輸入以下命令並按下 ENTER：

    dir

結果，您會收到目前目錄中的所有檔案與資料夾的相關資訊：

``` 
    Directory: C:\

03/21/2013  03:39 PM    <DIR>          Deploy
03/21/2013  02:55 PM    <DIR>          Intel
07/26/2012  12:33 AM    <DIR>          PerfLogs
04/10/2013  10:29 AM    <DIR>          Program Files
04/08/2013  10:28 AM    <DIR>          Program Files (x86)
03/22/2013  08:44 AM    <DIR>          Users
04/11/2013  03:00 PM    <DIR>              Windows
03/13/2013  02:53 PM                 117   pldok.log
03/21/2013  03:35 PM                 769   RHDSetup.exe
03/21/2013  03:37 PM            207   setup.doc
              3 File(s)        1,093 bytes
              7 Dir(s)21,386,002,432 bytes free
```

這是您僅輸入命令或可執行檔名稱後所會收到的結果範例。然而，許多從命令視窗內部執行的命令亦接受「引數」。引數是指傳遞至命令的額外資訊，可修改命令的行為。例如說，若是僅要查看目前目錄中的檔案與資料夾名稱而不要其他資訊 (例如檔案或資料夾的大小或建立的日期與時間)，在此情況下，您需要在執行 dir 命令時附加 **/b** 引數：

    dir /b

包含 **/b** 引數後，**dir** 命令僅會回報在目前目錄中所找到的資料夾與檔案名稱：

    Deploy
    Intel
    PerfLogs
    Program Files
    Program Files (x86)
    Users
    Windows
    pldok.log
    RHDSetup.exe
    setup.doc

在上述命令中，**/b** 引數是限制傳回資料為檔案與資料夾名稱的唯一所需資訊。這是命令列命令的常見情形：只要加上引數，即可變更命令的行為 (也就是包含 **/b** 引數可隱藏額外資訊，而排除 **/b** 引數則可顯示額外資訊)。然而，有時必須指定「引數值」。引數值是指傳遞至引數本身的額外資訊。例如說，**/o** 引數可讓您指定 dir 命令要如何排序傳回的資料。其中，您可使用引數值 **e** 以依照副檔名排序，或使用引數值 **s** 以依照檔案大小排序。例如，下列命令會依照副檔名將傳回的資料排序。請注意，引數值 **e** 是緊接在 **/o** 引數後方：

    dir /oe

使用範例資料夾所傳回的資料將會按照副檔名的字母順序排序：

``` 
    Directory: C:\

03/21/2013  03:39 PM    <DIR>          Deploy
03/21/2013  02:55 PM    <DIR>          Intel
07/26/2012  12:33 AM    <DIR>          PerfLogs
04/10/2013  10:29 AM    <DIR>          Program Files
04/08/2013  10:28 AM    <DIR>          Program Files (x86)
03/22/2013  08:44 AM    <DIR>          Users
04/11/2013  03:00 PM    <DIR>              Windows
03/21/2013  03:37 PM            207   setup.doc
03/21/2013  03:35 PM                 769   RHDSetup.exe
03/13/2013  02:53 PM                 117   pldok.log
              3 File(s)        1,093 bytes
              7 Dir(s)21,386,002,432 bytes free
```

或者協助您確實瞭解以上陳述：

setup. **doc**  
RHDSetup. **exe**  
pldok. **log**

雖然 Windows PowerShell 採取不同的術語，但 Windows PowerShell 的基本操作與命令視窗並無差異：輸入命令、視需要包含引數與引數值，然後按下 ENTER 以執行命令。然而，如先前所述，Windows PowerShell 採取的術語與命令介面不同。在 Windows PowerShell 中，您所執行的命令稱為 *Cmdlet*。相對地，傳遞至 Cmdlet 的引數稱為「參數」，而傳遞至參數的值稱為「參數值」。

上述定義是經過簡化的說明。就本質而言，Cmdlet 是僅能從 Windows PowerShell 環境中執行的迷你應用程式。然而，您亦可從 Windows PowerShell 中執行其他命令與應用程式，包括大部分可從命令視窗中執行的命令與應用程式。舉例來說，若要從 Windows PowerShell 中開啟記事本，僅需輸入下列命令並按下 ENTER：

    notepad.exe

不過，就管理 商務用 Skype Online 來說，大部分的系統管理員均仰賴 Windows PowerShell Cmdlet 執行系統管理工作。偶而會有 (但數量非常少) 能夠用於管理 商務用 Skype Online 的命令或應用程式。有時可直接使用 商務用 Skype Online Cmdlet 而無需任何額外引數 (如前所述，引數在 Windows PowerShell 中稱為參數)。例如，下列命令會呼叫 [Get-CsOnlineUser](get-csonlineuser.md) Cmdlet 而無需任何額外參數。該命令本身即會傳回所有 商務用 Skype Online 使用者的相關資訊：

    Get-CsOnlineUser

但是，大部分 商務用 Skype Online Cmdlet 亦接受參數 (以及參數值)。請參考下列命令：

    Get-CsOnlineUser -Identity "kenmyer@litwareinc.com"

此命令由三個部分組成：

  - **Get-CsOnlineUser** Cmdlet。

  - Identity 參數。請注意，在 Windows PowerShell 中，參數一律接在虛線 (-) 後方，也就是說，就同樣這個 Cmdlet 而言，UnassignedUser 參數將使用下列語法表示：
    
        -UnassignedUser
    
    瞭解這點相當重要，不僅是因為參數必須接於虛線之後，也是因為這跟命令視窗中引數接在斜線 (/) 後方的情形有所差異：
    
    ``` 
    /b
    ```

  - 參數值 **kenmyer@litwareinc.com**。

結果，該命令會傳回特定使用者 (識別身分為 kenmyer@litwareinc.com 的使用者) 的相關資訊。

## 請參閱

#### 概念

[Windows PowerShell 與 Lync Online 的簡介](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

