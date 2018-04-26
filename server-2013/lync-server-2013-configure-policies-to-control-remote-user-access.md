---
title: Lync Server 2013：設定原則以控制遠端使用者存取
TOCTitle: 設定原則以控制遠端使用者存取
ms:assetid: 8f556849-692b-44a0-9514-4468fc9a39d0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398725(v=OCS.15)
ms:contentKeyID: 49291646
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定原則以控制遠端使用者存取

 

_**上次修改主題的時間：** 2012-10-18_

您可以設定一或多個外部使用者存取原則，來控制遠端使用者是否能與內部 Lync Server 使用者共同作業。若要控制遠端使用者存取權，您可以設定全域、網站和使用者層級的原則。網站原則可覆寫全域原則，而使用者原則可覆寫網站和全域原則。如需關於可設定之原則類型的詳細資訊，請參閱＜ [管理 Lync Server 2013 的同盟與外部存取](lync-server-2013-managing-federation-and-external-access-to-lync-server-2013.md)＞。 套用到某原則層級的 Lync Server 原則設定，可能會覆寫套用到其他原則層級的設定。Lync Server 原則的優先順序是使用者原則 (影響力最大) 會覆寫網站原則，網站原則則會覆寫全域原則 (影響力最小)。亦即，愈接近原則所影響之物件的原則設定，對物件的影響力愈大。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>即便您並未對所屬組織啟用遠端使用者存取，仍舊可以設定相關原則來控制遠端使用者存取。但是，唯有在組織啟用遠端使用者存取時，您設定的原則才會生效。如需關於啟用遠端使用者存取的詳細資訊，請參閱＜ <a href="lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md">在 Lync Server 2013 中啟用或停用同盟與公用 IM 連線</a>＞。此外，如果您指定使用者原則來控制遠端使用者存取，則該原則僅適用已啟用 Lync Server 且設為使用該原則的使用者。如需關於指定可從遠端位置登入 Lync Server 之使用者的詳細資訊，請參閱＜ <a href="lync-server-2013-assign-an-external-user-access-policy-to-a-lync-enabled-user.md">在 Lync Server 2013 中將外部使用者存取原則指派給擁有 Lync 功能的使用者</a>＞。</td>
</tr>
</tbody>
</table>


請遵循以下程序來設定每個要用來控制遠端使用者存取的外部存取原則。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此程序只會說明如何設定原則以允許與遠端使用者通訊，不過，每個設定來支援遠端使用者存取的原則亦可設定同盟使用者存取和公用使用者存取。如需關於設定原則以支援同盟使用者的詳細資訊，請參閱＜ <a href="lync-server-2013-configure-policies-to-control-federated-user-access.md">在 Lync Server 2013 中設定控制同盟使用者存取的原則</a>＞。如需設定原則以支援公用使用者的詳細資訊，請參閱＜ <a href="lync-server-2013-create-or-edit-public-sip-federated-providers.md">在 Lync Server 2013 中建立或編輯公用 SIP 同盟提供者</a>＞。</td>
</tr>
</tbody>
</table>


## 若要設定外部存取原則以支援遠端使用者存取

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[外部使用者存取\]** 、 **\[外部存取原則\]** 。

4.  在 **\[外部存取原則\]** 頁面中，執行下列其中一項：
    
      - 若要設定全域原則支援遠端使用者存取，請依序按一下全域原則、 **\[編輯\]** 和 **\[顯示詳細資料\]** 。
    
      - 若要建立新的網站原則，請按一下 **\[新增\]** ，然後按一下 **\[站台原則\]** 。在 **\[選取網站\]** 的清單中按一下適當網站，然後按一下 **\[確定\]** 。
    
      - 若要建立新的使用者原則，按一下 **\[新增\]** ，再按一下 **\[使用者原則\]** 。在 **\[新的外部存取原則\]** 中，於 **\[名稱\]** 欄位中建立唯一名稱以代表使用者原則的涵蓋範圍 (例如，建立 **EnableRemoteUsers** 的使用者原則以啟用遠端使用者的通訊功能)。
    
      - 若要變更現有原則，按一下表中所列之適當原則，然後按一下 **\[編輯\]** ，接著按一下 **\[顯示詳細資料\]** 。

5.  (選用) 如果您想要新增或編輯描述，請在 **\[描述\]** 中指定原則資訊。

6.  執行下列其中一項作業：
    
      - 若要啟用原則的遠端使用者存取，請選取 **\[啟用與遠端使用者的通訊\]** 核取方塊。
    
      - 若要停用原則的遠端使用者存取，請清除 **\[啟用與遠端使用者的通訊\]** 核取方塊。

7.  按一下 \[認可\] 。

若要啟用遠端使用者存取，您還必須在組織中啟用遠端使用者存取支援。如需詳細資訊，請參閱部署文件或作業文件中的 [在 Lync Server 2013 中啟用或停用同盟與公用 IM 連線](lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md)。

如果這是使用者原則，則您必須同時將該原則套用至您要從遠端連接的使用者。如需詳細資訊，請參閱部署與作業文件中的 [在 Lync Server 2013 中將外部使用者存取原則指派給擁有 Lync 功能的使用者](lync-server-2013-assign-an-external-user-access-policy-to-a-lync-enabled-user.md)。

