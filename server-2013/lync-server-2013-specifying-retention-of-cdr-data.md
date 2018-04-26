---
title: 指定保留 CDR 資料
TOCTitle: 指定保留 CDR 資料
ms:assetid: c0fd6056-87bc-4136-902a-f1b37cd3a1ca
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182581(v=OCS.15)
ms:contentKeyID: 49292208
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 指定保留 CDR 資料

 

_**上次修改主題的時間：** 2013-02-23_

根據預設，詳細通話記錄 (CDR) 資料會在 60 天後清除。若要將資料保留更久或更短的時間，可以使用 **\[詳細通話記錄\]** 頁面上的設定。如果停用 CDR，則在啟用 CDR 之前擷取的資料也會遭清除。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您應該將 CDR 和「經驗品質」(QoE) 設定為保留相同天數的資料。通話詳細資料報告 (CDR) (可從監控伺服器報告網頁中取得) 中的每個通話包括 CDR 和 QoE 資訊。如果 CDR 和 QoE 的清除期間不同，則某些通話可能只包含 CDR 資料，某些通話可能只包含 QoE 資料。</td>
</tr>
</tbody>
</table>


使用下列程序可設定 CDR 資料的清除設定。

## 若要指定 CDR 資料的保留

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限) 或指派給 CsServerAdministrator 或 CsAdministrator 角色的使用者帳戶，登入部署 Lync Server 2013 之網路上的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[監控和封存\]**，然後按一下 **\[詳細通話記錄\]**。

4.  在 **\[詳細通話記錄\]** 頁面上，依序按一下表格中的適當網站、**\[編輯\]** 和 **\[顯示詳細資料\]**。

5.  若要開啟清除，請選取 \[啟用 CDR 的清除\]。

6.  在 \[將 CDR 保留最大持續期限 (天):\] 中，選取應該保留詳細通話記錄的最大天數。

7.  在 **\[將錯誤報告資料保留最大持續期限 (天):\]** 中，選取應該保留錯誤報告的最大天數。

8.  按一下 \[認可\]。

## 若要使用 Lync Server 管理命令介面 Cmdlet 指定 CDR 保留

您可以使用 Windows PowerShell 和 Set-CsCdrConfiguration Cmdlet 建立 CDR 保留設定。您可以從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 若要指定特定位置的 CDR 保留

  - 此命令會對 Redmond 網站啟用 CDR 資料的清除，並設定該網站將 CDR 資料和錯誤報告資料都保留 20 天。
    
        Set-CsCdrConfiguration -Identity "site:Redmond" -EnablePurging -KeepCallDetailForDays 20 -KeepErrorReportForDays 20

## 若要指定多個位置的 CDR 保留

  - 此命令會對組織中使用的所有 CDR 組態設定來設定 CDR 保留。
    
        Get-CsCdrConfiguration | Set-CsCdrConfiguration-EnablePurging -KeepCallDetailForDays 20 -KeepErrorReportForDays 20

如需詳細資訊，請參閱 [Set-CsCdrConfiguration](set-cscdrconfiguration.md) Cmdlet 的說明主題。

## 請參閱

#### 其他資源

[Lync Server 2013 中的詳細通話記錄 (CDR)](lync-server-2013-call-detail-recording-cdr.md)

