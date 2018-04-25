---
title: 設定封存選項
TOCTitle: 設定封存選項
ms:assetid: b2f7f74d-e1ad-494e-9d46-5eb0efe5fb29
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205182(v=OCS.15)
ms:contentKeyID: 49292050
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定封存選項

 

_**上次修改主題的時間：** 2012-10-10_

在 Lync Server 2013 控制台中，您使用 \[封存\] 設定來指定封存的實作方式。這包括下列封存組態：

  - 部署 Lync Server 2013 時預設會建立的全域組態。

  - 您可建立並使用的選用網站層級與集區層級組態，以指定在特定網站或集區實作封存的方式。

您一開始在部署封存時設定封存組態，但可以在部署之後變更、新增和刪除組態。在 Lync Server 2013 控制台中，您可使用 \[封存和監控\] 群組 的 \[封存設定\] 頁面來管理全域層級、網站層級與集區層級的設定。如需關於封存組態實作方式的詳細資訊，包括您可以指定的選項以及封存組態的階層，請參閱規劃文件、部署文件或作業文件中的[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)。如需關於如何在部署後管理設定的詳細資訊，請參閱作業文件中的[在 Lync Server 2013 中管理組織、網站及集區的封存設定選項](lync-server-2013-managing-archiving-configuration-options-for-your-organization-sites-and-pools.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要使用封存，您必須設定封存原則，以指定是否針對位於 Lync Server 2013 的使用者啟用內部通訊、外部通訊或兩者的封存。預設不會啟用內部或外部通訊的封存。在任何原則中啟用封存前，應先如本節所述，為您的部署和 (選用的) 特定網站與集區指定適當的封存組態。如需關於啟用封存的詳細資訊，請參閱部署文件中的<a href="lync-server-2013-configuring-and-assigning-archiving-policies.md">設定和指派封存原則</a>。<br />
如果您部署中的所有使用者不使用 Microsoft Exchange 整合，則您必須設定封存原則來指定是否啟用內部通訊、外部通訊的封存，或兩者皆啟用。依預設，在使用 Lync Server 2013 封存資料庫時，不會啟用內部與外部通訊的資料封存。在任何原則中啟用封存前，應先如本節所述，為您的部署和 (選用的) 特定網站與集區指定適當的封存組態。如需關於啟用封存以搭配使用 Lync Server 2013 封存資料庫的詳細資訊，請參閱部署文件中的<a href="lync-server-2013-configuring-and-assigning-archiving-policies.md">設定和指派封存原則</a>。</td>
</tr>
</tbody>
</table>


## 本章節內容

  - [在全域層級設定封存選項](lync-server-2013-configuring-archiving-options-at-the-global-level.md)

  - [設定網站的封存選項](lync-server-2013-configuring-archiving-options-for-a-site.md)

  - [設定集區的封存選項](lync-server-2013-configuring-archiving-options-for-a-pool.md)

