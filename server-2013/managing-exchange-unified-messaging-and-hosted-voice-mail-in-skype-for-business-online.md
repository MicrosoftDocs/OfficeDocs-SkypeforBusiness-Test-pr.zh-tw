---
title: 管理 Exchange 整合通訊與託管語音信箱
TOCTitle: 管理 Exchange 整合通訊與託管語音信箱
ms:assetid: 844bf8d5-e093-4dcd-abcf-48dc70e8c73c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362822(v=OCS.15)
ms:contentKeyID: 56269126
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 管理 Exchange 整合通訊與託管語音信箱

 

_**上次修改主題的時間：** 2015-06-22_

下列 Cmdlet 可用於管理 Exchange 整合通訊 (UM) 與託管語音信箱原則：


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
<td><p><a href="get-csexumcontact.md">Get-CsExUmContact</a></p>
<p><a href="new-csexumcontact.md">New-CsExUmContact</a></p>
<p><a href="remove-csexumcontact.md">Remove-CsExUmContact</a></p>
<p><a href="set-csexumcontact.md">Set-CsExUmContact</a></p></td>
<td><p>建立並管理用於自動語音應答與訂閱者存取服務的連絡人物件 (當 Exchange UM 為託管服務時)。</p>
<p>商務用 Skype Online 與 Exchange UM 搭配使用時，可提供多項語音相關功能，包括自動語音應答與訂閱者存取。自動語音應答可自動接聽電話並將電話路由至正確人員。訂閱者存取則可讓使用者連線至 Exchange UM 並擷取電子郵件、語音訊息、連絡人，以及行事曆資訊。</p>
<p>當 Exchange UM 作為託管服務提供時，必須使用 Windows PowerShell 建立用於自動語音應答與訂閱者存取服務的連絡人物件。這些物件乃是使用 CsExUmContact Cmdlet 加以建立與管理。</p></td>
</tr>
<tr class="even">
<td><p><a href="get-cshostedvoicemailpolicy.md">Get-CsHostedVoicemailPolicy</a></p>
<p><a href="grant-cshostedvoicemailpolicy.md">Grant-CsHostedVoicemailPolicy</a></p></td>
<td><p>管理組織中所使用的託管語音信箱原則。託管語音信箱原則可指定未接電話路由至 Exchange UM 服務的方式。這些原則僅會影響啟用 Exchange UM 託管語音信箱的使用者。若要確認使用者是否已啟用託管語音信箱，請透過 Windows PowerShell 命令提示字元執行類似下列命令：</p>
<pre><code>Get-CsOnlineUser -Identity &quot;kenmyer@litwareinc.com&quot; | Select-Object HostedVoiceMail</code></pre></td>
</tr>
</tbody>
</table>


您無法使用 商務用 Skype Online 系統管理中心管理 Exchange UM 設定與託管語音信箱原則。

## 請參閱

#### 概念

[Lync Online Cmdlet](the-skype-for-business-online-cmdlets.md)  
[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

