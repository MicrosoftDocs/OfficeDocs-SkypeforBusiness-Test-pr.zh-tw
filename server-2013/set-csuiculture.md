---
title: Set-CsUICulture
TOCTitle: Set-CsUICulture
ms:assetid: 53fbc126-1df9-4ea0-8055-4e9530ab89d6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398354(v=OCS.15)
ms:contentKeyID: 49290934
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsUICulture

 

_**上次修改主題的時間：** 2015-03-09_

可讓您修改 Lync Server 管理命令介面使用的文化特性 (也就是語言和區域設定)。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsUICulture -Culture <String> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將 Lync Server 管理命令介面 的文化特性設為英文 (美國)。作法是使用語言代碼 en-US。

    Set-CsUICulture -Culture "en-US"

## 範例 2

範例 2 會將 Lync Server 管理命令介面的文化特性設為預設的文化特性值。預設值即為您原本安裝 Lync Server 時所使用的文化特性設定。

    Set-CsUICulture -Culture "default"

## 詳細描述

雖然 Lync Server 有許多語言可使用，但是該軟體並非真正的多語系使用者介面 (MUI) 應用程式。總而言之，這表示每次您變更作業系統的語言時，Lync Server 管理命令介面 的使用者介面不會變更語言。例如，假設您已安裝英文 (美國) 版本的 Lync Server，並且執行英文 (美國) 的 Windows 作業系統。如果您變更作業系統文化特性 (也就是語言和地區設定) 為丹麥文，Lync Server 管理命令介面 不會自動跟著變更套件；而 Lync Server 管理命令介面 使用者介面 (包括錯誤訊息和說明文字) 仍舊是英文 (美國)。如果您需要變更 Lync Server 管理命令介面 的文化特性，您必須執行 **Set-CsUICulture** Cmdlet。

使用 **Set-CsUICulture** Cmdlet 時請牢記兩件事。首先，該 Cmdlet 只能用來修改本機電腦上的 Lync Server 管理命令介面 設定；**Set-CsUICulture** Cmdlet 無法變更 Lync Server 管理命令介面的遠端執行個體。這是因為所有電腦使用者都共用同一個 Lync Server 管理命令介面執行個體：如果允許遠端使用者變更文化特性，會立即變更 Lync Server 管理命令介面之其他任何使用者 (包括本機使用者) 的文化特性。

第二，您只能將語言設為美國英文 ("en-US") 或一開始安裝 Lync Server 時所使用的語言 ("default")。例如，如果您原本安裝義大利版的 Lync Server，則您設定 UI 文化特性時就有兩個選擇：英文和義大利文。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsUICulture** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。

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
<td><p><em>Culture</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>讓您可以指定 Lync Server 管理命令介面 使用的文化特性。將文化特性設為 &quot;en-US&quot; 以便使用美國英文，或將文化特性設為 &quot;default&quot; 以便使用原本安裝 Lync Server 時使用的語言。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Set-CsUICulture** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Set-CsUICulture** Cmdlet 不會傳回任何值或物件，而會修改現有 System.Globalization.CultureInfo 類別的現有執行個體。

## 請參閱

#### 其他資源

[Get-CsUICulture](get-csuiculture.md)

