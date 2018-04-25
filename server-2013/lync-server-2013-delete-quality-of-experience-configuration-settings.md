---
title: 刪除經驗品質組態設定
TOCTitle: 刪除經驗品質組態設定
ms:assetid: fd0c4c2f-3bfb-42cb-9b6a-f0f8d5aa9e81
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182613(v=OCS.15)
ms:contentKeyID: 49292902
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除經驗品質組態設定

 

_**上次修改主題的時間：** 2013-02-23_

「經驗品質」(QoE) 計量追蹤在組織中建立的音訊和視訊撥號品質，包括遺失的網路封包數量、背景雜訊和「抖動」(封包延遲差異) 量。這些計量都會儲存在資料庫中，除了其他資料 (例如詳細通話記錄) 之外，讓您可啟用和停用與其他資料記錄無關的 QoE。

安裝 Microsoft Lync Server 2013 時，會為您建立單一、全域集合的 QoE 組態設定。也有選項公系統管理員建立可套用至個別網站的自訂設定值集合。根據設計，在網站範圍進行的設定優先順序高於在全域範圍進行的設定。

請注意，您也可以「刪除」全域設定。但是，實際上並不會移除全域設定，而是將該集合中的所有屬性重設為預設值。例如，根據預設，是在 QoE 組態設定的集合中啟用永久刪除。假設您修改全域集合以停用永久刪除，則會將所有屬性重設回預設值。在此案例中這表示會再次啟用永久刪除。

您可使用 Lync Server 控制台 或 [Remove-CsQoEConfiguration](remove-csqoeconfiguration.md) Cmdlet 移除 QoE 組態設定。

## 使用 Lync Server 控制台 刪除 QoE 組態設定

1.  以 RTCUniversalServerAdmins 群組成員或者 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 角色成員的身分登入電腦。如需詳細資料，請參閱[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[監控和封存\]，然後按一下 \[經驗品質資料\]。

4.  在原則清單中，按一下您要的原則，再按一下 \[編輯\]，然後按一下 \[刪除\]。

5.  按一下 \[確定\]。

## 使用 Lync Server 管理命令介面 Cmdlet 移除 QoE 組態設定

您也可使用 Lync Server 管理命令介面 與 **Remove-CsQoEConfiguration** Cmdlet 移除 QoE 組態設定 **Remove-CsQoEConfiguration**。您可從 Lync Server 2013 管理命令介面 或 Windows PowerShell 的 如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。 遠端工作階段執行此 Cmdlet。

## 移除 QoE 組態設定的指定集合

  - 此命令會移除套用至 Redmond 網站的 QoE 組態設定：
    
        Remove-CsQoEConfiguration -Identity "site:Redmond"

## 移除套用至網站範圍的所有 QoE 組態設定

  - 此命令會移除套用至網站範圍的 QoE 組態設定：
    
        Get-CsQoEConfiguration -Filter "site:*" | Remove-CsQoEConfiguration

## 移除所有停用 QoE 監控的 QoE 組態設定

  - 此命令會移除所有停用 QoE 監控的 QoE 組態設定：
    
        Get-CsQoEConfiguration | Where-Object {$_.EnableQoE -eq $False} | Remove-CsQoEConfiguration

如需詳細資訊，請參閱[Remove-CsQoEConfiguration](remove-csqoeconfiguration.md)。

