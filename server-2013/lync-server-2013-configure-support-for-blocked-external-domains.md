---
title: Lync Server 2013：為封鎖的外部網域設定支援
TOCTitle: 為封鎖的外部網域設定支援
ms:assetid: 49103138-e1ab-42bf-91aa-57cf23bbf260
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ619176(v=OCS.15)
ms:contentKeyID: 49290812
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中為封鎖的外部網域設定支援

 

_**上次修改主題的時間：** 2012-09-08_

如果您已設定同盟協力廠商的支援，可以管理要禁止哪些網域與您的組織建立同盟。如果您啟用此選項，封鎖網域清單將作為封鎖清單 (不被允許的明確項目清單)，並套用於同盟網域探索中。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中啟用或停用探索同盟協力廠商](lync-server-2013-enable-or-disable-discovery-of-federation-partners.md)＞。

封鎖一個或多個外部網域，不讓它們連線至您的組織。若要這樣做，請將網域新增至封鎖網域清單。

## 將外部網域新增至封鎖網域清單

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[外部使用者存取\]** 。

4.  依序按一下 **\[同盟網域\]** 、 **\[新增\]** 和 **\[封鎖網域\]** 。

5.  在 **\[新增同盟網域\]** 中，執行下列動作：
    
      - 在 **\[網域名稱 (或 FQDN)\]** 中，輸入您要封鎖的同盟協力廠商網域名稱。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>名稱長度不可超過 256 個字元。<br />
        搜尋同盟協力廠商網域名稱時會執行尾碼比對。例如，如果輸入 <strong>contoso.com</strong> ，搜尋也會傳回網域 <strong>it.contoso.com</strong> 。<br />
        不能同時封鎖又允許同一個同盟協力廠商網域。 Lync Server 2013 會防止這種狀況發生，所以您不必讓清單維持同步。</td>
        </tr>
        </tbody>
        </table>
    
      - (選用) 在 **\[註解\]** 中，輸入您想與其他系統管理員分享的此設定相關資訊。

6.  按一下 \[認可\] 。

7.  為您要封鎖的每個同盟協力廠商重複步驟 4 到 6。

若要啟用同盟使用者存取，您也必須在組織中啟用同盟使用者存取支援。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中啟用或停用遠端使用者存取](lync-server-2013-enable-or-disable-remote-user-access.md)＞。

此外，您還必須設定原則，並將原則套用至您希望能與同盟使用者共同作業的使用者。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中設定控制同盟使用者存取的原則](lync-server-2013-configure-policies-to-control-federated-user-access.md)＞。

