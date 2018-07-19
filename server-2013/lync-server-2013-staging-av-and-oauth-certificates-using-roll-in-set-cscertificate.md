---
title: 於 Set-CsCertificate 使用 -Roll 以預備 Lync Server 2013 中的 AV 與 OAuth 憑證
TOCTitle: 於 Set-CsCertificate 使用 -Roll 以預備 Lync Server 2013 中的 AV 與 OAuth 憑證
ms:assetid: 22dec3cc-4b6b-4df2-b269-5b35df4731a7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ660292(v=OCS.15)
ms:contentKeyID: 49889979
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 於 Set-CsCertificate 使用 -Roll 以預備 Lync Server 2013 中的 AV 與 OAuth 憑證

 

_**上次修改主題的時間：** 2012-11-13_

音訊/視訊 (A/V) 通訊是 Microsoft Lync Server 2013 中的一個主要元件。應用程式共用和音訊/視訊會議等功能就需仰賴指派給 A/V Edge 服務 的憑證，尤其是 A/V 驗證服務。

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
<td><ol>
<li><p>這個新功能的主要目的是用來搭配 A/V Edge 服務 和 <em>OAuthTokenIssuer</em> 憑證。使用 A/V Edge 服務 和 OAuth 憑證類型也可以佈建其他憑證類型，不過就不能享有 A/V Edge 服務 憑證所具備的共存行為優勢。</p></li>
<li><p>用來管理 Microsoft Lync Server 2013 憑證的 Lync Server 管理命令介面 PowerShell Cmdlet 會將 A/V Edge 服務 憑證參照為 <em>AudioVideoAuthentication</em> 憑證類型，而將 OAuthServer 憑證參照為 <em>OAuthTokenIssuer</em> 類型。在本主題的其餘內容中，為了唯一識別憑證，也會以相同的識別碼類型 <em>AudioVideoAuthentication</em> 和 <em>OAuthTokenIssuer</em> 來參照憑證。</p></li>
</ol></td>
</tr>
</tbody>
</table>


A/V 驗證服務是專用來核發 Token，以供用戶端和其他 A/V 取用者使用。Token 是依據憑證上的屬性而產生，因此當憑證到期、連線中斷或必須重新加入時，就會導致新的憑證產生新的 Token。Lync Server 2013 中具備的新功能可以杜絕這個問題 – 其可在舊的憑證過期前先臨時發出新的憑證，以利兩個憑證都持續運作一段時間。此功能會使用 Set-CsCertificate Lync Server 管理命令介面 Cmdlet 中已更新的功能。現有的 –EffectiveDate 參數可使用新的 –Roll 參數，將新的 AudioVideoAuthentication 憑證放進憑證存放區。舊的 AudioVideoAuthentication 憑證仍會保留給已核發的 Token，以免其失效。只要一將新的 AudioVideoAuthentication 憑證準備就緒，就會發生下列一系列的事件：

<table>
<thead>
<tr class="header">
<th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用 Lync Server 管理命令介面 Cmdlet 以管理憑證時，您可以在 Edge Server 上針對不同用途，要求個別和不同的憑證。您可使用 Lync Server 部署精靈 中的 [憑證精靈] 來協助建立憑證，不過其通常是<strong>預設</strong>類型，其中將 Edge Server 所用的所有憑證都組合在單一的憑證上。若您要使用彙總的憑證，建議的做法是將 AudioVideoAuthentication 憑證從其他憑證用途中獨立出來。您可以佈建和臨時發出預設類型的憑證，但只有組合憑證的 AudioVideoAuthentication 部分可以臨時發出。舉例來說，當憑證過期時，立即訊息對話中的使用者將需要登出再重新登入，才能使用與 Access Edge Service 相關聯的新憑證。若是使用 Web Conferencing Edge Service 參與 Web 會議的使用者也需要採取類似的行為。OAuthTokenIssuer 憑證是一種特殊類型的憑證，在所有伺服器中都可以共用。您只需在一個位置建立並管理憑證，憑證就會存放在所有其他伺服器的中央管理存放區中。</td>
</tr>
</tbody>
</table>


在使用 Set-CsCertificate Cmdlet 以及在目前的憑證過期前利用此 Cmdlet 臨時發出憑證時，您需要更多資訊以全盤了解您的選項和需求。–Roll 參數很重要，但基本上為單一目的。若將其定義為參數，就必須提供 Set-CsCertificate 下列資訊︰會受影響的憑證 (由 –Type 定義，例如 AudioVideoAuthentication 和 OAuthTokenIssuer)，以及憑證何時生效 (由 -EffectiveDate 定義)。

**-Roll：**–Roll 為必要參數，且有必須搭配提供的相依性。下列為可完整定義哪些憑證將受影響以及套用方式的必要參數：

**-EffectiveDate：**參數 –EffectiveDate 可定義新的憑證何時和目前的憑證一起生效。–EffectiveDate 可以很接近目前憑證的到期日，或是更長的一段時間亦可。AudioVideoAuthentication 憑證的建議最低 –EffectiveDate 為 8 小時，其為使用 AudioVideoAuthentication 憑證時所發出之 AV Edge 服務 Token 的預設 Token 生命週期。

臨時發出 OAuthTokenIssuer 憑證時，在讓憑證生效前的前置重疊時間方面有些不同的需求。OAuthTokenIssuer 憑證的最低前置重疊時間為目前憑證到期時間的前 24 小時。共存的延伸前置重疊時間則取決於和 OAuthTokenIssuer 憑證相依的其他伺服器角色而定 (例如 Exchange Server)，其在憑證所建立的驗證和加密金鑰內容方面可具備較長的保留時間。

**-Thumbprint：**指紋是憑證上的一種屬性，且是唯一的。–Thumbprint 參數可用來識別將受 Set-CsCertificate Cmdlet 動作所影響的憑證。

**-Type：**–Type 參數可接受單一憑證使用類型或是以逗號分隔的憑證使用類型清單。憑證類型可讓 Cmdlet 以及伺服器判斷出憑證的用途為何。例如，AudioVideoAuthentication 類型是用於 A/V Edge 服務 以及 AV 驗證服務。若您決定要臨時發出並同時佈建不同類型的憑證，就必須考慮憑證的最長且必要的有效前置重疊時間。例如，若您要臨時發出 AudioVideoAuthentication 和 OAuthTokenIssuer 類型的憑證，您的最低 –EffectiveDate 就必須大於這兩個憑證；也就是要大於 OAuthTokenIssuer 的最低前置重疊時間 24 小時。若您想要臨時發出前置重疊時間為 24 小時的 AudioVideoAuthentication 憑證，請使用高於需求的 EffectiveDate 並個別臨時發出。

## 若要使用 –Roll 和 -EffectiveDate 參數來更新 A/V Edge 服務 憑證

1.  以 Administrators 群組成員的身分登入本機電腦。

2.  針對 A/V Edge 服務 上的現有憑證，使用可匯出的私密金鑰來要求更新或新的 AudioVideoAuthentication 憑證。

3.  將新的 AudioVideoAuthentication 憑證匯入 Edge Server 以及集區中的所有其他 Edge Server (若您有部署集區的話)。

4.  使用 Set-CsCertificate Cmdlet 並使用 –Roll 參數和 –EffectiveDate 參數來設定已匯入的憑證。生效日期應定義為目前憑證的到期時間 (14:00:00 或 2:00:00 PM) 扣除 Token 生命週期 (預設為八小時)。此即為憑證必須設為有效的時間，亦即 –EffectiveDate \<字串\>: “7/22/2012 6:00:00 AM”。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若為 Edge 集區，您就必須在第一個部署憑證之 –EffectiveDate 參數所定義的日期和時間之前，部署和佈建好 AudioVideoAuthentication 憑證，以避免由於舊憑證過期但尚未使用新憑證更新所有用戶端和取用者 Token 時導致的可能 A/V 通訊中斷問題。</td>
    </tr>
    </tbody>
    </table>
    
    Set-CsCertificate 命令搭配 –Roll 和 –EffectiveTime 參數：
    
        Set-CsCertificate -Type AudioVideoAuthentication -Thumbprint <thumb print of new certificate> -Roll -EffectiveDate <date and time for certificate to become active>
    
    Set-CsCertificate 命令範例：
    
        Set-CsCertificate -Type AudioVideoAuthentication -Thumbprint "B142918E463981A76503828BB1278391B716280987B" -Roll -EffectiveDate "7/22/2012 6:00:00 AM"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您必須將 EffectiveDate 格式化為符合您伺服器區域和語言設定。範例是使用英文 (美國) 區域和語言設定</td>
    </tr>
    </tbody>
    </table>


若要進一步了解 Set-CsCertificate、-Roll 和 –EffectiveDate 臨時發出新憑證，以核發新的 AudioVideoAuthentication Token，同時繼續使用現有的憑證來驗證取用者所使用的 AudioVideoAuthentication 的程序，視覺化的虛擬時間表是用來了解程序的有效方式。

在下列範例中，系統管理員判斷 A/V Edge 服務 憑證應在 07/22/2012 的下午 2:00:00 到期，因此管理員要求並收到新的憑證，然後將其匯入集區中的每個 Edge Server。在 07/22/2012 的上午 2 點時，管理員就開始搭配 –Roll、等於新憑證之指紋字串的 -Thumbprint，以及設為 07/22/2012 6:00:00 AM 的 –EffectiveTime 來執行 Get-CsCertificate。管理員會在每個 Edge Server 上執行此命令。

![使用 Roll 與 EffectiveDate 參數。](images/JJ660292.21d51a76-0d03-4ed7-a37e-a7c14940265f(OCS.15).jpg "使用 Roll 與 EffectiveDate 參數。")

當生效時間 (7/22/2012 6:00:00 AM) 到了時，新的憑證就會發出新的 Token。驗證 Token 時，會先以新的憑證來加以驗證。若驗證失敗，就會嘗試舊的憑證。直到舊憑證到期時間以前，都會一直繼續嘗試新憑證並恢復使用舊憑證的程序。當舊的憑證到期 (7/22/2012 2:00:00 PM) 之後，就只會由新的憑證來驗證 Token。您可使用 Remove-CsCertificate Cmdlet 和 –Previous 參數，順利地移除舊的憑證。

    Remove-CsCertificate -Type AudioVideoAuthentication -Previous

## 若要使用 –Roll 和 -EffectiveDate 參數來更新 OAuthTokenIssuer 憑證

1.  以 Administrators 群組成員的身分登入本機電腦。

2.  針對 A/V Edge 服務 上的現有憑證，使用可匯出的私密金鑰來要求更新或新的 OAuthTokenIssuer 憑證。

3.  將新的 OAuthTokenIssuer 憑證匯入集區中的前端伺服器 (若您有部署集區的話)。OAuthTokenIssuer 憑證是全域複寫的，因此僅需在部署中的任何伺服器上加以更新即可。前端伺服器是做為範例使用。

4.  使用 Set-CsCertificate Cmdlet 並使用 –Roll 參數和 –EffectiveDate 參數來設定已匯入的憑證。生效日期應定義為目前憑證的到期時間 (14:00:00 或 2:00:00 PM) 扣除至少 24 小時。
    
    Set-CsCertificate 命令搭配 –Roll 和 –EffectiveTime 參數：
    
        Set-CsCertificate -Type OAuthTokenIssuer -Thumbprint <thumb print of new certificate> -Roll -EffectiveDate <date and time for certificate to become active>
    
    Set-CsCertificate 命令範例：
    
        Set-CsCertificate -Type OAuthTokenIssuer -Thumbprint "B142918E463981A76503828BB1278391B716280987B" -Roll -EffectiveDate "7/21/2012 1:00:00 PM"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您必須將 EffectiveDate 格式化為符合您伺服器區域和語言設定。範例是使用英文 (美國) 區域和語言設定</td>
    </tr>
    </tbody>
    </table>


當生效時間到了 (7/21/2012 1:00:00 AM) 時，新的憑證就會發出新的 Token。驗證 Token 時，會先以新的憑證來加以驗證。若驗證失敗，就會嘗試舊的憑證。直到舊憑證到期時間以前，都會一直繼續嘗試新憑證並恢復使用舊憑證的程序。當舊的憑證到期 (7/22/2012 2:00:00 PM) 之後，就只會由新的憑證來驗證 Token。您可使用 Remove-CsCertificate Cmdlet 和 –Previous 參數，順利地移除舊的憑證。

    Remove-CsCertificate -Type OAuthTokenIssuer -Previous

## 請參閱

#### 概念

[在 Lync Server 2013 中規劃 Edge Server 憑證](lync-server-2013-plan-for-edge-server-certificates.md)  
[在 Lync Server 2013 中管理伺服器對伺服器驗證 (Oauth) 與夥伴應用程式](lync-server-2013-managing-server-to-server-authentication-oauth-and-partner-applications.md)  

#### 其他資源

[針對 Lync Server 2013 設定 Edge 憑證](lync-server-2013-set-up-edge-certificates.md)  
[Set-CsCertificate](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsCertificate)  
[Remove-CsCertificate](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsCertificate)

