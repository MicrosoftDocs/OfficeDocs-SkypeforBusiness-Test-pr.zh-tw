---
title: Convert-CsUserData
TOCTitle: Convert-CsUserData
ms:assetid: e52f8037-19f3-49c9-8dfc-79b0c27d8b94
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205337(v=OCS.15)
ms:contentKeyID: 49292623
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Convert-CsUserData

 

_**上次修改主題的時間：** 2015-03-09_

將匯出的使用者資料轉換成 Microsoft Lync Server 2010 或 Lync Server 2013 使用的資料格式。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Convert-CsUserData -InputFile <String> -OutputFile <String> -TargetVersion <Lync2010 | Current> [-ConfDirectoryFilter <String>] [-Force <SwitchParameter>] [-UserFilter <String>]

## 範例

## 範例 1

範例 1 所示的命令會將 C:\\Logs\\Lync2013Data.zip 檔案中儲存的使用者資料，轉換成 Lync Server 2010 所使用的使用者資料格式。轉換的資料則會以 XML 檔案 C:\\Logs\\Lync2010Data.xml 儲存。

    Convert-CsUserData -InputFile "C:\Logs\Lync2013Data.Zip" -OutputFile "C:\Logs\Lync2010Data.xml" -TargetVersion Lync2010

## 範例 2

範例 2 顯示如何轉換單一使用者的資料；在此範例中，即 SIP 位址為 kenmyer@litwareinc.com 的使用者。作法是加入 UserFilter 參數，再緊接著輸入使用者的 SIP 位址 (不含 sip: 首碼)。

    Convert-CsUserData -InputFile "C:\Logs\Lync2013Data.Zip" -OutputFile "C:\Logs\Lync2010data.xml" -TargetVersion Lync2010 -UserFilter "kenmyer@litwareinc.com"

## 詳細描述

使用 [Export-CsUserData](export-csuserdata.md) Cmdlet 匯出 **Convert-CsUserData** Cmdlet 資料，然後視需要將該資料轉換成 Microsoft Lync Server 2010 或 Lync Server 2013 所使用的使用者資料格式，以便 **Import-CsUserData** Cmdlet 將該資料匯入適當版本的 Lync Server。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Convert-CsUserData"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Convert-CsUserData** Cmdlet 所執行的功能。

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
<td><p><em>InputFile</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>含有要轉換之使用者資料的 .ZIP 檔案或 .XML 檔案完整路徑。例如：</p>
<p>-InputFile “C:\Data\Lync2010.zip&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>OutputFile</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>儲存轉換後資料之檔案的完整路徑。如果使用 Microsoft Lync Server 2010 格式輸出資料，則輸出檔案必須使用 .XML 副檔名，例如：</p>
<p>-OutputFile &quot;C:\Data\ConvertedLync2010Data.xml&quot;</p>
<p>如果使用 Lync Server 2013 格式，輸出檔案必須使用 .ZIP 副檔名：</p>
<p>-OutputFile &quot;C:\Data\ConvertedLyncData.zip&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetVersion</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.BlobStore.Cmdlets.ConvertTarget</p></td>
<td><p>表示轉換後資料的格式。允許的值為：</p>
<p>Lync2010</p>
<p>Current</p></td>
</tr>
<tr class="even">
<td><p><em>ConfDirectoryFilter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您轉換會議目錄資料。為達此目的，請加入 ConfDirectoryFilter 參數並指定會議目錄的 Identity：</p>
<p>-ConfDirectoryFilter 13</p>
<p>您可以使用以下命令擷取會議目錄的 Identity：</p>
<p>Get-CsConferenceDirectory | Select-Object Identity, ServiceId</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>UserFilter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您轉換單一使用者的資料。該使用者會使用其 SIP 位址 (不包括 sip: 首碼) 來指定。例如：</p>
<p>-UserFilter &quot;kenmyer@litwareinc.com&quot;</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Convert-CsUserData** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Convert-CsUserData** Cmdlet 會建立建立 XML 或 ZIP 檔案，視轉換後的資料要搭配 Lync Server 2010 或 Lync Server 2013 使用而定。

## 請參閱

#### 其他資源

[Export-CsUserData](export-csuserdata.md)  
[Import-CsUserData](import-csuserdata.md)  
[Sync-CsUserData](sync-csuserdata.md)  
[Update-CsUserData](update-csuserdata.md)

