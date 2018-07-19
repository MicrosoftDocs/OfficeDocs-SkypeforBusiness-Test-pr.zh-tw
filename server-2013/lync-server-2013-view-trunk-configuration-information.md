---
title: 檢視 Lync Server 2013 中的主幹設定資訊
TOCTitle: 檢視 Lync Server 2013 中的主幹設定資訊
ms:assetid: ebe10e14-08c2-4797-9254-9ed89516d5cd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721927(v=OCS.15)
ms:contentKeyID: 49890373
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視 Lync Server 2013 中的主幹設定資訊

 

_**上次修改主題的時間：** 2013-02-22_

SIP 主幹組態設定定義了中繼伺服器與服務提供者的公用交換電話網路 (PSTN) 閘道、IP 公用交換機 (PBX) 或工作階段界限控制器 (SBC) 之間的關係和功能。這些設定的功能如下所述：

  - 主幹的媒體旁路是否該啟用。

  - 已傳送該即時傳輸控制通訊協定 (RTCP) 封包下的條件。

  - 不論每個主幹是否需要安全即時通訊協定 (SRTP) 加密。

安裝 Microsoft Lync Server 2013 時，系統會建立 SIP 主幹組態設定值的全域集合。此外，管理員可在網站範圍或服務範圍建立自訂設定集合 (僅適用於 PSTN 閘道服務)。

## 使用 Lync Server 控制台檢視 SIP 主幹組態資訊

1.  在 Lync Server 控制台中，依序按一下 \[語音路由\]、\[主幹組態\]。

2.  在 \[主幹組態\] 索引標籤上可看到主幹組態設定值集合清單；每個集合您會看到各項值，例如 \[名稱\]、\[範圍\]、\[狀態\] 與 \[媒體旁路\] 屬性，以及與集合相關的各項數量，包括 \[PSTN 使用方式\]、\[來電號碼規則\] 與 \[撥打的號碼規則\]。如需主幹組態設定值集合的其他相關資訊，請按一下興趣集合，然後依序按一下 \[編輯\]、\[顯示詳細資料\]。請注意，您一次只能檢視一個主幹組態設定值集合的詳細資訊。

## 使用 Lync Server PowerShell Cmdlet 檢視 SIP 主幹組態資訊

要檢視 SIP 主幹組態設定值，也可使用 Lync Server PowerShell 與 Get-CsTrunkConfiguration Cmdlet。此 Cmdlet 可從 Lync Server 2013 管理命令介面或遠端工作階段 Windows PowerShell 執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 檢視 SIP 主幹組態資訊

  - 要檢視所有 SIP 主幹組態設定值的相關資訊，請在 Lync Server 管理命令介面輸入下列令命，然後按下 ENTER：
    
        Get-CsTrunkConfiguration
    
    這樣會傳回類似下列的資訊：
    
        Identity                                  : Global
        OutboundTranslationRulesList              : {}
        SipResponseCodeTranslationRulesList       : {}
        OutboundCallingNumberTranslationRulesList : {}
        PstnUsages                                : {}
        Description                               :
        ConcentratedTopology                      : True
        EnableBypass                              : False
        EnableMobileTrunkSupport                  : False
        EnableReferSupport                        : True
        EnableSessionTimer                        : False
        EnableSignalBoost                         : False
        MaxEarlyDialogs                           : 20
        RemovePlusFromUri                         : False
        RTCPActiveCalls                           : True
        RTCPCallsOnHold                           : True
        SRTPMode                                  : Required
        EnablePIDFLOSupport                       : False
        EnableRTPLatching                         : False
        EnableOnlineVoice                         : False
        ForwardCallHistory                        : False
        Enable3pccRefer                           : False
        ForwardPAI                                : False
        EnableFastFailoverTimer                   : True

如需詳細資訊，請參閱 [Get-CsTrunkConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsTrunkConfiguration) Cmdlet 的說明主題。

