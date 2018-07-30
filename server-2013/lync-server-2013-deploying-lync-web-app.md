---
title: 部署 Lync Web App
TOCTitle: 部署 Lync Web App
ms:assetid: b6301e98-051c-4e4b-8e10-ec922a8f508a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205190(v=OCS.15)
ms:contentKeyID: 49292081
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 部署 Lync Web App

 

_**上次修改主題的時間：** 2013-07-18_

Lync Web App 是隨 Lync Server 2013 安裝的網際網路資訊服務 (IIS) Web 用戶端，且依預設為啟用。無論是在伺服器上啟用 Lync Web App 或為使用者部署 Web 用戶端，都不需要執行額外的步驟。若使用者在未安裝 Lync 2013 用戶端的情況下按下會議 URL，系統會顯示選項給使用者，以使用最新版的 Lync Web App 加入會議。

Lync Web App 中的語音、視訊與共用功能需要 Microsoft ActiveX 控制項。您可事先安裝 ActiveX 控制項，或讓使用者在系統提示時進行安裝。當使用者第一次使用 Lync Web App 或第一次存取需要 ActiveX 控制項的功能時，即會出現提示。

> [!NOTE]  
> 在 Lync Server 2013 Edge Server 部署中，周邊網路中需要有 HTTPS 反向 Proxy 才能進行 Lync Web App 用戶端存取。您也必須發行簡單 URL。如需詳細資訊，請參閱<a href="lync-server-2013-setting-up-reverse-proxy-servers.md">設定 Lync Server 2013 的反向 Proxy 伺服器</a>與<a href="lync-server-2013-planning-for-simple-urls.md">在 Lync Server 2013 中規劃簡單 URL</a>。



## 啟用 Lync Web App 的多重因素驗證

Lync Web App 的 Lync Server 2013 版本支援多重因素驗證。除了使用者名稱與密碼之外，您可使用其他的驗證方法 (例如智慧卡或 PIN)，在從外部網路加入的使用者登入 Lync 會議時進行驗證。您可在 Lync Server 2013 中部署 Active Directory Federation Service (AD FS) 同盟伺服器並啟用被動驗證來啟用多重因素驗證。AD FS 設定之後，嘗試加入 Lync 會議的外部使用者會看見 AD FS 多重因素驗證網頁，當中包含使用者名稱與密碼挑戰，以及您已設定的其他驗證方法。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您計劃設定 AD FS 來進行多重因素驗證，下列為重要的考量事項：
<ul>
<li><p>如果會議參與者和召集人位於相同組織，或同樣來自 AD FS 同盟組織，則多重因素 ADFS 驗證可以正常運作。多重因素 ADFS 驗證無法用於 Lync 同盟使用者，因為 Lync 伺服器 Web 基礎結構目前並不支援它。</p></li>
<li><p>若您使用硬體負載平衡器，請在負載平衡器上啟用 Cookie 持續性，這樣來自 Lync Web App 用戶端的所有要求才能由相同的前端伺服器處理。</p></li>
<li><p>當您在 Lync Server 與 AD FS 伺服器之間建立信賴憑證者信任時，請指定長度足夠的 Token 檔案，以擴展您 Lync 會議的長度上限。一般來說，240 分鐘的 Token 檔案即足夠。</p></li>
<li><p>此設定並不會套用至 Lync 行動用戶端。</p></li>
</ul></td>
</tr>
</tbody>
</table>


**設定多重因素驗證**

1.  安裝 AD FS 同盟伺服器角色。如需詳細資訊，請參閱《Active Directory Federation Services 2.0 部署指南》，網址為[http://go.microsoft.com/fwlink/?linkid=267511\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=267511%26clcid=0x404)

2.  建立 AD FS 憑證。如需詳細資訊，請參閱與單一登入主題搭配使用之規劃與部署 AD FS 的＜同盟伺服器憑證＞一節，網址為 [http://go.microsoft.com/fwlink/?linkid=285376\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=285376%26clcid=0x404)。

3.  從 Windows PowerShell 命令列介面執行下列命令：
    
        add-pssnapin Microsoft.Adfs.powershell

4.  執行下列命令來建立合作關係：
    
        Add-ADFSRelyingPartyTrust -Name ContosoApp -MetadataURL https://lyncpool.contoso.com/passiveauth/federationmetadata/2007-06/federationmetadata.xml

5.  設定下列信賴憑證者規則：
    
      ```
      $IssuanceAuthorizationRules = '@RuleTemplate = "AllowAllAuthzRule" => issue(Type = "http://schemas.contoso.com/authorization/claims/permit", Value = "true");'$IssuanceTransformRules = '@RuleTemplate = "PassThroughClaims" @RuleName = "Sid" c:[Type == "http://schemas.contoso.com/ws/2008/06/identity/claims/primarysid"]=> issue(claim = c);'
      ```
    
      ```
      Set-ADFSRelyingPartyTrust -TargetName ContosoApp -IssuanceAuthorizationRules $IssuanceAuthorizationRules -IssuanceTransformRules $IssuanceTransformRules
      ```
    
      ```
      Set-CsWebServiceConfiguration -UseWsFedPassiveAuth $true -WsFedPassiveMetadataUri https://dc.contoso.com/federationmetadata/2007-06/federationmetadata.xml
      ```

## BranchCache 設定

Windows 7 與 Windows Server 2008 R2 中的 BranchCache 功能可能會干擾 Lync Web App Web 元件。若要避免 Lync Web App 使用者發生問題，請確定未啟用 BranchCache。

如需關於停用 BranchCache 的詳細資訊，請參閱《BranchCache 部署指南》，您可從 [http://go.microsoft.com/fwlink/?linkid=268788\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268788%26clcid=0x404) 的 Microsoft 下載中心取得 Word 格式的檔案，並在 [http://go.microsoft.com/fwlink/?linkid=268789\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268789%26clcid=0x404) 的 Windows Server 2008 R2 Technical Library 取得 HTML 格式的檔案。

## 驗證 Lync Web App 部署

您可使用 Test-CsUcwaConference Cmdlet 來驗證某組測試使用者是否可使用 Unified Communications Web API (UCWA) 參與會議。如需關於此 Cmdlet 的詳細資訊，請參閱 Lync Server 管理命令介面 文件中的 [Test-CsUcwaConference](https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsUcwaConference)。

## 疑難排解 Windows Server 2008 R2 上的外掛程式安裝

如果在執行 Windows Server 2008 R2 的電腦上安裝外掛程式失敗，您可能需要修改 Internet Explorer 安全性設定或 DisableMSI 登錄機碼設定。

**修改 Internet Explorer 中的安全性設定**

1.  開啟 \[Internet Explorer\]。

2.  依序按一下 \[工具\] 、\[網際網路選項\]，以及 \[進階\]。

3.  捲動至 \[安全性\] 區段。

4.  清除 \[不要將加密的網頁存到磁碟\]，然後按一下 \[確定\]。
    
    > [!NOTE]  
    > 若選取此設定，當嘗試從 Lync Web App 下載附件時，也會造成錯誤。
    


5.  重新加入會議。應該可正確下載外掛程式。

**修改 DisableMSI 登錄設定**

1.  按一下 \[開始\]，然後再按一下 \[執行\]。

2.  若要存取 \[登錄編輯程式\]，請輸入 **regedit**。

3.  瀏覽至 HKEY\_LOCAL\_MACHINE\\Software\\Policies\\Microsoft\\Windows\\Installer。

4.  編輯或新增 DisableMSI 登錄機碼的 REG\_DWORD 類型，並將它設為 0。

5.  重新加入會議。

## 請參閱

#### 概念

[在 Lync Server 2013 中設定會議加入頁面](lync-server-2013-configuring-the-meeting-join-page.md)  
[Lync Server 2013 的 Lync Web App 支援平台](lync-server-2013-lync-web-app-supported-platforms.md)

