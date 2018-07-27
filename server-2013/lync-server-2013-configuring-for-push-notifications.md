---
title: Lync Server 2013：設定推播通知
TOCTitle: 設定推播通知
ms:assetid: d77f2c06-0fe6-45d5-8f08-808ab871b3e0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690047(v=OCS.15)
ms:contentKeyID: 49292454
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定推播通知

 

_**上次修改主題的時間：** 2013-02-12_

推入通知 (其格式包括徽章、圖示或通知) 可傳送至行動裝置，即使行動應用程式非作用中亦然。推入通知會通知使用者新的或未接的 IM 邀請及語音信箱等事件。 Lync Server 2013 Mobility Service 將通知傳送至雲端架構的 Lync Server 推入通知服務，然後再將通知傳送至 Apple 推入通知服務 (APNS) (適用於執行 Lync 2010 Mobile 用戶端的 Apple 裝置) 或 Microsoft 推入通知服務 (MPNS) (適用於執行 Lync 2010 Mobile 或 Lync 2013 Mobile 用戶端的 Windows Phone 裝置)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您使用具備 Lync 2010 Mobile 或 Lync 2013 Mobile 用戶端的 Windows Phone，推入通知是重要的考量要點。<br />
如果您在 Apple 裝置上使用 Lync 2010 Mobile，推入通知是重要的考量要點。<br />
如果您在 Apple 裝置上使用 Lync 2013 Mobile，您將不再需要推入通知。</td>
</tr>
</tbody>
</table>


請執行下列動作，以設定您的拓撲支援推入通知：

  - 如果您的環境具有 Lync Server 2010 或 Lync Server 2013Edge Server，您必須新增裝載提供者 Microsoft Lync Online，然後設定組織與 Lync Online 之間的裝載提供者同盟。

  - 如果您的環境具有 Office Communications Server 2007 R2Edge Server，您必須設定與 push.lync.com 的直接 SIP 同盟。
    
    > [!NOTE]  
    > Push.lync.com 是推入通知服務的 Microsoft Office 365 網域。
    


  - 若要啟用推入通知，您必須執行 **Set-CsPushNotificationConfiguration** Cmdlet。預設會關閉推入通知。

  - 測試同盟設定和推入通知。

## 設定 Lync Server 2013 或 Lync Server 2010Edge Server 的推入通知

1.  以 RtcUniversalServerAdmins 群組成員的身分登入已安裝 Lync Server 管理命令介面和 Ocscore 的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  新增 Lync Server 線上裝載提供者。在命令列中輸入：
    
        New-CsHostingProvider -Identity <unique identifier for Lync Online hosting provider> -Enabled $True -ProxyFqdn <FQDN for the Access Server used by the hosting provider> -VerificationLevel UseSourceVerification
    
    例如：
    
        New-CsHostingProvider -Identity "LyncOnline" -Enabled $True -ProxyFqdn "sipfed.online.lync.com" -VerificationLevel UseSourceVerification
    
    > [!NOTE]  
    > 您只能與一個裝載提供者有一個同盟關係。換句話說，如果您已設定同盟關係為 sipfed.online.lync.com 的裝載提供者，請勿針對此關係新增其他裝載提供者，即使裝載提供者的身分識別不是 LyncOnline 亦然。
    


4.  設定組織與 Lync Online 推入通知服務之間的裝載提供者同盟。在命令列中輸入：
    
        New-CsAllowedDomain -Identity "push.lync.com"

## 設定 Office Communications Server 2007 R2Edge Server 的推入通知

1.  以 RtcUniversalServerAdmins 群組成員的身分登入 Edge Server。

2.  依序按一下 \[開始\] 、\[所有程式\] 、\[系統管理工具\] 和 \[電腦管理\] 。

3.  在主控台樹狀目錄中，展開 \[服務及應用程式\] ，以滑鼠右鍵按一下 \[Microsoft Office Communications Server 2007 R2\] ，然後按一下 \[內容\] 。

4.  在 \[允許\] 索引標籤上，按一下 \[新增\] 。

5.  在 \[新增同盟協力廠商\] 對話方塊中，執行下列動作：
    
      - 在 \[同盟協力廠商網域名稱\] 中，輸入 **push.lync.com** 。
    
      - 在 \[同盟協力廠商 Access Edge Server\] 中，輸入 **sipfed.online.lync.com**。
    
      - 按一下 \[確定\] 。

## 啟用推入通知

1.  以 CsAdministrator 角色成員的身分登入已安裝 Lync Server 管理命令介面和 Ocscore 的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  啟用推入通知。在命令列中輸入：
    
        Set-CsPushNotificationConfiguration -EnableApplePushNotificationService $True -EnableMicrosoftPushNotificationService $True

4.  啟用同盟。在命令列中輸入：
    
        Set-CsAccessEdgeConfiguration -AllowFederatedUsers $True

## 測試同盟和推入通知

1.  以 CsAdministrator 角色成員的身分登入已安裝 Lync Server 管理命令介面和 Ocscore 的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  測試同盟設定。在命令列中輸入：
    
        Test-CsFederatedPartner -TargetFqdn <FQDN of Access Edge server used for federated SIP traffic> -Domain <FQDN of federated domain> -ProxyFqdn <FQDN of the Access Edge server used by the federated organization>
    
    例如：
    
        Test-CsFederatedPartner -TargetFqdn accessproxy.contoso.com -Domain push.lync.com -ProxyFqdn sipfed.online.lync.com

4.  測試推入通知。在命令列中輸入：
    
        Test-CsMcxPushNotification -AccessEdgeFqdn <Access Edge service FQDN>
    
    例如：
    
        Test-CsMcxPushNotification -AccessEdgeFqdn accessproxy.contoso.com

## 請參閱

#### 其他資源

[Test-CsFederatedPartner](https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsFederatedPartner)  
[Test-CsMcxPushNotification](https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsMcxPushNotification)

