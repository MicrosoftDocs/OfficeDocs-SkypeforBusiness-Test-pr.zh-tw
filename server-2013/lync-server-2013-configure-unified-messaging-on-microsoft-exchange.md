---
title: 針對 Lync Server 2013 在 Microsoft Exchange 上設定整合通訊
TOCTitle: 針對 Lync Server 2013 在 Microsoft Exchange 上設定整合通訊
ms:assetid: 07547968-c59b-4dde-ace4-9fd286933759
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398129(v=OCS.15)
ms:contentKeyID: 49289984
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 針對 Lync Server 2013 在 Microsoft Exchange 上設定整合通訊

 

_**上次修改主題的時間：** 2013-02-24_

本主題說明如何在 Microsoft Exchange Server 上設定 Exchange 整合通訊 (UM)，來與企業語音一起使用。

> [!NOTE]  
> 本主題中的 Cmdlet 範例針對 Exchange 2007 版本的 Exchange 管理命令介面提供語法。如果您執行的是 Exchange 2010 或 Exchange 2013，請參閱適當的參考文件。



## 若要設定正在執行 Exchange Server UM 的伺服器

1.  針對每一個企業語音位置設定檔，建立 UM 工作階段初始通訊協定 (SIP) 統一資源識別元 (URI) 撥號對應表。如果您選擇使用 Exchange 管理主控台，請使用安全性設定 **Secured (偏好選項)** 來建立新的撥號對應表。
    
    > [!WARNING]
    > 如前建議，如果您將安全性設定值設定為 <strong>SIP Secured</strong>，僅要求將 SIP 流量加密，請注意如果前端集區已設定為需要加密 (這表示集區需要針對 SIP 與 RTP 流量進行加密)，則撥號對應表上的這項安全性設定並不足夠。當撥號對應表和集區安全性設定不相容時，所有來自前端集區對 Exchange UM 的呼叫將會失敗，因而導致您有「不相容的安全性設定」錯誤。
    
    如果您使用 Exchange 管理命令介面，請輸入：
    
        New-UMDialPlan -Name <dial plan name> -UriType "SipName" -VoipSecurity <SIPSecured|Unsecured|Secured> -NumberOfDigitsInExtension <number of digits> -AccessTelephoneNumbers <access number in E.164 format>
    
    如需詳細資訊，請參閱：
    
      - 若為 Office Communications Server 2007，請參閱＜如何建立整合通訊 SIP URI 撥號對應表＞(網址為 [http://go.microsoft.com/fwlink/?linkid=268632\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268632%26clcid=0x404)) 及＜New-UMDialplan：Exchange 2007 說明＞(網址為 [http://go.microsoft.com/fwlink/?linkid=268666\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268666%26clcid=0x404))。
    
      - 若為 Exchange 2010，請參閱＜建立 UM 撥號對應表＞(網址為 [http://go.microsoft.com/fwlink/?linkid=268674\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268674%26clcid=0x404)) 及＜New-UMDialplan：Exchange 2010 說明＞(網址為 [http://go.microsoft.com/fwlink/?linkid=268680\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268680%26clcid=0x404))。
    
      - 若為 Exchange 2013，請參閱＜整合通訊＞，網址為 [http://go.microsoft.com/fwlink/?linkid=266579\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=266579%26clcid=0x404)。
    
    > [!NOTE]  
    > 您要選取 <strong>SIPSecured</strong> 或是 <strong>Secured</strong> 安全性層級，取決於媒體加密已啟用還是停用安全即時傳輸通訊協定 (SRTP) 而定。若為 Lync Server 2010 與 Exchange UM 的整合，這應該對應至 Lync Server 媒體組態的加密層級。執行 <strong>Get-CsMediaConfiguration</strong> Cmdlet 即可檢視 Lync Server 媒體組態。如需詳細資訊，請參閱 Lync Server 管理命令介面文件中的 Get-CsMediaConfiguration。<br />
    > 如需選取適當 VoIP 安全性設定的詳細資訊，請參閱＜<a href="lync-server-2013-deployment-process-for-integrating-on-premises-unified-messaging.md">整合內部部署 Unified Messaging 和 Lync Server 2013 的部署程序</a>＞。


2.  執行下列 Cmdlet 以取得每個 UM 撥號對應表的完整網域名稱 (FQDN)：
    
    ``` 
    (Get-UMDialPlan <dialplanname>).PhoneContext  
    ```
    
    如需詳細資訊，請參閱：
    
      - 若為 Exchange 2007，請參閱＜Get-UMDialplan：Exchange 2007 說明＞，網址為 [http://go.microsoft.com/fwlink/?linkid=268678\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268678%26clcid=0x404)。
    
      - 若為 Exchange 2010，請參閱＜Get-UMDialplan：Exchange 2010 說明＞，網址為 [http://go.microsoft.com/fwlink/?linkid=268679\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268679%26clcid=0x404)。
    
      - 若為 Exchange 2013，請參閱＜整合通訊＞，網址為 [http://go.microsoft.com/fwlink/?linkid=266579\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=266579%26clcid=0x404)。

3.  記錄每個 UM 撥號對應表的撥號對應表名稱。根據您的 Exchange Server 版本而定，您稍後可能需要使用每個撥號對應表名稱的 FQDN 作為每個 UM 撥號對應表的對應 Lync Server 撥號對應表名稱，如此撥號對應表名稱才會相符。
    
    > [!NOTE]  
    > 只有在 UM 撥號對應表正在 Exchange 2010 SP1 <em>以前</em> 的 Exchange 版本上執行時，Lync Server 撥號對應表名稱才必須符合 UM 撥號對應表名稱。
    


4.  如下所示，將撥號對應表新增至執行 Exchange UM 的伺服器：
    
      - 如果您選擇使用 Exchange 管理主控台，您可以從伺服器的內容表新增此撥號對應表。如需特定的指示，請參閱 Exchange Server 產品文件。
        
        若為 Exchange 2007，請參閱＜如何將 Unified Messaging Server 新增至撥號對應表＞，網址為 [http://go.microsoft.com/fwlink/?linkid=268681\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268681%26clcid=0x404)。
        
        若為 Exchange 2010，請參閱＜檢視或設定 UM 伺服器的內容＞，網址為 [http://go.microsoft.com/fwlink/?linkid=268682\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268682%26clcid=0x404)。
        
        若為 Exchange 2013，請參閱＜整合通訊＞，網址為 [http://go.microsoft.com/fwlink/?linkid=266579\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=266579%26clcid=0x404)。
    
      - 如果您使用 Exchange 管理命令介面，請針對每一部 Exchange UM 伺服器執行下列命令：
        
            $ums=get-umserver; 
            $dp=get-umdialplan -id <name of dial-plan created in step 1>; 
            $ums[0].DialPlans +=$dp.Identity; 
            set-umserver -instance $ums[0]
    
    > [!Note]  
	> 在執行下列步驟之前，請先確定所有的 Enterprise Voice 使用者都已設定好 Exchange Server 信箱。<br />
    > 若為 Exchange 2007，請參閱 Exchange Server 2007 TechNet Library，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=268685%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=268685&amp;clcid=0x404</a>。<br />
    > 若為 Exchange 2010，請參閱 Exchange Server 2010 TechNet Library，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=268686%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=268686&amp;clcid=0x404</a>。<br />
    > 當您為在步驟 1 中所建立的每個撥號對應表指定信箱原則時，請選取預設原則或您所建立的原則。


5.  瀏覽到 \<*Exchange 安裝目錄*\>\\Scripts，如果 Exchange 部署在單一樹系中，請輸入：
    
        exchucutil.ps1
    
    或者，如果 Exchange 部署在多個樹系中，請輸入：
    
        exchucutil.ps1 -Forest:"<forest FQDN>"
    
    其中 *樹系 FQDN* 是指已部署 Lync Server 的樹系。
    
    如果您有與多個 IP 閘道關聯的一或多個 UM 撥號對應表，請繼續執行步驟 6。如果您的每個撥號對應表都只和一個 IP 閘道關聯，請略過步驟 6。
    
    > [!IMPORTANT]  
    > 請務必在執行 exchucutil.ps1 <em>之後</em>，重新啟動 <strong>[Lync Server 前端]</strong> 服務 (rtcsrv.exe)。否則，Lync Server 偵測不到拓撲中的整合通訊。
    


6.  使用 Exchange 管理命令介面或 Exchange 管理主控台，除了與您的撥號對應表關聯之 IP 閘道的撥出電話之外，停用所有 IP 閘道的撥出電話。
    
    > [!NOTE]  
    > 此步驟是要確保執行 Exchange Server 整合通訊的伺服器撥出給外部使用者的電話 (例如，在電話上播放的狀況) 會可靠地穿越公司防火牆。
    
    
    > [!IMPORTANT]  
    > 選取撥出電話要通過的 UM IP 閘道時，請選擇可處理最多流量的閘道。不要讓傳出流量通過連接至 Lync Server Director 集區的 IP 閘道。同時避免其他中央網站或分支網站中的集區。您可以使用下列任一種方法防止撥出電話通過 IP 閘道：
    
    
      - 如果您使用 Exchange 管理命令介面，請執行下列命令以停用每個 IP 閘道：
        
            Set-UMIPGateway <gatewayname> -OutcallsAllowed $false
        
        若為 Exchange 2007，請參閱＜Set-UMIPGateway：Exchange 2007 說明＞，網址為 [http://go.microsoft.com/fwlink/?linkid=268687\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268687%26clcid=0x404)。
        
        若為 Exchange 2010，請參閱＜Set-UMIPGateway：Exchange 2010 說明＞，網址為 [http://go.microsoft.com/fwlink/?linkid=268688\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268688%26clcid=0x404)。
    
      - 如果是使用 Exchange 管理主控台，請清除 **\[允許透過這個 IP 閘道的撥出電話\]** 核取方塊。
    
    > [!IMPORTANT]  
    > 如果您的 UM SIP URI 撥號對應表只與一個 IP 閘道關聯，請允許撥出的電話通過這個閘道。
    


7.  為每一個 Lync Server 撥號對應表建立 UM 自動語音應答。
    
    > [!IMPORTANT]  
    > 請勿在自動語音應答的名稱中加入任何空格。
    
    
        New-umautoattendant -name <auto attendant name> -umdialplan < name of dial plan created in step 1> -PilotIdentifierList <auto attendant phone number in E.164 format> -SpeechEnabled $true -Status Enabled
    
    如需詳細資訊，請參閱：
    
      - 若為 Exchange 2007，請參閱＜New-UMAutoAttendant：Exchange 2007 說明＞，網址為 [http://go.microsoft.com/fwlink/?linkid=268689\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268689%26clcid=0x404)。
    
      - 若為 Exchange 2010，請參閱＜New-UMAutoAttendant：Exchange 2010 說明＞，網址為 [http://go.microsoft.com/fwlink/?linkid=268690\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268690%26clcid=0x404)。
    
    您為 Lync Server 使用者啟用企業語音，並且知道使用者的 SIP URI 之後，應該針對每個使用者執行下列步驟。

8.  建立 Exchange UM 使用者 (每個使用者都應設定一個 Exchange 信箱) 與 UM 撥號對應表的關聯，並為每個使用者建立 SIP URI。
    
    > [!NOTE]  
    > 下列範例中的 <strong>SIPResourceIdentifier</strong> 必須是 Lync Server 使用者的 SIP 位址。
    
    
        enable-ummailbox -id <user name> -ummailboxpolicy <name of the mailbox policy for the dial plan created in step 1> -Extensions <extension> -SIPResourceIdentifier "<user name>@<full domain name>" -PIN <user pin>
    
    如需詳細資訊，請參閱：
    
      - 若為 Exchange 2007，請參閱＜Enable-UMMailbox：Exchange 2007 說明＞，網址為 [http://go.microsoft.com/fwlink/?linkid=268691\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268691%26clcid=0x404)。
    
      - 若為 Exchange 2010，請參閱＜Enable-UMMailbox：Exchange 2010 說明＞，網址為 [http://go.microsoft.com/fwlink/?linkid=268692\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268692%26clcid=0x404)。

