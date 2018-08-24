---
title: 修改經驗品質設定
TOCTitle: 修改經驗品質設定
ms:assetid: a6b41de2-1466-4240-8a70-14ce6f0f3ddc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182563(v=OCS.15)
ms:contentKeyID: 49291914
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 修改經驗品質設定

 

_**上次修改主題的時間：** 2013-02-23_

根據預設，經驗品質 (QoE) 資料會在 60 天後清除。若要將資料保留更久或更短的時間，可以使用 **\[經驗品質資料\]** 頁面上的設定。如果停用 QoE，則在啟用 QoE 之前擷取的資料也會遭清除。

> [!NOTE]  
> 您應該將詳細通話記錄 (CDR) 和 QoE 設定為保留相同天數的資料。通話詳細資料報告 (CDR) (可從 [監控報告] 首頁取得) 中的每個通話包括 CDR 和 QoE 資訊。如果 CDR 和 QoE 的清除期間不同，則某些通話可能只包含 CDR 資料，某些通話可能只包含 QoE 資料。



下列程序描述如何設定 QoE 資料的清除設定。

## 使用 Lync Server 控制台指定 QoE 資料的保留

1.  以 RTCUniversalServerAdmins 群組成員或者 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 角色成員的身分登入電腦。如需詳細資料，請參閱[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[監控和封存\]，然後按一下 \[經驗品質資料\]。

4.  在 **\[經驗品質資料\]** 頁面上，依序按一下表格中的適當網站、**\[編輯\]** 和 **\[顯示詳細資料\]**。

5.  若要開啟清除，請選取 \[啟用 QoE 的清除\]。

6.  在 \[將 QoE 保留最大持續期限 (天)\] 中，選取應該保留 QoE 資料的最大天數。

7.  按一下 \[認可\]。

## 使用 Windows PowerShell Cmdlet 指定 QoE 保留

您可以使用 Windows PowerShell 和 **Set-CsQoEConfiguration** Cmdlet 建立 QoE 保留設定。您可以從 Lync Server 2013 管理命令介面 或從 Windows PowerShell 的遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 指定特定位置的 QoE 保留

  - 此命令能夠清除 Redmond 網站的 QoE 資料，並將此網站設定成保留 QoE 資料 20 天。
    
        Set-CsQoeConfiguration -Identity "site:Redmond" -EnablePurging -KeepQoEDataForDays 20

## 指定多個位置的 QoE 保留

  - 此命令可為組織中使用的所有 QoE 組態設定進行 QoE 保留設定。
    
        Get-CsQoEConfiguration | Set-CsQoEConfiguration-EnablePurging -KeepQoEDataForDays 20 

如需詳細資訊，請參閱 [Set-CsQoEConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsQoEConfiguration) Cmdlet 的說明主題。

## 請參閱

#### 其他資源

[在 Lync Server 2013 中部署監控](lync-server-2013-deploying-monitoring.md)

