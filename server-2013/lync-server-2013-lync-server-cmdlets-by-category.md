---
title: Lync Server 2013 Cmdlet (按類別)
TOCTitle: Lync Server 2013 Cmdlet (按類別)
ms:assetid: 4ce274d7-b0ec-40b8-b85e-9a0613916ffb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398306(v=OCS.15)
ms:contentKeyID: 49290850
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 Cmdlet (按類別)

 

_**上次修改主題的時間：** 2015-03-09_

Microsoft Lync Server 2013 提供將近 550 個 Cmdlet，專門設計來讓系統管理員可以從命令列管理 Lync Server。您可以從 Lync Server 管理命令介面存取這些 Cmdlet。您可以直接從命令列擷取某個 Cmdlet 的說明，方法為輸入類似下列命令：

    Get-Help New-CsVoicePolicy -Full

上述命令會擷取 **New-CsVoicePolicy** Cmdlet 所有可用的說明。請將 **New-CsVoicePolicy** 的部分換成您要擷取說明的 Cmdlet 名稱。

若要擷取用來管理 Microsoft Lync Server 2013 的 Cmdlet 的完整清單，請在 Lync Server 管理命令介面命令提示字元中輸入：

    Get-Command * -Module Lync -CommandType cmdlet

如果您不確定需要哪個 Cmdlet，我們也提供 Cmdlet 及其說明主題的分類清單。您會發現某些 Cmdlet 出現在多個類別中，這是刻意的設計，因為它們適用於產品的多個區域。以下是類別清單：

## 本章節內容


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><a href="lync-server-2013-user-management-cmdlets.md">使用者管理 Cmdlet</a></p></td>
<td><p><a href="lync-server-2013-voice-application-cmdlets.md">語音應用程式 Cmdlet</a></p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-client-management-cmdlets.md">用戶端管理 Cmdlet</a></p></td>
<td><p><a href="lync-server-2013-advanced-enterprise-voice-cmdlets.md">進階 Enterprise Voice Cmdlet</a></p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-im-and-presence-cmdlets.md">IM 和顯示狀態 Cmdlet</a></p></td>
<td><p><a href="lync-server-2013-pstn-connectivity-cmdlets.md">PSTN 連線 Cmdlet</a></p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-conferencing-cmdlets.md">會議 Cmdlet</a></p></td>
<td><p><a href="lync-server-2013-phones-and-devices-cmdlets.md">電話和裝置 Cmdlet</a></p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-infrastructure-and-deployment-cmdlets.md">基礎結構和部署 Cmdlet</a></p></td>
<td><p><a href="lync-server-2013-migration-and-coexistence-cmdlets.md">移轉和並存 Cmdlet</a></p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-security-cmdlets.md">安全性 Cmdlet</a></p></td>
<td><p><a href="lync-server-2013-lync-server-management-shell-configuration-cmdlets.md">Lync Server 管理命令介面組態 Cmdlet</a></p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-server-roles-and-services-cmdlets.md">伺服器角色和服務 Cmdlet</a></p></td>
<td><p><a href="lync-server-2013-mobility-cmdlets.md">行動 Cmdlet</a></p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-application-management-cmdlets.md">應用程式管理 Cmdlet</a></p></td>
<td><p><a href="lync-server-2013-persistent-chat-server-cmdlets.md">Persistent Chat Server Cmdlet</a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/en-us/powershell/module/skype/">Lync Server 2013 中的同盟和外部存取 Cmdlet</a></p></td>
<td><p><a href="lync-server-2013-centralized-logging-cmdlets.md">Centralized Logging Cmdlet</a></p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-enterprise-voice-cmdlets.md">Enterprise Voice Cmdlet</a></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## 請參閱

#### 其他資源

[Lync Server PowerShell 部落格](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x404)

