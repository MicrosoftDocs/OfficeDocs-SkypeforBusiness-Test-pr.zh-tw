---
title: 刪除專員群組
TOCTitle: 刪除專員群組
ms:assetid: df385fd1-62f4-42b7-a349-4eb38dea50c8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182597(v=OCS.15)
ms:contentKeyID: 49292563
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除專員群組

 

_**上次修改主題的時間：** 2012-11-01_

使用下列其中一個程序來刪除代理人群組。

## 使用 Lync Server 控制台刪除代理人群組

1.  以 RTCUniversalServerAdmins 群組成員或支援回應群組的某個預先定義之管理角色成員的身分登入。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[回應群組\]，然後按一下 \[群組\]。

4.  在 **\[回應群組\]** 頁面上的搜尋欄位中，輸入您要刪除之代理人群組的全部或部分名稱。

5.  在結果清單中，依序按一下要刪除的群組、\[編輯\] 和 \[刪除\]。

6.  按一下 **\[確定\]**。

## 使用 Cmdlet 刪除代理人群組

1.  以 RTCUniversalServerAdmins 群組成員或支援回應群組的某個預先定義之管理角色成員的身分登入。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  在命令列中執行：
    
        Get-CsRgsAgentGroup -Identity <Application Server service> -Name "<name of agent group>" | Remove-CsRgsAgentGroup
    
    例如：
    
        Get-CsRgsAgentGroup -Identity service:ApplicationServer:redmond.contoso.com -Name "Human Resources" | Remove-CsRgsAgentGroup

## 請參閱

#### 工作

[在 Lync Server 2013 中建立或修改代理人群組](lync-server-2013-create-or-modify-an-agent-group.md)  

#### 其他資源

[Remove-CsRgsAgentGroup](remove-csrgsagentgroup.md)  
[Get-CsRgsAgentGroup](get-csrgsagentgroup.md)

