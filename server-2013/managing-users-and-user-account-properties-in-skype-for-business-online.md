---
title: 管理使用者與使用者帳戶內容
TOCTitle: 管理使用者與使用者帳戶內容
ms:assetid: 5d13ab15-0e12-4bd0-a970-f130de980404
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362790(v=OCS.15)
ms:contentKeyID: 56269091
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 管理使用者與使用者帳戶內容

 

_**上次修改主題的時間：** 2015-06-22_

下列 Cmdlet 可管理 商務用 Skype Online 使用者帳戶。


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
<td><p><a href="get-csonlineuser.md">Get-CsOnlineUser</a></p></td>
<td><p>傳回帳戶位於您的 商務用 Skype Online 租用戶的使用者相關資訊。</p></td>
</tr>
<tr class="even">
<td><p><a href="get-csuseracp.md">Get-CsUserAcp</a><br />
<a href="remove-csuseracp.md">Remove-CsUserAcp</a><br />
<a href="set-csuseracp.md">Set-CsUserAcp</a></p></td>
<td><p>可讓您針對個別使用者指派、修改或取消指派音訊會議提供者。</p>
<p>音訊會議提供者是提供會議服務給組織的第三方公司，包括即時翻譯、記錄以及個別會議即時總機服務等高階服務。</p>
<p>這些 Cmdlet 並不會傳回可指派給這些使用者的音訊提供者。如需該類資訊，請改為執行下列命令：</p>
<pre><code>Get-CsAudioConferencingProvider</code></pre></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Set-CsUser Cmdlet 亦包含在可供 商務用 Skype Online 系統管理員使用的 Cmdlet 組中。然而，Set-CsUser 目前無法用於管理 商務用 Skype Online (除非是設定 AudioVideoDisabled 參數)。若您嘗試以其他任何參數執行 Cmdlet，將會失敗並看到類似下列的錯誤訊息：<br />
Unable to set “SipAddress”. This parameter is restricted within Remote Tenant PowerShell. (無法設定 &quot;SipAddress&quot;。此參數限制於遠端租用戶 PowerShell 內。)</td>
</tr>
</tbody>
</table>


此外，音訊會議提供者亦可透過 商務用 Skype Online 系統管理中心指派 (或取消指派) 給使用者帳戶：

![Lync 管理中心電話撥入式會議內容](images/Dn362790.0c61f0c2-8aef-4020-a0a8-02580d43092a(OCS.15).png "Lync 管理中心電話撥入式會議內容")

## 請參閱

#### 概念

[Lync Online Cmdlet](the-skype-for-business-online-cmdlets.md)  
[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

