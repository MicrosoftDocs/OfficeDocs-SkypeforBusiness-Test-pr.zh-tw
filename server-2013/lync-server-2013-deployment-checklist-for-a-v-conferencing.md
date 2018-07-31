---
title: A/V 會議的部署檢查單
TOCTitle: A/V 會議的部署檢查單
ms:assetid: 6d47426f-6559-407b-9ac1-2453f0b7a2a2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ619183(v=OCS.15)
ms:contentKeyID: 49291253
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# A/V 會議的部署檢查單

 

_**上次修改主題的時間：** 2015-03-09_

在部署其他 Lync Server 2013 元件時，部署 A/V 會議會要求您使用拓撲產生器建立並發行納入會議的拓撲。

## 部署順序

您可在部署初始拓撲的同時，或者在已部署至少一個前端集區或 Standard Edition 伺服器 之後部署會議。

## 會議部署程序

下表提供將會議部署至現有拓撲所需的步驟概觀。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>階段</th>
<th>步驟</th>
<th>角色和群組成員資格</th>
<th>文件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>安裝必備硬體和軟體</strong></p></td>
<td><p>在前端集區前端伺服器與 Standard Edition 伺服器執行會議。除了安裝這些伺服器所需的條件，沒有其他硬體或軟體需求。</p>
<div class="alert">

> [!NOTE]  
> Lync Server 2013 使用 Office Web Apps 及 Office Web Apps Server 以處理 PowerPoint 簡報的共用與轉譯。如需安裝與設定 Office Web Apps Server 的詳細資訊，請參閱＜<a href="lync-server-2013-enabling-office-web-apps-server-and-lync-server-2013.md">設定 Office Web Apps Server 與 Lync Server 2013 的整合</a>＞。


</div></td>
<td><p>為本機系統管理員成員之網域使用者</p></td>
<td><p>〈支援〉文件中的<a href="lync-server-2013-supported-hardware.md">Lync Server 2013 的受支援硬體</a></p>
<p>〈支援〉文件中的<a href="lync-server-2013-server-software-and-infrastructure-support.md">Lync Server 2013 中的伺服器軟體和基礎結構支援</a></p>
<p>〈規劃〉文件中的<a href="lync-server-2013-determining-your-system-requirements.md">判定 Lync Server 2013 的系統需求</a>。</p>
<p>〈規劃〉文件中的<a href="lync-server-2013-technical-requirements-for-archiving.md">Lync Server 2013 中封存的技術需求</a>。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><strong>建立適當的內部拓撲以支援會議</strong></p></td>
<td><p>執行拓撲產生器以將會議新增至拓撲，然後發行拓撲。</p></td>
<td><p>定義拓撲，須以本機使用者群組成員帳戶進行</p>
<p>若要發行拓撲，須使用 Domain Admins 群組及 RTCUniversalServerAdmins 群組成員帳戶進行，而且在您要用於 Lync Server 2013 檔案儲存區的檔案共用上必須具有完整控制權限 (讀取/寫入/修改)，以便拓撲產生器可設定所需的 DACL</p></td>
<td><p>〈部署〉文件中的<a href="lync-server-2013-define-and-configure-a-topology-in-topology-builder.md">針對 Lync Server 2013 在拓撲建置器中定義和設定拓撲</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>設定會議原則及支援</strong></p></td>
<td><p>使用 Lync Server 2013 控制台或 Lync Server 管理命令介面設定會議設定。</p></td>
<td><p>RTCUniversalServerAdmins 群組 (僅限 Windows PowerShell) 或將使用者指派至 [] 或 CSAdministrator 角色</p></td>
<td><p>〈作業〉文件中的<a href="lync-server-2013-conferencing-policies.md">Lync Server 2013 中的會議原則</a>。</p></td>
</tr>
</tbody>
</table>


## 請參閱

#### 其他資源

[Lync Server 2013 中的會議概觀](lync-server-2013-overview-of-conferencing.md)  
[在 Lync Server 2013 中定義會議需求](lync-server-2013-defining-your-requirements-for-conferencing.md)

