---
title: Lync Server 2013：設定原則以控制公用使用者存取
TOCTitle: 設定原則以控制公用使用者存取
ms:assetid: 090aea0f-ef0b-49da-9c80-02d9279f2fa6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520946(v=OCS.15)
ms:contentKeyID: 49290019
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定原則以控制公用使用者存取

 

_**上次修改主題的時間：** 2013-10-07_

公用立即訊息 (IM) 連線可以讓您組織中的使用者利用 IM 與公用 IM 服務提供者所提供之 IM 服務的使用者進行通訊，IM 服務提供者包括網際網路服務的 Windows Live 網路、Yahoo\! 和 AOL。您可以設定一個或多個外部使用者存取原則以控制公用使用者是否能夠與內部 Lync Server 使用者共同作業。公用立即訊息連線是依賴部署和使用者設定的附加功能。它也需仰賴公用 IM 提供者的服務佈建。如需如何佈建部署來使用公用提供者的詳細資訊，請參閱＜Microsoft Lync Server、Office Communications Server 和 Live Communications Server 的公用 IM 連線佈建指南＞，網址為： <http://go.microsoft.com/fwlink/?linkid=269821>

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
<li><p>自 2012 年 9 月 1 日起，Microsoft Lync 公用 IM 連線使用者訂閱授權 (&quot;PIC USL&quot;) 無法再以新合約或續約的方式購買。持有使用中授權的客戶將可繼續與 Yahoo! Messenger 維持同盟關係直至服務終止日。目前已公佈 AOL 與 Yahoo! 在 2014 年 6 月的結束日期。如需詳細資訊，請參閱 <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Lync Server 2013 中的公用立即訊息連線的支援</a>。</p></li>
<li><p>PIC USL 是針對每位使用者的每月訂閱授權，為 Lync Server 或 Office Communications Server 與 Yahoo! Messenger 同盟的必要授權。Microsoft 是否提供此項服務視 Yahoo! 的支援而定，而此基礎合約將告結束。</p></li>
<li><p>更勝以往，Lync 成為連接全世界組織之間以及個人之間的強大工具。除了 Lync Standard CAL 之外，與 Windows Live Messenger 同盟不需要其他使用者/裝置授權。此清單更將加入 Skype 同盟，讓 Lync 使用者可透過 IM 和語音觸及數億位使用者。</p></li>
</ul></td>
</tr>
</tbody>
</table>


若要存取 Microsoft Lync Server 公用 IM 連線佈建網站，請使用下列連結： <http://go.microsoft.com/fwlink/?linkid=212638>

若要控制公用使用者存取權，您可以在全域、網站和使用者層級設定原則。如需您可以設定之原則類型的詳細資訊，請參閱部署文件或規劃文件中的＜ [在 Lync Server 2013 中設定外部使用者存取支援](lync-server-2013-configuring-support-for-external-user-access.md)＞。 套用到某原則層級的 Lync Server 原則設定，可能會覆寫套用到其他原則層級的設定。Lync Server 原則的優先順序是使用者原則 (影響力最大) 會覆寫網站原則，網站原則則會覆寫全域原則 (影響力最小)。亦即，愈接近原則所影響之物件的原則設定，對物件的影響力愈大。

在 IM 邀請方面，回應將視用戶端軟體而定。除非使用者設定的規則 (亦即，在使用者用戶端的 \[允許\] 和 \[封鎖\] 清單中) 明確封鎖外部傳送者，否則會接受要求。另外，如果使用者已選擇封鎖所有不在其 \[允許\] 清單內的 IM 使用者，IM 邀請也會遭到封鎖。

> [!NOTE]  
> 即便您並未對所屬組織啟用同盟關係，仍可設定原則來控制公用使用者存取。不過，只有當您為組織啟用同盟關係時，所設定的原則才會生效。如需啟用同盟關係的詳細資訊，請參閱部署或作業文件中的＜ <a href="lync-server-2013-enable-or-disable-remote-user-access.md">在 Lync Server 2013 中啟用或停用遠端使用者存取</a>＞。此外，如果您指定使用者原則以控制公用使用者存取，則該原則僅適用已啟用 Lync Server 使用權限且設為使用該原則的使用者。如需指定可以登入 Lync Server 之公用使用者的詳細資訊，請參閱部署或作業文件裡的＜ <a href="lync-server-2013-assign-an-external-user-access-policy-to-a-lync-enabled-user.md">在 Lync Server 2013 中將外部使用者存取原則指派給擁有 Lync 功能的使用者</a>＞。



請使用下列步驟來設定原則，以支援一個或多個公用 IM 提供者的使用者存取。

## 設定外部存取原則以支援公用使用者存取

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[外部使用者存取\]** 、 **\[外部存取原則\]** 。

4.  在 **\[外部存取原則\]** 頁面中，執行下列其中一項：
    
      - 若要設定全域原則以支援公用使用者存取，依序按一下全域原則、\[編輯\] 和 \[顯示詳細資料\] 。
    
      - 若要建立新的網站原則，請按一下 **\[新增\]** ，然後按一下 **\[站台原則\]** 。在 **\[選取網站\]** 的清單中按一下適當網站，然後按一下 **\[確定\]** 。
    
      - 若要建立新的使用者原則，按一下 \[新增\] ，再按一下 \[使用者原則\] 。在 \[新的外部存取原則\] 中，於 \[名稱\] 欄位中建立唯一名稱以代表使用者原則的涵蓋範圍 (例如，建立 **EnablePublicUsers** 的使用者原則以啟用公用使用者的通訊功能)。
    
      - 若要變更現有原則，按一下表中所列之適當原則，然後按一下 **\[編輯\]** ，接著按一下 **\[顯示詳細資料\]** 。

5.  (選用) 如果您想要新增或編輯描述，請在 **\[描述\]** 中指定原則資訊。

6.  執行下列其中一項作業：
    
      - 若要啟用原則的公用使用者存取功能，請選取 \[啟用與公用使用者的通訊\] 核取方塊。
    
      - 若要停用原則的公用使用者存取功能，請清除 \[啟用與公用使用者的通訊\] 核取方塊。

7.  按一下 \[認可\] 。

若要啟用公用使用者存取功能，您也必須對組織中的同盟關係啟用支援。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中設定控制同盟使用者存取的原則](lync-server-2013-configure-policies-to-control-federated-user-access.md)＞。

如果這是使用者原則，您也必須將該原則套用至您希望能夠與公用使用者共同作業的公用使用者。如需詳細資訊，請參閱＜ [指派每位使用者的原則](lync-server-2013-assigning-per-user-policies.md)＞。

## 請參閱

#### 工作

[在 Lync Server 2013 中建立或編輯公用 SIP 同盟提供者](lync-server-2013-create-or-edit-public-sip-federated-providers.md)  

#### 其他資源

[在 Lync Server 2013 中管理組織的 SIP 同盟提供者](lync-server-2013-manage-sip-federated-providers-for-your-organization.md)

