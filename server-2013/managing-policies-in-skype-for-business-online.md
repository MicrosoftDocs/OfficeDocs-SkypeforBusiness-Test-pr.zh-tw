---
title: 管理原則
TOCTitle: 管理原則
ms:assetid: 91372888-a96e-44db-a0dc-d08facbfce87
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362826(v=OCS.15)
ms:contentKeyID: 56269130
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 管理原則

 

_**上次修改主題的時間：** 2015-06-22_

下列 Cmdlet 可管理 商務用 Skype Online 原則。原則有助決定可供使用者與組織整體使用的 商務用 Skype Online 功能。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="get-csclientpolicy.md">Get-CsClientPolicy</a><br />
<a href="grant-csclientpolicy.md">Grant-CsClientPolicy</a></p></td>
<td><p>用戶端原則用於決定可供使用者使用的 Lync 用戶端功能。例如，您可能僅會提供檔案傳輸功能給部分使用者，其他使用者則不會提供。</p></td>
</tr>
<tr class="even">
<td><p><a href="get-csconferencingpolicy.md">Get-CsConferencingPolicy</a><br />
<a href="grant-csconferencingpolicy.md">Grant-CsConferencingPolicy</a></p></td>
<td><p>會議原則可決定會議中所能使用的功能，包括會議是否可以加入 IP 音訊和視訊，乃至於會議出席人數的上限等等。</p></td>
</tr>
<tr class="odd">
<td><p><a href="get-csexternalaccesspolicy.md">Get-CsExternalAccessPolicy</a><br />
<a href="grant-csexternalaccesspolicy.md">Grant-CsExternalAccessPolicy</a></p></td>
<td><p>外部存取原則可用於判定是否允許您的使用者與來自同盟網域的使用者進行通訊，及/或是否允許您的使用者與具有公用 IM 提供者帳戶的使用者進行通訊，例如 Windows Live 或 AOL。</p></td>
</tr>
<tr class="even">
<td><p><a href="get-csvoicepolicy.md">Get-CsVoicePolicy</a><br />
<a href="grant-csvoicepolicy.md">Grant-CsVoicePolicy</a><br />
<a href="remove-csvoicepolicy.md">Remove-CsVoicePolicy</a></p></td>
<td><p>語音原則可用於管理企業語音功能，例如同時響鈴 (設定第二支電話在有人撥打您的辦公室電話時響鈴) 與來電轉接。</p></td>
</tr>
</tbody>
</table>


您亦可使用 商務用 Skype Online 系統管理中心管理選定會議原則設定：

![Lync 管理中心一般選項內容](images/Dn362833.acf90793-7ee4-4faf-b791-f149dd5df2a5(OCS.15).png "Lync 管理中心一般選項內容")

您還可以使用 商務用 Skype Online 系統管理中心管理外部存取原則設定：

![管理中心外部通訊選項](images/Dn362826.e5cfb159-b096-463e-b1ef-2b42eb29168a(OCS.15).png "管理中心外部通訊選項")

## 請參閱

#### 概念

[Lync Online Cmdlet](the-skype-for-business-online-cmdlets.md)  
[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

