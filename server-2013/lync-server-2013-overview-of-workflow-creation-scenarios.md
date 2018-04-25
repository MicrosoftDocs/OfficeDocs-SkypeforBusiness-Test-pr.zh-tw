---
title: Lync Server 2013：建立工作流程的案例概觀
TOCTitle: 建立工作流程的案例概觀
ms:assetid: 05e0c175-0f1a-4bb1-b048-c68584d00649
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204646(v=OCS.15)
ms:contentKeyID: 49289965
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立工作流程的案例概觀

 

_**上次修改主題的時間：** 2012-10-17_

當您建立工作流程時，有兩種可能的情況：

  - 系統管理員建立及設定工作流程 - CsResponseGroupAdministrator 角色成員 (或同等權限) 建立及啟動工作流程和工作流程中的所有元素，例如代理群組、佇列、假日和上班時間、等候音樂等。

  - 系統管理員建立工作流程，而一般管理員設定選項 - CsResponseGroupAdministrator 角色成員 (或同等權限) 定義主要 SIP URI、顯示名稱，指派一或多個 CsResponseGroupManager 角色成員，以及選取佇列並啟動工作流程。然後，CsResponseGroupManager 會登入並編輯工作流程設定，包括建立代理群組、將群組指派給佇列，以及設定電話號碼、假日和上班時間、等候音樂等。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>當您想建立受管理的工作流程時，您必須建立並啟動工作流程。儲存作用中的受管理工作流程之後，即可修改及停用工作流程。</td>
    </tr>
    </tbody>
    </table>

