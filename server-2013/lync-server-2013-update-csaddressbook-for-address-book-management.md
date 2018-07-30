---
title: 適用於通訊錄管理的 Update-CsAddressBook
TOCTitle: 適用於通訊錄管理的 Update-CsAddressBook
ms:assetid: 0ffd2ef8-201c-44aa-8c64-1c7b0eaa7d48
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg429695(v=OCS.15)
ms:contentKeyID: 49290114
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 適用於通訊錄管理的 Update-CsAddressBook

 

_**上次修改主題的時間：** 2012-11-01_

誰可以執行這個 Cmdlet：根據預設，下列群組成員已獲得授權，可在本機執行 Update-CsAddressBook Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中輸入下列命令：

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Update-CsAddressBook"}

Update-CsAddressBook Cmdlet 會取代 Office Communications Server 中的 **abserver.exe –syncNow** 命令。此 Cmdlet 的目的在於立即啟動同步處理，而非等待排程的時間。第一個範例命令會更新組織中的所有通訊錄。第二個範例命令只會更新與所定義伺服器關聯的通訊錄。

> [!NOTE]  
> 在 Lync Server 2013 中，Lync Server 使用者複寫器會採用 Active Directory 的變更，並依據所設定的間隔來更新 Lync Server 使用者資料庫。Lync Server 使用者複寫器也會快速將變更傳播到 RTCab 資料庫，不需要系統管理員執行 Update-CSAddressBook。唯有在通訊錄檔案下載啟用時，系統管理員才需要執行 Update -CSAddressBook。



例如：

```
Update-CsAddressBook
```
```
Update-CsAddressBook -Fqdn atl-abs-001.contoso.com
```

如需完整命令的詳細說明，請參閱主要 Lync Server Windows PowerShell RTCCmdlets 參考中的下列項目。

## 請參閱

#### 其他資源

[Update-CsAddressBook](https://docs.microsoft.com/en-us/powershell/module/skype/Update-CsAddressBook)

