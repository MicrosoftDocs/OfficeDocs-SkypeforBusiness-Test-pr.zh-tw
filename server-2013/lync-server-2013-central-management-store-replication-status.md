---
title: Lync Server 2013：一般管理存放區覆寫狀態
TOCTitle: 一般管理存放區覆寫狀態
ms:assetid: f514f88d-986b-4e45-b79b-e04a7616c1fe
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn720926(v=OCS.15)
ms:contentKeyID: 62240031
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的一般管理存放區覆寫狀態

 

_**上次修改主題的時間：** 2015-01-26_

系統管理員對 Lync Server 進行某些變更 (例如，當系統管理員建立新的語音原則或變更 Address Book Server 組態設定) 時，該變更會記錄於中央管理存放區中，變更亦必須複寫到執行 Lync Server 服務或伺服器角色的所有電腦。

為了覆寫資料，Master Replicator (執行於中央管理伺服器) 會建立已變更組態資料的快照，然後將該快照的複本傳送至執行 Lync Server 服務或伺服器角色的每一部電腦。在這些電腦上，覆寫代理會收到快照並上載所變更的資料。然後，代理會將報告最新複寫狀態的訊息傳送給 Master Replicator。

Get-CsManagementStoreReplicationStatus cmdlet 可讓您確認您組織中任何 (或所有) Lync Server 電腦的覆寫狀態。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 Get-CsManagementStoreReplicationStatus cmdlet：RTCUniversalUserAdmins，RTCUniversalServerAdmins。

若要傳回已獲指派此 Cmdlet 之 RBAC 角色的清單 (包括您自行建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 命令提示字元中執行下列命令：

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Get-CsManagementStoreReplicationStatus"}

## 請參閱

#### 其他資源

[Get-CsManagementStoreReplicationStatus](get-csmanagementstorereplicationstatus.md)

