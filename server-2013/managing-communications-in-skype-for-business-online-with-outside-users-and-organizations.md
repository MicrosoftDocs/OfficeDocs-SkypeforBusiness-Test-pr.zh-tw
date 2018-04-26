---
title: 管理與外部使用者以及組織的通訊
TOCTitle: 管理與外部使用者以及組織的通訊
ms:assetid: 8a64f0fe-1e79-47d8-835e-548d7ac0757e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362813(v=OCS.15)
ms:contentKeyID: 56269117
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 管理與外部使用者以及組織的通訊

 

_**上次修改主題的時間：** 2015-06-22_

下列 Cmdlet 可用於管理與外部網域以及公用立即訊息 (IM) 提供者的同盟：


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
<td><p><a href="new-csedgeallowallknowndomains.md">New-CsEdgeAllowAllKnownDomains</a></p></td>
<td><p>允許使用者與封鎖網域清單所指定的網域以外的所有網域進行通訊。</p>
<p>同盟乃是可讓使用者與來自其他網域的使用者交換 IM 與目前狀態資訊的服務。一般來說，系統管理員可使用允許與封鎖清單指定使用者可與之通訊的外部網域。</p></td>
</tr>
<tr class="even">
<td><p><a href="new-csedgeallowlist.md">New-CsEdgeAllowList</a></p></td>
<td><p>將使用者通訊限制為指定的網域集合。</p>
<p>系統將僅允許使用者與允許網域清單中所出現的網域進行通訊。</p></td>
</tr>
<tr class="odd">
<td><p><a href="new-csedgedomainpattern.md">New-CsEdgeDomainPattern</a></p></td>
<td><p>修改允許或封鎖網域清單。</p></td>
</tr>
<tr class="even">
<td><p><a href="get-cstenantfederationconfiguration.md">Get-CsTenantFederationConfiguration</a><br />
<a href="set-cstenantfederationconfiguration.md">Set-CsTenantFederationConfiguration</a></p></td>
<td><p>啟用及停用與其他網域的同盟以及與公用提供者的同盟。</p></td>
</tr>
<tr class="odd">
<td><p><a href="get-cstenanthybridconfiguration.md">Get-CsTenantHybridConfiguration</a><br />
<a href="set-cstenanthybridconfiguration.md">Set-CsTenantHybridConfiguration</a></p></td>
<td><p>指派適當值至混合式組態設定。</p>
<p>在混合式或「分割網域」部署中，組織有部分使用者具有位於 商務用 Skype Online 的帳戶，同時又有其他使用者具有位於 Lync Server 2013 的帳戶。根據預設，位於 商務用 Skype Online 的使用者並無企業語音所提供之完整功能範圍的存取權限。若要將該類企業語音功能的存取權限提供給 商務用 Skype Online 使用者，系統管理員需要將適當值指派給混合式組態設定。這些值僅可使用 <strong>CsTenantHybridConfiguration</strong> Cmdlet 加以管理。</p></td>
</tr>
<tr class="even">
<td><p><a href="get-cstenantpublicprovider.md">Get-CsTenantPublicProvider</a><br />
<a href="set-cstenantpublicprovider.md">Set-CsTenantPublicProvider</a></p></td>
<td><p>管理與公用提供者的同盟。</p>
<p>公用提供者是指針對一般大眾提供 SIP 通訊服務的組織。當您與公用提供者建立同盟關係時，實際上就等於和任何具有該提供者所提供帳戶的使用者建立同盟。</p></td>
</tr>
</tbody>
</table>


您亦可使用 商務用 Skype Online 系統管理中心針對同盟網域以及公用提供者管理同盟設定：

![Lync Online 管理中心組織設定](images/Dn362813.f860d03f-5906-49b0-bcc7-7634afe7005e(OCS.15).png "Lync Online 管理中心組織設定")

## 請參閱

#### 概念

[Lync Online Cmdlet](the-skype-for-business-online-cmdlets.md)  
[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

