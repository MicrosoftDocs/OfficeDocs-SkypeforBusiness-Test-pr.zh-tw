---
title: Lync Server 2013：修改行動憑證
TOCTitle: 修改行動憑證
ms:assetid: 4e9107af-20f4-4c2a-8c98-ca35b39a4e2d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690015(v=OCS.15)
ms:contentKeyID: 49290874
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中修改行動憑證

 

_**上次修改主題的時間：** 2014-06-20_

為了支援您的 Lync 環境與行動用戶端之間的安全連線，您需要使用某些額外的主體替代名稱 (SAN) 項目來更新 Director 集區、前端集區 和反向 Proxy 的安全通訊端層 (SSL) 憑證。如果需要參考更詳細的行動憑證需求資訊，請參閱＜[Lync Server 2013 行動技術需求](lync-server-2013-technical-requirements-for-mobility.md)＞的＜憑證參考＞一節，但基本上您需要藉由加入其他 SAN 項目，以便從憑證授權單位取得新憑證，然後使用本文的步驟新增那些憑證。

在開始之前，了解您的憑證已使用的主體替代名稱通常是個好主意。如果不確定已設定的內容，您可藉助許多方法來確定。僅管該處的選項會執行 **Get-CsCertificate** 及其他 PowerShell 命令來檢視此資訊，(我們將在以下逐一說明) 但預設會截斷該資料，因此您可能看不到需要的所有屬性。為了更清楚檢視憑證及其所有屬性，您可以移至 Microsoft Management Console (MMC) 並載入憑證嵌入式管理單元 (我們也會在底下逐一說明)，或只要檢查「Lync Server 部署精靈」即可。

如上所述，下列步驟將引導您使用 Lync Server 管理命令介面 和 MMC 來逐步更新憑證。如果您希望改用 \[Lync Server 部署精靈\] 的 \[憑證精靈\] 來執行這個動作，您可以檢閱＜[在 Lync Server 2013 中設定 Director 的憑證](lync-server-2013-configure-certificates-for-the-director.md)＞的 Director 或 Director 集區 (如果已設定，但也許您還未設定) 相關資訊。如需前端伺服器或前端集區的詳細資訊，您可以參閱＜[在 Lync Server 2013 中設定伺服器憑證](lync-server-2013-configure-certificates-for-servers.md)＞。

最後一個注意事項是，您在 Lync Server 2013 環境中可能擁有單一的 Default 憑證，或您可能有 Default (Web 服務除外的每件事)、WebServicesExternal 和 WebServicesInternal 以外的憑證。不論您的設定為何，這些步驟應可協助您解決問題。

## 使用 Lync Server 管理命令介面以新的主體替代名稱來更新憑證

1.  您需要使用具有本機系統管理員權限的帳戶登入 Lync Server 2013 伺服器。此外，如果您正在步驟 12 及 13 中執行 PowerShell **Request-CsCertificate**，該帳戶需要具有指定之憑證授權單位 (CA) 的權限。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  指派更新的憑證前，您需要瞭解哪些憑證已經指派給伺服器，以及使用類型為何。在命令列中輸入：
    
        Get-CsCertificate

4.  檢閱上一個步驟的輸出，看看是否有單一憑證指派至多個用途，或者是否為每個用途指派不同的憑證。查閱 Use 參數，以找出憑證的用法。針對所顯示的憑證比較 Thumbprint 參數，看看相同的憑證是否有多個用途。請注意 Thumbprint 參數。

5.  更新憑證。在命令列中輸入：
    
        Set-CsCertificate -Type <type of certificate as displayed in the Use parameter> -Thumbprint <unique identifier>
    
    例如，如果 **Get-CsCertificate** Cmdlet 顯示一個 Use 為 Default 的憑證、一個 Use 為 WebServicesInternal 的憑證，以及一個 Use 為 WebServicesExternal 的憑證 , 而且它們全都有相同的 Thumbprint 值，您應該在命令列中輸入：
    
        Set-CsCertificate -Type Default,WebServicesInternal,WebServicesExternal -Thumbprint <Certificate Thumbprint>
    
    **重要：**
    
    如果為每個用途指派不同的憑證 (這會針對每個憑證，在上方核取不同的 Thumbprint 值)，則切勿以多種類型來執行 **Set-CsCertificate** Cmdlet，如上述範例所示。在此情況下，要為每個用途個別執行 **Set-CsCertificate** Cmdlet。例如：
    
        Set-CsCertificate -Type Default -Thumbprint <Certificate Thumbprint>
        Set-CsCertificate -Type WebServicesInternal -Thumbprint <Certificate Thumbprint>
        Set-CsCertificate -Type WebServicesExternal -Thumbprint <Certificate Thumbprint>

6.  如果要檢視憑證，依序按一下 \[開始\] 和 \[執行…\]。輸入 MMC 以開啟 Microsoft Management Console。

7.  從 MMC 功能表中，依序選取 \[檔案\] 、\[新增/移除嵌入式管理單元…\] 和 \[憑證\]。按一下 \[新增\] 。出現提示時，選取 \[電腦帳戶\] ，然後按 \[下一步\] 。

8.  如果憑證位於這台電腦上，請選取 \[本機電腦\]。如果憑證位於另一台電腦上，則應選取 \[另一台電腦\]，接著可輸入電腦的完整網域名稱；或按一下 \[請輸入物件名稱來選取\] 中的 \[瀏覽\]，再輸入電腦的名稱。按一下 \[檢查名稱\]。解析出電腦的名稱之後，將會加上底線。依序按一下 \[確定\] 和 \[完成\]。按一下 \[確定\] 以認可選取項目，然後關閉 \[新增/移除嵌入式管理單元\] 對話方塊。

9.  如果要檢視憑證的屬性，依序展開 \[憑證\] 和 \[個人\] ，然後選取 \[憑證\] 。選取要檢視的憑證，用滑鼠右鍵按一下憑證，然後選取 \[開啟\] 。

10. 在 \[憑證\] 檢視中，選取 \[詳細資料\] 。您可以在此處選取 \[主體\] 來選取憑證主體名稱，隨即顯示指派的主體名稱和相關屬性。

11. 如果要檢視指派的主體替代名稱，請選取 \[主體替代名稱\]，隨即會在這裡顯示所有指派的主體替代名稱。依預設，在這裡中找到的主體替代名稱類型為 \[DNS 名稱\]。您應該會看到下列成員 (全部都應該是以 DNS 主機 (A，若是 IPv6 則為 AAAA) 記錄形式顯示的完整網域名稱)：
    
      - 此集區的集區名稱，或如果不是集區，則為單一伺服器名稱
    
      - 被指派憑證的伺服器名稱
    
      - 簡單 URL 記錄，通常為 meet 和 dialin
    
      - Web 服務內部名稱和 Web 服務外部名稱 (例如，webpool01.contoso.net、webpool01.contoso.com)，視在 拓撲產生器中所做的選擇以及覆寫的 Web 服務選擇而定。
    
      - 如果已經指派，則為 lyncdiscover.\<SIP 網域\> 和 lyncdiscoverinternal.\<SIP 網域\> 記錄。
    
    最後一項是您最感興趣的 - 是否有 lyncdiscover 和 lyncdiscoverinternal SAN 項目。
    
    如果有多個要檢查的憑證，請重複這些步驟。取得此資訊之後，即可關閉憑證檢視和 MMC。

12. 如果自動探索服務主體替代名稱遺漏，而您對 Default、WebServicesInternal 和 WebServiceExternal 類型使用單一 Default 憑證，請執行下列動作：
    
      - 在 Lync Server 管理命令介面命令列提示字元中輸入：
        
            Request-CsCertificate -New -Type Default,WebServicesInternal,WebServicesExternal -Ca dc\myca -AllSipDomain -verbose
        
        如果您有多個 SIP 網域，則無法使用新的 AllSipDomain 參數，而必須使用 DomainName 參數。當您使用 DomainName 參數時，必須定義 lyncdiscoverinternal 和 lyncdiscover 記錄的 FQDN。例如：
        
            Request-CsCertificate -New -Type Default,WebServicesInternal,WebServicesExternal -Ca dc\myca -DomainName "LyncdiscoverInternal.contoso.com, LyncdiscoverInternal.contoso.net" -verbose
    
      - 如果要指派憑證，請輸入：
        
            Set-CsCertificate -Type Default,WebServicesInternal,WebServicesExternal -Thumbprint <Certificate Thumbprint>
        
        其中 「Thumbprint」 會顯示新核發的憑證指紋。

13. 若是遺失內部自動探索 SAN，並且針對 Default、WebServicesInternal 及 WebServicesExternal 使用不同憑證時，請執行下列動作：
    
      - 在 Lync Server 管理命令介面命令列提示字元中輸入：
        
            Request-CsCertificate -New -Type WebServicesInternal -Ca dc\myca -AllSipDomain -verbose
        
        如果您有多個 SIP 網域，則無法使用新的 AllSipDomain 參數，而必須使用 DomainName 參數。當您使用 DomainName 參數時，必須為 SIP 網域 FQDN 使用適當的首碼。例如：
        
            Request-CsCertificate -New -Type WebServicesInternal -Ca dc\myca -DomainName "LyncdiscoverInternal.contoso.com, LyncdiscoverInternal.contoso.net" -verbose
    
      - 若是遺失外部自動探索主體替代名稱，在命令列中輸入：
        
            Request-CsCertificate -New -Type WebServicesExternal -Ca dc\myca -AllSipDomain -verbose
        
        如果您有多個 SIP 網域，則無法使用新的 AllSipDomain 參數，而必須使用 DomainName 參數。當您使用 DomainName 參數時，必須為 SIP 網域 FQDN 使用適當的首碼。例如：
        
            Request-CsCertificate -New -Type WebServicesExternal -Ca dc\myca -DomainName "Lyncdiscover.contoso.com, Lyncdiscover.contoso.net" -verbose
    
      - 如果要指派個別憑證類型，請輸入：
        
            Set-CsCertificate -Type Default -Thumbprint <Certificate Thumbprint>
            Set-CsCertificate -Type WebServicesInternal -Thumbprint <Certificate Thumbprint>
            Set-CsCertificate -Type WebServicesExternal -Thumbprint <Certificate Thumbprint>
        
        其中 「Thumbprint」 代表對新發行的個別憑證顯示的指紋。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>請注意，只有在執行步驟 12 和 13 的帳戶具有可存取憑證授權單位的適當權限時，才應該執行這些步驟。如果您無法以取得那些權限的帳戶登入，或正在為您的憑證使用公用或憑證授權單位，則將需要透過 [Lync Server 部署精靈] 要求它們，如本文上方所述。</td>
    </tr>
    </tbody>
    </table>

