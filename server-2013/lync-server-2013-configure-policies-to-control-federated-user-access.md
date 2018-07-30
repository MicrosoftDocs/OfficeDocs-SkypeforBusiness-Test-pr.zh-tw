---
title: Lync Server 2013：設定控制同盟使用者存取的原則
TOCTitle: 設定控制同盟使用者存取的原則
ms:assetid: 5485e208-81e4-4e59-9aeb-1232c11dd8a2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398359(v=OCS.15)
ms:contentKeyID: 49290939
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定控制同盟使用者存取的原則

 

_**上次修改主題的時間：** 2014-02-05_

當您設定原則以支援與同盟協力廠商的通訊時，這些原則會套用至同盟網域的使用者。您可以設定一或多個外部使用者存取原則，以控制同盟網域的使用者是否能夠與您的 Lync Server 2013 使用者共同作業。若要控制同盟使用者存取，請在全域、網站與使用者層級設定相關原則。 套用到某原則層級的 Lync Server 原則設定，可能會覆寫套用到其他原則層級的設定。Lync Server 原則的優先順序是使用者原則 (影響力最大) 會覆寫網站原則，網站原則則會覆寫全域原則 (影響力最小)。亦即，愈接近原則所影響之物件的原則設定，對物件的影響力愈大。

> [!NOTE]  
> 即便您並未對所屬組織啟用同盟，仍舊可以設定原則來控制同盟使用者存取。不過，只有當您為組織啟用同盟時，所設定的原則才會生效。如需有關啟用同盟的詳細資訊，請參閱部署文件或作業文件中的 <a href="lync-server-2013-enable-or-disable-remote-user-access.md">在 Lync Server 2013 中啟用或停用遠端使用者存取</a>。此外，如果您指定使用者原則以控制同盟使用者存取，則該原則僅會套用至已啟用 Lync Server 2013 且設為使用該原則的使用者。



## 若要設定原則以支援同盟網域使用者存取

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[外部使用者存取\]** 、 **\[外部存取原則\]** 。

4.  在 **\[外部存取原則\]** 頁面中，執行下列其中一項：
    
      - 若要設定全域原則以支援同盟使用者存取，依序按一下全域原則、 **\[編輯\]** 以及 **\[顯示詳細資料\]** 。
    
      - 若要建立新的網站原則，請按一下 **\[新增\]** ，然後按一下 **\[站台原則\]** 。在 **\[選取網站\]** 的清單中按一下適當網站，然後按一下 **\[確定\]** 。
    
      - 若要建立新的使用者原則，按一下 **\[新增\]** ，再按一下 **\[使用者原則\]** 。在 **\[新的外部存取原則\]** 中，於 **\[名稱\]** 欄位中建立唯一名稱以代表使用者原則的涵蓋範圍 (例如，建立 **EnableFederatedUsers** 的使用者原則以啟用同盟網域使用者的通訊功能)。
    
      - 若要變更現有原則，按一下表中所列之適當原則，然後按一下 **\[編輯\]** ，接著按一下 **\[顯示詳細資料\]** 。

5.  (選用) 如果您想要新增或編輯描述，請在 **\[描述\]** 中指定原則資訊。

6.  執行下列其中一項作業：
    
      - 若要啟用原則的同盟使用者存取功能，請選取 **\[啟用與同盟使用者的通訊\]** 核取方塊。
    
      - 若要停用原則的同盟使用者存取功能，請清除 **\[啟用與同盟使用者的通訊\]** 核取方塊。

7.  按一下 \[認可\] 。

若要啟用同盟使用者存取，您也必須在組織中啟用同盟支援。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中啟用或停用同盟與公用 IM 連線](lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md)＞。

如果這是使用者原則，則您也必須將該原則套用至您希望能與同盟使用者共同作業的使用者。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中將外部使用者存取原則指派給擁有 Lync 功能的使用者](lync-server-2013-assign-an-external-user-access-policy-to-a-lync-enabled-user.md)＞。

## 使用 Windows PowerShell 設定現有原則以支援同盟網域使用者的存取

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  在 Lync Server 管理命令介面中輸入下列資訊：
    
        Set-CsExternalAccessPolicy -Identity <name of global, site or user policy - policy must exist when using Set-CsExternalAccessPolicy > -Description <descriptive name for policy> -EnableFederationAccess <$true, $false> -EnableXmppAccess <$true, $false> -EnablePublicCloudAcess <$true, $false> -EnablePublicCloudAudioVideoAcess <$true, $false> -EnableOutsideAcess <$true, $false>
    
    一個命令範例，會將適用於同盟使用者存取的全域原則設定為啟用、將 XMPP 網域存取設定為啟用、將遠端使用者存取設定為啟用、將公用提供者存取設定為啟用，以及為支援它的公用提供者授與使用音訊和視訊的能力：
    
        Set-CsExternalAccessPolicy -Identity global -EnableFederationAccess $true -EnableXmppAccess $true -EnableOutsideAccess $true -EnablePublicCloudAccess $true -EnablePublicCloudAudioVideoAccess $true
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>參數「EnablePublicCloudAudioVideoAccess」在 Lync Server 控制台 中沒有對應的選取項目</td>
    </tr>
    </tbody>
    </table>


## 使用 Windows PowerShell 建立新原則以支援適用於同盟網域使用者的存取

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  在 Lync Server 管理命令介面中輸入下列資訊：
    
        New-CsExtenalAccessPolicy -Identity <name of site or user policy - you cannot create a new global policy using New-CsExternalAccessPolicy > -Description <descriptive name for policy> -EnableFederationAccess <$true, $false> -EnableXmppAccess <$true, $false> -EnablePublicCloudAccess <$true, $false> -EnablePublicCloudAudioVideoAccess <$true, $false> -EnableOutsideAccess <$true, $false>
    
    建立新網站原則的範例：
    
        New-CsExternalAccessPolicy -Identity site:Redmond -EnableFederationAccess $true -EnableXmppAccess $true -EnableOutsideAccess $true -EnablePublicCloudAccess $true -EnablePublicCloudAudioVideoAccess $true

## 使用 Windows PowerShell 刪除或重設原則以支援適用於同盟網域使用者的存取

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  在 Lync Server 管理命令介面中輸入下列資訊：
    
        Remove-CsExternalAccessPolicy -Identity <name of global, site or user policy> 
    
    重設全域原則的範例 (全域原則只能移除它的設定。無法刪除原則)：
    
        Remove-CsExternalAccessPolicy -Identity global 
    
    若要移除網站原則，請輸入：
    
        Remove-CsExternalAccessPolicy -Identity site:Redmond 
    
    刪除網站原則 Redmond。若要刪除名為 UserEAPPolicy 的使用者原則，請輸入：
    
        Remove-CsExternalAccessPolicy -Identity UserEAPPolicy

## 請參閱

#### 工作

[在 Lync Server 2013 中啟用或停用同盟與公用 IM 連線](lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md)  
[在 Lync Server 2013 中將外部使用者存取原則指派給擁有 Lync 功能的使用者](lync-server-2013-assign-an-external-user-access-policy-to-a-lync-enabled-user.md)  

#### 其他資源

[在 Lync Server 2013 中管理組織的 SIP 同盟網域](lync-server-2013-manage-sip-federated-domains-for-your-organization.md)  
[在 Lync Server 2013 中管理組織的 SIP 同盟提供者](lync-server-2013-manage-sip-federated-providers-for-your-organization.md)  
[Set-CsExternalAccessPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsExternalAccessPolicy)  
[New-CsExternalAccessPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsExternalAccessPolicy)  
[Get-CsExternalAccessPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsExternalAccessPolicy)  
[Remove-CsExternalAccessPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsExternalAccessPolicy)  
[Grant-CsExternalAccessPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Grant-CsExternalAccessPolicy)

