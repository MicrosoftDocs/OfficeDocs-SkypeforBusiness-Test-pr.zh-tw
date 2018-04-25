---
title: 拓撲測試的問題
TOCTitle: 拓撲測試的問題
ms:assetid: 821e8916-7b5d-4f64-8fb0-e5cc392ec1bb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205045(v=OCS.15)
ms:contentKeyID: 49291500
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 拓撲測試的問題

 

_**上次修改主題的時間：** 2012-09-21_

與 **Test-CsTopology** Cmdlet 相同之處在於，Best Practice Analyzer 提供一種方式，讓您驗證 Lync Server 2013 是否在全域層級運作正常。根據預設，這個 Cmedlet 之類的 Best Practice Analyzer 會檢查整個 Lync Server 2013 基礎結構，以驗證必要的服務都在執行，而且已針對這些服務及安裝 Lync Server 2013 時建立之萬用安全群組設定適當的使用者權限。

除了完整驗證 Lync Server 的有效性以外， **Test-CsTopology** 也可檢查特定服務的有效性。如需關於使用 Cmdlet 測試特定服務的詳細資訊，請參閱＜Lync Server 管理命令介面＞文件中的＜[Test-CsTopology](test-cstopology.md)＞。使用下列資訊有助於解決您拓撲的問題。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>端視 Edge Server 以及任何相關周邊網路設定而定，包括防火牆設定和周邊，Best Practices Analyzer 可能無法存取和掃描 Edge Server。如果將 Edge Server 包含在掃描內，而且報告指出存取 Edge Server 發生問題，請清除 [Edge Server] 核取方塊，並再次執行掃描，以避免問題出現在報告中。</td>
</tr>
</tbody>
</table>


## 解決拓撲的問題

如果拓撲測試發現拓撲的問題，這些問題可能是在您發行或啟用拓撲時發生的問題所造成。

變更拓撲時，變更在發行和啟用後才會生效。您必須使用拓撲產生器進行拓撲變更。進行變更後，即可使用拓撲產生器發佈和啟用這些變更。

發佈變更時，系統會將新資訊 (例如，新網站或新伺服器角色) 寫入 中央管理存放區。不過，這些新物件 (或新修改的物件) 並不會立即加入您的拓撲中。物件必須等到更新後的拓撲啟用後才會加入拓撲。當您在 拓撲產生器 中選取 \[發佈\] 選項時，以下兩個步驟都會發生：發佈變更 (也就是寫入 中央管理存放區)，然後啟用新拓撲。

根據預設，RTCUniversalServerAdmins 群組的成員有權執行 **Publish-CsTopology** Cmdlet 及 **Enable-CsTopology** Cmdlet。但是，如果尚未指派設定權限，則您必須以網域系統管理員的身分登入，才能執行 **Publish-CsTopology**若要給予 RTCUniversalServerAdmins 實際使用 **Publish-CsTopology** Cmdlet 的權限，您必須在每個有電腦執行 Lync Server 服務的 Active Directory 容器上執行 **Grant-CsSetupPermission** Cmdlet。若要給予 RTCUniversalServerAdmins 使用 **Enable-CsTopology** Cmdlet 的權限，您必須對於每個有電腦執行 Lync Server 服務的 Active Directory 網域服務容器執行 **Set-CsSetupPermission** Cmdlet。請注意，這適用於使用拓撲產生器使用啟用和發佈拓撲。如果您尚未使用 **Set-CsSetupPermission** 指派權限，則只有網域管理員才能透過拓撲產生器啟用和發行拓撲。

