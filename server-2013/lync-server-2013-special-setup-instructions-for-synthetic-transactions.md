---
title: 綜合交易的特殊設定指示
TOCTitle: 綜合交易的特殊設定指示
ms:assetid: 694cbe05-5dba-4035-a01c-c87ebfb0478b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688080(v=OCS.15)
ms:contentKeyID: 49890101
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 綜合交易的特殊設定指示

 

_**上次修改主題的時間：** 2013-01-22_

在現有的監看員節點上可執行大多數綜合交易；也就是說，一旦將綜合交易新增至監看員節點組態設定，監看員節點就可在其測試通過期間開始使用綜合交易。不過，並非所有綜合交易皆如此。需要特殊設定指示的綜合交易就是例外， 我們會在後續章節中討論。

## 資料會議綜合交易

如果您的監看員節點電腦位於週邊網路外，可能就無法執行資料會議綜合交易，除非您先停用網路服務帳戶的 Internet Explorer Proxy 設定。若要停用此服務的 Proxy 設定，請完成下列程序：

1.  在監看員節點電腦上，依序按一下 **\[開始\]**、**\[所有程式\]** 及 **\[附屬應用程式\]**，再以滑鼠右鍵按一下 **\[命令提示字元\]**，然後按一下 **\[以系統管理員身分執行\]**。

2.  在主控台視窗中輸入下列命令，然後按 ENTER 鍵：
    
        bitsadmin /util /SetIEProxy NetworkService NO_PROXY

下列訊息會出現在命令視窗中：

    BITSAdmin is deprecated and is not guaranteed to be available in future versions of Windows. Administration tools for the BITS service are now provided by BITS PowerShell cmdlets.
    
    Internet proxy settings for account NetworkService set to NO_PROXY. 
    (connection = default)

此訊息表示您已停用網路服務帳戶的 Internet Explorer Proxy 設定。

## Exchange 整合通訊綜合交易

Exchange 整合通訊 (UM) 綜合交易會驗證測試使用者能否連線至位於 Exchange 中的語音信箱帳戶。需使用語音信箱帳戶預先設定這些測試使用者之後，他們才可使用 Exchange UM 測試。

## 常設聊天室綜合交易

若要使用常設聊天室綜合交易，系統管理員必須先建立通道，並賦予測試使用者使用權限。您可使用 [Test-CsPersistentChatMessage](https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsPersistentChatMessage) Cmdlet 以正確設定這些測試使用者：

    $cred1 = Get-Credential "litwareinc\kenmyer"
    $cred2 = Get-Credential "litwareinc\pilar"
    
    Test-CsPersistentChatMessage -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress sip:kenmyer@litwareinc.com -SenderCredential $cred1 -ReceiverSipAddress sip:pilar@litwareinc.com -ReceiverCredential $cred2 -TestUser1SipAddress sip:kenmyer@litwareinc.com -TestUser2SipAddress sip:pilar@litwareinc.com -Setup $True

必須從企業內部執行此設定工作：

  - 如果從非伺服器電腦執行，則執行 Cmdlet 的使用者須為角色型存取控制 (RBAC) 的 PersistentChatAdministrators 角色成員。

  - 如果從伺服器本身執行，則執行 Cmdlet 的使用者應為 RTCUniversalServerAdmins 群組的成員。

在上述命令中，已包含設定參數並設為 True ($True)。如果包含 Setup 參數，Test-CsPersistentChatMessage 會建立特殊常設聊天室空間並將測試使用者填入該聊天室。這樣可確保確實有聊天室可供測試之用。請注意，Setup 參數僅可從前端伺服器執行。

Test-CsPersistentChatMessage 建立的聊天室僅可由系統管理員刪除。

## PSTN 對等通話綜合交易

[Test-CsPstnPeerToPeerCall](https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsPstnPeerToPeerCall) 綜合交易會驗證透過公用交換電話網路 (PSTN) 進行和接受通話的能力。

若要執行此綜合交易，系統管理員必須進行下列設定：

  - 兩名測試使用者 (發話者和受話者) 皆啟用企業語音。

  - 每個使用者帳戶的直接內部撥號 (DID) 號碼。

  - 語音原則和語音路由可讓撥打至受話者號碼的通話到達 PSTN 閘道。

  - 接受通話的 PSTN 閘道，與依據撥打的號碼將通話路由傳送回受話者主集區的媒體。

## 整合連絡人存放區綜合交易

整合連絡人存放區綜合交易會驗證 Lync Server 2013 是否能代表 Microsoft Exchange Server 2013 的使用者擷取連絡人。

若要使用此綜合交易，必須符合下列條件：

  - 必須在 Lync Server 2013 和 Exchange 2013 之間設定[在 Lync Server 2013 中管理伺服器對伺服器驗證 (Oauth) 與夥伴應用程式](lync-server-2013-managing-server-to-server-authentication-oauth-and-partner-applications.md)。

  - 測試使用者必須具備有效的 Exchange 2013 信箱。

在符合這些條件後，系統管理員可執行下列命令，以確定 SIP 位址為 kenmyer@litwareinc.com 的使用者，可從整合連絡人存放區擷取其連絡人：

    Test-CsUnifiedContactStore -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress "sip:kenmyer@litwareinc.com" -RegistrarPort 5061 -Authentication TrustedServer -Setup

請注意用於前述命令中的 Setup 參數的使用方式。若執行 Test-CsUnifiedContactStore 時包含 Setup 參數，則指定的使用者之連絡人 (在此例中為 sip:kenmyer@litwareinc.com)，將移至整合連絡人存放區，(當然，如果使用者的連絡人已經位於整合連絡人存放區中，就無須移動)。通常 Setup 參數僅使用一次 (第一次執行 Test-CsUnifiedContactStore 時)，且僅應配合測試使用者來使用；也就是說，配合不會實際登入 Lync Server 的使用者帳戶使用。在測試使用者轉移到整合連絡人存放區後，您無須使用 Setup 參數，即可藉由呼叫 Test-CsUnifiedContactStore 來驗證能否擷取使用者的連絡人：

    Test-CsUnifiedContactStore -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress "sip:kenmyer@litwareinc.com" -RegistrarPort 5061 -Authentication TrustedServer

## XMPP 綜合交易

使用 XMPP (Extensible Messaging and Presence Protocol，可延伸訊息和目前狀態通訊協定) IM 綜合交易時，需配合一或多個同盟網域來設定 XMPP 功能。

若要啟用 XMPP 綜合交易，須在可路由的 XMPP 網域提供 XmppTestReceiverMailAddress 參數和使用者帳戶。例如：

    Set-CsWatcherNodeConfiguration -Identity pool0.contoso.com -Tests @{Add="XmppIM"} -XmppTestReceiverMailAddress user1@litwareinc.com

在此範例中，需使用 Lync Server 2013 規則，才能將 litwareinc.com 的訊息路由傳送至 XMPP 閘道。

