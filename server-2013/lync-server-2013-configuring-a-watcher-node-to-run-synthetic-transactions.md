---
title: 設定監看員節點以執行綜合交易
TOCTitle: 設定監看員節點以執行綜合交易
ms:assetid: cedda508-8881-4079-88d5-49798f342ddf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205314(v=OCS.15)
ms:contentKeyID: 49292360
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定監看員節點以執行綜合交易

 

_**上次修改主題的時間：** 2015-03-09_

在安裝 System Center 代理程式檔案之後，您接下來必須設定監看員節點本身。設定監看員節點的步驟會因為監看員節點位在周邊網路之內或之外而有所差異。

設定監看員節點時，您也必須選擇該節點採用的驗證方法類型。Lync Server 2013 可讓您選擇下列兩種驗證方法之一：受信任伺服器或認證驗證。這兩種方法間的差異，如下表所示：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>設定</th>
<th>說明</th>
<th>支援的位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>受信任伺服器</p></td>
<td><p>使用憑證來模擬內部伺服器和略過驗證質詢。</p>
<p>這種方法適合偏好在每個監看員節點上管理單一憑證而不是許多使用者密碼的管理員使用。</p></td>
<td><p>企業內部。</p>
<p>請注意，若使用這種方法，監看員節點和受監控的集區必須位於相同的網域中。如果監看員節點和受監控的集區位於不同的網域，請改為使用認證驗證。</p></td>
</tr>
<tr class="even">
<td><p>認證驗證</p></td>
<td><p>以 Windows 認證管理員在每個監看員節點上安全地儲存使用者名稱與密碼。</p>
<p>此模式較偏重於密碼管理，但對於位在企業外部的監看員節點，這是唯一的選項。這些監看員節點在驗證時無法視為受信任的端點。</p></td>
<td><p>企業外部。</p>
<p>企業內部。</p></td>
</tr>
</tbody>
</table>


您也應該確認您的防火牆擁有 MonitoringHost.exe 與 PowerShell.exe 的輸入規則。如果這些程序遭到防火牆封鎖，您的綜合交易將會失敗，並顯示 504 (伺服器逾時) 錯誤。

