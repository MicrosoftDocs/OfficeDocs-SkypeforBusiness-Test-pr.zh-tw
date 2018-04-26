---
title: Edge Server Cmdlet
TOCTitle: Edge Server Cmdlet
ms:assetid: 1a5427f4-a0d1-4652-8135-91333158ffc8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg415635(v=OCS.15)
ms:contentKeyID: 49290242
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Edge Server Cmdlet

 

_**上次修改主題的時間：** 2013-10-07_

Edge Server 可為您提供一種方式，將 Microsoft Lync Server 2013 的功能延伸至未登入您內部網路的人員。例如，如果您有遠端使用者 (不是透過內部網路，而是透過網際網路登入 Lync Server 2013 的已驗證使用者)，將需要設定執行 Lync Server Access Edge Service 的 Edge Server。此外，如果您要與其他組織建立同盟，或者如果要賦予使用者與擁有公用立即訊息服務 (例如 Yahoo\!、AOL 或 MSN) 帳戶之人員進行通訊的權限，也需要 Edge Server。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>自 2012 年 9 月 1 日起，Microsoft Lync 公用 IM 連線使用者訂閱授權 (&quot;PIC USL&quot;) 無法再以新合約或續約的方式購買。持有使用中授權的客戶將可繼續與 Yahoo! Messenger 維持同盟關係直至服務終止日。目前已公佈 AOL 與 Yahoo! 在 2014 年 6 月的結束日期。如需詳細資訊，請參閱<a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Lync Server 2013 中的公用立即訊息連線的支援</a>。</p></li>
<li><p>PIC USL 是針對每位使用者的每月訂閱授權，為 Lync Server 或 Office Communications Server 與 Yahoo! Messenger 同盟的必要授權。Microsoft 是否提供此項服務視 Yahoo! 的支援而定，而此基礎合約將告結束。</p></li>
<li><p>更勝以往，Lync 成為連接全世界組織之間以及個人之間的強大工具。除了 Lync Standard CAL 之外，與 Windows Live Messenger 同盟不需要其他使用者/裝置授權。此清單更將加入 Skype 同盟，讓 Lync 使用者可透過 IM 和語音觸及數億位使用者。</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Edge Server Cmdlet

下表列出的 Cmdlet 與管理 Edge Server 直接相關：

**Edge Server**

  -   
    [Get-CsAccessEdgeConfiguration](get-csaccessedgeconfiguration.md)

  -   
    [Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)

  -   
    [Get-CsAVEdgeConfiguration](get-csavedgeconfiguration.md)

  -   
    [New-CsAVEdgeConfiguration](new-csavedgeconfiguration.md)

  -   
    [Remove-CsAVEdgeConfiguration](remove-csavedgeconfiguration.md)

  -   
    [Set-CsAVEdgeConfiguration](set-csavedgeconfiguration.md)

  -   
    [Test-CsAVEdgeConnectivity](test-csavedgeconnectivity.md)

  -   
    [Set-CsEdgeServer](set-csedgeserver.md)

## 請參閱

#### 其他資源

[Lync Server PowerShell 部落格](http://go.microsoft.com/fwlink/?linkid=203150)

