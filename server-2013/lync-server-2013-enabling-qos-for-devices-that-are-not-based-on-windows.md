---
title: 針對非 Windows 型裝置啟用 QoS
TOCTitle: 針對非 Windows 型裝置啟用 QoS
ms:assetid: 26f793df-aef8-4028-9e3b-6c2c37ea61b9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204750(v=OCS.15)
ms:contentKeyID: 49290386
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 針對非 Windows 型裝置啟用 QoS

 

_**上次修改主題的時間：** 2012-11-01_

當您安裝 Microsoft Lync Server 2013 時，若是使用非 Windows 作業系統之組織，將不會在其使用的所有裝置上啟用服務品質 (QoS)。您可以從 Lync Server 2013 管理命令介面中執行下列命令，以針對此進行確認：

    Get-CsMediaConfiguration

假設您已對媒體組態設定執行變更，就應該會得到類似下列的資訊：

    Identity                          : Global
    EnableQoS                         : False
    EncryptionLevel                   : RequireEncryption
    EnableSiren                       : False
    MaxVideoRateAllowed               : VGA600K
    EnableG722StereoCodec             : True
    EnableH264Codec                   : True
    EnableAdaptiveBandwidthEstimation : True

若 EnableQoS 屬性設為 False (如同先前的輸出)，表示沒有在使用非 Windows 作業系統的電腦及裝置上啟用服務品質。根據預設會為 Lync Phone Edition 裝置啟用 QoS；但無法停用 Lync Phone Edition 的服務品質。

若要啟用全域範圍的服務品質，請從 Lync Server 管理命令介面中執行下列命令：

    Set-CsMediaConfiguration -EnableQoS $True

先前的命令會啟用全域範圍的 QoS；但需要注意的是，媒體組態設定也會套用至網站範圍。若您要為網站啟用服務品質，就必須在呼叫 Set-CsMediaConfiguration 時包含組態設定的識別。例如，此命令會啟用 Redmond 網站的 QoS：

    Set-CsMediaConfiguration -Identity site:Redmond -EnableQoS $True

> [!NOTE]  
> 您是否需要啟用網站範圍的 QoS？答案是不一定。指派至網站範圍的設定會優先於指派至全域範圍的設定。假設您已啟用全域範圍的 QoS，但停用網站範圍的 QoS (針對 Redmond 網站)。則在此情況中，會因為網站設定優先，而停用 Redmond 網站的服務品質。若要啟用 Redmond 網站的 QoS，就必須使用會套用至網站的媒體組態設定。



若您想要同時啟用所有媒體組態設定 (不論範圍為何) 的 QoS，請從 Lync Server 管理命令介面中執行此命令：

    Get-CsMediaConfiguration | Set-CsMediaConfiguration -EnableQoS $True

您可以藉由將 EnableQoS 屬性的值設為 False，為使用非 Windows 作業系統的裝置停用 QoS。例如：

    Set-CsMediaConfiguration -Identity site:Redmond -EnableQoS $False

這使您能夠在網路的某些部分停用服務品質的同時，於網路的其他部分啟用 QoS (例如在 Redmond 網站上)。

您僅能使用 Lync Server 管理命令介面啟用及停用 QoS。Lync Server 控制台中並不提供這些選項。

