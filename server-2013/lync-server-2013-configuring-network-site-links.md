---
title: 設定網路站台連結
TOCTitle: 設定網路站台連結
ms:assetid: 7e9147ae-e727-46c8-8c1a-6c13201f09be
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg521023(v=OCS.15)
ms:contentKeyID: 49291454
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定網路站台連結

 

_**上次修改主題的時間：** 2012-11-01_

在通話許可控制 (CAC) 組態中，您可以建立網路網站間原則以定義直接連結的網站之間的頻寬限制。當網路網站共用直接連結時，您可以定義這兩個網站之間音訊與視訊連線的頻寬限制。您無法以 Lync Server 控制台 來設定網路網站原則，而只能從 Lync Server 管理命令介面使用 Cmdlet 加以設定。您可以使用 Lync Server 管理命令介面來建立、修改及移除網路網站連結 (也稱為網路網站間原則)。

## 若要建立網路網站連結

1.  以 RTCUniversalServerAdmins 群組成員身分或使用[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)中描述的必要使用者權限，登入裝有 Lync Server 管理命令介面的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  在命令提示字元中輸入下列命令，其中的值換成您組態適用的有效值：
    
        New-CsNetworkInterSitePolicy -Identity Reno_Portland -NetworkSiteID1 Reno -NetworkSiteID2 Portland -BWPolicyProfileID LowBWLimits
    
    此範例會建立名為 Reno\_Portland 的新網路網站連結，設定 Reno 與 Portland 這兩個網路網站間的頻寬限制。網路網站與頻寬原則設定檔在執行此命令前即必須存在。

如需參數說明的詳細資訊，請參閱 Lync Server 管理命令介面文件中的 [New-CsNetworkInterSitePolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsNetworkInterSitePolicy)。若要擷取可套用至網路網站連結之頻寬原則設定檔的清單，請呼叫 **Get-CsNetworkBandwidthPolicyProfile** Cmdlet。如需詳細資訊，請參閱 Lync Server 管理命令介面文件中的 [Get-CsNetworkBandwidthPolicyProfile](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkBandwidthPolicyProfile)。

## 若要修改網路網站連結

1.  以 RTCUniversalServerAdmins 群組成員身分或使用[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)中描述的必要使用者權限，登入裝有 Lync Server 管理命令介面的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  使用 **Set-CsNetworkInterSitePolicy** Cmdlet 來修改某個網路網站連結的內容。您可以修改相連網站的其中一端網站 (或兩端網站都修改)，並且可以修改與連結相關聯的頻寬原則設定檔。以下範例將說明如何修改網站連結 Reno\_Portland 的頻寬原則設定檔：
    
        Set-CsNetworkInterSitePolicy -Identity Reno_Portland -BWPolicyProfileID HighBWLimits

如需參數說明的詳細資訊，請參閱 Lync Server 管理命令介面文件中的 [Set-CsNetworkInterSitePolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsNetworkInterSitePolicy)。

## 若要刪除網路網站連結

1.  以 RTCUniversalServerAdmins 群組成員身分或使用[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)中描述的必要使用者權限，登入裝有 Lync Server 管理命令介面的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  使用 **Remove-CsNetworkInterSitePolicy** Cmdlet 來移除網路網站連結。下列範例會刪除 Reno\_Portland 網路網站連結：
    
        Remove-CsNetworkInterSitePolicy -Identity Reno_Portland

如需參數說明的詳細資訊，請參閱 Lync Server 管理命令介面文件中的 [Remove-CsNetworkInterSitePolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsNetworkInterSitePolicy)。

## 請參閱

#### 概念

[通話許可控制 Cmdlet](https://docs.microsoft.com/en-us/powershell/module/skype/)  

#### 其他資源

[New-CsNetworkInterSitePolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsNetworkInterSitePolicy)  
[Set-CsNetworkInterSitePolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsNetworkInterSitePolicy)  
[Remove-CsNetworkInterSitePolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsNetworkInterSitePolicy)  
[Get-CsNetworkInterSitePolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkInterSitePolicy)  
[Get-CsNetworkBandwidthPolicyProfile](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkBandwidthPolicyProfile)

