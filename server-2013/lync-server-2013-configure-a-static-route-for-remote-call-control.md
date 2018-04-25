---
title: Lync Server 2013：設定遠端呼叫控制的靜態路由
TOCTitle: 設定遠端呼叫控制的靜態路由
ms:assetid: f7003023-443d-48ee-989b-71e8b0b0abbd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615051(v=OCS.15)
ms:contentKeyID: 49292845
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定遠端呼叫控制的靜態路由

 

_**上次修改主題的時間：** 2012-09-22_

遠端呼叫控制需要每個 Lync Server 集區都設定了從該集區到 SIP/CSTA 閘道 (該閘道連接到專用交換機 (PBX)) 的路徑。此路徑需要各集區都有一個靜態路由用於每個閘道，集區會將與傳送至 PBX 之通話相關聯的 SIP 呼叫控制訊息 Proxy 至閘道。如果您為遠端呼叫控制設定了全域靜態路由，則未在集區層級設定靜態路由的集區將會使用全域靜態路由。

## 若要為遠端呼叫控制設定靜態路由

1.  以 RTCUniversalServerAdmins 群組成員的身分，或是已對其指派 **New-CsStaticRoute** Cmdlet 的角色存取控制 (RBAC) 角色，登入已安裝 Lync Server 管理命令介面的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  若要建立靜態路由並將它放在變數 $TLSRoute 或 $TCPRoute 中，請執行下列其中一項：
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若要比對網域的子網域，您可以在 MatchUri 參數中指定萬用字元值。例如， <strong>*.contoso.net</strong> 。該值會比對結尾尾碼為 <strong>contoso.net</strong> 的所有網域。</td>
    </tr>
    </tbody>
    </table>
    
      - 若是傳輸層安全性 (TLS) 連線，請在命令提示字元中輸入下列命令：
        
            $TLSRoute = New-CsStaticRoute -TLSRoute -Destination <gateway FQDN> -Port <gateway SIP listening port> -UseDefaultCertificate $true -MatchUri <destination domain>
        
        例如：
        
            $TLSRoute = New-CsStaticRoute -TLSRoute -Destination rccgateway.contoso.net -Port 5065 -UseDefaultCertificate $true -MatchUri *.contoso.net
        
        如果 UseDefaultCertificate 設為 False，您必須指定 TLSCertIssuer 和 TLSCertSerialNumber 參數。這些參數分別指出核發靜態路由所用憑證的憑證授權單位 (CA) 名稱，以及 TLS 憑證的序號。如需這些參數的詳細資訊，請在命令提示字元下輸入下列命令以參閱 Lync Server 管理命令介面說明：
        
            Get-Help New-CsStaticRoute -Full
    
      - 若是傳輸控制通訊協定 (TCP) 連線，請在命令提示字元中輸入下列命令：
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>如果您要指定完整網域名稱 (FQDN)，必須先設定網域名稱系統 (DNS) A 記錄。</td>
        </tr>
        </tbody>
        </table>
        
            $TCPRoute = New-CsStaticRoute -TCPRoute -Destination <gateway IP address or FQDN> -Port <gateway SIP listening port> -MatchUri <destination domain>
        
        例如：
        
            $TCPRoute = New-CsStaticRoute -TCPRoute -Destination 192.168.0.240 -Port 5065 -MatchUri *.contoso.net
        
        以下是靜態路由之選用參數的預設值：
        
          - Enabled = True
        
          - MatchOnlyPhoneUri = False
        
          - ReplaceHostInRequestUri = False
        
        強烈建議您不要變更這些預設值。不過，如果您必須變更任何這些參數，請在命令提示字元下輸入下列命令以參閱 Lync Server 管理命令介面說明：
        
            Get-Help New-CsStaticRoute -Full

4.  若要將新建立的靜態路由保存在 中央管理存放區中，請視需要執行下列其中一項：
    
        Set-CsStaticRoutingConfiguration -Route @{Add=$TLSRoute}
    
        Set-CsStaticRoutingConfiguration -Route @{Add=$TCPRoute}

## 請參閱

#### 工作

[在 Lync Server 2013 中為遠端呼叫控制設定信任的應用程式項目](lync-server-2013-configure-a-trusted-application-entry-for-remote-call-control.md)  
[在 Lync Server 2013 中定義 SIP/CSTA 閘道 IP 位址](lync-server-2013-define-a-sip-csta-gateway-ip-address.md)

