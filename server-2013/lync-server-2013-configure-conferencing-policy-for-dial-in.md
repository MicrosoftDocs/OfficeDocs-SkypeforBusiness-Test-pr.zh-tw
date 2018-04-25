---
title: Lync Server 2013：設定電話撥入式會議的會議原則
TOCTitle: 設定電話撥入式會議的會議原則
ms:assetid: 9bf926d6-0248-4352-98c3-9c5a333debbc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398810(v=OCS.15)
ms:contentKeyID: 49291799
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定電話撥入式會議的會議原則

 

_**上次修改主題的時間：** 2014-03-21_

會議原則是指定參與者之會議經驗的使用者帳戶設定。您可以建立網站範圍或使用者範圍的會議原則。會議原則設定涉及許多會議排程和參與方面的事宜。支援參與者參加電話撥入式會議的會議原則設定有數種。因此在設定電話撥入式會議時，您應驗證這些欄位的設定是否適合您的組織，並根據需求加以修改。

請驗證會議原則中的下列欄位：

  - **允許參與者邀請匿名使用者**    這項設定可允許會議召集人邀請匿名 (即未經過驗證) 參與者參加會議。這項設定是電話撥入式會議的選用設定。在預設的全域會議原則中，此設定是預設選取的設定。

  - **啟用 PSTN 電話撥入式會議**    這項設定可允許使用者從 PSTN 利用電話撥號的方式加入會議的音訊部分。這項設定是電話撥入式會議的必要設定。在預設的全域會議原則中，此設定是預設選取的設定。

  - **允許匿名參與者撥出**    這項設定可允許已加入會議的匿名使用者撥出電話號碼來加入會議的音訊部分。這項設定是電話撥入式會議的選用設定。在預設的全域會議原則中，此設定不是預設選取的設定。

  - **允許未啟用 企業語音的參與者撥出**    此設定允許未啟用 企業語音的會議參與者和召集人撥出電話號碼以加入會議的音訊部分。撥出通話是根據召集人被指派的語音原則來授權。在預設的全域會議原則中，此設定不是預設選取的設定。此設定的預設值為停用。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若要啟用此功能，未啟用企業語音的會議召集人應已被指派適當的語音原則，以便授權在該使用者召集的會議進行任何撥出。您可以使用 Lync Server 管理命令介面將語音原則指派給未啟用企業語音的使用者。如果使用者沒有被明確指派語音原則，則會使用站台語音原則來授權撥出要求。如果未有站台語音原則，則會使用全域語音原則。</td>
    </tr>
    </tbody>
    </table>


本節的程序說明如何修改會議原則。如需如何設定預設會議原則中各項參與者體驗設定的詳細資訊，請參閱＜ [建立或修改會議的組態設定集合](lync-server-2013-create-or-modify-a-collection-of-meeting-configuration-settings.md)＞。如需如何為特定使用者或使用者群組建立會議原則的詳細資訊，請參閱＜ [在 Lync Server 2013 中建立或修改會議原則](lync-server-2013-create-or-modify-a-conferencing-policy.md)＞。如需所有可用會議原則設定的清單，請參閱＜ [Lync Server 2013 中的會議原則設定參考](lync-server-2013-conferencing-policy-settings-reference.md)＞。

## 若要修改電話撥入式會議的會議原則

1.  以 RTCUniversalServerAdmins 群組成員或 **Cs-ServerAdministrator** 、 **CsAdministrator** 角色成員的身分登入電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[會議\]。

4.  在 **\[會議原則\]** 索引標籤中，按兩下會議原則名稱以開啟 **\[編輯會議原則\]** 對話方塊。

5.  驗證電話撥入式會議的欄位是否適合您的組織，並根據需求修改設定。

6.  按一下 \[認可\] 。

