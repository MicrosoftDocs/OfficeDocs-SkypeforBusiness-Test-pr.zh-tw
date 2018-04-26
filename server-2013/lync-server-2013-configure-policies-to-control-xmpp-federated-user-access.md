---
title: Lync Server 2013：設定原則以控制 XMPP 同盟使用者存取
TOCTitle: 設定原則以控制 XMPP 同盟使用者存取
ms:assetid: 0fe0ff75-e52a-4e3e-923a-64f6412ac4e4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ552446(v=OCS.15)
ms:contentKeyID: 49290113
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定原則以控制 XMPP 同盟使用者存取

 

_**上次修改主題的時間：** 2012-11-01_

此為初稿文件，可能隨時變更。空白主題是內容的預留位置。

當您設定支援可延伸訊息和目前狀態通訊協定 (XMPP) 同盟協力廠商的原則時，這些原則會套用至 XMPP 同盟網域的使用者，但不會套用至工作階段初始通訊協定 (SIP) 立即訊息 (IM) 服務提供者 (例如 Windows Live) 或 SIP 同盟網域的使用者。請針對您要讓使用者新增連絡人或進行通訊的每個 XMPP 同盟網域，各設定一個 **XMPP 同盟協力廠商**。XMPP 同盟協力廠商原則只能用在單一範圍，雖然不是定義為全域原則，但作用是全域原則。若要為 XMPP 同盟協力廠商定義全域、網站或使用者原則，請先針對您需要的範圍建立及設定外部存取原則，以設定原則範圍。如需您可以為外部存取和同盟設定之原則類型的詳細資訊，請參閱操作文件中的＜ [管理 Lync Server 2013 的同盟與外部存取](lync-server-2013-managing-federation-and-external-access-to-lync-server-2013.md)＞。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>所有 <strong>同盟和外部存取</strong>原則都是透過頻內佈建來套用。您套用至使用者、屬於網站或是全域範圍的原則，都會在登入期間傳送至用戶端。您可以設定原則來控制 XMPP 同盟協力廠商存取，即使您尚未為組織啟用 XMPP 同盟也一樣。不過，您必須已經為組織部署、啟用及設定 XMPP 協力廠商同盟，您設定的原則才會生效。如需部署及設定 XMPP 協力廠商同盟的詳細資訊，請參閱部署文件中的＜ <a href="lync-server-2013-configuring-sip-federation-xmpp-federation-and-public-instant-messaging.md">在 Lync Server 2013 中設定 SIP 同盟、XMPP 同盟及 Public Instant Messaging</a>＞。此外，如果您在外部存取原則中指定使用者原則，以控制 XMPP 同盟協力廠商，該原則只會套用至已啟用 Lync Server 2013 並設定為使用該原則的使用者。</td>
</tr>
</tbody>
</table>


## 為 XMPP 同盟協力廠商編輯全域原則

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[外部使用者存取\]** 、 **\[外部存取原則\]** 。

4.  在「外部存取原則」 頁面上，針對全域原則執行下列動作：

5.  按一下全域原則，按一下 \[編輯\] ，然後按一下 \[顯示詳細資料\]。

6.  提供全域原則的說明 (選用)。

7.  選取 \[啟用與同盟使用者的通訊\] 。

8.  選取 \[啟用與XMPP 同盟使用者的通訊\] 。

9.  按一下 \[認可\] 以儲存對全域原則的變更。

## 為 XMPP 同盟協力廠商建立網站或使用者原則

1.  按一下 \[新增\] ，然後按一下 \[站台原則\] 或 \[使用者原則\] 。在 \[選取站台\] 的清單中按一下適當網站，然後按一下 \[確定\] 。

2.  提供網站原則的說明 (選用)。

3.  在網站或使用者原則中，選取 \[啟用與同盟使用者的通訊\] 。

4.  選取 \[啟用與XMPP 同盟使用者的通訊\] 。

5.  按一下 \[認可\] 將變更儲存至網站或使用者原則。

## 為 XMPP 同盟協力廠商編輯現有的原則

1.  若要變更現有原則，請在清單中選取適當的原則，然後按一下 \[編輯\] ，再按一下 \[顯示詳細資料\] 。

2.  變更或更新原則的說明 (選用)。

3.  選取或取消選取 \[啟用與同盟使用者的通訊\] 。

4.  選取或取消選取 \[啟用與 XMPP 同盟使用者的通訊\] 。

5.  按一下 \[認可\] 以儲存對原則的變更。

## 使用 Windows PowerShell 為 XMPP 同盟協力廠商編輯現有的原則

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  在 Lync Server 管理命令介面中輸入下列資訊：
    
        Set-CsExternalAccessPolicy -Identity <name of global, site or user policy - policy must exist when using Set-CsExternalAccessPolicy > -Description <descriptive name for policy> -EnableFederationAccess <$true, $false> -EnableXmppAccess <$true, $false>
    
    下列範例命令會將同盟使用者存取權的全域原則設為 True (已啟用)，並將 XMPP 網域存取權設為 True (已啟用)：
    
        Set-CsExternalAccessPolicy -Identity global -EnableFederationAccess $true -EnableXmppAccess $true

## 使用 Windows PowerShell 為 XMPP 同盟協力廠商建立網站或使用者原則

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  在 Lync Server 管理命令介面中輸入下列資訊：
    
        New-CsExternalAccessPolicy -Identity <name of global, site or user policy - policy must exist when using Set-CsExternalAccessPolicy > -Description <descriptive name for policy> -EnableFederationAccess <$true, $false> -EnableXmppAccess <$true, $false>
    
    下列範例命令會將同盟使用者存取權之 Redmond 網站的網站原則設為已啟用，並將 XMPP 網域存取權設為已啟用：
    
        New-CsExternalAccessPolicy -Identity site:Redmond -EnableFederationAccess $true -EnableXmppAccess $true

## 使用 Windows PowerShell 為 XMPP 同盟協力廠商刪除現有的原則

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  在 Lync Server 管理命令介面中輸入下列資訊：
    
        Remove-CsExternalAccessPolicy -Identity <name of global, site or user policy>
    
    下列範例命令會刪除使用者原則：
    
        Remove-CsExternalAccessPolicy -Identity EAPUserPolicySetXMPP

4.  下列範例命令會將全域原則重設為預設值：
    
        Remove-CsExternalAccessPolicy -Identity global

## 請參閱

#### 工作

[在 Lync Server 2013 中將外部使用者存取原則指派給擁有 Lync 功能的使用者](lync-server-2013-assign-an-external-user-access-policy-to-a-lync-enabled-user.md)  
[在 Lync Server 2013 中啟用或停用同盟與公用 IM 連線](lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md)  

#### 其他資源

[在 Lync Server 2013 中管理 XMPP 同盟夥伴](lync-server-2013-manage-xmpp-federated-partners-for-your-organization.md)  
[Set-CsExternalAccessPolicy](set-csexternalaccesspolicy.md)  
[New-CsExternalAccessPolicy](new-csexternalaccesspolicy.md)  
[Get-CsExternalAccessPolicy](get-csexternalaccesspolicy.md)  
[Remove-CsExternalAccessPolicy](remove-csexternalaccesspolicy.md)  
[Grant-CsExternalAccessPolicy](grant-csexternalaccesspolicy.md)

