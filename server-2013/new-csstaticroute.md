---
title: New-CsStaticRoute
TOCTitle: New-CsStaticRoute
ms:assetid: 1df0c537-f24f-4a63-be6d-70d016f985a5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398265(v=OCS.15)
ms:contentKeyID: 49290276
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsStaticRoute

 

_**上次修改主題的時間：** 2015-03-09_

建立新的靜態電話路由。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsStaticRoute -Destination <String> -MatchUri <String> -Port <UInt16> -TLSRoute <SwitchParameter> [-Enabled <$true | $false>] [-MatchOnlyPhoneUri <$true | $false>] [-ReplaceHostInRequestUri <$true | $false>] [-TLSCertIssuer <String>] [-TLSCertSerialNumber <Byte[]>] [-UseDefaultCertificate <$true | $false>] <COMMON PARAMETERS>

    New-CsStaticRoute -Destination <String> -MatchUri <String> -Port <UInt16> -TCPRoute <SwitchParameter> [-Enabled <$true | $false>] [-MatchOnlyPhoneUri <$true | $false>] [-ReplaceHostInRequestUri <$true | $false>] <COMMON PARAMETERS>

    COMMON PARAMETERS:

## 範例

## 範例 1

範例 1 所示的命令會建立新的靜態路由，然後將該路由新增至通用靜態路由組態集合。為了執行此工作，第一個命令會使用 **New-CsStaticRoute** Cmdlet 建立僅存於記憶體中的路由，此路由會使用 TCP 做為其傳輸通訊協定。該路由會指向下一個躍點 IP 位址 192.168.0.100、使用連接埠 8025，然後比對來自網域 litwareinc.com 的所有 URI。所產生的路由物件會以名稱為 $x 的變數儲存。

然後，範例中的第二個命令會將新路由新增至通用靜態路由組態集合。作法是呼叫 **Set-CsStaticRoutingConfiguration** Cmdlet 搭配 Route 參數。參數值 @{Add=$x} 會將以 $x 儲存的路由物件新增至已經在全域集合中的現有路由集。

    $x = New-CsStaticRoute -TCPRoute -Destination "192.168.0.100" -Port 8025 -MatchUri "litwareinc.com" 
    
    Set-CsStaticRoutingConfiguration -Identity global -Route @{Add=$x}

## 範例 2

範例 2 會示範如何建立使用 TLS 做為其傳輸通訊協定的新靜態路由，然後將該路由新增至通用靜態路由組態集合。為達成此目的，範例中的第一個命令會使用 **New-CsStaticRoute** Cmdlet 建立僅存於記憶體中的路由，並使用 TLS 做為其傳輸通訊協定。該路由會指向 "atl-proxy-001.litwareinc.com" 做為目的地、使用連接埠 8025，且會比對任何使用網域尾碼 "litwareinc.com" 的 URI。此外，儲存在名為 $x 之變數中的新路由物件會使用預設的憑證進行驗證 (-UseDefaultCertificate $True)。

已建立路由物件之後，接著範例中的第二個命令會將新路由新增至全域靜態路由組態集合。

    $x = New-CsStaticRoute -TLSRoute -Destination "atl-proxy-001.litwareinc.com" -Port 8025 -MatchUri "*.litwareinc.com" -UseDefaultCertificate $True
    
    Set-CsStaticRoutingConfiguration -Identity global -Route @{Add=$x}

## 範例 3

範例 3 會使用 TLS 與特定憑證建立一個新靜態路由；這由包括必要的 TLS 參數所指示。

已建立路由物件後，接著範例中的第二個命令會將新路由新增至全域靜態路由組態集合。

    $x = New-CsStaticRoute -TLSRoute -Destination "atl-proxy.litwareinc.com" -Port 5061 -MatchUri "litwareinc.com" -UseDefaultCertificate $False -TLSCertIssuer "CN=CertificateAuthority, DC=litwareinc, DC=com" -TLSCertSerialNumber 0x8f,0x33,0x70,0x93,0x70,0x05,0x33,0x00,0x02,0x33
    
    Set-CsStaticRoutingConfiguration -Identity global -Route @{Add=$x}

## 詳細描述

當您傳送 SIP 訊息給某人，該訊息可能需要在傳遞之前周遊多個子網路和網路；訊息所經歷的路徑通常稱為路由。在網路中，有兩種路由類型：動態及靜態。透過動態路由，伺服器使用演算法判斷訊息應轉送的下一個位置 (下一個躍點)。使用靜態路由時，訊息路徑是由系統管理員預先決定的。當伺服器收到訊息時，該伺服器會檢查訊息位址，然後將該訊息轉送到系統管理員預先設定的下一個躍點伺服器。如果設定正確，靜態路由有助於確保訊息即時且準確送達，而且可將伺服器竊聽減到最少。靜態路由的缺點是在網路故障時，無法動態地重新路由傳送訊息。

新的靜態路由是使用 **New-CsStaticRoute** Cmdlet 建立的。使用 **New-CsStaticRoute** Cmdlet 建立路由之後，接著您必須使用 **Set-CsStaticRoutingConfiguration** Cmdlet 將路由新增至路由組態設定集合。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsStaticRoute** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsStaticRoute"}

## 參數


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>必要</th>
<th>類型</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Destination</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>如果路由使用傳輸層安全性 (TLS) 做為傳輸通訊協定，則 Destination 即為下一個躍點伺服器的完整網域名稱 (FQDN)。例如：-Destination &quot;atl-proxy-001.litwareinc.com&quot;。</p>
<p>如果路由使用傳輸控制通訊協定 (TCP) 做為傳輸通訊協定，則 Destination 即為下一個躍點路由器的 IP 位址。例如：-Destination &quot;192.168.0.240&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>MatchUri</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>FQDN 或網域尾碼，用來決定訊息是否傳送至此路由所處理的使用者。例如，您可以使用 FQDN &quot;litwareinc.com&quot;。此模式會比對具有結尾為網域名稱 &quot;litwareinc.com&quot; 之 SIP 位址的任何使用者。</p>
<p>若要比對網域的子網域，您可以使用萬用字元值，例如 &quot;*.litwareinc.com&quot;。該值會比對結尾尾碼為 &quot;litwareinc.com&quot; 的所有網域。例如：northamerica.litwareinc.com; asia.litwareinc.com; and europe.litwareinc.com。</p></td>
</tr>
<tr class="odd">
<td><p><em>Port</em></p></td>
<td><p>必要</p></td>
<td><p>System.UInt16</p></td>
<td><p>SIP 路由使用的連接埠號碼。例如：-Port 7742。</p></td>
</tr>
<tr class="even">
<td><p><em>TCPRoute</em></p></td>
<td><p>必要</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>設定 TCP 做為新路由的傳輸通訊協定。</p></td>
</tr>
<tr class="odd">
<td><p><em>TLSRoute</em></p></td>
<td><p>必要</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>設定 TLS 做為新路由的傳輸通訊協定。</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果設為 True，則會啟用路由，而符合 MatchURI 模式的所有訊息將會路由至下一個躍點伺服器。如果設為 False，則會停用路由，而且將不會在路由訊息時使用。預設值為 True。</p></td>
</tr>
<tr class="odd">
<td><p><em>MatchOnlyPhoneUri</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果設為 True，只會比對位址設定為電話統一資源識別元 (URI) (例如 sip:kenmmyer@litwareinc.com;user=phone) 的訊息，而且可能會路由。如果設為 False (預設值)，則會比對所有訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>ReplaceHostInRequestUri</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果設為 True ($True)，則要求 URI 的主機部分將會以下一個躍點伺服器的位址取代。如果設為 False，則會使用原本的要求 URI。要求 URI 表示要求 (訊息) 已設定位址要傳送到的使用者或服務的 URI。預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>TLSCertIssuer</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>發行靜態路由中使用之憑證的憑證授權單位 (CA) 名稱。如果您已經設定 TCP 做為傳輸通訊協定，則不會使用此參數。</p>
<p>如果加入 TLSCertIssuer 參數，則也必須使用 TLSCertSerialNumber 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>TLSCertSerialNumber</em></p></td>
<td><p>選用</p></td>
<td><p>System.Byte[]</p></td>
<td><p>靜態路由中要使用之 TLS 憑證的序號。序號必須以位元組陣列的方式傳遞；也就是說，您必須以雙字元值的陣列來傳遞序號。例如：-TLSCertSerialNumber 0x01, 0xA4, 0xD5, 0x67, 0x89。</p>
<p>如果您已經設定 TCP 做為傳輸通訊協定，則不會使用此參數。</p>
<p>如果加入 TLSCertSerialNumber 參數，則也必須使用 TLSCertIssuer 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>UseDefaultCertificate</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設定路由使用您的預設 Lync Server 憑證做為其驗證憑證。如果不想使用預設憑證，則必須使用 TLSCertIssuer 和 TLSCertSerialNumber 參數指定不同的憑證。</p>
<p>若要檢視預設憑證，請使用以下命令：</p>
<p>Get-CsCertificate | Where-Object {$_.Use –eq &quot;urn:certref:Default&quot;}</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsStaticRoute** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsStaticRoute** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.Route 物件的新執行個體。

## 請參閱

#### 其他資源

[New-CsStaticRoutingConfiguration](new-csstaticroutingconfiguration.md)  
[Set-CsStaticRoutingConfiguration](set-csstaticroutingconfiguration.md)

