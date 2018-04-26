---
title: Get-CsAudioConferencingProvider
TOCTitle: Get-CsAudioConferencingProvider
ms:assetid: 4632e9d0-aa87-459f-ad7e-27125c11da5b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994030(v=OCS.15)
ms:contentKeyID: 52056097
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAudioConferencingProvider

 

_**上次修改主題的時間：** 2015-03-09_

傳回授權供組織使用之音訊會議提供者的資訊。音訊會議提供者是為組織提供會議服務的協力廠商公司。

**Get-CsAudioConferencingProvider** Cmdlet 僅可與 Microsoft Lync Online 搭配使用。

## 語法

    Get-CsAudioConferencingProvider [[-Identity] <XdsGlobalRelativeIdentity>] [-LocalStore][<CommonParameters>]Get-CsAudioConferencingProvider [-Filter <string>] [-LocalStore] [<CommonParameters>]

## 範例

## 範例 1

範例 1 所示的命令會傳回可供組織使用之所有音訊會議提供者的資訊。

    Get-CsAudioConferencingProvider

## 範例 2

範例 2 會針對單一音訊會議提供者 (Identity 為 Fabrikam Telecom 的提供者) 傳回資訊。

    Get-CsAudioConferencingProvider -Identity "Fabrikam Telecom"

## 範例 3

範例 3 示範如何使用萬用字元值 (和 Filter 參數) 傳回音訊會議提供者的相關資訊。在此範例中，篩選值 "\*Fabrikam\*" 會傳回 Identity 中任何位置含有字串值 "Fabrikam" 的所有音訊會議提供者。

    Get-CsAudioConferencingProvider -Filter "*Fabrikam*"

## 詳細描述

音訊會議提供者是提供組織會議服務的第三方公司。總而言之，音訊會議提供者提供處於異地之使用者在未連接至公司網路或網際網路，可參與會議之語音部分的方法。音訊會議提供者通常會提供高階服務，例如現場翻譯、記錄及現場個別會議總機服務。

在組織與音訊會議提供者簽約後，可使用 **Set-CsUserAcp** Cmdlet 將使用者指派給該提供者。系統管理員可使用 **Get-CsAudioConferencingProvider** Cmdlet 來擷取可的音訊會議提供者的相關資訊。

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
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您在指示要傳回的一或多個音訊會議提供者時使用萬用字元。例如，此語法可傳回 Identity 中某個位置含有字串值 &quot;fabrikam&quot; 之所有音訊會議提供者的相關資訊：</p>
<p>-Filter &quot;*fabrikam*&quot;</p>
<p>請注意，您不能在同一個命令中同時使用 Filter 參數和 Identity 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>所傳回音訊會議提供者的唯一識別碼。例如：</p>
<p>-Identity &quot;Fabrikam Telecom&quot;</p>
<p>命令中若未加入 Identity 參數和 Filter 參數，<strong>Get-CsAudioConferencingProvider</strong> Cmdlet 會傳回所有可用提供者的資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取音訊會議提供者資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsAudioConferencingProvider** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsAudioConferencingProvider** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.AudioConferencingProvider.AudioConferencingProvider\#Decorated 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsUserAcp](get-csuseracp.md)  
[Remove-CsUserAcp](remove-csuseracp.md)  
[Set-CsUserAcp](set-csuseracp.md)

