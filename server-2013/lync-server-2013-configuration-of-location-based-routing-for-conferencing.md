---
title: Lync Server 2013：以位置為基礎的路由會議設定
TOCTitle: 以位置為基礎的路由會議設定
ms:assetid: d8c708cc-a1b1-48b1-808c-a64df15f7701
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362846(v=OCS.15)
ms:contentKeyID: 56269157
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中以位置為基礎的路由會議設定

 

_**上次修改主題的時間：** 2014-09-29_

「以位置為基礎的路由會議」應用程式依賴 Lync Server 2013 以位置為基礎的路由設定。以下是主要設定：

  - 參與者加入會議的位置是根據其網站判定。必須在 Lync Server 中定義網站及其相關網路子網路，才能強制執行以位置為基礎的路由。

  - 若要為會議強制執行以位置為基礎的路由，必須針對以位置為基礎的路由啟用 Lync 參與者。

  - 若要針對 PSTN 端點加入會議強制執行以位置為基礎的路由，必須針對以位置為基礎的路由設定用來連線 PSTN 端點的 SIP 主幹。

如需部署和設定 Lync Server 2013 以位置為基礎之路由的更多資訊，請參閱[設定以位置為基礎的路由](lync-server-2013-configuring-location-based-routing.md)。

## 啟用以位置為基礎的路由會議應用程式

預設會停用以位置為基礎的路由會議應用程式。啟用此應用程式前，需要為應用程式決定要指派的適當優先順序。若要決定此優先順序，請在 Lync Server 管理命令介面 中執行下列 Cmdlet：

Get-CsServerApplication -Identity Service:Registrar:\<Pool FQDN\>

在此 Cmdlet 中，\<Pool FQDN\> 是要在其中啟用以位置為基礎之路由會議應用程式的集區。

此 Cmdlet 將傳回 Lync Server 所代管應用程式的清單及每個應用程式的優先順序值。指派給以位置為基礎之路由會議應用程式的優先順序值應大於 "UdcAgent" 應用程式，並且小於 "DefaultRouting"、"ExumRouting" 和 "OutboundRouting" 應用程式的優先順序值。指派給以位置為基礎之路由會議應用程式的優先順序值建議比 "UdcAgent" 應用程式的優先順序值高一點。

例如，如果 "UdcAgent" 應用程式的優先順序值為 "2"、"DefaultRouting" 應用程式的優先順序值 "8"、"ExumRouting" 應用程式的優先順序值為 "9"，而 "OutboundRouting" 應用程式的優先順序值 "10"，則您應將優先順序值 "3" 指派給以位置為基礎的路由會議應用程式。這麼做會按下列順序放置應用程式的優先順序：其他應用程式 (優先順序：0 到 1)、"UdcAgent" (優先順序：2)、以位置為基礎的路由會議應用程式 (優先順序：3)、其他應用程式 (優先順序：4 到 8)、"DefaultRouting" (優先順序：9)、"ExumRouting" (優先順序：10) 及 "OutboundRouting" (優先順序：11)。

找到以位置為基礎之路由會議應用程式的正確優先順序值後，請為已啟用「以位置為基礎的路由」之使用者所在的每個前端集區或 Standard Edition Server 輸入下列 Cmdlet：

New-CsServerApplication -Identity Service:Registrar:\<Pool FQDN\>/LBRouting -Priority \<Application Priority\> -Enabled $true -Critical $true -Uri http://www.microsoft.com/LCS/LBRouting

例如：

New-CsServerApplication -Identity Service:Registrar:LS2013CU2LBRPool.contoso.com/LBRouting -Priority 3 -Enabled $true -Critical $true -Uri http://www.microsoft.com/LCS/LBRouting

使用此 Cmdlet 之後，會重新啟動集區中所有前端伺服器，或已啟用以位置為基礎之路由會議應用程式的 Standard Edition Server。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在重新啟動適用集區中的所有前端伺服器，或重新啟動 Standard Edition Server 之前，不會針對會議或咨詢轉接強制執行強制以位置為基礎的路由。若在前述 Cmdlet 中將 <strong>–Critical</strong> 設為 <strong>$true</strong>，您的 Lync 服務將立即重新啟動。如果不想立即重新啟動這些服務，請立即將 <strong>–Critical</strong> 設為 <strong>$false</strong>，稍後再於重新啟動服務後，使用 <strong>Set-CsServerApplication</strong> 將 <strong>-Critical</strong> 變為 <strong>$true</strong>。</td>
</tr>
</tbody>
</table>


成功啟用以位置為基礎的路由會議應用程式，並且重新啟動所有適用的 Lync 伺服器後，系統將監視已啟用「以位置為基礎的路由」之 Lync 使用者召集的所有會議，以避免 PSTN 公用電話旁路

