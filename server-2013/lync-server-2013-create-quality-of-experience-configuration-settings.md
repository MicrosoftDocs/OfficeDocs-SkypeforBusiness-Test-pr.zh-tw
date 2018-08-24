---
title: 建立經驗品質的組態設定
TOCTitle: 建立經驗品質的組態設定
ms:assetid: 64f05569-07c7-4f76-a96b-ea4125a510d5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg521006(v=OCS.15)
ms:contentKeyID: 49291135
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 建立經驗品質的組態設定

 

_**上次修改主題的時間：** 2015-03-09_

「經驗品質 (QoE)」計量在追蹤組織中進行之音訊和視訊通話的品質，包括遺失的網路封包數量、背景雜訊和「抖動」(封包延遲差異) 等項目的數量。這些計量會儲存在與其他資料 (例如詳細通話記錄) 不同的資料庫中，讓您可獨立於其他資料記錄來啟用和停用 QoE。

在安裝 Microsoft Lync Server 2013 時，就會建立單一、全域的 QoE 組態設定集合。系統管理員也可以選擇建立網站範圍的自訂設定。只要使用這些網站範圍的設定，其優先順序就高於全域設定。例如，如果為 Redmond 網站建立網站範圍的設定，則會使用這些設定 (而非全域設定) 來管理 Redmond 的 QoE。

可使用 Lync Server 控制台或 [New-CsQoEConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsQoEConfiguration) Cmdlet 來建立 QoE 組態設定。如果使用 Lync Server 控制台來建立新的設定，則可使用下列選項：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>UI 設定</th>
<th>PowerShell 參數</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>名稱</p></td>
<td><p>Identity</p></td>
<td><p>要建立之設定的唯一識別碼。QoE 組態設定僅可在網站範圍內建立。</p></td>
</tr>
<tr class="even">
<td><p>啟用 QoE 資料的監控</p></td>
<td><p>EnableQoE</p></td>
<td><p>指定是否將收集 QoE 記錄並儲存至監控資料庫。</p></td>
</tr>
<tr class="odd">
<td><p>啟用 QoE 資料的清除</p></td>
<td><p>EnablePurging</p></td>
<td><p>指定是否在 <strong>[將 QoE 資料保留最大持續期間 (天)]</strong> 屬性中定義的期間經過之後，將清除記錄。</p></td>
</tr>
<tr class="even">
<td><p>將 QoE 資料保留最大持續期間 (天)</p></td>
<td><p>KeepQoEDataForDays</p></td>
<td><p>QoE 資料從資料庫清除之前將會儲存的天數。如果停用清除，將會忽略此值。</p></td>
</tr>
</tbody>
</table>


> [!NOTE]  
> New-CsQoEConfiguration Cmdlet 包含 Lync Server 控制台中未提供的其他選項。如需詳細資訊，請參閱 <a href="https://docs.microsoft.com/en-us/powershell/module/skype/New-CsQoEConfiguration">New-CsQoEConfiguration</a> 說明主題。



## 使用 Lync Server 控制台建立 QoE 組態設定

1.  以 RTCUniversalServerAdmins 群組成員或者 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 角色成員的身分登入電腦。如需詳細資料，請參閱[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[監控和封存\]**，然後按一下 **\[經驗品質資料\]**。

4.  在 **\[經驗品質資料\]** 頁面上，按一下 **\[新增\]**。

5.  在 **\[選取站台\]** 中，按一下要套用原則的網站，並按一下 **\[確定\]**。

6.  在 **\[新的經驗品質設定\]** 中，執行下列動作：
    
      - 選取 **\[啟用經驗品質 (QoE) 資料的監控\]** 開啟監控功能。
    
      - 選取 **\[啟用經驗品質 (QoE) 資料的清除\]** 開啟清除功能。
    
      - 在 **\[將 QoE 資料保留最大持續期間 (天)\]** 中，選取應該保留 QoE 記錄的最大天數。

7.  按一下 **\[認可\]**。

## 使用 Windows PowerShell Cmdlet 建立 QoE 組態設定

您也可以使用 Windows PowerShell 及 New-CsQoEConfiguration Cmdlet 來建立 QoE 組態設定。您可從 Lync Server 2013 管理命令介面或者從 Windows PowerShell 的遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 建立新的 QoE 組態設定集合

  - 下列命令會建立要套用至 Redmond 網站的新 QoE 組態設定集合：
    
        New-CsQoEConfiguration -Identity "site:Redmond"

## 建立新的 QoE 組態設定集合並停用 QoE 監控

  - 因為上述命令未指定參數 (除了必要的 Identity 參數)，新的組態設定集合會將預設值用於其所有屬性。若要使用不同的屬性值來建立設定，只要包含適當的參數及參數值即可。例如，若要建立預設為允許停用經驗品質記錄之 QoE 組態設定的集合，請使用如下的命令：
    
        New-CsQoEConfiguration -Identity "site:Redmond" -EnableQoE $False

## 建立新的 QoE 組態設定集合時指定多個屬性值

  - 您可藉由包含多個參數來指定多個參數值。例如，下列命令會將新設定架構為將 QoE 資料保留 30 天，並在上午 3:00 清除舊資料：
    
        New-CsQoEConfiguration -Identity "site:Redmond" -KeepQoEDataForDays 30 -PurgeHourOfDay 3

如需詳細資訊，請參閱 [New-CsQoEConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsQoEConfiguration) Cmdlet 的說明主題。

