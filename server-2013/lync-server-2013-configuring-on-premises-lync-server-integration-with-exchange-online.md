---
title: Lync Server 2013：設定內部部署 Lync Server 與 Exchange Online 整合
TOCTitle: 設定內部部署 Lync Server 2013 與 Exchange Online 整合
ms:assetid: 95a20117-2064-43c4-94fe-cac892cadb6f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh533880(v=OCS.15)
ms:contentKeyID: 49291715
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定內部部署 Lync Server 2013 與 Exchange Online 整合

 

_**上次修改主題的時間：** 2014-07-02_

使用內部部署的 Lync Server 2013 部署的客戶，可以在混合部署模式中，設定與 Microsoft Exchange Online 之 Microsoft Outlook Web App 的互通性。互通性功能包含單一登入，以及與 Outlook Web App 介面的立即訊息 (IM) 和目前狀態整合。若要啟用此整合，您必須完成下列工作，在內部部署的 Lync Server 部署中設定 Edge Server：

  - 設定共用 SIP 位址空間

  - 在 Edge Server 上設定裝載提供者

  - 確認複寫已更新的 中央管理存放區

## 設定共用 SIP 位址空間

若要整合內部部署的 Lync Server 2013 與 Exchange Online，您必須設定共用的 SIP 位址空間。 Lync Server 和 Exchange Online 服務支援相同的 SIP 網域位址空間。

您可以使用 Lync Server 管理命令介面來設定 Edge Server 進行同盟，方法是使用下列範例中所示的參數來執行 **Set-CSAccessEdgeConfiguration** Cmdlet：

    Set-CsAccessEdgeConfiguration -AllowFederatedUsers $True

  - **AllowFederatedUsers** 參數指定是否允許內部使用者與同盟網域的使用者進行通訊。此屬性也會判斷內部使用者是否可以透過 Lync Server 和 Exchange Online 與共用 SIP 位址空間案例中的使用者進行通訊。

如需使用 Lync Server 管理命令介面的詳細資訊，請參閱＜ [Lync Server 管理命令介面](lync-server-2013-lync-server-management-shell.md)＞。

## 在 Edge Server 上設定裝載提供者

您可以使用 Lync Server 管理命令介面在 Edge Server 上設定裝載提供者，方法是使用下列範例中的參數來執行 **New-CsHostingProvider** Cmdlet：

    New-CsHostingProvider -Identity "Exchange Online" -Enabled $True -EnabledSharedAddressSpace $True -HostsOCSUsers $False -ProxyFqdn "exap.um.outlook.com" -IsLocal $False -VerificationLevel UseSourceVerification

> [!NOTE]  
> 如果您正在使用中國的 21Vianet 所營運的 Office 365，請使用 21Vianet 所營運之服務的 FQDN (&quot;exap.um.partner.outlook.cn&quot;)，取代此範例中 <strong>ProxyFqdn</strong> 參數的值 (&quot;exap.um.outlook.com&quot;)。



  - **Identity** 可為所建立的裝載提供者指定唯一的字串值識別碼 (例如 "Exchange Online" )。您必須以雙引號括住內含空格的值。

  - **Enabled** 指出網域與裝載提供者之間的網路連線是否已啟用。此值必須設定為 True。

  - **EnabledSharedAddressSpace** 指出是否將在共用 SIP 位址空間案例中使用裝載提供者。此值必須設定為 True。

  - **HostsOCSUsers** 指出裝載提供者用於裝載 Office Communications Server 或 Lync Server。此值必須設定為 False。

  - **ProxyFQDN** 指定裝載提供者所使用之 Proxy 伺服器的完整網域名稱 (FQDN)。若是 Exchange Online，FQDN 為 exap.um.outlook.com。

  - **IsLocal** 指出裝載提供者使用的 Proxy 伺服器是否包含在您的 Lync Server 拓撲內。此值必須設定為 False。

  - **VerificationLevel** 指出傳送至裝載提供者或從裝載提供者發出之訊息的允許驗證層級。指定 **UseSourceVerification**，其依賴包含在裝載提供者發出之訊息內的驗證層級。如果沒有指定這個層級，訊息會視為無法驗證而被拒絕。

## 確認複寫已更新的中央管理存放區

您在前幾節中使用 Cmdlet 所做的變更會自動套用至 Edge Server，且複寫時間通常不到一分鐘。您可以使用下列 Cmdlet 來驗證複寫狀態，然後確認變更是否已套用至 Edge Server。

若要驗證複寫狀態，請在 Lync Server 部署的內部伺服器上，執行下列 Cmdlet：

    Get-CsManagementStoreReplicationStatus

若要確認是否已套用變更，請在 Edge Server 上執行下列 Cmdlet：

    Get-CsHostingProvider -LocalStore

## 請參閱

#### 其他資源

[在主控 Exchange UM 上提供 Lync Server 2013 使用者語音信箱](lync-server-2013-providing-lync-server-users-voice-mail-on-hosted-exchange-um.md)  
[Lync Server 2013 中的主控 Exchange 整合通訊整合](lync-server-2013-hosted-exchange-unified-messaging-integration.md)

