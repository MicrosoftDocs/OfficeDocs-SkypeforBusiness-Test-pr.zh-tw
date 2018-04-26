---
title: 設定自動探索的憑證
TOCTitle: 設定自動探索的憑證
ms:assetid: 1842191d-df9a-41e0-9286-08c25f9b5dca
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945617(v=OCS.15)
ms:contentKeyID: 52056060
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定自動探索的憑證

 

_**上次修改主題的時間：** 2012-12-12_

Director 集區、前端集區及反向 Proxy 的憑證需要額外的主體替代名稱項目，以支援與 Lync 用戶端的安全連線。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以使用 <strong>Get-CsCertificate</strong> Cmdlet 來檢視目前指派的憑證相關資訊。然而，預設檢視會截斷憑證屬性，而且不會顯示 SubjectAlternativeNames 屬性中所有的值。您可以使用 <strong>Get-CsCertificate</strong>、<strong>Request-</strong>CsCertificate 和 <strong>Set-CsCertificate</strong> Cmdlet 來檢視部分資訊，並要求及指派憑證。不過，如果您不確定目前憑證上主體替代名稱 (SAN) 的屬性，這並不是最好的方法。如果要檢視憑證和所有屬性成員，建議使用 <em>Microsoft Management Console (MMC)</em> 憑證嵌入式管理單元或使用 Lync Server 部署精靈。在 Lync Server 部署精靈中，您可以使用「憑證精靈」來檢視憑證屬性。下列程序中詳述使用 Lync Server 管理命令介面和 <em>Microsoft Management Console (MMC)</em> 來檢視、要求和指派憑證的程序。如果要使用 Lync Server 部署精靈，且您已部署選用的 Director 或 Director 集區，請參閱下列詳細資訊：<a href="lync-server-2013-configure-certificates-for-the-director.md">在 Lync Server 2013 中設定 Director 的憑證</a>。若是前端伺服器或前端集區，請參閱下列詳細資訊：<a href="lync-server-2013-configure-certificates-for-servers.md">在 Lync Server 2013 中設定伺服器憑證</a>。<br />
此程序中的最初步驟是準備步驟，引導您了解目前憑證扮演的角色。依預設，憑證不會有 lyncdiscover.&lt;SIP　網域&gt; 或 lyncdiscoverinternal.&lt;內部網域名稱&gt; 項目，除非您先前已安裝 Mobility Service 或已預先準備您的憑證。這個程序使用 SIP 網域名稱範例 ‘contoso.com’ 及內部網域名稱範例 ‘contoso.net’。<br />
Lync Server 2013 和 Lync Server 2010 的預設憑證設定是使用單一憑證 (名為 ‘Default’)，而其目的是 Default (適用於所有用途，除了 Web 服務)、WebServicesExternal 和 WebServicesInternal。選用設定是針對每種用途使用不同的憑證。憑證可以使用 Lync Server 管理命令介面和 Windows PowerShell Cmdlet 來管理，或使用 Lync Server 部署精靈中的「憑證精靈」來管理。</td>
</tr>
</tbody>
</table>


## 使用 Lync Server 管理命令介面以新的主體替代名稱來更新憑證

1.  使用具有本機系統管理員權限的帳戶登入電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  找出哪些憑證已經指派給伺服器，以及使用類型為何。在下一個步驟中，您會需要此資訊來指派更新的憑證。在命令列中輸入：
    
        Get-CsCertificate

4.  查閱上一個步驟的輸出，看看是否有單一憑證指派至多個用途，或者是否為每個用途指派不同的憑證。查閱 Use 參數，以找出憑證的用法。針對所顯示的憑證比較 Thumbprint 參數，看看相同的憑證是否有多個用途。

5.  更新憑證。在命令列中輸入：
    
        Set-CsCertificate -Type <type of certificate as displayed in the Use parameter> -Thumbprint <unique identifier>
    
    例如，如果 **Get-CsCertificate** Cmdlet 顯示一個 Use 為 Default 的憑證、一個 Use 為 WebServicesInternal 的憑證，以及一個 Use 為 WebServicesExternal 的憑證 , 而且它們全都有相同的 Thumbprint 值，在命令列中輸入：
    
        Set-CsCertificate -Type Default,WebServicesInternal,WebServicesExternal -Thumbprint <Certificate Thumbprint>
    
    **重要：**
    
    如果為每個用途指派不同的憑證 (每個憑證的 Thumbprint 值都不同)，則切勿以多種類型來執行 **Set-CsCertificate** Cmdlet。在此情況下，要為每個用途個別執行 **Set-CsCertificate** Cmdlet。例如：
    
        Set-CsCertificate -Type Default -Thumbprint <Certificate Thumbprint>
        Set-CsCertificate -Type WebServicesInternal -Thumbprint <Certificate Thumbprint>
        Set-CsCertificate -Type WebServicesExternal -Thumbprint <Certificate Thumbprint>

6.  如果要檢視憑證，依序按一下 \[開始\] 和 \[執行…\]。輸入 MMC 以開啟 Microsoft Management Console。

7.  從 MMC 功能表中，依序選取 \[檔案\]、\[新增/移除嵌入式管理單元…\] 和 \[憑證\]。按一下 \[新增\]。出現提示時，選取 \[電腦帳戶\]，然後按 \[下一步\]。

8.  如果憑證位於這部電腦上，請選取 \[本機電腦\]。如果憑證位於另一部電腦上，則選取 \[另一部電腦\]，輸入電腦的完整網域名稱或按一下 \[請輸入物件名稱來選取\] 中的 \[瀏覽\]，輸入電腦的名稱。按一下 \[檢查名稱\]。解析出電腦的名稱之後，將會加上底線。依序按一下 \[確定\] 和 \[完成\]。按一下 \[確定\] 以認可選取項目，然後關閉 \[新增/移除嵌入式管理單元\] 對話方塊。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果主控台未顯示該憑證，請確認未選取 [使用者] 或 [服務]。您必須選取 [電腦]，否則就無法找到適當的憑證。</td>
    </tr>
    </tbody>
    </table>


9.  如果要檢視憑證的屬性，依序展開 \[憑證\] 和 \[個人\]，然後選取 \[憑證\]。選取要檢視的憑證，用滑鼠右鍵按一下憑證，然後選取 \[開啟\]。

10. 在 \[憑證\] 檢視中，選取 \[詳細資料\]。您可以在此處選取 \[主體\] 來選取憑證主體名稱，隨即顯示指派的主體名稱和相關屬性。

11. 如果要檢視指派的主體替代名稱，請選取 \[主體替代名稱\]，隨即顯示所有指派的主體替代名稱。依預設，在屬性中找到的主體替代名稱類型為 \[DNS 名稱\]。您應該會看到下列成員 (全部都應該是以 DNS 主機 (A，若是 IPv6 則為 AAAA) 記錄形式顯示的完整網域名稱)：
    
      - 此集區的集區名稱，或如果不是集區，則為單一伺服器名稱
    
      - 被指派憑證的伺服器名稱
    
      - 簡單 URL 記錄，通常為 meet 和 dialin
    
      - Web 服務內部名稱和 Web 服務外部名稱 (例如，webpool01.contoso.net、webpool01.contoso.com)，視在拓撲產生器中所做的選擇以及覆寫的 Web 服務選擇而定。
    
      - 如果已經指派，則為 lyncdiscover.\<SIP 網域\> 和 lyncdiscoverinternal.\<SIP 網域\> 記錄。
    
    最後一項是您最感興趣的 – 是否有 lyncdiscover 和 lyncdiscoverinternal SAN 項目。
    
    取得此資訊之後，即可關閉憑證檢視和 MMC。

12. 如果遺失自動探索服務，亦即 lyncdiscover.\<網域名稱\> 和 lyncdiscoverinternal.\<網域名稱\> (視此為外部或內部憑證而定) 主體替代名稱，並且將單一 Default 憑證用於 Default、WebServicesInternal 及 WebServiceExternal 類型，請執行下列動作︰
    
      - 在 Lync Server 管理命令介面命令列提示字元中輸入：
        
            Request-CsCertificate -New -Type Default,WebServicesInternal,WebServicesExternal -Ca dc\myca -AllSipDomain -verbose
        
        如果您有多個 SIP 網域，則無法使用新的 AllSipDomain 參數，而必須使用 DomainName 參數。當您使用 DomainName 參數時，必須定義 lyncdiscoverinternal 和 lyncdiscover 記錄的 FQDN。例如：
        
            Request-CsCertificate -New -Type Default,WebServicesInternal,WebServicesExternal -Ca dc\myca -DomainName "LyncdiscoverInternal.contoso.com, LyncdiscoverInternal.contoso.net" -verbose
    
      - 如果要指派憑證，請輸入：
        
            Set-CsCertificate -Type Default,WebServicesInternal,WebServicesExternal -Thumbprint <Certificate Thumbprint>
        
        其中 “Thumbprint” 會顯示新核發的憑證指紋。

13. 若是遺失內部自動探索主體替代名稱，並且針對 Default、WebServicesInternal 及 WebServicesExternal 使用不同憑證時，請執行下列動作：
    
      - 在 Lync Server 管理命令介面命令列提示字元中輸入：
        
            Request-CsCertificate -New -Type WebServicesInternal -Ca dc\myca -AllSipDomain -verbose
        
        如果您有許多 SIP 網域，則不能使用新的 AllSipDomain 參數，而必須使用 DomainName 參數。當您使用 DomainName 參數時，必須為 SIP 網域 FQDN 使用適當的前置詞。例如：
        
            Request-CsCertificate -New -Type WebServicesInternal -Ca dc\myca -DomainName "LyncdiscoverInternal.contoso.com, LyncdiscoverInternal.contoso.net" -verbose
    
      - 若是遺失外部自動探索主體替代名稱，在命令列中輸入：
        
            Request-CsCertificate -New -Type WebServicesExternal -Ca dc\myca -AllSipDomain -verbose
        
        如果您有許多 SIP 網域，則不能使用新的 AllSipDomain 參數，而必須使用 DomainName 參數。當您使用 DomainName 參數時，必須為 SIP 網域 FQDN 使用適當的前置詞。例如：
        
            Request-CsCertificate -New -Type WebServicesExternal -Ca dc\myca -DomainName "Lyncdiscover.contoso.com, Lyncdiscover.contoso.net" -verbose
    
      - 如果要指派個別憑證類型，請輸入：
        
            Set-CsCertificate -Type Default -Thumbprint <Certificate Thumbprint>
            Set-CsCertificate -Type WebServicesInternal -Thumbprint <Certificate Thumbprint>
            Set-CsCertificate -Type WebServicesExternal -Thumbprint <Certificate Thumbprint>
        
        其中 “Thumbprint” 會顯示新核發的個別憑證指紋。

