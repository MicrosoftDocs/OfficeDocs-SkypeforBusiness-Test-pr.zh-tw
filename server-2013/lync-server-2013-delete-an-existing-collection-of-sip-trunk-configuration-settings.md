---
title: 在 Lync Server 2013 中刪除現有的 SIP 主幹組態設定集合
TOCTitle: 在 Lync Server 2013 中刪除現有的 SIP 主幹組態設定集合
ms:assetid: 3b25f14d-884b-42dd-a866-460d276d3e43
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688024(v=OCS.15)
ms:contentKeyID: 49890024
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中刪除現有的 SIP 主幹組態設定集合

 

_**上次修改主題的時間：** 2013-02-22_

SIP 主幹組態設定用於定義中繼伺服器與服務提供者的公用交換電話網路 (PSTN) 閘道、IP 公用交換機 (PBX) 或工作階段邊界控制器 (SBC) 之間的關係和功能。這些設定將指定下列項目：

  - 主幹是否啟用媒體旁路。

  - 傳送即時傳輸控制通訊協定 (RTCP) 封包的情況。

  - 每個主幹是否需要安全即時通訊協定 (SRTP) 加密。

安裝 Microsoft Lync Server 2013 時即會建立 SIP 主幹組態設定的全域集合。此設定的全域集合無法刪除。不過可以使用 Lync Server 控制台或 [Remove-CsTrunkConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsTrunkConfiguration) Cmdlet，將全域集合中的屬性「重設」為預設值。例如，如果已將 Enable3pccRefer 屬性設為 True，則在重設全域集合時，Enable3pccRefer 屬性會還原為預設值 False。

管理員也可建立網站範圍或服務範圍 (針對個別 PSTN 閘道) 的自訂主幹組態設定；這些自訂設定是可移除的。移除這些自訂設定時，請注意下列事項：

  - 如移除服務範圍設定，原先這些設定所管理的 SIP 主幹會由套用網站的設定來管理 (如果存在的話)。如果網站設定不存在，這些主幹將會由主幹組態設定的全域集合來管理。

  - 如移除網站範圍設定，則所有原先這些設定管理的 SIP 主幹將會由主幹組態設定的全域集合來管理。

## 使用 Lync Server 控制台移除主幹組態設定

1.  在 Lync Server 控制台中按一下 **\[語音路由\]**，然後按一下 **\[主幹組態\]**。

2.  在 **\[主幹組態\]** 索引標籤中，選取要刪除的 SIP 主幹組態設定集合，然後按一下 **\[編輯\]**，再按一下 **\[刪除\]**。如要在同一個操作中刪除多個集合，先按一下要刪除的第一個集合，然後按住 Ctrl 鍵，再按一下其他任何要移除的集合。

3.  集合的 **\[狀態\]** 屬性將會更新為 **\[未認可\]**。如要認可變更並刪除集合，請按一下 **\[認可\]**，然後按一下 **\[全部認可\]**。

4.  在 **\[未認可的語音組態設定\]** 對話方塊中，按一下 **\[確定\]**。

5.  在 **\[Microsoft Lync Server 2013 控制台\]** 對話方塊中，按一下 **\[確定\]**。

6.  如果您改變心意決定不要刪除集合，請按一下 **\[認可\]**，然後按一下 **\[取消所有未認可的變更\]**。在顯示 **\[Microsoft Lync Server 2013 控制台\]** 對話方塊時，按一下 **\[確認\]**。

## 使用 Lync Server PowerShell Cmdlet 移除主幹組態設定

也可使用 Windows PowerShell 及 Remove-CsTrunkConfiguration Cmdlet 來刪除主幹組態設定。可從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 移除指定的設定集合

  - 以下命令會移除已套用至 Redmond 網站的主幹組態設定：
    
        Remove-CsTrunkConfiguration -Identity site:Redmond

## 移除所有已套用至網站範圍的集合

  - 以下命令會移除所有已套用至服務範圍的主幹組態設定：
    
        Get-CsTrunkConfiguration -Filter "service:*" | Remove-CsTrunkConfiguration

## 移除所有已啟用媒體旁路的集合

  - 以下命令會移除所有已啟用媒體旁路的主幹組態設定：
    
        Get-CsTrunkConfiguration | Where-Object {$_.EnableBypass -eq $True} | Remove-CsTrunkConfiguration

如需詳細資訊，請參閱 [Remove-CsTrunkConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsTrunkConfiguration) Cmdlet 的說明主題。

