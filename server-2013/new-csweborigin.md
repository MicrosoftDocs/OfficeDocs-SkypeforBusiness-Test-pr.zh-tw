---
title: New-CsWebOrigin
TOCTitle: New-CsWebOrigin
ms:assetid: 16053a99-b5ff-45e1-be95-b04e3f2fe528
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ950236(v=OCS.15)
ms:contentKeyID: 52056054
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsWebOrigin

 

_**上次修改主題的時間：** 2015-03-09_

建立可新增至網域集合的新網域物件，而這些網域可將跨網域指令碼要求傳送至 Lync Server 2013 部署。

此 Cmdlet 推出於 Lync Server 2013 2013 年 2 月的累計更新。

## 語法

    New-CsWebOrigin -Url <String>

## 範例

## 範例 1

範例 1 所示的命令會將網域 http://fabrikam.com 新增至針對 Redmond 網站所建之新的 Web 服務組態設定集合。為完成此作業，範例中的第一個命令使用 **New-CsWebOrigin** Cmdlet 建立 fabrikam.com 的網域物件。產生的網域物件儲存於名為 $x 的變數中。

範例中的第二個命令使用 **New-CsWebServiceConfiguration** Cmdlet，建立 Redmond 網站的 Web 服務組態設定。其中語法 "–CrossDomainAuthorizationList $x" 會將 http://fabrikam.com 新增至可執行跨網域指令碼的網域集合。

    $x = New-CsWebOrigin -Url "http://fabrikam.com"
    New-CsWebServiceConfiguration -Identity "site:Redmond" - CrossDomainAuthorizationList $x

## 範例 2

範例 2 所示的命令會將網域 http://fabrikam.com 新增至現有的 Web 服務組態設定集合。為完成此作業，範例中的第一個命令使用 **New-CsWebOrigin** Cmdlet 建立 fabrikam.com 的網域物件。產生的網域物件儲存於名為 $x 的變數中。

範例中的第二個命令使用 **Set-CsWebServiceConfiguration** Cmdlet，將 http://fabrikam.com 新增至套用於 Redmond 網站的 Web 服務組態設定。其中語法 @{Add=$x} 會新增該網域至已在可執行跨網域指令碼之網域集合中的任何網域。若要以 http://fabrikam.com 取代現有的集合，可使用語法 @{Replace=$x}。

    $x = New-CsWebOrigin -Url "http://fabrikam.com"
    Set-CsWebServiceConfiguration -Identity "site:Redmond" - CrossDomainAuthorizationList @{Add=$x}

## 詳細描述

New-CsWebOrigin Cmdlet 是用於指定可主控 Web 應用程式的網域，而這些 Web 應用程式可將跨網域指令碼要求傳送至 Lync Server 2013 部署。這個 Cmdlet 主要用於在 Unified Communications Web API 上方所建立的應用程式。

若要新增網域至 Web 服務組態設定集合，您首先必須使用 New-CsWebOrigin Cmdlet 建立網域物件。此網域物件將只存在於記憶體中，因此必須儲存在變數中。建立此物件之後，就可使用 New-CsWebServiceConfiguration Cmdlet 或 Set-CsWebServiceConfiguration Cmdlet，將其新增至 Web 服務組態設定集合。

若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsWebOrigin"}

**Lync Server 控制台：**Lync Server 控制台不提供 **New-CsWebOrigin** Cmdlet 所執行的功能。

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
<td><p><em>Url</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>可傳送跨網域指令碼要求之網域的 URL。URL 必須在前面加上 http: 或 https: 前置詞。例如︰</p>
<p>-Url &quot;http://contoso.com&quot;</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsWebOrigin** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsWebOrigin** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.Web.Origin 物件的新執行個體。

## 請參閱

#### 其他資源

[New-CsWebServiceConfiguration](new-cswebserviceconfiguration.md)  
[Set-CsWebServiceConfiguration](set-cswebserviceconfiguration.md)

