---
title: 整合 Microsoft Lync Server 2013 與 Microsoft Outlook Web App 2013
TOCTitle: 整合 Microsoft Lync Server 2013 與 Microsoft Outlook Web App 2013
ms:assetid: 513d4cc7-aa87-4f68-b99d-d58b63bdf242
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688055(v=OCS.15)
ms:contentKeyID: 49890064
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 整合 Microsoft Lync Server 2013 與 Microsoft Outlook Web App 2013

 

_**上次修改主題的時間：** 2013-02-03_

除了與 Microsoft Outlook 2013 整合，Microsoft Lync Server 2013 也可以與 Microsoft Outlook Web App 2013 完全整合；此外，還將立即訊息和目前狀態新增至 Outlook Web App，讓您的整合連絡人清單可在 Outlook Web App 和 Microsoft Lync 2013 之間共用。為了與 Lync Server 2013 和 Outlook Web App 整合，您必須先確認 Unified Communications Managed API 4.0 Runtime 已安裝在您的 Microsoft Exchange Server 2013 後端伺服器中，方法是尋找下列登錄值是否存在：

HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\MSExchange OWA\\InstantMessaging\\ImplementationDLLPath

ImplementationDLLPath 應指向 Microsoft.Rtc.Internal.Ucweb.dll 檔案的資料夾位置。如果沒有，或如果登錄值不存在，則您應該從 Microsoft 下載中心下載並安裝 UCMA Runtime 安裝程式，網址為 <http://www.microsoft.com/zh-tw/download/details.aspx?id=34992>。在同一網頁上可找到如何安裝 UCMA Runtime 的資訊。

**回溯相容性**

Lync Server 2013 可與整合通訊和 Outlook Web App 兩者的 Microsoft Exchange Server 2010 版本整合。如需詳細資訊，請參閱＜部署內部部署 Exchange UM 以提供 Lync Server 2010 語音信箱＞一文，網址為 [http://technet.microsoft.com/zh-tw/library/gg398768.aspx](lync-server-2013-deploying-on-premises-exchange-um-to-provide-lync-server-2013-voice-mail.md)。如果與 Exchange 2010 整合，則將不會有 Lync Server 特定功能，如整合連絡人存放區和 Lync 至 Exchange 封存。

Microsoft Lync 2013 也可與 Exchange 2010 和 Outlook 2010 搭配使用。不過，同樣地，Lync 2013 使用者將無法使用如整合連絡人存放區和高解析度相片等新功能。這些新功能同時需要 Lync Server 2013 和 Exchange 2013。

**針對 Outlook Web App 建立信任的應用程式集區**

如果您已在同一部電腦上安裝 Microsoft Exchange 整合通訊通話路由器服務和 Microsoft Exchange 整合通訊服務，則無需針對 Outlook Web App 建立信任的應用程式集區。(這是假設討論中的伺服器有裝載 SipName UM 撥號對應表。) 如果您使用單一電腦裝載這兩項服務，則可跳至本文中標題為＜**在 Outlook Web App 上啟用立即訊息**＞一節。

Lync Server 2013 可以自動探索任何裝載 SipName UN 撥號對應表的 Exchange 伺服器；這些伺服器會自動新增至 Lync Server 已知伺服器清單。您不需要建立信任的應用程式集區，並且將這些伺服器新增至已知伺服器清單。事實上，這麼做會造成 Outlook Web App 整合停止運作。

> [!NOTE]  
> 這是因為現在 Lync Server 拓撲對同一部電腦將會有兩個項目︰自動探索的項目和手動新增的項目。如果要解決這個問題，使得 Outlook Web App 能再次運作，則可使用 Windows PowerShell 移除伺服器的信任集區和信任應用程式項目。如需詳細資訊，請參閱＜<a href="https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsTrustedApplicationPool">Remove-CsTrustedApplicationPool</a>＞和＜<a href="https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsTrustedApplication">Remove-CsTrustedApplication</a>＞ Cmdlet 的說明主題。



如果這兩項服務在不同的電腦上執行，則在確認已安裝 Unified Communications Managed API 4.0 Runtime 之後，接著必須建立 Lync Server 信任應用程式集區以及與 Outlook Web App 關聯的信任應用程式；如此會將伺服器新增至已知伺服器清單。如果要這樣做，請首先在 Lync Server 管理命令介面中執行類似下列的命令：

    New-CsTrustedApplicationPool -Identity atl-owa-001.litwareinc.com -Registrar atl-cs-001.litwareinc.com -Site Redmond -RequiresReplication $False

在上述命令中，atl-owa-001.litwareinc.com 是 Outlook Web App 集區的完整網域名稱；它必須是出現在提供存取 Outlook Web App 之憑證的「主體名稱」和「主體替代名稱 (SAN)」欄位中的同一個名稱。同樣地，atl-cs-001.litwareinc.com 是將主控新的信任應用程式集區之 Lync Server 2013 集區的完整網域名稱。同時要注意的是，指定的網站 Redmond 代表 Lync Server 網站的 SiteID。SiteID 不必與網站的 DisplayName 相同；您可以從 Lync Server 管理命令介面執行下列命令，以擷取 Lync Server 網站的 SiteID：

    Get-CsSite | Select-Object DisplayName, SiteID

在建立信任的應用程式集區之後，請使用類似下列的命令來設定應用程式識別碼和 Outlook Web App 的連接埠：

    New-CsTrustedApplication -ApplicationId OutlookWebApp -TrustedApplicationPoolFqdn atl-owa-001.litwareinc.com  -Port 5199

在上述命令中，ApplicationID 只是用於分辨信任的應用程式的易記識別碼。ApplicationID 可以是任何文字字串，不包括空格或其他禁止的字元 (為了確保您建立的是有效識別碼，建議您在指定 ApplicationId 時只使用字母和數字)。指派給 Port 參數的值也是留待系統管理員決定：可以是任何可用的網路連接埠。

在建立信任的應用程式之後，您必須執行下列命令以啟用您的 Lync Server 拓樸的變更：

    Enable-CsTopology

請注意，您必須也將 Exchange 用戶端存取和信箱伺服器新增至所有的 SIP Uri 撥號對應表。這接著會以 Lync Server 的 ExUmRouting 拓撲，將伺服器設定為信任的 SIP 對等。

**在 Outlook Web App 上啟用立即訊息**

正確設定 Lync Server 之後，您就可以開始設定 Outlook Web App。此程序中的第一步是在前端伺服器的所有 Outlook Web App 虛擬目錄上啟用立即訊息。(不需要在後端伺服器的虛擬目錄上啟用立即訊息。事實上，建議您不要在後端伺服器上啟用立即訊息。) 您可以從 Exchange 管理命令介面內執行下列命令，以在用戶端存取伺服器上啟用立即訊息：

    Get-OwaVirtualDirectory | Set-OwaVirtualDirectory -InstantMessagingEnabled $True -InstantMessagingType OCS

> [!NOTE]  
> 當您安裝 Outlook Web App 時，預設為啟用立即訊息；也就是說，InstantMessagingEnabled 屬性會設為 True。不過，您還是必須執行上述命令，以將立即訊息類型設為 OCS。InstantMessagingType 預設是設為 None。



接下來，您必須新增下列兩行至 Outlook Web App 的 Web.config 檔案 (此檔案通常位於資料夾 C:\\Program Files\\Microsoft\\Exchange Server\\V15\\ClientAccess\\Owa 中)。這兩行應該新增在 Web.config 檔案的 \<AppSettings\> 節點下，而且此程序只應在已安裝 Outlook Web App 的後端伺服器上執行：

    <add key="IMCertificateThumbprint" value="EA5A332496CC05DA69B75B66111C0F78A110D22d"/>
    <add key="IMServerName" value="atl-cs-001.litwareinc.com"/>

在上述範例中，IMCertificateThumbprint 的值必須是安裝在後端伺服器上 Exchange 2013 憑證的指紋。您可以從 Exchange 管理命令介面執行下列命令，以擷取該資訊：

    Get-ExchangeCertificate

同時要注意的是，指派給 IMServerName 的值必須是您針對 Outlook Web App 建立信任應用程式集區所在之 Lync Server 集區的完整網域名稱，

用於 Outlook Web App 的憑證必須是 Lync Server 信任的憑證。 要確保憑證會受到 Lync Server 和 Exchange 兩者信任的一個方法是，使用內部憑證授權單位在信箱伺服器上建立憑證，並確認該伺服器 FQDN 用於主體名稱，且此 FQDN 顯示在憑證替代名稱欄位中。憑證在建立後即可匯入後端伺服器。因此，同一個憑證會用於兩個用途︰1) Exchange 整合通訊和 Lync Server 之間的通訊；以及，2) Outlook Web App 和 Lync Server 之間的整合。

在更新 Web.config 檔案之後，您應該接著在 Exchange 後端伺服器上執行下列命令，以便回收 Outlook Web App 集區：

    C:\Windows\System32\Inetsrv\Appcmd.exe recycle apppool /apppool.name:"MSExchangeOWAAppPool"

如果回收作業成功，您會在 Exchange Management Shell 中看到下列訊息：

    "MSExchangeOWAAppPool" successfully recycled

**設定 Outlook Web App 信箱原則**

您可以在此時使用下列命令，針對適當的 Outlook Web App 信箱原則 (一或多個原則) 設定立即訊息。例如，在其中一部信箱伺服器上執行此命令會針對 Deafult 原則啟用立即訊息：

    Set-OwaMailboxPolicy -Identity "Default" -InstantMessagingEnabled $True -InstantMessagingType "OCS"

而此命令會為您所有 Outlook Web App 信箱原則啟用立即訊息：

    Get-OwaMailboxPolicy | Set-OwaMailboxPolicy -InstantMessagingEnabled $True -InstantMessagingType "OCS"

在啟用信箱原則之後，所有由該原則管理的使用者都將會擁有 Lync Server 和 Outlook Web App 的完全整合，但條件如下：

  - 使用者在 Exchange 2013 上有信箱。

  - 已為使用者啟用 Lync Server 2013。

  - 使用者有有效的 SIP Proxy 位址。

**在 Outlook Web App 中停用立即訊息**

如先前所述，Outlook Web App 預設會啟用立即訊息。這表示說，如果不將 Outlook Web App 與 Lync Server 整合，使用者每次登入 Outlook Web App 時都會看到空白的目前狀態圖示和錯誤訊息。如果要避免發生此問題，請使用下列 Exchange 管理命令介面命令，在 Outlook Web App 中停用立即訊息︰

    Get-OwaVirtualDirectory | Set-OwaVirtualDirectory -InstantMessagingEnabled $False

**驗證與 Outlook Web App 的整合**

如果要驗證立即訊息和目前狀態已與 Outlook Web App 整合，請登入 Outlook Web App 2013。在畫面的右上角會看到您的 Exchange 顯示名稱。如果該名稱旁邊顯示目前狀態圖示 (例如，表示您目前狀態為線上的綠色圖示)，這表示已成功整合 Lync Server 和 Outlook Web App。

在首次登入 Outlook Web App 之後，請檢查信箱伺服器上的事件記錄檔是否寫入事件識別碼為 112 (且來源為 MSExchange OWA) 的事件。此事件表示已成功初始化 Instant Messaging Endpoint Manager。如果立即訊息似乎無法運作，則請在信箱伺服器上的 C:\\Program Files\\Microsoft\\Exchange server\\V15\\Logging\\OWA\\InstantMessaging 資料夾中尋找記錄檔。如果不存在 Logging 或 InstantMessaging 資料夾，則表示整合失敗。在此情況下，您可以在 Lync Server 上使用 SIPStack 追蹤 (所有層級和所有旗標)，嘗試判斷整合失敗的原因。

