---
title: 針對 Microsoft Lync Server 2013 Voicemail 設定 Microsoft Exchange Server 2013 Unified Messaging
TOCTitle: 針對 Microsoft Lync Server 2013 Voicemail 設定 Microsoft Exchange Server 2013 Unified Messaging
ms:assetid: 1be9c4f4-fd8e-4d64-9798-f8737b12e2ab
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ687983(v=OCS.15)
ms:contentKeyID: 49889963
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 針對 Microsoft Lync Server 2013 Voicemail 設定 Microsoft Exchange Server 2013 Unified Messaging

 

_**上次修改主題的時間：** 2013-02-04_

Microsoft Lync Server 2013 可讓您將語音留言儲存在 Microsoft Exchange Server 2013 中，且這些語音留言之後可以在使用者的收件匣中顯示為電子郵件訊息。在 2010 版本的 Lync Server 和 Exchange 中都具備這項功能，不過，在 2013 版本中，由於引進了 UM 通話路由器元件，因此大幅簡化了「整合通訊」的設定程序。此元件是安裝在 Exchange 2013 Client Access Server 上，所有傳送至 Exchange 整合通訊的通話 (如語音留言) 都會先路由傳送至通話路由器，然後才會重新導向適當的信箱伺服器。

若您已設定好 Lync Server 2013 和 Exchange 2013 之間的伺服器對伺服器驗證，您就可以開始設定整合通訊了。若要進行這項作業，您必須先在 Exchange 伺服器上建立並指派新的整合通訊撥號對應表。例如，下列兩個命令 (從 Exchange 管理命令介面執行) 可設定新的 Exchange 3 位數撥號對應表：

    New-UMDialPlan -Name "RedmondDialPlan" -VoIPSecurity "Secured" -NumberOfDigitsInExtension 3 -URIType "SipName" -CountryOrRegionCode 1
    Set-UMDialPlan "RedmondDialPlan" -ConfiguredInCountryOrRegionGroups "Anywhere,*,*,*" -AllowedInCountryOrRegionGroups "Anywhere"

在上述範例的第一個命令中，VoIPSecurity 參數和參數值 "Secured" 指出信號通道是使用傳輸層安全性 (TLS) 來加密的。URIType "SipName" 指出會使用 SIP 通訊協定來傳送和接收訊息，而 CountryOrRegionCode 的 1 則指出撥號對應表是套用至美國。

在第二個命令中，傳送至 ConfiguredInCountryOrRegionGroups 參數的參數值指定了可使用此撥號對應表的的國內群組。參數值 "Anywhere,\*,\*,\*" 可設定下列項目：

  - 群組名稱 ("Anywhere")

  - AllowedNumberString (\*, 萬用字元表示可允許任何號碼字串)

  - DialNumberString (\*, 萬用字元表示可允許任何撥號)

  - TextComment (\*, 萬用字元表示可允許任何文字命令)

建立並設定新的撥號對應表之後，您必須將新的撥號對應表新增至整合通訊伺服器，然後修改該伺服器的啟動模式；明確地說，您必須將啟動模式設定為「雙重」模式。您可從 Exchange 管理命令介面來執行這兩項工作：

    Set-UmServer -Identity "atl-exchangeum-001.litwareinc.com" -DialPlans "RedmondDialPlan" -UMStartupMode "Dual"

設定好整合通訊伺服器之後，您接下來應該執行 Enable-ExchangeCertificate Cmdlet 以確認 Exchange 憑證有套用至整合通訊服務：

    Enable-ExchangeCertificate -Server "atl-umserver-001.litwareinc.com" -Thumbprint "EA5A332496CC05DA69B75B66111C0F78A110D22d" -Services "SMTP","IIS","UM"

正確指派憑證之後，您就必須停止並重新啟動整合通訊伺服器上的 MsExchangeUM 服務。每當您變更啟動模式時，都必須停止並重新啟動此服務。

完成整合通訊伺服器的設定之後，您就可以開始設定 UM 通話路由器：

    Set-CsUMCallRouterSettings -Server "atl-exchange-001.litwareinc.com" -UMStartupMode "Dual" -DialPlans "RedmondDialPlan" 
    Enable-ExchangeCertificate -Server "atl-umserver-001.litwareinc.com" -Thumbprint "45BAA32496CC891169B75B9811320F78A1075DDA" -Services "IIS","UMCallRouter"

由於啟動模式已變更，因此您必須停止並重新啟動主控 UM 通話路由器之電腦上的 MsExchangeUMCR 服務。

若要完成整合通訊設定，您還需要建立 UM 信箱原則，然後使用該原則來啟用使用者的整合通訊。您可使用類似下列的命令，來建立信箱原則：

    New-UMMailboxPolicy -ID "RedmondMailboxPolicy" -AllowedCountryOrRegionGroups "Anywhere"

您可使用類似下列的命令，來啟用使用者的整合通訊：

    Enable-UMMailbox -Extensions 100 -SIPResourceIdentifier "kenmyer@litwareinc.com" -Identity "litwareinc\kenmyer" -UMMailboxPolicy "RedmondMailboxPolicy"

在上一個命令中，Extensions 參數代表使用者的電話分機號碼。在此範例中，使用者的分機號碼為 100。

啟用 kenmyer@litwareinc.com 的信箱後，該使用者應該就能使用 Exchange 整合通訊。您可從 Lync Server 管理命令介面執行 [Test-CsExUMConnectivity](https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsExUMConnectivity) Cmdlet，以驗證使用者是否能連線至 Exchange UM：

    $credential = Get-Credential "litwareinc\kenmyer"
    
    Test-CsExUMConnectivity -TargetFqdn "atl-cs-001.litwareinc.com" -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $credential

若您還有第二個啟用了整合通訊的使用者，您可使用 [Test-CsExUMVoiceMail](test-csexumvoicemail.md) Cmdlet 來驗證第二個使用者是否能語音留言給第一個使用者。

    $credential = Get-Credential "litwareinc\pilar"
    
    Test-CsExUMVoiceMail -TargetFqdn "atl-cs-001.litwareinc.com" -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $credential

