---
title: Get-CsAdServerSchema
TOCTitle: Get-CsAdServerSchema
ms:assetid: fba777e5-886c-4914-a492-f2237721c57c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413070(v=OCS.15)
ms:contentKeyID: 49292911
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAdServerSchema

 

_**上次修改主題的時間：** 2015-03-09_

傳回指出 Active Directory 結構描述設定是否正確，以便於安裝 Lync Server 的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsAdServerSchema [-Report <String>]

## 範例

## 範例 1

範例 1 所示的命令會傳回 Active Directory 伺服器架構的目前狀態。如果架構處於最新狀態，命令會傳回下列值：SCHEMA\_VERSION\_STATE\_CURRENT。

    Get-CsAdServerSchema

## 範例 2

範例 2 也會傳回 Active Directory 伺服器架構的目前狀態。此外，命令會將更多有關該架構的詳細資訊寫入名稱為 C:\\Logs\\Server\_Schema.html 的檔案。此資訊包括諸如架構主要版本與次要版本的事項。

    Get-CsAdServerSchema -Report C:\Logs\Server_Schema.html

## 詳細描述

除非您已正確擴充 Active Directory 架構，否則無法安裝 Lync Server；這表示必須先將 Lync Server 特定的物件和屬性新增至 Active Directory 網域服務，才能執行安裝。例如，必須修改使用者帳戶物件，才能允許屬性執行諸如下列的動作：指出已指派給使用者的語音原則，或者報告該帳戶是否已啟用 Enterprise Voice。

**Get-CsAdServerSchema** Cmdlet 會傳回單一值，告知您 Active Directory 是否已擴充，以及是否已準備好安裝 Lync Server。如果 **Get-CsAdServerSchema** Cmdlet 傳回SCHEMA\_VERSION\_STATE\_CURRENT 值，表示架構已經擴充。如果 Cmdlet 傳回任何其他值，則表示架構尚未擴充。

**Get-CsAdServerSchema** Cmdlet 通常會在安裝精靈中執行；如果安裝精靈判斷架構並未正確準備，則您會收到錯誤訊息且安裝精靈會停止。但是，您也可以獨立執行 **Get-CsAdServerSchema** Cmdlet，而不和安裝精靈一起執行，讓您有機會可以在嘗試安裝 Lync Server 之前先確認架構狀態。

**Get-CsAdServerSchema** Cmdlet 執行的功能與下列 Microsoft Office Communications Server 2007 R2 命令相同：Lcscmd.exe /domain /action:CheckSchemaPrepState。

誰可以執行這個 Cmdlet：根據預設，擁有 Active Directory 讀取權限的使用者可在本機執行 **Get-CsAdServerSchema** Cmdlet。一般來說，所有網域成員均擁有此權限。

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
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\SchemaPrep.html&quot;</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsAdServerSchema** Cmdlet 不會接受管線傳送的輸入。

## 傳回類型

**Get-CsAdServerSchema** Cmdlet 會傳回 Microsoft.Rtc.Management.Deployment.SchemaVersionState 物件的執行個體。

## 請參閱

#### 其他資源

[Install-CsAdServerSchema](install-csadserverschema.md)

