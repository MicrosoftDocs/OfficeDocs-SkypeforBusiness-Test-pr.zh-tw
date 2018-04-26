---
title: 適用於通訊錄管理的 Get-CsService
TOCTitle: 適用於通訊錄管理的 Get-CsService
ms:assetid: 373b717d-5efa-4c36-a899-a23a5bd922b4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg429698(v=OCS.15)
ms:contentKeyID: 49290581
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 適用於通訊錄管理的 Get-CsService

 

_**上次修改主題的時間：** 2012-11-01_

誰可以執行這個 Cmdlet：根據預設，下列群組成員已獲得授權，可在本機執行 Get-CsService Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中輸入下列命令：

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Get-CsService"}

Get-CsService 適合用於擷取和顯示基礎結構目前已定義的 Web 服務設定。在定義集區的完整網域名稱 (FQDN) 和參數 WebServer 後，此 Cmdlet 會傳回伺服器提供的 Web 服務，包括通訊錄處理常式和通訊群組清單延伸 URI。

例如：

    Get-CsService -PoolFqdn "fe01.contoso.net" -WebServer

此 Cmdlet 會傳回下列項目：

Identity :WebServer:pool01.contoso.net

FileStore :FileStore:dc01.contoso.net

UserServer :UserServer:pool01.contoso.net

PrimaryHttpPort :80

PrimaryHttpsPort :443

ExternalHttpPort :8080

ExternalHttpsPort :4443

PublishedPrimaryHttpPort :80

PublishedPrimaryHttpsPort :443

PublishedExternalHttpPort :80

PublishedExternalHttpsPort :443

ReachPrimaryPsomServerPort :8060

ReachExternalPsomServerPort :8061

AppSharingPortStart :49152

AppSharingPortCount :16383

LIServiceInternalUri :https://internalweb.contoso.net/locationinformation/liservice.svc

ABHandlerInternalUri :https://internalweb.contoso.net/abs/handler

ABHandlerExternalUri :https://csweb.contoso.com/abs/handler

DLExpansionInternalUri :https://internalweb.contoso.net/groupexpansion/service.svc

DLExpansionExternalUri :https://csweb.contoso.com/groupexpansion/service.svc

CAHandlerInternalUri :https://internalweb.contoso.net/CertProv/CertProvisioningService.svc

CAHandlerInternalAnonUri :http://internalweb.contoso.net/CertProv/CertProvisioningService.svc

CollabContentInternalUri :https://internalweb.contoso.net/CollabContent

CollabContentExternalUri :https://csweb.contoso.com/CollabContent

CAHandlerExternalUri :https://csweb.contoso.com/CertProv/CertProvisioningService.svc

DeviceUpdateDownloadInternalUri :https://internalweb.contoso.net/RequestHandler/ucdevice.upx

DeviceUpdateDownloadExternalUri :https://csweb.contoso.com/RequestHandlerExt/ucdevice.upx

DeviceUpdateStoreInternalUri :http://internalweb.contoso.net/RequestHandler/Files

DeviceUpdateStoreExternalUri :https://csweb.contoso.com/RequestHandlerExt/Files

RgsAgentServiceInternalUri :https://internalweb.contoso.net/RgsClients/AgentService.svc

RgsAgentServiceExternalUri :https://csweb.contoso.com/RgsClients/AgentService.svc

MeetExternalUri :https://csweb.contoso.com/Meet

DialinExternalUri :https://csweb.contoso.com/Dialin

CscpInternalUri :https://internalweb.contoso.net/Cscp

ReachExternalUri :https://csweb.contoso.com/Reach

ReachInternalUri :https://internalweb.contoso.net/Reach

WebTicketExternalUri :https://csweb.contoso.com/WebTicket/WebTicketService.svc

WebTicketInternalUri :https://internalweb.contoso.net/WebTicket/WebTicketService.svc

ExternalFqdn :csweb.contoso.com

InternalFqdn :internalweb.contoso.net

DependentServiceList :{Registrar:pool01.contoso.net, ConferencingServer:pool01.contoso.net}

ServiceId :1-WebServices-1

SiteId :Site:Redmond

PoolFqdn :pool01.contoso.net

Version :5

Role :WebServer

如需完整命令的詳細說明，請參閱主要 Lync Server Windows PowerShell RTCCmdlets 參考中的下列項目。

## 請參閱

#### 其他資源

[Get-CsService](get-csservice.md)

