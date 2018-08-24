---
title: 在 Lync Server 2013 中測試 SIP 主幹組態設定
TOCTitle: 在 Lync Server 2013 中測試 SIP 主幹組態設定
ms:assetid: c8712308-0e2d-4e39-8f90-d1a250487a94
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721880(v=OCS.15)
ms:contentKeyID: 49890307
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中測試 SIP 主幹組態設定

 

_**上次修改主題的時間：** 2012-11-01_

SIP 主幹組態設定定義了中繼伺服器與公用交換電話網路 (PSTN) 閘道、IP 公用交換機 (PBX) 或是服務提供者處的工作階段界限控制器 (SBC) 之間的關係和功能。這些設定可指定：

  - 是否應在主幹上啟用媒體旁路。

  - 傳送即時傳輸控制通訊協定 (RTCP) 封包的條件。

  - 各個主幹是否需要安全即時通訊協定 (SRTP) 加密。

當您安裝 Microsoft Lync Server 2013 時，系統會為您建立一組全域 SIP 主幹組態設定集合。此外，系統管理員可建立網站範圍或服務範圍 (僅針對 PSTN 閘道服務) 的自訂設定集合。系統管理員也可以使用 Test-CsTrunkConfiguration Cmdlet，確認主幹可以將使用者撥打的號碼轉換成閘道能夠處理的數字。

若要測試主幹組態設定，只能以 Windows PowerShell 和 [Test-CsTrunkConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsTrunkConfiguration) Cmdlet 進行。此 Cmdlet 可以從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 測試主幹組態設定

  - 此命令會確認 Redmond 網站的主幹組態設定可以正確地轉換撥打的號碼 4255551212。
    
        $trunk = Get-CsTrunkConfiguration -Identity "site:Redmond"
        Test-CsTrunkConfiguration -DialedNumber 4255551212 -TrunkConfiguration $trunk

