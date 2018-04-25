---
title: 設定和指派封存原則
TOCTitle: 設定和指派封存原則
ms:assetid: acd18ea8-c7f1-4178-871a-cd3b75bdaa8b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205175(v=OCS.15)
ms:contentKeyID: 49291997
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定和指派封存原則

 

_**上次修改主題的時間：** 2012-10-01_

在 Lync Server 2013 中，您可使用原則為 Lync Server 2013 上的使用者啟用與停用內部通訊與外部通訊的封存。這包含下列封存原則：

  - 部署 Lync Server 2013 時預設建立的全域原則。

  - 您可建立並用來指定如何為特定網站或使用者實作封存的選用網站層級與使用者層級原則。

您一開始會在部署封存時設定封存原則，但可在部署後變更、新增與刪除原則。在 Lync Server 2013 控制台中，您可使用 \[封存和監控\] 群組 的 \[封存原則\] 頁面來管理全域層級、網站層級與使用者層級的原則。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要控制封存的實作，您必須在 [封存] 設定中指定選項，例如是否要封存 IM 或會議、是否使用關鍵模式，以及清除選項。依預設，在全域 [封存] 設定或任何網站或集區 [封存] 設定中不會啟用任何選項。您應該先在 [封存] 設定中指定所有適當的選項之後，才在 [封存] 原則中啟用內部或外部通訊的封存。如需詳細資訊，請參閱作業文件中的<a href="lync-server-2013-managing-archiving-configuration-options-for-your-organization-sites-and-pools.md">在 Lync Server 2013 中管理組織、網站及集區的封存設定選項</a>。<br />
如果您整合 Lync Server 儲存與 Exchange 2013 儲存，Exchange 使用者原則的優先順序會高於 Lync Server 2013 封存原則，但僅限位於 Exchange 2013 上，將信箱置於就地保留的使用者。</td>
</tr>
</tbody>
</table>


如需關於如何實作原則的詳細資訊，包含原則的階層，請參閱規劃文件、部署文件或作業文件中的[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)。如需關於部署後如何管理原則的詳細資訊，請參閱作業文件中的[在 Lync Server 2013 中管理內部與外部通訊的封存](lync-server-2013-managing-the-archiving-of-internal-and-external-communications.md)。

## 本章節內容

  - [設定封存的全域原則](lync-server-2013-configuring-the-global-policy-for-archiving.md)

  - [設定封存的網站原則](lync-server-2013-setting-up-site-policies-for-archiving.md)

  - [設定使用者的封存原則](lync-server-2013-setting-up-archiving-policies-for-users.md)

