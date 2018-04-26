---
title: Lync Server 2013：為遠端呼叫控制設定信任的應用程式項目
TOCTitle: 為遠端呼叫控制設定信任的應用程式項目
ms:assetid: 37777f93-8b24-40cf-808e-7c6230eb2132
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558636(v=OCS.15)
ms:contentKeyID: 49290593
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中為遠端呼叫控制設定信任的應用程式項目

 

_**上次修改主題的時間：** 2012-10-22_

SIP/CSTA 閘道必須設定作為信任的應用程式， Lync Server 才能套用靜態路由以將通話路由至該閘道。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您是從舊版的 Lync Server 部署移轉使用者，請確定已先移除所有為 SIP/CSTA 閘道建立的現有受信任應用程式項目 (舊稱為授權主機項目)，再執行本主題中的程序。如需詳細資訊，請參閱＜ <a href="lync-server-2013-remove-a-legacy-authorized-host-optional.md">在 Lync Server 2013 中移除舊版授權主機 (選用)</a>＞。</td>
</tr>
</tbody>
</table>


## 若要設定 SIP/CSTA 閘道的受信任應用程式項目

1.  以 RTCUniversalServerAdmins 群組成員身分，或您已將 **New-CsTrustedApplicationPool** Cmdlet 指派給的角色型存取控制 (RBAC) 角色，登入已安裝 Lync Server 管理命令介面的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  若要建立受信任應用程式項目，請執行下列其中一項作業：
    
      - 若是傳輸層安全性 (TLS) 連線，請在命令提示字元中輸入下列命令：
        
            New-CsTrustedApplicationPool -Identity <FQDN of the SIP/CSTA gateway> [-Registrar <Service ID or FQDN of the Registrar service>] -Site <Site ID for the site where you want to create the trusted application pool>
        
        例如：
        
            New-CsTrustedApplicationPool -Identity rccgateway.contoso.net -Registrar registrar1.contoso.net -Site co1 -TreatAsAuthenticated $true -ThrottleAsServer $true
    
      - 若是傳輸控制通訊協定 (TCP) 連線，請在命令提示字元中輸入下列命令：
        
            New-CsTrustedApplicationPool -Identity <IP address or FQDN of the SIP/CSTA gateway> [-Registrar <Service ID or FQDN of the Registrar service>] -Site <Site ID for the site where you want to create the trusted application pool>
        
        例如：
        
            New-CsTrustedApplicationPool -Identity 192.168.0.240 -Registrar registrar1.contoso.net -Site co1 -TreatAsAuthenticated $true -ThrottleAsServer $true

4.  若要將受信任應用程式新增至集區，請執行下列其中一項作業：
    
      - 若是 TLS 連線，請在命令提示字元中輸入下列命令：
        
            New-CsTrustedApplication -ApplicationID <application name> -TrustedApplicationPoolFqdn <FQDN of the SIP/CSTA gateway> -Port <SIP listening port on the gateway>
        
        例如：
        
            New-CsTrustedApplication -ApplicationID RccGateway-1 -TrustedApplicationPoolFqdn rccgateway.contoso.net -Port 5065
    
      - 若是 TCP 連線，請在命令提示字元中輸入下列命令：
        
            New-CsTrustedApplication -ApplicationID <application name> -TrustedApplicationPoolFqdn <IP address or FQDN of the SIP/CSTA gateway> -Port <SIP listening port on the gateway> -EnableTcp
        
        例如：
        
            New-CsTrustedApplication -ApplicationID RccGateway-1 -TrustedApplicationPoolFqdn 192.169.0.240 -Port 5065 -EnableTcp

5.  若要實作您已發行的拓撲變更，請在命令提示字元中輸入下列命令：
    
        Enable-CsTopology

## 請參閱

#### 工作

[在 Lync Server 2013 中設定遠端呼叫控制的靜態路由](lync-server-2013-configure-a-static-route-for-remote-call-control.md)  
[在 Lync Server 2013 中定義 SIP/CSTA 閘道 IP 位址](lync-server-2013-define-a-sip-csta-gateway-ip-address.md)

