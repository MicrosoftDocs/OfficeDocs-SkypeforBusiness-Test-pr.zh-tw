---
title: 刪除工作流程
TOCTitle: 刪除工作流程
ms:assetid: 0469a6b8-ce1e-459b-bc3d-4c8adf2d97d5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520944(v=OCS.15)
ms:contentKeyID: 49289945
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除工作流程

 

_**上次修改主題的時間：** 2012-11-01_

請使用下列其中一個程序來刪除工作流程：

## 使用 Lync Server 控制台刪除工作流程

1.  以 RTCUniversalServerAdmins 群組成員或支援回應群組的某個預先定義之管理角色成員的身分登入。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[回應群組\]**，然後按一下 **\[工作流程\]**。

4.  在 **\[工作流程\]** 頁面上，按一下 **\[建立或編輯工作流程\]**。

5.  在 **\[選取服務\]** 搜尋欄位中，輸入裝載您要刪除之工作流程的 **ApplicationServer** 服務的部分或完整名稱。

6.  在服務清單中，按一下所需的服務，然後按一下 **\[確定\]**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>回應群組設定工具網頁隨即開啟。連線至 <strong>https://<em>&lt;webPoolFqdn&gt;</em>/RgsConfig</strong>，也可以直接從網頁瀏覽器開啟回應群組設定工具網頁。</td>
    </tr>
    </tbody>
    </table>


7.  在 **\[管理現有的工作流程\]** 下，找出您要刪除的工作流程，然後按一下 **\[執行\]** 下的 **\[刪除\]**。

8.  按一下 **\[是\]**。

## 使用 Cmdlet 刪除工作流程

1.  以 RTCUniversalServerAdmins 群組成員或支援回應群組的某個預先定義之管理角色成員的身分登入。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  在命令列中執行：
    
        Get-CsRgsWorkflow -Identity <Application Server service> -Name "<name of workflow>" | Remove-CsRgsWorkflow
    
    例如：
    
        Get-CsRgsWorkflow -Identity service:ApplicationServer:redmond.contoso.com -Name "Help Desk" | Remove-CsRgsWorkflow

