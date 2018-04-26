---
title: Get-CsUICulture
TOCTitle: Get-CsUICulture
ms:assetid: b8df7083-068b-4d5e-a9b4-448602de6586
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412900(v=OCS.15)
ms:contentKeyID: 49292109
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsUICulture

 

_**上次修改主題的時間：** 2015-03-09_

傳回 Lync Server 管理命令介面使用之文化特性的資訊 (即語言和地區設定)。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsUICulture

## 範例

## 範例 1

範例 1 所示的命令會傳回有關目前 Lync Server 管理命令介面使用的文化特性基本資訊。

    Get-CsUICulture

## 詳細描述

雖然 Lync Server 有許多語言可使用，但是該軟體並非真正的 MUI (多語系使用者介面) 應用程式。總而言之，這表示每次您變更作業系統的語言時，Lync Server 管理命令介面 的使用者介面不會變更語言。例如，假設您已安裝英文 (美國) 版本的 Lync Server，並且執行英文 (美國) 的 Windows 作業系統。如果您變更作業系統文化特性 (也就是語言和地區設定) 為丹麥文，Lync Server 管理命令介面不會自動跟著變更套件；而 Lync Server 管理命令介面使用者介面 (包括錯誤訊息和說明文字) 仍舊是英文 (美國)。如果您需要變更 Lync Server 管理命令介面的文化特性，您必須執行 **Set-CsUICulture** Cmdlet。

**Get-CsUICulture** Cmdlet 可讓您指定目前 Lync Server 管理命令介面所使用的文化特性。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsUICulture** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。

## 參數


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>必要</th>
<th>類型</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>此 Cmdlet 只提供一般的 Windows PowerShell 參數。</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsUICulture** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsUICulture** Cmdlet 會傳回 System.Globalization.CultureInfo 類別的執行個體。

## 請參閱

#### 其他資源

[Set-CsUICulture](set-csuiculture.md)

