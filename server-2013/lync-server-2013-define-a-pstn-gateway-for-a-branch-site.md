---
title: Lync Server 2013：定義分支網站的 PSTN 閘道
TOCTitle: 定義分支網站的 PSTN 閘道
ms:assetid: 87be2fe2-1d56-4062-b430-439d4536414c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398689(v=OCS.15)
ms:contentKeyID: 49291571
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中定義分支網站的 PSTN 閘道

 

_**上次修改主題的時間：** 2012-09-21_

請在中央網站執行這項程序，其中至少包含一個 前端集區或 Standard Edition 伺服器。

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
<td>在執行此程序之前，必須符合下列條件：
<ul>
<li><p>必須在中央網站設定 Lync Server 2013  通訊軟體。</p></li>
<li><p>必須將 中繼伺服器部署於中央網站。</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 定義 PSTN 閘道

1.  依序按一下 \[開始\] 、\[程式集\] 、\[Microsoft Lync Server\] 及 \[Lync Server 拓撲建置器\] 。

2.  在主控台樹狀目錄中依序展開中央網站和 \[分公司網站\] ，並展開要定義公用交換電話網路 (PSTN) 閘道的分支網站名稱，然後展開 \[共用元件\] 。

3.  以滑鼠右鍵按一下 **\[PSTN 閘道\]** ，然後按一下 **\[新增 IP/PSTN 閘道\]** 。

4.  按一下 \[定義新的 IP/PSTN 閘道\] 對話方塊中的 \[閘道 FQDN 或 IP 位址\] ，然後輸入部署於分支網站之閘道的完整網域名稱 (FQDN) 或 IP 位址。

5.  按一下 **\[IP/PSTN 閘道的聆聽連接埠\]** ，然後接受預設值。

6.  在 **\[SIP 傳輸通訊協定\]** 清單中按一下閘道使用的傳輸通訊協定，然後按一下 \[確定\] 。
    
    > [!NOTE]  
    > 基於安全性考量，我們強烈建議您使用支援傳輸層安全性 (TLS) 的 PSTN 閘道。
    


<table>
<thead>
<tr class="header">
<th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用 <strong>Set-CsPstnGateway</strong> Cmdlet 修改 PSTN 閘道的屬性。如需詳細資訊，請參閱＜ Lync Server 管理命令介面 說明＞中的＜ <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsPstnGateway">Set-CsPstnGateway</a>＞。</td>
</tr>
</tbody>
</table>


設定分支網站恢復的 \[下一個步驟\] ： [在 Lync Server 2013 中為分支網站恢復設定使用者](lync-server-2013-configuring-users-for-branch-site-resiliency.md)

## 請參閱

#### 概念

[Lync Server 2013 中的 PSTN 閘道部署選項](lync-server-2013-pstn-gateway-deployment-options.md)

